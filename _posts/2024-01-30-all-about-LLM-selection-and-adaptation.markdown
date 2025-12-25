---
layout: post
title:  "All about LLM selection and adaptation"
date:   2024-01-30 08:45:52 -0500
categories: LLMs

---
This will be the first entry on the Diary of an AI Practitioner, recounting the knowledge I acquired along the way working on a text summarization task. I hope this will be a useful and fun read for another fellow AI enthusiast. 

Large Language Models or LLMs for short have been extremely popular to the general public since openAI launched their first user-facing product in November 2022. Commendably, chat GPT got extremely popular in a matter of days and everyone jumped right in to try out this new and cool chatbot. I must confess I was a bit of a skeptic in the beginning, but as I tried it out I saw the root of everyone’s excitement. 

Writing and I have had a love-hate relationship, with chat GPT I finally found a way to craft difficult emails faster, or even brainstorm the content of a new post more easily. One year later, I developed my first text summarization model using the pre-trained model FLAN-T5 from Hugging Face’s open-source library. 

There are some key differences in how one should approach a Gen AI initiative. The core point is that you need to define clearly from the very beginning the project scope. It’s not like the other ML projects that we’ve all been in, where mid-way through the project the business stakeholders are still not sure what they really want. Gen AI is expensive so we need to be mindful and plan carefully. The project’s use case will determine whether you will choose to work with an existing model or pretrain your own. Note that the cost of training GPT4 was more than $100 million and took around 100 days. I don’t want to assume, but most likely the first option is closer to everyone's pockets and needs. 

Hugging Face is a great open-source library that makes it accessible to play with a variety of models and datasets. 

Now you might ask, what model should I choose? 

From my understanding, a bigger LLM isn't always a necessity. It comes back to what your goal is. If you want to perform one single task (eg. text summarization) and are not interested in translation or question answering, then you can choose a model that performs well on that single operation. And don’t worry there are “model cards” that inform you of each model’s characteristics. However, you might need a model to perform multiple different tasks, thus a larger model might be better suited for your use case. I know that this nuanced answer might not be what you had hoped for, but it can be a great start to experimentation!

The third section in a project’s lifecycle is known as model adaptation. Let’s say you’ve chosen a particular model, in our case FLAN-T5, to assess its performance on your goal. The first technique to leverage is prompt engineering. Based on McKinsey’s article prompt engineering is the practice of designing inputs for generative AI tools that will produce optimal outputs. If that confuses you, you’re not the only one. 

The way I think about prompt engineering is using natural language to direct the model to perform a certain task. You can use zero-shot prompting, which is when you simply state your question to the model. Usually, larger models, such as GPT4 or Gemini, perform better on zero-shot prompting compared to smaller ones, like FLAN-T5. Other useful prompt engineering techniques are one-shot and few-shot prompting. Both techniques provide the model with one or more examples before the question you want a completion for. This way the model can better comprehend the task you want it to execute as well as the structure you want the output to have, which can lead to an increase in performance. 

All methodologies though have their limitations and prompt engineering is no stranger to it. LLMs have a constrained context window, which you can think of it as the model’s memory span or ability to interact with the outside world. Thus, when the context window’s capacity is reached, the model will not take into account all the text that’s been given. Another point to mention here is that when you implement few shot prompting adding more than 6 examples has been found to not further increase the model’s accuracy. In this case, you’ll need to either use another model or move into fine-tuning the current model. 
  
Let’s talk about Fine-tuning!

Fine-tuning a model is the operation of updating a model’s weights by training it with more data, which can yield to better performance results for your use case. But, there are some caveats. If you fine-tune a model on one single task, it will likely start performing worse on others. This is known as catastrophic forgetting. It might not be a problem for you though, as you might need the model to only summarize text. But if that’s not your intention you’ll need to fine-tune the model across multiple tasks, hence multiple datasets. As you can see the compute resources are exponentially rising. 

When planning to full-fine tune an LLM you’ll need compute resources for all the model parameters, such as the model’s temporary memory, forward activations, gradients, optimizers, and trainable weights. For example, if you are planning to fully fine-tune a model like GPT4 you’ll need to have the compute resources for its 1.76 trillion parameters. 

But it’s not all that gloomy, thankfully for people’s ingenuity some workarounds have been found. Methods like Parameter Effificent Fine-tuning (PEFT) or ​​Low-Rank Adaptation (LoRA) are here to save you!

But all that will be talked about in the next diary entry. :)


