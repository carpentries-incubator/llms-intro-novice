---
title: 'Large Language Models'
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What does a large language model do?
- How is a large language model developed?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

After this episode, learners will be able to:

- Summarise how a language model produces output based on its training data and conditioning.

::::::::::::::::::::::::::::::::::::::::::::::::

The term "generative AI" refers to a range of artificial intelligence models that produce output similar to the data on which they have been trained, based on some input provided.
The category includes many different models that have been trained to produce different kinds of output from different inputs, e.g. text to text, text to image, text to video, image to text.
The technology at the centre of the most well-known and widely-used text generating AI tools is the _Large Language Model_ (LLM).

## Advanced Pattern Matching 
Language models encapsulate patterns in data and produce output based on those patterns.
What factors influence the output produced by a model?

TODO: a figure summarising the process outlined below.

### Model training
Patterns are "learned" by the model through a process of _training_: a large volume of data is processed to identify the statistical relationships between elements of that data, which are then stored in the model.
In language models, these elements of data are _tokens_: words, parts of words, and other building blocks of text.
Patterns are identified in the use of these tokens during the training process, such as which combinations of tokens often appear in sequence.

:::::::::::::::::::::::::::::::::::::::: challenge

### Exploring tokens
Use [an online tokeniser tool](https://www.danieldemmel.me/tokenizer/) to count the number of tokens in this sentence:

> In biology, depolarization or hypopolarization is a change within a cell, during which the cell undergoes a shift in electric charge distribution, resulting in less negative charge inside the cell compared to the outside.

Scroll down the page to explore the breakdown of tokens from different systems.
Try out some other sentences and paragraphs.
What do you learn about how text is broken into tokens?


::::::::::::::::::::::::::::::: solution

Text is most commonly split into one token per word, with additional tokens for punctuation.
Spaces before words are often included in the word's token, and some words are decomposed into multiple tokens representing common building blocks of the language e.g. suffixes like "ing", "ize", and "ed" or prefixes like "pre", "de", "uni", etc.

::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

The training process for cutting edge large language model systems involves the processing of colossal and diverse volumes of data.
The models themselves must be very large in order to capture the patterns in such a deep and wide range of data.
The result is an enormous set of numerical parameters that determine the probability of each possible next token in its output.
These are referred to as the model's _weights_.

### Fine tuning
The initial training is followed by a second process of _fine tuning_ where the model's weights are further adjusted through testing and feedback.
This process involves prompting the model with known examples and comparing outputs to the correct or preferred solutions, and people prompting the model and rating the quality of the output produced. 
The results of these tests are used to further adjust the weights towards the kinds of responses that are preferred.

### The system prompt
A chatbot has an internal prompt containing a fixed set of instructions from its developers.
This _system prompt_ is included alongside the user's prompt whenever the model generates output.
It may contain guidance on everything from the tone chatbot's output to how it should avoid infringing copyright in its responses.

### The context window
In addition to the inherent weights of the model, the content of the output is influenced by the context of the task at hand.
This context includes information about the system prompt, the user's prompt, the history of the dialogue between the user and the model, and the contents of any files that have been processed so far.
It is stored in the _context window_ of the model.
Since the training data of a large language model is so diverse and general, the data in the context window is very important for specialising the kind of language that will be included in its responses.
The size of the context window varies greatly from model to model, but they all have a limit on how much they can store.
The capacity of the context window, and ensuring that the most relevant information remains in the context, become increasingly important considerations as the size of a project grows.

::::::::::::::::::::::::::::::::::::::: discussion

### How context influence output?
Your task is to predict the next word in the following sentence:

> On the way to the meeting, I picked up a \_\_\_\_

How would your answer change, if you knew that the sentence was part of:

1. A text message about what the author had for lunch.
2. A chapter in a novel about secret agents and espionage.
3. An excuse for being late to a work meeting.

::::::::::::::::::::::::::::::::::::::::::::::::::

Every time a chatbot is prompted, the entire context is fed into the model, which predicts and returns a new sequence of tokens.
The output is a simulation of the language that the model was trained on.

::::::::::::::::::::::::::::::::::::: keypoints 

- Large language models generate text output based on patterns in its training data and the context it stores about the task or project.
- The development of a model includes training on a large volume of data and fine tuning of the resulting weights. 
  The responses produced by a chatbot are also influenced by a fixed system prompt and the contents of the model's context window.

::::::::::::::::::::::::::::::::::::::::::::::::
