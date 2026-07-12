# Classic NLP (Natural Language Processing)




[Natural Language Processing - Tokenization (NLP Zero to Hero - Part 1)](https://www.youtube.com/watch?v=fNxaJsNG3-s&list=PLQY2H8rRoyvzDbLUZkbudP-MFQZwNmU4S)

### 1 - Tokenization : 

+ ###### Character-Level Tokenization

+ Instead of splitting a sentence into **words**, the text is split into **individual characters**  using ***ASCII***.

![[Pasted image 20260712230612.png|312]]



+ In Natural Language Processing (NLP), computers do not understand words the way humans do. The first step is **tokenization**, where a sentence is split into individual words (called **tokens**).

![[Pasted image 20260712231907.png|345]]

+ the two sentences are almost identical:

```
I love my ...
```

The only difference is the last word:

- dog → ***ID 004**
- cat → ***ID 005***

Each word in the **vocabulary** is assigned a **unique numerical ID**.

+ *Example :* This example demonstrates how the **Tokenizer** in TensorFlow/Keras converts words into unique numerical IDs.

```Python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras.preprocessing.text import Tokenizer

senteces = ['I love my dogs', 'I love my cats', 'you love my dog']
tokenizer = Tokenizer(num_words = 1000) # num_words=1000 means the tokenizer can keep up to 1000 of the most frequent words.
ff = tokenizer.fit_on_texts(senteces)
word_index = tokenizer.word_index # Returns a dictionary that maps each word to its integer ID.
print(word_index)
```

+ *Output :*

```
{'love': 1, 'my': 2, 'i': 3, 'dogs': 4, 'cats': 5, 'you': 6, 'dog': 7}
```


+ Try the code : [Bitly | bit.ly/346Z4iO](https://bit.ly/tfw-nlp1)
