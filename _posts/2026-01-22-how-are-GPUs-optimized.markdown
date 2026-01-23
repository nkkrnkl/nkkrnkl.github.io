---
layout: post
title:  "How are GPUs optimized?"
date:   2026-01-22 08:45:52 -0500
categories: GPUs

---
I came across an old blog post by J. Appleyard on optimizations for Recurrent Neural Networks in cuDNN 5. You might think, "Why look at a cuda library from 10 years ago?" But by looking back, we can uncover how these low-level operations work as we continue to face similar problems today.  

In one of my classes, a PhD student mentioned how shockingly underutilized GPU resources are during LLM inference. According to the paper [Increasing GPU Utilization during Generative Inference for Higher Throughput](https://proceedings.neurips.cc/paper_files/paper/2023/file/3a13be0c5dae69e0f08065f113fb10b8-Paper-Conference.pdf), an NVIDIA A100 GPU was sometimes utilized at only 0.4% when serving GPT-J.  

With compute being costly and scarce, efficient GPU usage is paramount.  

This is why I'd like to share what I've learned about achieving higher GPU performance.  

In this post, we’ll look at 3 operations which were first introduced in cuDNN 5. All the proposed optimizations in J. Appleyard’s blog achieved a near 70% peak floating-point performance for a Long Short-Term Memory (LSTM) network on an NVIDIA Tesla M40. 

For context, the LSTM architecture was: **512 hidden units**, **64 mini-batch size**, **Tesla M40 GPU** (24 Streaming Multiprocessors).  

### But before we jump further, what is an LSTM?
Recurrent Neural Networks (RNNs) process sequential data, such as text, speech, and financial data. In text generation, an RNN predicts the next word based on the previous sentence, which can be thought of as a sequence. However, RNNs have a core limitation known as the vanishing gradient problem. This occurs when the sequences become larger, the network starts ‘forgetting’ certain information.


**LSTM** is a type of RNN that addresses the vanishing gradient problem by using a "cell state" that allows information to flow without being repeatedly multiplied by small numbers. Even with the industry's focus on Transformers, I believe it’s crucial to learn how to scale and parallelize different architectures. 

### The Three Optimizations

Before cuDNN 5, researchers used individual cuBLAS (Basic Linear Algebra Subprograms) functions, which resulted in low GPU utilization. This is because if you run many small matrix-matrix multiplications (GEMMs) for each LSTM gate, you create many small grid launches. Therefore, the GPU spends more time scheduling threads and fetching weights from memory than actually doing the math. GPUs require parallelism to reach their peak performance.  
 

To achieve a **5.5x increase** in GPU utilization, cuDNN 5 implemented three optimizations:

<style>
.optimization-table {
    width: 100%;
    border-collapse: collapse;
    margin: 1.5em 0;
    font-size: 0.95rem;
    background: #fff;
    border: 1px solid #e0e0e0;
}
.optimization-table th,
.optimization-table td {
    border: none;
    border-bottom: 1px solid #e8e8e8;
    padding: 16px 20px;
    text-align: left;
    vertical-align: top;
    line-height: 1.6;
}
.optimization-table th {
    background-color: #fafafa;
    font-weight: 700;
    color: #333;
}
.optimization-table td:first-child {
    font-weight: 600;
    color: #222;
    min-width: 160px;
}
.optimization-table tr:last-child td {
    border-bottom: none;
}
</style>

<table class="optimization-table">
<thead>
<tr>
<th>Optimization</th>
<th>How it Works</th>
<th>Why it Matters</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Combining GEMMs</strong></td>
<td>Stack multiple weight matrices into one large operation.</td>
<td>Increases work per thread helping with GPU utilization.</td>
</tr>
<tr>
<td><strong>Streaming GEMMs</strong></td>
<td>Uses CUDA Streams to run the input GEMM and the recurrent GEMM simultaneously.</td>
<td>Exploits the fact that these two operations don't depend on each other.</td>
</tr>
<tr>
<td><strong>Fusing Point-wise Ops</strong></td>
<td>Combines sigmoids, tangent, and additions into a single kernel.</td>
<td>Prevents the GPU from writing/reading intermediate data to memory repeatedly.</td>
</tr>
</tbody>
</table>

#### 1. Combining GEMMs
One LSTM unit requires 8 GEMMs (4 for input x_i and 4 for the hidden states). By stacking these matrices, we combine multiple small operations into a single GEMM, increasing work per thread and thereby improving occupancy. This keeps the GPU’s execution units constantly working on mathematical operations.

#### 2. Streaming GEMMs
In an LSTM, the input GEMM (data coming into the layer) and the recurrent GEMM (hidden state from the previous time step) are independent. Therefore, we can double the number of concurrent blocks by using CUDA streams, which execute multiple operations simultaneously. This ensures that more Streaming Multiprocessors (SMs) are active at once.

#### 3. Fusing Point-wise Operations
Every time a new kernel is launched, the CPU and GPU have to communicate, which adds latency. For LSTMs, launching a new kernel for every point-wise operation, such as calculating sigmoids for the gates or a tanh for the cell state, creates kernel launch overhead and a memory bandwidth bottleneck. Therefore, combining all these operations into a single CUDA kernel can significantly reduce data transfers to and from global memory, allowing the GPU to read the data once, perform all the math in the same kernel, and write the final result back just once.

Achieving a 5.5x improvement through these three optimizations showcases the importance of fully utilizing the silicon we have with our own code. While modern GPUs such as the H100 and A100 have automated much of this in the hardware, we still need to learn how they work to leverage the power of the GPUs we have.

#### Sources

* [Optimizing Recurrent Neural Networks with cuDNN 5](https://developer.nvidia.com/blog/optimizing-recurrent-neural-networks-cudnn-5/) 
* [Increasing GPU Utilization during Generative Inference for Higher Throughput](https://proceedings.neurips.cc/paper_files/paper/2023/file/3a13be0c5dae69e0f08065f113fb10b8-Paper-Conference.pdf)