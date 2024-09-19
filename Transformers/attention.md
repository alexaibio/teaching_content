# Attention mechanism explained from zero.

Embedding is widely known technics to compress long vector of features into a much smaller vector of a fixed size. 

For exmaple, being in NLP domain we can imagine we need to compare how one piece of text is simiar to another. 
The common technic for that is Bag Of Words (BofW) when we simply count how name of every particular words there in yhi text and then boil down text into one dimensional vector of lenths equal to vocabulary (list of all possible words) and adding a number of words to an apprprite position in this vector.

It is easy to imagine that the lenth of such vector might easy be 10000 or so, that makes operation on this vector not so convinient. On top of that each text might have a different number of words, so vector will have different size which will make impossible the distance calculation etc.
By opration is usually mean a distance (similarity) calculation and embeddings have a nice property of similar by meaning words are close to each other, it is actually a third important property of embedding vectors

So, it would make sence first, to make then a fixed size and second reduce that size to lest say 512 or 256. 

That operation of reducsing (compressing) size is called embedding and result in vectors of fixed size.
There are many technics to create embeddings, for example
- Word2Vec
- Matrix Factorization
- GloVe
- etc

But they all are kind of "fixed" embeddings, so once we have text сщкзгы and calculated embedding for every single word in a text they are fixed, we are not changing it. 

But in reality the meaning of the word might be sligtly changing depending on context. For example the meaning of apple in context of fruits is different from apple in context of mobile phone vendors.

Attention is exactly mechanizm to  solve this problem of variation of embedding depending on context.

Lets furure out how it works step by step

## Start: initial embeddings
For example we have a sentence of 5 words.
Lets assume we already have embeddings for all these five words and lets imagine the length of these embeddings is 3. So we have an embedding matrix like this

![Initial embeddings table](img/emb1.png)


## Pairwise similarities, Key, Query
the next step will be to understand dependencies between every word in our sentence. Since we have 5 words in our current sentence what we can do is to calculate pairwise similarities between all words.

The simpliest way to define a similarity is a dot-product. For example if we have three vectors,
a = [1  0 0]
b = [0 10 2]
c = [2  0 2]

It is obvios that according to dot product similarity the A vector is highly similar to itself 
dot(a,a) = 1*1 +0*0 + 0*0 = 1

A is more similar to C then to B becuase A and B have a similar first feature 
dot(a,b) = 1*0 + 0*0 + 0*2 = 0
dot(a,c) = 1*2 + 0*0 + 0*2 = 2

A nice way to calculase all pairwise similarities at once for all words is to multiply the whole embedding matrix bu itself. 

In attention paradigm those two matrices are called K (keyes) and Q (queries) but in fact it is the same matrix. I can speculate that the idea behind this names was like we call every word a Key and Query it with every word for similarity, but this is just a speculation

So, we can nicely write this multiplication as 

Q*K^T

or vizualize it as follows
![Pairwise similarity matrix](img/pairwise.png)


## Similarity technical tricks, scaled and softmax normalized

The dot-product similary has one drawback, it havily influenced by absolute values of features and by length of embedding vectros to compare. 
To partially aleviate this issue a scaled dot-product is used.

Scaled dot product is nothing more them regular dot product but diveded by square root of length od embedding. So it because less dependent on length of embedding vector itself.

In our case we have embeddings of dimension 3 and the similarity between Apple and Apple are

(apple, apple) = (5*5 + 2*2 + 0*0) / sqrt(3) = 16.7

and much less between apple and phone

(apple, phone) = (5*0 + 2*5 + 0*0) / sqrt(3) = 5.8

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

Note that matrix is not symmetric in contrast to pairwise similarity matrix because
The resulting matrix does not have to be symmetric. In fact, it often won’t be symmetric in the general attention mechanism because the relationship between tokens is usually asymmetric. For example, one word might attend more to another than vice versa, depending on the context.


## Generate many different embeddings based on initial one
As I previously mentioned the embedding for each word might might vary depending on a sentence. But adjusting embeddings via training is very costly process. We might use some tricks to generate such new slightly modified embeddings via lenes transformations such that it accounts for the sentence context somehow.

Namely we can use similarity information between all words (calculated above) to make these new embeddings somehow meaningful.

So, thr idea behind this is as follows.
- We have an initial embedding for Apple 
- we can calculate new embedding for Apple as a sum of embeddings of all the other words in the sentence but weighed by the similarity of Apple with each of the word

For example, for Apple = [5 2 0] we can calculate a new embedding (based on a given sentence) as follows

new Apple embedding = Apple[5 2 0] * sim(Apple, Apple) + is[0 0 5]* sim(Apple, is) + phone[0 5 0]* sime(Apple, phone) + The[0 0 6]* sim(Apple, the) 






