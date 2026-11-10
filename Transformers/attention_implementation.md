# Practice attention implementaion

## Self-attention in real worls


In contrast to toy example in the previous article in real transformer implementation attantion is not directly caclulated to
we do embeddings adjustments not by changing the original matrices, but by attaching weigths to  K Q V matrices(which are initially copied from embeddings matrix), so 

Q = initial embeddings x Learnable Weights Q

K = initial embeddings x Learnable Weights K

V = initial embeddings x Learnable Weights V

![Linear layer: from input embeddings to Q, K, V](img/linear_x_to_kqv.png)





## Masked Attention implementation

From the previous post we can remember that we adjust each word embedding to a phrase content by 
- first, calculation pairwise similarity between all words in a phrase
- scaling and normalizing it by dividing and softmaxing
- modify each feature (aka coordinate) by summing all word coordinates weithed by its similarity to a given word

That is all right, with one nuance. 
One way of foundational model training in generative settings is about to predict next token based on previous tokens, but if we modify embeddings based on all words in a sentence we kind of violate this idea. So, to be consistent at every time step we have to mask all future tokens from any similarity etc calculations, so, predicting next token we have  to only relay on the past tokens.

Here we show how to do it in computationally efficient way.

- **pairwise matrix**: First of all we need to compute pairwise dot-product similarity matrix as usial, but do not softmax it
- **create lower triangular matrix**: Create a lower triangular matrix, so later on we can use it to mask future token
- **do masking**
- **take final softmax**

![Masking future token](img/masking.png)


## Multihead Attention and Head Size

разница между self-attention and multihead attention в том что

- мы используем много матриц K, Q and V а потом concatenate результаты от каждого head - то есть вытягиваем в линию -  The feed-forward layer is not expecting eight matrices – it’s expecting a single matrix (a vector for each word). So we need a way to condense these eight down into a single matrix.
- но потом используем Linear layer чтобы сжать размерность в исходную
- How do we do that? We concat the matrices then multiply them by an additional weights matrix WO



![Multi head attention](img/multi_head.png)




## implementation tricks: FlashAttention
Standard attention requires storing large intermediate matrices (like the attention scores and softmax values), which consume a lot of memory, especially for long sequences.

FlashAttention uses a memory-efficient algorithm to avoid storing these intermediate matrices, significantly reducing memory overhead.



## Cross-Attention
Cross-Attention is very similar to Self-Attention, but with one important difference: instead of calculating attention between words within the same phrase, it calculates attention between two different sequences.

For example, imagine we have two sequences: an English sentence and its French translation. When generating the French translation, each word in the decoder can attend to all words in the original English sentence. This allows the model to determine which parts of the input sentence are most relevant when generating the next word.

Technically, the main difference is that Queries (Q) come from one sequence, while Keys (K) and Values (V) come from another sequence. The Query represents what information we are looking for, while Keys and Values represent the information available from the other sequence. The attention mechanism calculates how relevant each element of the second sequence is to each element of the first sequence and uses these weights to construct new, context-aware representations.

The mathematical formula remains the same

Важный нюанс: Cross-Attention не обязательно работает между двумя текстовыми последовательностями. Например, в мультимодальных моделях одна последовательность может представлять текст, а другая — изображение. Тогда текстовые Query обращаются к визуальным Key и Value.