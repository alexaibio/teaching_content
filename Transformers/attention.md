# Self-Attention mechanism for Transformers explained.

## Embeddings
Embedding is a widely known technique used to compress high-dimensional vectors of features into smaller, fixed-size vectors while preserving the relative distances between the original vectors.

For exmaple, being in NLP domain we can imagine we need to compare how one piece of text is simiar to another. 
The common technic to represent a text in machine learning is Bag Of Words (BofW). The idea is to simply count words in the text and then represent this text as one-dimensional vector of lenths equal to vocabulary (list of all possible words) and adding a number of words to an appropriate position in this vector.

It is easy to imagine that the lenth of such vector might easily exceed 10000 or so (since potentially might be 10000 english words), that makes operation on this vector not so convinient, espesially taking into account that the vector might be extreemly sparse. On top of that each texts might have different number of words, so vector might potentially have different size which will make hard to calculate the distance.
One of manipulation we might do with those vectors is a distance (similarity) calculation and embeddings have a nice property of similar by meaning words are close to each other, it is actually a third important property of embedding vectors

So, it would make sence make them fixed in size and reduce that size to some asseptable valuelest say 512 or 256. 

That operation of representing long vector with shorter one is called embedding and result in vectors of fixed size.

There are many technics to create embeddings, for example
- Word2Vec
- Matrix Factorization
- GloVe
- etc

But they all are kind of "fixed" embeddings, so once we have text and calculated embedding for every single word in a text they are fixed, we are not changing it. 

But in reality the meaning of the word might be sligtly changing depending on context. For example the meaning of apple in context of fruits is different from apple in context of mobile phone vendors.

Attention is exactly mechanism to solve this problem of variation of embedding depending on context.

Lets furure out how it works step by step

## Input word embeddings
For example we have a sentence of 5 words.
Lets assume we already calculated embeddings for all these five words. They might be calculated by some methods above or even have a random initial values and supposed to be trained later. But out assumptions that those embeddings already reflect some relationships between these words, for example the similarity between apple and garden is higher then between apple and phone.
Lets imagine now that  the length of these embeddings is 3. 
So we have an embedding matrix like this

![Initial embeddings table](img/emb1.png)


## One Sentence: Pairwise word similarities, Key, Query
the next step will be to understand dependencies between every word in our sentence. 

Since we have 5 words in our current sentence what we can do is to calculate pairwise similarities between all words.

The simpliest way to define a similarity is a dot-product. For example if we have three vectors,

a = [1  0 0]

b = [0 10 2]

c = [2  0 2]

It is obvios that according to dot product similarity the A vector is highly similar to itself

dot(a,a) = 1 * 1 + 0 * 0 + 0 * 0 = 1

A is more similar to C then to B becuase A and B have a similar first feature 

dot(a,b) = 1 * 0 + 0 * 0 + 0 * 2 = 0

dot(a,c) = 1 * 2 + 0 * 0 + 0 * 2 = 2

A nice way to calculase all pairwise similarities at once for all words is to multiply the whole embedding matrix by itself. 

In attention paradigm those two matrices are called **K (keyes)** and **Q (queries)** but in fact they are the same matrices. 

I can speculate that the idea behind this names was like we call every word a Key and Query it with every word for similarity, but this is just a speculation

So, we can nicely write this matrix multiplication as 

Q*K^T

or vizualize it as follows to have a pairwise similrity matrx among all words in our sentence
![Pairwise similarity matrix](img/pairwise.png)


## Technical tricks: scaled and softmax normalized similarity

The dot-product similary has one drawback, it havily influenced by absolute values of features and by length of embedding vectors to compare. 
To partially aleviate this issue a scaled dot-product is used.

Scaled dot product is nothing more them regular dot product but diveded by square root of length od embedding. So it because less dependent on length of embedding vector itself.

In our case we have embeddings of dimension 3 and the similarity between Apple and Apple are

(apple, apple) = (5 * 5 + 2 * 2 + 0 * 0) / sqrt(3) = 16.74

and much less between apple and phone

(apple, phone) = (5 * 0 + 2 * 5 + 0 * 0) / sqrt(3) = 5.77

note that we divide by square root of embedding dimensions length because embeddings are usually a pretty long vector, it might be 512 or 1024, so the dot product tends to be very large in this case, we we kind of scale down those similariry numbers to make it more tracktable

Another trick we would like to do with embedding vectors is to take a softmax on them, which essensially make the whole vector sum up to 1, i.e normalize it. 

note that softmax is applied across each row, not column because
- in the attention mechanism, each word (or token) in the input sequence is attending to all other words.
- The row-wise softmax is done to normalize the attention weights for each query (which corresponds to each row) with respect to all the keys (corresponding to columns).
- This results in the attention scores across the key dimension summing to 1 for each query. Effectively, it means "how much attention" each query pays to all the other tokens in the sequence.

so we can summarize all above in this matrix formula

![Calculation scaled dot-product similarity matrix normalized by softmax](img/softmax_mult.png)

or vizualized

![scaled dot-product with softmax vizualization](img/pairwise_scaled.png)

Note that matrix is not symmetric in contrast to pairwise similarity matrix. 
The resulting matrix does not have to be symmetric. In fact, it often won’t be symmetric in the general attention mechanism because the relationship between words(tokens) is usually asymmetric. For example, one word might attend more to another than vice versa, depending on the context.



## Generate embeddings adjusted to a phrase
So, what we have till now
- a sentence
- initial embeddings for each word in this sentence
- calculated similarity matrix for all words in the sentence

What we are going to do next is to adjust our initial embedding such that they reflect somehow the fact that they are in the same phrase.

So that, we multiply our pairvise similarity matrix on our initial embeddings matrix (now we call it V, values, but again it is essentially the same input embedding table).

As a result we have and adjusted embedding table and can use them futher for any task, like classification or futher down in our transformer architecture.

Let's broke it down to numbers.

![Adjusted Embeddings](img/adjusted_embed.png)

For Apple we have initial embeddings: [5 2 0]


We will calculate new adjusted embeddings as follows.

For fruit feature:    dot([1 0 0 0 0], [5 0 0 2 0]) = 0
For computer feature: dot([1 0 0 0 0], [2 0 5 0 0]) = 2
for language feature: dot([1 0 0 0 0], [0 5 0 0 6]) = 0

and so on.

In our case the values of features did not change much dur to hature of our initial embeddings, but in reality the new adjusted embeddings will reflect the sentence context better then our initial general embeddings.

So, after our self attentionrecalculation we will have slightly different embeddings

The embeddings are adjusted according to how much attention they give to each other. For example, the word "is" now has a stronger association with the "language" embedding (since the value for that dimension has been amplified).

NOTE/Explanation
In self-attention, when we calculate new embeddings by performing a weighted sum over values, we're essentially combining the meaning of different words based on the relationships between them that have been determined by the attention mechanism.


## What next
Lets understand how embeddings and self-attention adjustments work across sentences, especially in the context of training a Transformer.


It is important to understand that when you apply self-attention and adjust the embeddings for a particular sentence, this adjustment is only temporary for that specific forward pass

- Input Embeddings: At the start, every word (or token) in your sentence is converted into a vector representation (embedding). These embeddings are static; they are a fixed part of the model's learned parameters after training. For example, in a trained model, the embedding for "Apple" or "phone" is constant across all sentences.

- Self-Attention Mechanism: During the forward pass of a Transformer, the self-attention mechanism dynamically adjusts these embeddings based on the relationships (similarity or attention) between words in the sentence only during that pass.

So, the adjustments you make using self-attention (the values you compute after multiplying the softmax scores with the value matrix 𝑉 are specific to that sentence and do not carry over to the next sentence.


## Attention and Transformer training
- Embeddings are learned: The embeddings themselves are learned during training. Each word or token in the vocabulary has an associated embedding vector that is updated by backpropagation. The idea is that words or tokens with similar meanings (based on the training data) will have embeddings that are close to each other in the vector space.

- Self-Attention Mechanism: The self-attention mechanism learns the best way to weight relationships between words in a sentence. During the forward pass, the attention mechanism computes pairwise relationships between words and adjusts their embeddings based on these relationships.

- Forgetting Adjustments: Once the forward pass is done and the loss is computed, the specific adjustments made for that sentence during self-attention are forgotten. The only thing that persists are the learned parameters (such as embeddings and attention weights) which get updated after backpropagation.

## Attention and inference
Once the model is trained:

- The learned embeddings (which have been optimized during training) are static and are not modified during inference.
- For each new sentence, the self-attention mechanism dynamically adjusts the embeddings temporarily based on the sentence structure, computes the output (such as predicted next word, classification, etc.), and then moves on to the next sentence.




## ----- TBD ------> Generate many different embeddings based on initial one
As I previously mentioned the embedding for each word might might vary depending on a sentence. But adjusting embeddings via training is very costly process. We might use some tricks to generate such new slightly modified embeddings via linear transformations such that it accounts for the sentence context somehow.

Namely we can use similarity information between all words (calculated above) to make these new embeddings somehow meaningful.

So, the idea behind this is as follows.
- We have an initial embedding for Apple 
- we can calculate new embedding for Apple as a sum of embeddings of all the other words in the sentence but weighed by the similarity of Apple with each of the word

For example, for Apple = [5 2 0] we can calculate a new embedding (based on a given sentence) as follows

new Apple embedding = 

  - Apple[5 2 0] * sim(Apple, Apple) + 
  - is[0 0 5] * sim(Apple, is) + 
  - phone[0 5 0] * sim(Apple, phone) + 
  - The[0 0 6] * sim(Apple, the) 
=
  - Apple[5 2 0] * 1 +
  - is[0 0 5] * 0 +
  - phone[0 5 0] * 0.0002 + 
  - The[0 0 6] * 0
= [5 2 0] + [0 0.001 0] = [5 2.001 0]

That operation will generate a new apple embedding which will encorporate information about all word in this sentence, saying for example that Apple is used in the same sentence with garden and phone.

![Full attention formula](img/attention.png)





