# Book Buddy: Interactive Storytelling using a Gemma-based RAG 📖

- _[Read the blog post.](https://jigyasa-grover.github.io/BookBuddyInteractiveStorytellingUsingAGemmaBasedRAG/)_
- _[Check out the Colab Notebook.](https://github.com/jigyasa-grover/Book-Buddy-Interactive-Storytelling-using-a-Gemma-based-RAG/blob/main/Book_Buddy_Interactive_Storytelling_using_a_Gemma_based_RAG_%F0%9F%93%96.ipynb)_


![image](https://github.com/jigyasa-grover/Book-Buddy-Interactive-Storytelling-using-a-Gemma-based-RAG/assets/9291400/dfd26272-b5ac-42ad-8027-9f9dca3b87e5)

In the realm of AI-driven interactive storytelling, the fusion of Retrieval Augmented Generation (RAG) and Google's Gemma language model opens new avenues for creating engaging narratives and educational experiences. RAG, often likened to an "open-book" approach for AI, empowers models like Gemma to access and synthesize vast amounts of information to answer specific queries or weave intricate tales.

## RAG and Gemma 🤝🏻 
[Retrieval-Augmented Generation (RAG)](https://cloud.google.com/use-cases/retrieval-augmented-generation) leverages a dual-model approach: a retriever to fetch relevant information and a generator to craft responses in natural language. This method not only enhances the accuracy of AI-generated content but also reduces computational overhead compared to traditional fine-tuning methods. 

[Gemma](https://ai.google.dev/gemma), a lightweight, text-to-text, decoder-only large language model, is known for its precision and efficiency, emerges as an ideal candidate for such tasks, making it a potent tool for interactive storytelling.

![image](https://github.com/jigyasa-grover/Book-Buddy-Interactive-Storytelling-using-a-Gemma-based-RAG-/assets/9291400/6a281de4-b369-415c-839e-63c48f3422df)

_[A generic RAG architecture, courtesy (arxiv) 'Retrieval-Augmented Generation for AI-Generated Content: A Survey'](https://arxiv.org/pdf/2402.19473)_.


## Crafting Interactive Narratives 🏰
Imagine a scenario where readers can interact with a virtual "Book Buddy," a character powered by Gemma-based RAG. This AI companion can dynamically respond to queries from the storylines and provide detailed explanations on demand. Whether guiding readers through complex plotlines or explaining background lore, Gemma excels in delivering coherent, engaging content tailored to user interactions.


# **Let's Build "Book Buddy" 🛠️**

- _[Read the blog post.](https://jigyasa-grover.github.io/BookBuddyInteractiveStorytellingUsingAGemmaBasedRAG/)_
- _[Check out the Colab Notebook.](https://github.com/jigyasa-grover/Book-Buddy-Interactive-Storytelling-using-a-Gemma-based-RAG/blob/main/Book_Buddy_Interactive_Storytelling_using_a_Gemma_based_RAG_%F0%9F%93%96.ipynb)_

To delve deeper into the capabilities of Gemma-based RAG for interactive storytelling, let's embark on a hands-on journey that creates a dynamic system capable of answering questions about the classic text ["Alice's Adventures in Wonderland" by Lewis Carroll](https://www.gutenberg.org/files/11/11-0.txt), available from Project Gutenberg.

By leveraging Gemma's capabilities, we can prototype interactive narratives that respond intelligently to user prompts, offering a personalized storytelling experience. Whether deployed in educational settings to elucidate historical events or within gaming environments to create dynamic quests, the versatility of Gemma-based RAG enriches the user experience through immersive, responsive storytelling.

- Setting up the environment 🌳
- Loading and splitting the data 📚
- Loading the embedding model 🤳🏻
- Storing the embeddings in a vector database 🧳
- Setting up the retriever 🔬
- Setting up the generator 🎡
- Setting up the conversational retrieval chain ⛓️
- Asking Book Buddy a question 🙋🏻‍♀️
- Tying it all in 🎀
- Testing BookBuddy 🧪
  ```
  Question:  Who has written Alice’s Adventures in Wonderland?
  Answer:   Lewis Carroll.
  
  Current Chat History:  [('Who has written Alice’s Adventures in Wonderland?', ' Lewis Carroll.')]
  
  Question:  What game does Alice play?
  Answer:   Alice plays a game of croquet in Wonderland.
  
  Current Chat History:  [('Who has written Alice’s Adventures in Wonderland?', ' Lewis Carroll.'), ('What game does Alice play?', ' Alice plays a game of croquet in Wonderland.')]
  
  Question:  Who said - Off with their heads?
  Answer:   The Queen of Hearts said "Off with their heads".
  
  Current Chat History:  [('Who has written Alice’s Adventures in Wonderland?', ' Lewis Carroll.'), ('What game does Alice play?', ' Alice plays a game of croquet in Wonderland.'), ('Who said - Off with their heads?', ' The Queen of Hearts said "Off with their heads".')]
  
  Question:  What was the last part of the cat to disappear?
  Answer:   The grin.
  
  Current Chat History:  [('Who has written Alice’s Adventures in Wonderland?', ' Lewis Carroll.'), ('What game does Alice play?', ' Alice plays a game of croquet in Wonderland.'), ('Who said - Off with their heads?', ' The Queen of Hearts said "Off with their heads".'), ('What was the last part of the cat to disappear?', ' The grin.')]
  
  Question:  What is written on the potion bottle that Alice drinks?
  Answer:   The potion bottle says "Drink me."
  
  Current Chat History:  [('Who has written Alice’s Adventures in Wonderland?', ' Lewis Carroll.'), ('What game does Alice play?', ' Alice plays a game of croquet in Wonderland.'), ('Who said - Off with their heads?', ' The Queen of Hearts said "Off with their heads".'), ('What was the last part of the cat to disappear?', ' The grin.'), ('What is written on the potion bottle that Alice drinks?', ' The potion bottle says "Drink me."')]
  
  Question:  Who fell asleep at the Tea Party?
  Answer: The person who fell asleep at the Tea Party is the Dormouse.
  
  Current Chat History:  [('Who has written Alice’s Adventures in Wonderland?', ' Lewis Carroll.'), ('What game does Alice play?', ' Alice plays a game of croquet in Wonderland.'), ('Who said - Off with their heads?', ' The Queen of Hearts said "Off with their heads".'), ('What was the last part of the cat to disappear?', ' The grin.'), ('What is written on the potion bottle that Alice drinks?', ' The potion bottle says "Drink me."'), ('Who fell asleep at the Tea Party?', 'The person who fell asleep at the Tea Party is the Dormouse.')]
  
  Question:  What is rule 42 and why is it important for Alice?
  Answer:   Rule 42 is the oldest rule in the book and it dictates that all persons more than a mile high must leave the court. This impacts Alice because she is not a mile high and therefore must leave the court.
  
  Current Chat History:  [('Who has written Alice’s Adventures in Wonderland?', ' Lewis Carroll.'), ('What game does Alice play?', ' Alice plays a game of croquet in Wonderland.'), ('Who said - Off with their heads?', ' The Queen of Hearts said "Off with their heads".'), ('What was the last part of the cat to disappear?', ' The grin.'), ('What is written on the potion bottle that Alice drinks?', ' The potion bottle says "Drink me."'), ('Who fell asleep at the Tea Party?', 'The person who fell asleep at the Tea Party is the Dormouse.'), ('What is rule 42 and why is it important for Alice?', ' Rule 42 is the oldest rule in the book and it dictates that all persons more than a mile high must leave the court. This impacts Alice because she is not a mile high and therefore must leave the court.')]
  
  Question:  From what is the Caterpillar in Alice’s Adventures in Wonderland smoking?
  Answer:    A hookah.
  
  Current Chat History:  [('Who has written Alice’s Adventures in Wonderland?', ' Lewis Carroll.'), ('What game does Alice play?', ' Alice plays a game of croquet in Wonderland.'), ('Who said - Off with their heads?', ' The Queen of Hearts said "Off with their heads".'), ('What was the last part of the cat to disappear?', ' The grin.'), ('What is written on the potion bottle that Alice drinks?', ' The potion bottle says "Drink me."'), ('Who fell asleep at the Tea Party?', 'The person who fell asleep at the Tea Party is the Dormouse.'), ('What is rule 42 and why is it important for Alice?', ' Rule 42 is the oldest rule in the book and it dictates that all persons more than a mile high must leave the court. This impacts Alice because she is not a mile high and therefore must leave the court.'), ('From what is the Caterpillar in Alice’s Adventures in Wonderland smoking?', '  A hookah.')]
  
  Question:  Which character serves as herald to the King and Queen of Hearts?
  Answer:   The White Rabbit.
  
  Current Chat History:  [('Who has written Alice’s Adventures in Wonderland?', ' Lewis Carroll.'), ('What game does Alice play?', ' Alice plays a game of storytelling in Wonderland.'), ('Who said - Off with their heads?', ' The Rabbit said "Off with their heads".'), ('Where was the cat from?', ' The context does not contain any information regarding who said "Off with their heads", so I cannot answer this question from the provided context.'), ('What was the last part of the cat to disappear?', ' The grin.'), ('What is written on the potion bottle that Alice drinks?', ' The potion bottle says "Drink me."'), ('Who fell asleep at the Tea Party?', '\n\nThe person who fell asleep at the Tea Party is the Dormouse.'), ('What is rule 42 and why is it important for Alice?', ' Rule 42 is the oldest rule in the book and it dictates that all persons more than a mile high must leave the court. This impacts Alice because she is not a mile high and therefore must leave the court.'), ('From what is the Caterpillar in Alice’s Adventures in Wonderland smoking?', '  A hookah.'), ('Which character serves as herald to the King and Queen of Hearts?', ' The White Rabbit.')]
  ```
