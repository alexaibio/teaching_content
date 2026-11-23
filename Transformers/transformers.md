# "Attention is all you need" transformer architecture

## Intro
The architecture described in this article does a translation from one language to another. It consists of encoder and decoder parts, both of them contains several block with attention inside.
Lets illustrate how it works in general: how to train and how to do inferences.

Lets start from understanding how tje separate blocks are working.

Encoder
- input embedding
- positional encoding
- multiple multi head attention blocks

Decoder
- why encoder-decoder architecture?
- masked multi head attention
- cross attention


<img src="img/all_you_need_2.png" alt="Attention is all you need architecture" width="80%">


## Blocks
Что делает Encoder?
1. Token IDs преобразуются в embeddings.
2. Добавляется positional encoding.
3. Проходят через Multi-Head Self-Attention.
4. Проходят через Feed Forward Network.
5. Всё повторяется для каждого Encoder layer.
Note: Encoder видит всё предложение целиком.

Decoder устроен немного сложнее Encoder.

В каждом Decoder layer есть три основных блока:
1. Masked Multi-Head Self-Attention.
2. Encoder-Decoder Attention (Cross-Attention).
3. Feed Forward Network.

Main differencies with encoder:
- Attetion is masked (Causal)
- There is a cross-attention too

There are Labels also. Куда подаётся Label?

Label вообще не передаётся ни Encoder, ни Decoder.

Он нужен на этапе Training для вычисления Loss. Обычно используется CrossEntropyLoss.


## Transient nature of Attention
Lets understand how embeddings and self-attention adjustments work across sentences, especially in the context of training a Transformer.

It is important to understand that when you apply self-attention and adjust the embeddings for a particular sentence, this adjustment is only temporary for that specific forward pass

- Input Embeddings: At the start, every word (or token) in your sentence is converted into a vector representation (embedding). These embeddings are static; they are a fixed part of the model's learned parameters after training. For example, in a trained model, the embedding for "Apple" or "phone" is constant across all sentences.

- Self-Attention Mechanism: During the forward pass of a Transformer, the self-attention mechanism dynamically adjusts these embeddings based on the relationships (similarity or attention) between words in the sentence only during that pass.

So, the adjustments you make using self-attention (the values you compute after multiplying the softmax scores with the value matrix 𝑉 are specific to that sentence and do not carry over to the next sentence.


### Attention and Transformer training
- Embeddings are learned: The embeddings themselves are learned during training. Each word or token in the vocabulary has an associated embedding vector that is updated by backpropagation. The idea is that words or tokens with similar meanings (based on the training data) will have embeddings that are close to each other in the vector space.

- Self-Attention Mechanism: The self-attention mechanism learns the best way to weight relationships between words in a sentence. During the forward pass, the attention mechanism computes pairwise relationships between words and adjusts their embeddings based on these relationships.

- Forgetting Adjustments: Once the forward pass is done and the loss is computed, the specific adjustments made for that sentence during self-attention are forgotten. The only thing that persists are the learned parameters (such as embeddings and attention weights) which get updated after backpropagation.

### Attention and inference
Once the model is trained:

- The learned embeddings (which have been optimized during training) are static and are not modified during inference.
- For each new sentence, the self-attention mechanism dynamically adjusts the embeddings temporarily based on the sentence structure, computes the output (such as predicted next word, classification, etc.), and then moves on to the next sentence.



## TODO
Learning happens at two levels:
1. Embedding learning: модель учится создавать начальные представления токенов (X).
2. Attention learning: модель учится преобразовывать X в Q, K, V с помощью обучаемых матриц.
Именно поэтому Transformer способен не просто использовать заранее заданную семантическую близость слов, а самостоятельно научиться определять, какие взаимосвязи важны для конкретной задачи.