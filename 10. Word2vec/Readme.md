# Word2Vec with spaCy

This notebook demonstrates how to work with **word vectors (word embeddings)** using spaCy's pretrained English model `en_core_web_lg`.

The notebook covers:

* Loading a pretrained spaCy model
* Checking whether words have vectors
* Understanding OOV (Out Of Vocabulary)
* Checking vector dimensions
* Calculating similarity between words
* Creating a reusable word-similarity function
* Performing arithmetic on word vectors
* Comparing vectors using cosine similarity

---

## 1. Introduction

In Natural Language Processing (NLP), computers cannot directly understand words in the same way humans do.

A word can therefore be represented as a numerical vector.

For example:

```text
king → [0.12, -0.45, 0.78, ...]
```

This numerical representation is called a **word vector** or **word embedding**.

Words with similar meanings or similar usage patterns can have vectors that are close to each other in the vector space.

This notebook uses pretrained word vectors provided by spaCy.

> **Note:** The notebook uses pretrained vectors with spaCy. It does not train a Word2Vec model from scratch.

---

# 2. Technologies Used

The notebook uses:

* Python
* spaCy
* Scikit-learn
* Pretrained English word vectors

The main spaCy model used is:

```text
en_core_web_lg
```

---

# 3. Installation

First install spaCy and scikit-learn:

```bash
pip install spacy scikit-learn
```

Then download the large English spaCy model:

```bash
python -m spacy download en_core_web_lg
```

---

# 4. Loading the spaCy Model

The model is loaded using:

```python
import spacy

nlp = spacy.load("en_core_web_lg")
```

Here:

* `spacy` is the NLP library.
* `nlp` is the loaded language-processing pipeline.
* `en_core_web_lg` is the large English model containing pretrained word vectors.

---

# 5. Checking Word Vectors

The notebook processes a sentence and checks whether each token has a vector.

Example:

```python
doc = nlp("dog cat banana kem")

for token in doc:
    print(token.text, "Vector:", token.has_vector, "OOV:", token.is_oov)
```

Two important properties are used.

## `has_vector`

```python
token.has_vector
```

This checks whether spaCy has a vector representation for the token.

It returns:

```text
True
```

or:

```text
False
```

---

## `is_oov`

OOV means:

**Out Of Vocabulary**

```python
token.is_oov
```

This tells us whether the word is outside the model's vocabulary.

It returns:

```text
True
```

or:

```text
False
```

---

# 6. Checking Vector Dimensions

A word vector is an array containing numerical values.

The notebook checks the vector shape using:

```python
doc[0].vector.shape
```

It also checks the vecto

