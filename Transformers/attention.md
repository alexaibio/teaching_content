# Self-Attention mechanism for Transformers explained.

## Fixed Embeddings

Embedding is a well-known technique used to compress high-dimensional feature vectors into smaller, fixed-size vectors while preserving the relative distances between the original vectors.

To illustrate this concept, let's consider an example from the NLP domain. Suppose we need to compare two texts and determine how similar they are.

The first step is to convert the text into a numerical vector. A common technique for representing text as numbers in NLP is the Bag of Words (BoW) approach. The idea is simple: count the occurrences of each word in the text and represent the text as a one-dimensional vector, where each position corresponds to a word in the vocabulary (the list of all possible words), and the number in that position represents the word count in the given text.

It's easy to see that the length of such a vector can easily exceed 10,000, given that there are potentially over 10,000 words in the English language. This makes working with these vectors inconvenient, especially since they tend to be sparse. Additionally, different texts may have varying vocabulare lengths, resulting in vectors of different sizes, which makes calculating distances between them problematic.

The solution is to compress these vectors in the following way:
- Ensure they are of the same size.
- Compress them into a much smaller size, such as 256 or 512 dimensions.
- Preserve the meaning of the text, meaning all similarities between the texts must be retained.

This process of transforming long vectors into shorter ones while preserving the relative distances is called embedding, which results in vectors of fixed size.

Many techniques exist for creating embeddings, including:
- Word2Vec
- Matrix Factorization
- GloVe
- And others




## Static vs context aware Embeddings

In practice, embeddings are not calculated for the whole text but for each individual word within a text. So, in a given phrase, each word is replaced by its embedding for further manipulation.

However, these pre-calculated embeddings have a significant limitation: they do not account for the context of the phrase — they remain the same in all instances.

For example, consider the phrases:
- "An apple is a fruit."
- "I bought a new Apple phone."

In both cases, the word "Apple" will be represented by exactly the same embedding vector, for example,
$ Apple[5, 0, 0, 2, 0] $

So, once we've generated embeddings for each word in a text, these embeddings are static and do not change.

But as the example above shows, the meaning of the word "Apple" can vary depending on the context.

It would be ideal to have an algorithm that can temporarily adjust the word embedding vectors to fit the context of the phrase in which the word is used. 




## Self - Attention

Self-Attention does excatly that. It is the mechanism used to adjust embeddings based on the specific context of a phrase, allowing the meaning of a word to adapt according to where it is used. This results in embeddings that better capture the true meaning of a word (e.g., "Apple" as a phone versus "apple" as a fruit), improving performance in downstream tasks.

This process is quite similar to how humans understand words in natural language. Many words have the same spelling but completely different meanings, yet we easily interpret them correctly based on the context.

We can schematically represent self-attention as follows.

![Attention idea](img/attention_intro.png)

$$y_i = \sum_j w_{ij} x_j$$

Basically, we substitute our input embeddings $X$ with adjusted embeddings $Y$.

New embeddings are derived from the initial embeddings by summing them with the embeddings of all other words in the given phrase, weighted by an "attention" coefficient represented by the weight matrix $W$
This matrix $W$ essentially captures pairwise similarities between all words in the phrase, scaled and normalized in a way that will be further explained.

In other words, these new embeddings represent each feature as a sum of the same features for all other words in the phrase, weighted by the similarity between the original word and each other word. This weighting coefficient is referred to as the **attention** of one word to another.

This concept may still feel a bit abstract, but let’s illustrate it with an example below.


For the phrase “Apple is a fruit,” the new adjusted embedding for "Apple" would be:

$$Apple = weight * Apple + weight * is + weight * fruit$$

Since the similarity of "Apple" with itself is typically close to one, the initial embedding will still play a central role. However, due to a relatively high similarity between "Apple" and "fruit," the "Apple" embedding will shift in the embedding space slightly closer to "fruit," giving "Apple" a bit more “fruitiness” in this particular context. In other phrases, "Apple" might shift toward "phone" or remain mostly unchanged if there are no words significantly influencing its meaning.

It’s also important to note one key advantage of self-attention: embedding adjustments are achieved through simple matrix multiplication rather than through extensive training (matrix $W$ is calculated, not trained). Thus, there are no parameters requiring training—these weights are derived purely from matrix multiplication without the need for training iterations.


# Working Example
## Start from fixed Input word embeddings
Let's begin with a sentence of five words.

Assume we already have embeddings for each of these five words. These embeddings could have been calculated using methods discussed earlier or might even be initialized with random values, intended to be refined through learning later on.

Our assumption is that these embeddings already capture certain relationships between words; for example, the similarity between "apple" and "garden" is higher than between "apple" and "phone." If embeddings are initialized randomly, this relationship may not hold initially, but as the embeddings are trained, these patterns should emerge over time.

For simplicity, let's set the length of each embedding vector to 3. This gives us an embedding matrix structured as follows:

![Initial embeddings table](img/emb1.png)


## K, Q: Calculate attention weights as pairwise word similarities for one phrase
The first step is to understand the dependencies between each word in our sentence.

For example, given the word "Apple," which other word in the sentence shares the most similar meaning? It might be "Phone" or "Fruit." When interpreting "Apple," we need to pay special attention to those words, while less attention is needed for others like "the" or "is," since they don’t contribute much to the meaning of "Apple."

As we know, each word’s embeddings are trained to reflect the actual meaning, with distances between embeddings representing semantic similarities. So, calculating the similarity between two words gives us an idea of how much they influence each other or whether they belong to the same meaning cluster.

To capture these relationships for the whole context, we calculate the pairwise similarities between all words in a given phrase.

The simplest way to define similarity is by using a dot product. For example, if we have three vectors

$a = [1, 0, 0]$

$b = [0, 10, 2]$

$c = [2,  0, 2]$



According to dot product similarity, vector "a" is highly similar to itself, which makes complete sense:

$$dot(a,a) = 1 * 1 + 0 * 0 + 0 * 0 = 1$$


Vector "a" is more similar to "c" than to "b" because "a" and "c" share a similar first feature, while "a" and "b" do not: 

$$dot(a,b) = 1 * 0 + 0 * 0 + 0 * 2 = 0$$

$$ot(a,c) = 1 * 2 + 0 * 0 + 0 * 2 = 2$$

Then, a convenient way to calculate all pairwise similarities in one step is to multiply the embedding matrix by itself.

In the attention paradigm, these matrices are referred to as **K (keys)** and **Q (queries)**, though in practice, they are often the same matrix.


So, we can nicely write this matrix multiplication as 

$$Q*K^T$$

or vizualize it as follows to have a pairwise similrity matrix among all words in our sentence
![Pairwise similarity matrix](img/pairwise.png)


### Technical Tricks: Scaled and Softmax-Normalized Similarity

The dot product similarity has one drawback: it is heavily influenced by the absolute values of features and by the length of the embedding vector. To partially address this, a scaled dot product is used.

The scaled dot product is simply the regular dot product divided by the square root of the embedding length, making it less dependent on the length of the embedding vector itself.

For example, with embeddings of dimension 3, the similarity between "Apple" and itself is calculated as follows:

$$similarity(apple, apple) = (5 * 5 + 2 * 2 + 0 * 0) / sqrt(3) = 16.74$$

And between "Apple" and "Phone," it is much smaller:

$$ similarity(apple, phone) = (5 * 0 + 2 * 5 + 0 * 0) / sqrt(3) = 5.77 $$


The division by the square root of the embedding dimension helps to scale down the values, which is especially useful when embeddings are large vectors (e.g., 512 or 1024 dimensions), as their dot product can result in high values.

Another useful transformation for embedding vectors is to apply softmax normalization, which ensures that the values in each row sum to 1 along one dimension, normalizing the attention weights across each query (i.e., each row).

Softmax is applied across each row, not each column, for the following reasons:
- in the attention mechanism, each word (or token) in the input sequence is "attending" to all other words.
- The row-wise softmax is done to normalize the attention weights for each query (which corresponds to each row) with respect to all the keys (corresponding to columns).
- This results in the attention scores across the key dimension summing to 1 for each query. Effectively, it means "how much attention" each query pays to all the other tokens in the sequence.

The entire process can be summarized with the following matrix formula


$$\text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)$$

or vizualized:

![scaled dot-product with softmax vizualization](img/pairwise_scaled.png)

Note that, unlike a typical pairwise similarity matrix, this matrix is not symmetric. In fact, the resulting matrix often won't be symmetric in the general attention mechanism, as relationships between words (tokens) are usually asymmetric. For example, "Apple" may depend on "Fruit," but "Fruit" does not depend on "Apple" to the same degree.



## V: Applying Attention and generate new embeddings adjusted to a phrase's meaning

Here's what we've gathered so far:
- A sentence with 5 words (e.g., apple, is, phone, garden, the).
- Initial 3-dimensional embeddings for each word in the sentence.
- A normalized and softmaxed similarity matrix for all words in the sentence. This similarity matrix can be thought of as an "attention" matrix because each row represents how much attention (or similarity) a word (like "Apple") has to each other word in the phrase.

So, now we have that $W$ matrix which we mentioned in the first paragraph.

Now, we might adjust each word’s embedding to reflect the fact that these words co-occur in the same phrase. In other words, if we have "Apple" and "Phone" in the same phrase, we want to shift the default embedding of "Apple" slightly away from "Fruits" and closer to "Phones" in the embedding space.  


How do we do this?

Let’s examine how the attention matrix and initial embeddings interact: 

![Calculation new embeddings, multiplying by V](img/V_new_embeddings.png)

Initially, for Apple we have the following embeddings: 

$$ [ 5 (fruits), 2 (computers), 0 (language)] $$


What we do next is the following
- Start with the "fruitness" of Apple, which is 5.
- Look up similarities for "Apple" with all other words in the sentence. This is the first row of the attention (key/query) matrix:  $[0.99997	0.00000	0.00002	0.00002	0.00000 ]$
- Apple is mostly similar to itself (0.9997) and and has minor similarities to "Phone" and "Garden."
- so we shift apple as a point in embedding space a bit close to Phone and Garden by having a dot product
 $ dot ([0.99997	0.00000	0.00002	0.00002	0.00000 ]  x  [5 0 0 2 0] ) = 4.99986$

Now, Apple’s "fruitness" is still close to 5, but we’ve added a small influence from "Garden" and "Phone," slightly shifting "Apple" toward the embedding clusters of "Garden" and "Phones."

As mentioned initially, this adjustment happens by summing the initial embedding of "Apple" with the weighted contributions of all other embeddings in the phrase. If another word in the phrase has high similarity to "Apple" (like "fruit" or "phone"), it will pull the embedding of "Apple" closer to itself, situating it nearer to the clusters of "fruits" or "phones." 



### Apply the Operation to Entire Matrices: Multiply the Attention Matrix by V

We can perform this operation for all embeddings simultaneously by multiplying our pairwise similarity matrix (the attention matrix) with our initial embeddings matrix (now called V or values). Essentially, this V matrix is the same as our initial input embedding table.

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

This multiplication results in an adjusted embedding table, which can then be passed along in the transformer architecture for further processing.

Let's break down each step in the calculation:

![Adjusted Embeddings](img/adjusted_embed.png)


Each embedding is now adjusted based on the attention it pays to every other word in the sentence. For example, the word "is" may now have a stronger association with the "language" embedding (as seen by the amplified value in that dimension).




# Conclusion

This process allows us to adjust each word's embedding to better reflect the specific meaning within a given phrase.

We achieve this by calculating a "self-attention" matrix, which enables us to weight the original embeddings through matrix multiplication.

An important note is that all of this is done without training—simply through matrix multiplication—making any further training significantly less computationally intensive.


