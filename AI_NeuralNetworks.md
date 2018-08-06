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

- MS has CNTK (Cognitive Toolkit)
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
  - this gets heavily used
- Gated Recurrent Unit (GRU)
  - Uses a similar strategy as LTSM, but uses a different memory structure.
  - Used mostly for music and speech recognition
- Auto Encoder (AE)
  - Basically "unsupervised training"
  - Previous to AE, we used Baysian Networks
  - One intermediate layer
  - SAME number of inputs and outputs (, SQRT inputs = # intermediate nodes)?
  - Supervised training
  - Skynet-ish... 
  - CNTK, Tensor Flow type of thing; TensorFlow is a good getting started thing
    - Python tends to be the language used (possibly due to it's Functional nature)
  - Singularity idea is just nonsense. Worried about this kind of stuff impacting job market too quickly (suppliment such and such)
  - A few types
    - Variational AE (VAE)
      - Hidden layer is probablistic, allowing for generalization rather than exactness
      - Denoising AE (DAE) 
      - Sparse AE (SAE)
        - more intermediate nodes per layer than inputs and outputs
- Markov Chain (MC)
  - connects every node to every node; not input -> hidden layer -> output, but input <-> output
  - Not useful in _every_ context. This is what would be used instead of a Baysian Filter (comes down to a finite state machine)
- Hopfield Network (HN)
  - all nodes connected
  - some nodes are probablistic
  - some nodes are other...

... left... easy to wikipedia this.