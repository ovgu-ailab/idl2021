---
layout: default
title: Assignment 7
id: ass7
---

# Assignment 7: Attention-based Neural Machine Translation
**Deadline: December 6th, 9am**

In this task, you will implement a simple NMT with attention for a language pair 
of your choice.  
We will follow the corresponding 
[TF Tutorial on NMT](https://www.tensorflow.org/tutorials/text/nmt_with_attention).

Please do **not** just use the exemplary English-Spanish example to reduce temptation
 of simply copying the tutorial.  
You can find data sets [here](http://www.manythings.org/anki/). We recommend
 picking a language pair where you understand both languages (so if you do speak 
 Spanish... feel free to use it ;)). 
This makes it easier (and more fun) for you to evaluate the results.
However, keep in mind that some language pairs have a very large amount of examples,
whereas some only have very few, which will impact the learning process and the
quality of the trained models.

You may run into issues with the code in two places:
1. The downloading of the data inside the notebook might not work (it crashes
with a 403 Forbidden error). In that case, you can simply download & extract the
data on your local machine and upload the .txt file to your drive, and then mount
it and load the file as you've done before.
2. The `load_data` function might crash. It expects each line to result in
*pairs of sentences*, but there seems to be a third element which talks about
attribution of the example. If this happens, you can use `line.split('\t')[:-1]` to
exclude this in the function.

Recommendation: Start with a small number of training examples. Use one of the 
training examples to evaluate whether training worked properly. 
Only switch to the complete data set if you're sure that your code works, 
because training is quite slow.

Tasks:
- Follow the tutorial and train the model on your chosen language pair 
(using Bahdanau attention).
- You might need to adapt the preprocessing depending on the language.
- Implement other attention mechanisms and train models with them:
  - dot product attention <img src="https://latex.codecogs.com/svg.latex?h_t^T%20\cdot%20\overline{h}_s" />
  - Luong's multiplicative attention <img src="https://latex.codecogs.com/svg.latex?h_t^T%20W%20\overline{h}_s" />
- Optional: The tutorial implements the training step with an explicit loop
  over the decoder time steps. However, the decoder model/layer is written in
  such a way that it can actually process the whole sequence in one go, which
  would be much faster because optimized RNN implementations can be used 
  (we observed about a 5x speedup).
  Can you re-write the training step in this way? Be careful that the training
  performance doesn't degrade (the tutorial includes code to overfit on one 
  batch) as there may be problems with your code even if it runs without errors!
    

Hint: Take care to save your models or their weights (in the drive) 
so you do not lose your
training progress if the runtime resets!

Compare the attention weight plots for some examples between the attention 
mechanisms.  
We recommend to add `,vmax=1.0` when creating the plot in 
`ax.matshow(attention, cmap='viridis')` in the `plot_attention` function
so the colors correspond to the same 
attention values in different plots. 
- Do you see qualitative differences in the attention weights between different
 attention mechanisms?  
- Do you think that the model attends to the correct tokens in the input language
 (if you understand both languages)?

Here are a few questions for you to check how well you understood the tutorial.  
Please answer them (briefly) in your solution!  
- Which parts of the sentence are used as a token? Each character, each word, 
or are some words split up?
- Do the same tokens in different language have the same ID?   
  e.g. Would the same token index map to the German word `die` and to the 
  English word `die`?
- What is the relation between the encoder output and the encoder hidden state
 which is used to initialize the decoder hidden state 
 (for the architecture used in the tutorial)?
- Is the decoder attending to all previous positions, including the previous
 decoder predictions?
- Does the encoder output change in different decoding steps?
- Does the context vector change in different decoding steps?
- The decoder uses teacher forcing. Does this mean the time steps can be computed
 in parallel?
- Why is a mask applied to the loss function?
- When translating the same sentence multiple times, do you get the same result?
Why (not)? If not, what changes need to be made to get the same result each time?

Hand in all of your code, i.e. the working tutorial code along with all changes/additions you made. Include outputs which document some of your experiments. Also
remember to answer the questions above! Of course you can also write about other
observations you made.
