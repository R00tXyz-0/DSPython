# Classic NLP (Natural Language Processing)




[Natural Language Processing - Tokenization (NLP Zero to Hero - Part 1)](https://www.youtube.com/watch?v=fNxaJsNG3-s&list=PLQY2H8rRoyvzDbLUZkbudP-MFQZwNmU4S)

### 1 - Tokenization : 

+ ###### Character-Level Tokenization

+ Instead of splitting a sentence into **words**, the text is split into **individual characters**.

```
L I S T E N 
↓ ↓ ↓ ↓ ↓ ↓
1 2 3 4 5 6
```

+ In Natural Language Processing (NLP), computers do not understand words the way humans do. The first step is **tokenization**, where a sentence is split into individual words (called **tokens**).

```
i   love  my dog
001 002  003 004

i   love  my cat
001 002  003 005
```

+ the two sentences are almost identical:

```
I love my ...
```

The only difference is the last word:

- dog → ***ID 004***
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




### 2 - Sequencing : 

+ Convert Sentences from words to sequences (ordred listes), with the same sequence of the words in the sentences.

+ This transformation is essential because machine Learning and deep learning models cannot process raw text directly. Instead, they require numerical input.

```
Sentence: "I love my dog"
            ↓ 
Tokenization ["I", "love", "my", "dog"] 
            ↓ 
Vocabulary I → 4 love → 1 my → 2 dog → 3 
            ↓ 
Sequence [4, 1, 2, 3]
```

+ Using Python : 

```python

import tensorflow as tf
from tensorflow import keras
from tensorflow.keras.preprocessing.text import Tokenizer

senteces = ['I love my dogs', 'I love my cats', 'you love my dog']
tokenizer = Tokenizer(num_words = 1000) # num_words=1000 means the tokenizer can keep up to 1000 of the most frequent words.
tokenizer.fit_on_texts(senteces)
word_index = tokenizer.word_index # Returns a dictionary that maps each word to its integer ID.

sequence = tokenize.text_to_sequece(senteces)

print(word_index)
print(senteces)
```

+ *Output :*

```
{'love': 1, 'my': 2, 'i': 3, 'dogs': 4, 'cats': 5, 'you': 6, 'dog': 7} 
[[3, 1, 2, 4], [3, 1, 2, 5], [6, 1, 2, 7]]
```

+ ###### Out-of-Vocabulary : 

+ An **Out-of-Vocabulary (OOV)** word is a word that **does not exist in the tokenizer's vocabulary** because it was never seen during training.

+ During training, the tokenizer builds a vocabulary by scanning all training texts and assigning an integer ID to every unique word.

+ Any new word encountered after training that is not present in this vocabulary is considered an **OOV word**.



+ *Examples :*

```python
test_data = [ 'I love my dogs', 
			'my dog loves my manatee']
			
tokenizer = Tokenizer(num_words = 1000) 
tokenizer.fit_on_texts(senteces)
word_index = tokenizer.word_index
			
test_seq = test_data.texts_to_sequence(test_data)

print(test_seq)
```

+ *Output :*

```
[[4, 2, 1, 3], [1, 3, 1]]
```


+ As we see in the example The tokenizer Simply **ignores every unknown word**, *loves* and *manatee* they ignored. So the problem where the tokenizer ignoring unknown words causes  **loss of information**.

##### The Solution: OOV Token

TensorFlow provides a solution called the **Out-of-Vocabulary token**.

Instead of removing unknown words, we replace them with a special token.

* *Example:*

```python
test_data = [ 'I love my dogs', 
			'my dog loves my manatee']
			
tokenizer = Tokenizer(
    num_words= 1000,
    oov_token="<OOV>"
)


tokenizer = Tokenizer(num_words = 1000) 
tokenizer.fit_on_texts(test_data)
word_index = tokenizer.word_index
			
test_seq = test_data.texts_to_sequence(test_data)

print(test_seq)
```

+ *Output :*

```
{'<OOV>': 1, 'my': 2, 'i': 3, 'love': 4, 'dogs': 5, 'dog': 6, 'loves': 7, 'manatee': 8} 
[[3, 4, 2, 5], [2, 6, 7, 2, 8]]
```

+ The model understands that there is an unknown word at the end of the sentence.
+ If these words were absent from the training vocabulary, a tokenizer without OOV handling would simply remove them.

+ Using an OOV token allows the model to continue processing the sentence without completely losing these positions.

+ ###### Padding Sequence :

+ Padding is a preprocessing technique used in NLP to make all input sequences the same length by adding a special value (usually `0`) to shorter sequences.

+ After tokenization and sequencing, sentences usually have different lengths like : 

+ *Example:* before padding

```python
[[4, 2, 3, 5],
 [4, 2, 3],
 [7, 2, 3, 5, 9, 10]]
```

Since neural networks (RNNs, LSTMs, GRUs, Transformers) expect input tensors with a uniform shape, these sequences cannot be processed together directly.

Padding solves this problem by adding `0`s to shorter sequences.


+ *Use Padding in with to improve the sequence with `0`s*

```python
from tensorflow.keras.preprocessing.sequence import pad_sequences 
padded = pad_sequences(sequences)
```


+ *Example* : After using padding

```Python
[[4, 2, 3, 5, 0, 0],
 [4, 2, 3, 0, 0, 0],
 [7, 2, 3, 5, 9, 10]]
```
+ Some Option in ``pad_sequences`` function : `maxlen`, `truncating`, `padding` etc...
+ for more information about paddings check : [Understanding Padding in NLP: Types and When to Use Them | by Saad Sohail | Medium](https://saadsohail5104.medium.com/understanding-padding-in-nlp-types-and-when-to-use-them-bacae6cae401)

+ ###### Summary :

- ***Padding*** adds a special value (`0`) to shorter sequences.
- It ensures that **all sequences have the same length**.
- This allows neural networks to process multiple sequences together efficiently during training.
