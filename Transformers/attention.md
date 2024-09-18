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

But they all are kind of "fixed" embeddings, so once we have text and calculated embedding for that text (or a single word) it is fixed, we are not changing it. 

But in reality the meaning of the word might be sligtly changing depending on context. For example the meaning of apple in context of fruits is different from apple in context of mobile phone vendors.
