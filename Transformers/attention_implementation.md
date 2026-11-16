# Attention implementaion flavours


## Self-attention in real world
In our previous post we explained a simplified version of self-attention.

It is simplified because we calculated attention weights directly from the original embedding matrix by computing pairwise similarities between embeddings. It might seem that there is no learning here.

However, in real Transformer implementations, three separate learnable weight matrices are used: W_Q, W_K, and W_V.
So, Q, K, V are not copied from the input embeddings X but are result of the multiplications.

Q = X*W_Q,  K = X*W_K,  V = X*W_V

The initial embedding matrix X is learned first (downstream before attention) in a separate embeddings layer (with positioning information).

Then thise 3 weight matrices allow the model to learn three different representations of the input embeddings, each serving a specific purpose:

Q and K allow the model to learn which tokens are relevant to each other.

V allows the model to learn what information should be passed between tokens.



<img src="img/linear_x_to_kqv.png" alt="Linear layer: from input embeddings to Q, K, V" width="70%">


## Cross-Attention
Cross-Attention is very similar to Self-Attention, but with one important difference: instead of calculating attention between words within the same phrase, it calculates attention between two different sequences.

For example, imagine we have two sequences: an English sentence and its French translation. When generating the French translation, each word in the decoder can attend to all words in the original English sentence. This allows the model to determine which parts of the input sentence are most relevant when generating the next word.

Technically, the main difference is that Queries (Q) come from one sequence, while Keys (K) and Values (V) come from another sequence. The Query represents what information we are looking for, while Keys and Values represent the information available from the other sequence. The attention mechanism calculates how relevant each element of the second sequence is to each element of the first sequence and uses these weights to construct new, context-aware representations.




## Multihead Attention and Head Size

Remember that a simple one-head attention calculates the final embedding with respect to the relation between words in whole sentence. It does it from one point of view only. 
What we can do is to take a look on the sentence from several points of views, i.e train several sets of V,K,Q matrices, so now several realtionships might be captired, for example.

Head 1: semantic relationships between Apple and Fruit.
Head 2: context relationships between Apple and Phone.

That trick is called multi-head attention. The overall schema is as follows.
<img src="img/multi_head_attention.png" alt="Multi head attention" width="100%">

(Courtesy https://sebastianraschka.com/llm-architecture-gallery/mha/)

But now in the output we have several embedding vectors instead of one. To compress them back to a size on one embedding we concatenate all those vectors and then use an additional linear layer (with weight matrix WO) to compress them back.  


So, the general schema of multi head attention is as follows.

<img src="img/multi_head.png" alt="Multi head attention" width="60%">

But one more complication: in a real transformer a bit different contatination schema is used.
For example if we have

d_{model} = 512

num_heads = 8

Instead of having each head produce full 512 embedding vector, we can generate a smaller output called Head dimension =  512/8.
In that case the matric dimension is significantly reduced.


## How to Mask Attention

### CLM - Causal Masking (Autoregressive) Attention (GPT-style) mask
GPT, LLaMA, Mistral - predict token

From the previous post we can remember that we adjust each word (token) embedding to a phrase content by 
- first, calculation pairwise similarity between all words (tokens) in a phrase
- scaling and normalizing it by dividing and softmaxing
- calculate new embeddings or contextualized representations by attention formula


That is all right, with one nuance. 
One way of foundational model training in generative settings is about to predict next token based on previous tokens, but if we modify embeddings based on all words (tokens) in a sentence we kind of know the future. So, to isolate future from the model we have to mask all future tokens. So, predicting next token we have  to only relay on the past tokens.

Here is an example of how to do it in computationally efficient way.

- **pairwise matrix**: First of all we need to compute pairwise dot-product similarity matrix as usial, but do not softmax it
- **create lower triangular matrix**: Create a lower triangular matrix, so later on we can use it to mask future token
- **do masking**
- **take final softmax**

![Masking future token](img/masking.png)


### Padding Mask (Key Padding Mask) - variable length
This kind of masking allows working with sequences of different length.

Lets imagine we combine a batch from two sentences
- "I love machine learning"
- "I love AI"

To make both phrases to have the same length we do padding - add a spesial PAD token to the and of second phrase.
So, in order to forbid the model to take into account those PADs, we multiply attention matrices by Padding Mask.



### MLM: Bidirectional (Full) Attention + MLM (Masked Language Modeling)
BERT, RoBERTa
It is no always neccesary to mask future tokens. 
For example in BERT style models (decoder only) our goal is not to generate next token, but just predict token (to create embedding for example). In that case we mask lets say 15% of tokens and ask model to reconstract them and for that reconstraction we can use all tokens not only past ones. 

Note, that padding mask still can be used


### Sliding window attention and attention hierarhy
Both Causal and Full attention might be applied in a window to save on computations.

In general we can classify off types of attention as follows
- Dense Attention: Full / Bidirectional or Causal.
- Sparse Attention: Sliding Window, Dilated, Block Sparse.
- Training objectives: Autoregressive Prediction, MLM.







## implementation tricks: FlashAttention
Standard attention requires storing large intermediate matrices (like the attention scores and softmax values), which consume a lot of memory, especially for long sequences.

FlashAttention uses a memory-efficient algorithm to avoid storing these intermediate matrices, significantly reducing memory overhead.



