---
layout: post
title:  "Here is a sleek fine tuning technique to use"
date:   2024-02-28 08:45:52 -0500
categories: LLMs

---
This month's discussion will be about fine-tuning LLMs to adjust the models’ weights to perform specific tasks with higher precision. I need to stress here from the beginning that not all use cases require fine-tuning an LLM. However, you may consider this technique if other methods, aka few-shot prompting and model experimentation, have failed to yield the desired outcomes. 

We need to keep in mind that LLMs are trained for general-purpose tasks from a vast amount of data found on the web. Therefore, they will likely have little knowledge of a highly specialized industry like healthcare, the financial sector, or perhaps education. This comes as a good segway to a valid concern of these systems, hallucinations. An LLM will sound like an expert, even if the generated content is not based on accurate information. Imagine being a patient and asking a model what to do when you have a specific disease, but getting faulty instructions. It would have detrimental consequences for the society if such models were deployed. This is the reason why fine-tuning an LLM could be a great solution to overcome the aforementioned challenges. 

But as you may have guessed fine-tuning all the model’s weights is not as simple, because it requires a lot of computing. So some researchers had a profound idea; why can’t we update a subset of an LLMs’ weights? This is how a very popular methodology was born, known as Parameter Efficient Fine Tuning (PEFT).

Now what is PEFT?
PEFT is when the original weights of an LLM are frozen, which can save a lot of compute and storage costs without compromising on the performance. PEFT helps mitigate the issue of catastrophic forgetting, which can occur during full fine-tuning on a specific task. There are five tradeoffs that different PEFT methods address; parameter efficiency, training speed, inference costs, model performance, and memory efficiency. For the purpose of this post, we’ll be focusing on Low-Rank Adaptation (LoRA).

LoRA was introduced in a paper published in 2021 with the title LoRA: Low-Rank Adaptation of Large Language Models. This technique became very popular due to its ability to significantly reduce the trainable parameters of an LLM, hence being both storage- and compute-efficient, as well as having no additional inference latency. This was achieved by freezing most of the original weights in the self-attention layers of the encoder and injecting trainable rank decomposition matrices into each layer of the Transformer architecture.  

LoRA is an approximaization technique using the Rank Factorization Theorem from linear algebra to estimate the lower rank of the matrix’s model weights. 

Let’s see how its performed on a high level; 

1) The pre-trained model weights are frozen (W).
   
2) Two lower rank decomposition matrices are introduced A and B, approximating the change in the frozen weights matrix (dW). The result of their product has the same dimensions as the matrix’s weight. It’s important to note that the smaller the rank of the decomposition matrices the smaller the trainable parameters.
   
3) Then the product of those two matrices, A and B, known as the adapter, is trained with the pre-trained model.
   
4) Lastly, the trained adapter is incorporated into the different layers of the pretrained model (W’ = W + AB).

One extremely useful element of LoRA is its flexibility, as a single GPU can be substantial to perform it. 

Now that we know the basics of LoRA let’s experiment with it.

Here, is a great [link](https://huggingface.co/docs/diffusers/main/en/training/lora) from the Hugging Face library to use in your future projects. 

Sources:

1) Hu, E.J. et al. (2021) Lora: Low-rank adaptation of large language models, arXiv.org. Available at: https://doi.org/10.48550/arXiv.2106.09685 (Accessed: 04 March 2024).
   
2) Shrish (2023) Lora: Low-rank adaptation from the First Principle, Medium. Available at: https://medium.com/@Shrishml/lora-low-rank-adaptation-from-the-first-principle-7e1adec71541 (Accessed: 04 March 2024). 

