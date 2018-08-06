# AI And Neural Networks

@GregLevenhagen

At it's core Neural Networks are Linear Algebra, Mathematics. 

## How did we start

Alan Turing 1956. First practical implementation.

Turing until today: neural networks grew because of gaming. Google's breakthrough [DeepMind](https://www.deepmind.com).

## How's it used?

Tons of cases. ML, Automation, robotics, augmented intelligence, financial systemes, voice, image and character (OCR), mfg, verification, etc.

- Side note: Seth Juarez is talking AI on Wed.

AI has TONS of branches. 

- ML
  - Deep learning
  - Supervised
  - Unsupervized
- NLP (natural lang)
  - content extraction
  - classification
  ...
...

## Content and Essence

- MS has CNTK
- Google has TensorFlow
- Ask Neural Nets... "is this a human?" "is this a dog?", etc.
  - Rather than ask this, let's ask the AI after we train it, what it thinks a _blank_ is. I.e. not "is this a cat" to "what is a cat"?
- "Mona Lisa, in lego"

## Terms

A neural network at large is a collection of functions. Input functions connect to intermediate (or hidden) functions which connect to reduced number of output functions. Outputs of a function link to inputs of another. Node = Function. Training means running things through the network and get to a threshold of about 90%, then it can self learn.

- Artificial NN (ANN) - Feed Forward
- Radial Basis N (RBF) - Feed Forward
  - sigmoid
  - radial base functions
- Deep NN (DNN)
  - we start adding in layers
  - Graph Theory applies here
  - mimics biological mapping
  - each hidden layer helps gain confidence in result as well as processing time
  - this is the crux of the stuff happening over the last 6 years tied in with the hardware and data that we have
- Recurrent NN (RNN)
  - like a DNN, but nodes can loop back on themselves, which gives more confidence
- Long / Short Term Memory (LTSM)
  - builds on RNN, but gives memory to the hidden nodes, can refine and refine
  - uses a technique of Memoization
