---
layout: post
title: "Generative AI and How it works"
author: umesh
categories: [AI, Machine Learning, Neural Networks ]
tags: [Tools, Development]
image: https://cdn.prod.website-files.com/59e16042ec229e00016d3a66/6441d5f76d21e1e4dee9ffa2_Gen%20AI%20blog_Blog%20hero.webp
---

# Foundations of Generative AI

In this blog, we will walk through the term Generative AI, what it is and how it works behind the scenes.

### What is Generative AI?

Generative Ai is a subset of Artificial Intelligence which often gets confused with other similar terminologies like Machine learning, neural networks and Ai itself. 

Understanding Generative AI: The layers

Artificial Intelligence: Ai is the broader concept, It is basically machines performing tasks that typically require human intelligence.

Machine Learning: Learn to identify patterns and make predictions from data.

Neural Networks: USes layered neural networks to process vast amounts of data.

Generative AI: creates new content like images, video, audio, text based on learned patterns.


### How does it work

Everythimg starts with a prompt and ends with the destination thta is the answer. 

1. The Prompt

Your instruction or question to the AI. The more precise and syntactical the prompt the more accurate and elaborate output we get. We can discuss more about that in another post.

For example: When did india get independece from the british?

2. Tokens

The given prompt is converted into individual bits known as tokens.

3. Embeddings

Further tags are added to the tokens to add context.

![walking]({{ site.baseurl }}/assets/images/Gen_AI_flowchart)

4. Neural Network

The vast network where AI looks for any possible connections and pathways.

5. Self Attention

The tokens talk to each other to identify relationships.

6. Transformers

Transformers focus on managing the self attentions. It will check for important connections between the tokens.

7. LLM (Large Language Model)

This is the key compenent leading the best possible way from the learned patterns along the way.


### What exactly is Prompt

AI prompt has 6 parts.

Purpose: What is the goal or aim of the your question. Write a code, analyze a document, prepare a presentation etc

Role: What persona it should take up, like assume it to be a teacher, a musician, a painter etc. This give AI to think the role which we have given it to assume.

![walking]({{ site.baseurl }}/assets/images/Prompt)

Output: How should the AI structure its output. It will give the output based on the structure we need. Be it a flowchart, image, video, code syntax etc.

Markers: The markers act as guidelines or boundaries for the AI to act upon. Like setting limits to write a paragrapgh within 200 lines. Defining exact criteria helps AI to think more efficiently. 

Patterns: Provide templates, examples which can be given to the AI. 

Tone: Set the tone in the question. Formal, informal, humourous, serious or something else.

###  Example Prompts (Using the Framework) 

#### Travel Itinerary 

○ Prompt: "Create a 3-day travel itinerary for Paris. Act as an experienced travel agent. Provide a day-by-day plan with activities and restaurant suggestions. The budget is mid-range, and the focus is on art museums and iconic landmarks. Use an enthusiastic and informative tone." 

○ (P) Create Itinerary (R) Travel Agent (O) Day-by-Day plan (M) 3-day, Paris, Budget, Art and Landmarks (P) Day-by-day Format (T) Enthusiastic 

#### ● Email Draft 

○ Prompt: "Write a formal email to a client apologizing for a delay in service. The tone should be professional and empathetic." 

○ (P) Write Email (O) Formal Email (T) Professional, Empathetic 

#### ● Article Summary 

○ Prompt: "Summarize this news article about artificial intelligence in three bullet points. Focus on the main benefits and challenges." 

○ (P) Summarize article (O) Three Bullet Points (M) Benefits and challenges 

#### ● Explaining a Concept 

○ Prompt: "Explain blockchain technology as if you are talking to a 10-year-old. Act as a friendly explainer. The tone should be simple and clear." 

○ (P) Explain Blockchain (R) Friendly Explainer (T) Simple, Clear


 


