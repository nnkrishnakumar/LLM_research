# LLM_research
LLM_research paper

LLAMA Architecture:
-------------------
> LLaMA (Large Language Model Meta AI) is a family of autoregressive large language models (LLMs) released by Meta AI. The architecture of LLaMA is based on the transformer architecture, 
which has been the standard for language modeling since 2018. However, there are several modifications made to enhance the model's performance 1, 2:

> Activation Function: LLaMA uses the SwiGLU activation function instead of the commonly used ReLU (Rectified Linear Unit) 2.
> Positional Embeddings: LLaMA replaces absolute positional embeddings with rotary positional embeddings (RoPE). These are added at each layer of the network 2.
> Normalization: Instead of using standard layer-normalization, LLaMA employs root-mean-squared layer-normalization to improve training stability 2.
> Context Length: The context length is increased from 2K (Llama 1) tokens to 4K (Llama 2) tokens 1.
> The LLaMA models were trained on a large dataset, with the first version (LLaMA-1) trained on a dataset with 1.4 trillion tokens. This data included webpages scraped by CommonCrawl, open-source repositories of source code from GitHub, Wikipedia in 20 different languages, public domain books from Project Gutenberg, LaTeX source code for scientific papers uploaded to ArXiv, and questions and answers from Stack Exchange websites 1.

The second version, LLaMA-2, was trained on a larger dataset with 2 trillion tokens. This dataset was curated to remove websites that often disclose personal data of people and upsample sources considered trustworthy 1.




Activation function available in LLAMA:
--------------------------------------
SwiGLU(x) = x * sigmoid(beta * x) + (1 - sigmoid(beta * x)) * x

Rectified Linear Units (ReLU)f(x)=max(0,x)


***********************************************************************************************************************
sigmoid mathmatical formula : σ(x) = 1 / (1 + e^-x)

>>> sigmoid function is generally use as activation function in neural network.





LLM research paper:
------------------
LLM:(Large Language Model):
--------------------------

Transformer: LLM built using Transformer.
-----------




WORKING OF RNN :
----------------

RNN use for various use cases: 

Like:

> sentence auto completion
> google translator 
> NER:(Name Entity Recognition)
> sentiment analayis


Question: why can't we use simple neural network to work with sequence.

Problem1: No fixed size of neurons in a layers.(Variable size of input output neurons)
Problem2: Too much computation 
probelm3: Parameters are not shared


Encoder & Decoder:
------------------
In Natural Language Processing (NLP), encoder-decoder models are commonly used to handle tasks such as machine translation, text summarization, question answering, and dialogue systems. 

These models consist of two main components: an encoder and a decoder.

Encoder
-------
The role of the encoder is to take an input sequence and generate a contextual representation, also known as the context, which captures the essence of the input sequence. 
This context serves as the input for the decoder. The encoder uses a Recurrent Neural Network (RNN) to process the input sequence, generating a final hidden state that represents the context.

Here is an example of how to implement an RNN encoder using TensorFlow:

import tensorflow as tf

model = tf.keras.Sequential([
 tf.keras.layers.Embedding(vocab_size, 64),
 tf.keras.layers.GlobalAveragePooling1D(),
 tf.keras.layers.Dense(64, activation='relu'),
 tf.keras.layers.Dense(1, activation='sigmoid')
])


Decoder
-------

The decoder takes the context generated by the encoder as input and generates an output sequence. 
The decoder also uses an RNN, taking the final hidden state of the encoder as its initial hidden state. The decoder continues generating output until an end-of-sequence marker is generated.

Here is an example of how to implement an RNN decoder using TensorFlow:

import tensorflow as tf

model = tf.keras.Sequential([
 tf.keras.layers.Embedding(vocab_size, 64),
 tf.keras.layers.Bidirectional(tf.keras.layers.LSTM(64)),
 tf.keras.layers.Dense(64, activation='relu'),
 tf.keras.layers.Dense(1, activation='sigmoid')
])


Attention Mechanism

While LSTM and GRU units improve RNN’s performance with longer sequences, certain tasks, like neural machine translation, require even more power to work properly. An attention mechanism allows the decoder to focus on specific parts of the input sequence to properly produce the next output.

Training the Encoder-Decoder Model

The training data consists of sets of input sentences and their respective output sequences. The loss is calculated using cross-entropy loss in the decoder, and the total loss is calculated by averaging the cross-entropy loss per target word. The weights are updated using the gradient descent optimization method.



What is **vocab_size?
---------------------
In the context of Natural Language Processing (NLP), the vocabulary size refers to the total number of unique words or tokens present in the dataset 2.

For instance, if you have a corpus of English texts, the vocabulary size would be the count of unique words across all the texts. Each unique word is assigned a unique index, which is used in the embedding layer of the model to convert the words into numerical vectors that the model can understand 1.

In the context of the TensorFlow example provided earlier, vocab_size would be the number of unique words in your dataset. It's used to define the size of the embedding layer, which should match the number of unique words in your vocabulary.

Here's how you might calculate vocabulary size:

from collections import Counter

# Assuming `sentences` is a list of sentences, where each sentence is a list of words
all_words = [word for sentence in sentences for word in sentence]
vocabulary = list(set(all_words))
vocab_size = len(vocabulary)
1

Keep in mind that the vocabulary size can significantly impact the performance and efficiency of your model. A larger vocabulary size means more unique words to learn and remember, which can lead to longer training times and require more computational resources 3. On the other hand, if the vocabulary size is too small, it might not capture all the nuances of the language, leading to worse performance 


What are **optimizers?
----------------------

list of all optimizers:

Here is a comprehensive list of optimization algorithms used in neural networks:

1> Stochastic Gradient Descent (SGD): 
    > This is the most basic form of gradient descent where we update our weight matrix in the direction of steepest descent as defined by the negative of the gradient. 
    > SGD has three variants: 
        > Batch SGD, 
        > Mini-Batch SGD, 
        > Stochastic SGD.
                                            from keras.optimizers import SGD

                                            opt = SGD(lr=0.01, momentum=0.9)
                                            model.compile(loss='mean_squared_error', optimizer=opt)
        
2> RMSprop: 
    > RMSprop (Root Mean Square Propagation) optimizer is an optimizer that utilizes the magnitude of the recent gradient descents to normalize the gradients. It does so by keeping a moving average of squared gradients.

                                            from keras.optimizers import RMSprop

                                            opt = RMSprop(learning_rate=0.001, rho=0.9, epsilon=None, decay=0.0)
                                            model.compile(loss='mean_squared_error', optimizer=opt)

3> Adagrad: 
    > Adagrad is another optimizer that adapts the learning rate for each weight individually. It's good for dealing with sparse data.
                                            from keras.optimizers import Adagrad

                                            opt = Adagrad(learning_rate=0.01, epsilon=1e-08)
                                            model.compile(loss='mean_squared_error', optimizer=opt)

4> Adadelta: 
    > Adadelta is an extension of Adagrad that seeks to reduce its aggressive, monotonically decreasing learning rate. Instead of accumulating all past squared gradients, Adadelta restricts the window of accumulated past gradients.
                                            from keras.optimizers import Adadelta

                                            opt = Adadelta(learning_rate=1.0, rho=0.95, epsilon=None, decay=0.0)
                                            model.compile(loss='mean_squared_error', optimizer=opt)

5> Adam: 
    > Adam (Adaptive Moment Estimation) is an algorithm that computes adaptive learning rates for each parameter. 
    > It combines the advantages of two other extensions of stochastic gradient descent: 
        > AdaGrad and 
        > RMSProp.
                                            from keras.optimizers import Adam

                                            opt = Adam(learning_rate=0.001, beta_1=0.9, beta_2=0.999, epsilon=None, decay=0.0, amsgrad=False)
                                            model.compile(loss='mean_squared_error', optimizer=opt)

6> Adamax: 
    > Adamax is similar to Adam but uses the infinity norm instead of the second moment, making it more suitable for problems with large amounts of noise.
                                            from keras.optimizers import Adamax
                                            opt = Adamax(learning_rate=0.002, beta_1=0.9, beta_2=0.999, epsilon=None, decay=0.0)
                                            model.compile(loss='mean_squared_error', optimizer=opt)

7> Nadam: 
    > Nadam is a combination of Nesterov Adam optimizer and the Adam optimizer. It is a variant of Adam optimizer with Nesterov momentum.
                                            from keras.optimizers import Nadam
                                            opt = Nadam(learning_rate=0.002, beta_1=0.9, beta_2=0.999, epsilon=None, schedule_decay=0.004)
                                            model.compile(loss='mean_squared_error', optimizer=opt)

8> Mini-Batch Gradient Descent: 
    > This is an improvement over both Stochastic Gradient Descent (SGD) and standard Gradient Descent. 
    > It updates the model parameters after every batch. The dataset is divided into various batches and after every batch, the parameters are updated.

9> AdaDelta: 
    > AdaDelta is an extension of Adagrad that seeks to reduce its aggressive, monotonically decreasing learning rate. Instead of accumulating all past squared gradients, AdaDelta restricts the window of accumulated past gradients. It takes an exponentially decaying average of squared gradients and updates the parameters accordingly.

10> AdaMax: 
    > AdaMax is a variant of Adam based on the infinity norm. It replaces the root mean square operation in Adam with the infinity norm to achieve the same benefits of Adam but with a simpler implementation.

11> Gradient Descent with Momentum: 
    > This is a variant of the standard gradient descent algorithm that adds a fraction of the direction of the previous step to the current step. This helps to accelerate the convergence in the relevant direction and dampens oscillations.
                                            from keras.optimizers import SGD
                                            opt = SGD(lr=0.01, momentum=0.9)
                                            model.compile(loss='mean_squared_error', optimizer=opt)


12> Nesterov Accelerated Gradient: 
    > This is another variant of the standard gradient descent algorithm that includes a "lookahead" term, allowing it to converge faster and avoid local minima 1.
                                            from keras.optimizers import SGD
                                            opt = SGD(lr=0.01, momentum=0.9, nesterov=True)
                                            model.compile(loss='mean_squared_error', optimizer=opt)


13> AdamW: 
    > AdamW is a variant of Adam that decouples the weight decay from the optimization steps. This helps to prevent the optimization from being dominated by the weight decay.
                                            from keras.optimizers import Adam
                                            opt = Adam(weight_decay=0.01)
                                            model.compile(loss='mean_squared_error', optimizer=opt)

14> Ftrl: 
    > Ftrl (Follow-the-regularized Leader) is an optimization algorithm developed by Google for large scale machine learning. It is especially effective for tasks involving large sparse datasets 1.
                                            from keras.optimizers import Ftrl
                                            opt = Ftrl()
                                            model.compile(loss='mean_squared_error', optimizer=opt)

15> Amsgrad: 
    > Amsgrad is a variant of Adam that corrects the issue of slow convergence in Adam. It does so by keeping track of the maximum gradient value seen so far and uses that to update the learning rate 1.
                                            from keras.optimizers import Adam
                                            opt = Adam(amsgrad=True)
                                            model.compile(loss='mean_squared_error', optimizer=opt)

DIFFERENT TYPES OF RNN:
-----------------------
1> Many to Many --> it means many input and many output as well
2> Many to One-->  it means we pass many input to our RNN and get single output as result , example : sentiment analaysis 
3> One to manay--> it means we pass one input and it generated multiple output, example : music geneation 


Vanishing Gradient and exploding gradient:
------------------------------------------

Vanishing gradient: 
-------------------
    > As number of hidden layers grow, gradient becomes very small and weights will hardly change. This will hamper the learning process.
    > Vanishing gradient problems is more prominent in very deep neural networks.


Vanishing Grandient problem in RNN:
-----------------------------------
with traditional RNN:

if we will pass a sentence it always errase from the memory beacuse of big collection of word, here in this case vanishing gradient problem is more promient. To solve this problem we introduce:
    1> LSTM
    2> GRU
    These two are advance RNN.


1> LSTM:   URL: to learn LSTM better : https://colah.github.io/posts/2015-08-Understanding-LSTMs/
   -----

LSTM:
-----
    > 3 Gates: Input, Output, forget
    > More accurte on longer sequence, less efficient.
    > Invented in 1995-1997

    import keras
    from keras.models import Sequential
    from keras.layers import GRU, LSTM
    import numpy as np

    # define model where LSTM is also output layer
    model_2 = Sequential()
    model_2.add(LSTM(1, input_shape=(50,1)))
    model_2.compile(optimizer='adam', loss='mse')

GRU: 
----
    > 2 Gates: reset , update
    > More efficient computationwise getting more popular
    > Invented in 2014

    import keras
    from keras.models import Sequential
    from keras.layers import GRU, LSTM
    import numpy as np

    # define model where GRU is also output layer
    model_1 = Sequential()
    model_1.add(GRU(1, input_shape=(20,1)))
    model_1.compile(optimizer='adam', loss='mse')



Bidirectional RNN:
------------------
Name Entity Recognition:
-----------------------
A Bidirectional Recurrent Neural Network (BRNN) is a type of Recurrent Neural Network (RNN) that processes input data in both forward and backward directions. This dual processing allows the network to capture information from both the past and future contexts when making predictions, which can significantly improve the model's accuracy.

In a BRNN, the input data is passed through two separate RNNs: one processes the data in the forward direction, while the other processes it in the reverse direction. The outputs of these two RNNs are then combined in some way to produce the final output. One common way to combine the outputs of the forward and reverse RNNs is to concatenate them. Other methods, such as element-wise addition or multiplication, can also be used.

The working of a BRNN involves several steps:

> Inputting a sequence: 
    > A sequence of data points, each represented as a vector with the same dimensionality, are fed into a BRNN. The sequence might have different lengths.

> Dual Processing: 
    > Both the forward and backward directions are used to process the data. On the basis of the input at that step and the hidden state at step t-1, the hidden state at time step t is determined in the forward direction. The input at step t and the hidden state at step t+1 are used to calculate the hidden state at step t in a reverse way.

> Computing the hidden state: 
    > A non-linear activation function on the weighted sum of the input and previous hidden state is used to calculate the hidden state at each step. This creates a memory mechanism that enables the network to remember data from earlier steps in the process.

> Determining the output: 
    > A non-linear activation function is used to determine the output at each step from the weighted sum of the hidden state and a number of output weights. This output has two options: it can be the final output or input for another layer in the network.

> Training: 
    > The network is trained through a supervised learning approach where the goal is to minimize the discrepancy between the predicted output and the actual output. The network adjusts its weights in the input-to-hidden and hidden-to-output connections during training through backpropagation 


Covnerting word to numbers| word embedding:
-------------------------------------------
> Issue with options available:
    >Option 1:                                                                                                              not valid to capture emotion
        > Assiging unique numbers is problematic task beacuse They don't capture relationship between words.

    > Option 2:                                                                                                             not valid to capture emotion
        > one hot encoding 
            > Dont capture relationship between words
            > computationally in-efficient.

    > Option 3:                                                                                                             valid to capture emotions
        > word embedding:                                                                                                --------------------------------
            Some of the popular techniques for generating word embeddings include : 
            1 > TF IDF 
            2 > Word2Vec
            3 > GloVe (Global Vectors) 
            4 > FastText
            5 > ELMo (Embeddings from Language Models)
            
Word embedding: valid to capture emotions:
---------------------------------------------
How can we capture similarity between two words?

    > Word embedding is a technique used in natural language processing (NLP) that represents words as numbers (specifically, real-valued vectors) so that a computer can work with them 5. This approach allows words with similar meanings to have a similar representation, which is beneficial for machine learning algorithms that analyze text data.

    > Each word is represented by a real-valued vector, often tens or hundreds of dimensions. This is contrasted to the thousands or millions of dimensions required for sparse word representations, such as a one-hot encoding 2. The vector values are learned in a way that resembles a neural network, and hence the technique is often lumped into the field of deep learning.

    > Word embeddings can be generated using various methods, including language modeling and feature learning techniques. These methods map words or phrases from the vocabulary to vectors of real numbers 1. Some of the popular techniques for generating word embeddings include Word2Vec, GloVe (Global Vectors), FastText, and ELMo (Embeddings from Language Models).

    > Word embeddings offer several advantages over traditional approaches to representing words in natural language processing. They allow for efficient computation and storage, and they can capture semantic relationships between words more effectively than sparse vector techniques 5. However, they also have some disadvantages. Training word embeddings can be computationally expensive, particularly when using large datasets or complex models. Furthermore, word embeddings are only as good as their training data, and they may struggle with words that have the same spelling but different meanings (homographs)


More on word embedding:
-----------------------
Creating word embeddings can be done in both supervised and unsupervised ways. Here are some of the common methods:

> Unsupervised Methods: 
    > These methods generate word embeddings without using any labeled data. The most common unsupervised method is Word2Vec, which uses a shallow, two-layer neural network to learn word associations from a large corpus of text. It captures the context of a word in a document, semantic and syntactic similarity, relation with other words, etc. 
    > There are two main architectures: 
        1> Continuous Bag of Words (CBOW) and 
        2> Skip-Gram.
    > Unsupervise technique for embedding:
        > word2Vec
        > glove
        
> Supervised Methods: 
    > These methods generate word embeddings using labeled data. An example of a supervised method is BERT (Bidirectional Encoder Representations from Transformers), which uses an attention mechanism for generating high-quality word embeddings that are contextualized. When the embedding goes through the training process, they are passed through each BERT layer so that its attention mechanism can capture the word associations based on the words on the left and those on the right.

Note that while BERT is typically seen as a supervised method, it can also be used in an unsupervised manner for tasks like clustering or dimensionality reduction.


* End to end implementation of word2Vec in <Activation_function.ipynb> file with explaination  












