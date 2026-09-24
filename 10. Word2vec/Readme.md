# 🧠 Word2Vec & Word Embeddings with spaCy

> A practical NLP notebook for exploring **word vectors, semantic similarity, OOV words, vector arithmetic, and cosine similarity** using spaCy's pretrained English language model.

---

<p align="center">

**Natural Language Processing • Word Embeddings • spaCy • Vector Similarity**

</p>

---

## 📌 Project Overview

Words are one of the most important forms of information in Natural Language Processing. However, machine learning models cannot directly work with words as humans understand them.

To make text understandable to machines, words can be represented as **numerical vectors**.

For example:

```text
"king"
   ↓
Numerical Vector
   ↓
[0.12, -0.45, 0.78, ...]
```

These numerical representations are called **word vectors** or **word embeddings**.

This notebook provides a practical introduction to working with pretrained word vectors using **spaCy** and explores how these vectors can be used to understand relationships between words.

---

## ✨ What This Notebook Covers

| Topic                  | Description                                      |
| ---------------------- | ------------------------------------------------ |
| 🧩 Word Vectors        | Representing words as numerical vectors          |
| 📚 Vocabulary          | Understanding words available to the model       |
| ❓ OOV                  | Identifying Out-Of-Vocabulary words              |
| 📐 Vector Dimensions   | Understanding the size of word vectors           |
| 🔗 Word Similarity     | Comparing semantic relationships between words   |
| ⚙️ Similarity Function | Creating reusable similarity functionality       |
| ➕ Vector Arithmetic    | Performing mathematical operations on embeddings |
| 📊 Cosine Similarity   | Measuring similarity between vectors             |

---

## 🛠️ Tech Stack

**Language**

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python\&logoColor=white)

**Libraries**

![spaCy](https://img.shields.io/badge/spaCy-NLP-09A3D5?logo=spacy\&logoColor=white)
![Scikit Learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikit-learn\&logoColor=white)

**Model**

```text
en_core_web_lg
```

---

# 🚀 Getting Started

## 1. Clone the Repository

```bash
git clone <your-repository-url>
cd <your-repository-name>
```

---

## 2. Install Required Libraries

Install spaCy:

```bash
pip install spacy
```

Install scikit-learn:

```bash
pip install scikit-learn
```

Or install both together:

```bash
pip install spacy scikit-learn
```

---

## 3. Download the spaCy Model

This notebook uses the large English spaCy model:

```bash
python -m spacy download en_core_web_lg
```

The model is important because the notebook works with **pretrained word vectors**.

---

# 📂 Project Structure

```text
Word2Vec/
│
├── 📓 Werd2vec.ipynb
│
└── 📄 README.md
```

### `Werd2vec.ipynb`

The main Jupyter Notebook containing all experiments and Python code.

### `README.md`

Documentation explaining the project, installation, concepts, and usage.

---

# 🧩 1. Loading the NLP Model

The notebook begins by importing spaCy and loading the pretrained model.

```python
import spacy

nlp = spacy.load("en_core_web_lg")
```

Here:

* `spacy` → NLP library
* `nlp` → loaded NLP pipeline
* `en_core_web_lg` → large English model containing pretrained word vectors

Once loaded, text can be processed using:

```python
doc = nlp("dog cat banana kem")
```

spaCy converts the text into a document containing individual tokens.

---

# 🔍 2. Checking Word Vectors

The notebook checks whether individual tokens have vector representations.

```python
for token in doc:
    print(
        token.text,
        "Vector:",
        token.has_vector,
        "OOV:",
        token.is_oov
    )
```

Two important properties are used here.

### `has_vector`

```python
token.has_vector
```

Checks whether spaCy has a vector representation for the token.

Possible values:

```text
True
False
```

---

# ❓ 3. Understanding OOV

OOV stands for:

> **Out Of Vocabulary**

The notebook checks OOV status using:

```python
token.is_oov
```

This tells us whether a token is outside the model's vocabulary.

```text
is_oov = True
    ↓
Token is Out Of Vocabulary

is_oov = False
    ↓
Token is not Out Of Vocabulary
```

This is especially useful when working with real-world text because datasets may contain words that are not present in a pretrained model's vocabulary.

---

# 📐 4. Understanding Vector Dimensions

A word vector is represented as an array of numerical values.

The notebook checks the shape of a vector using:

```python
doc[0].vector.shape
```

It also checks the vector representation of `"bread"`:

```python
base_token = nlp("bread")
base_token.vector.shape
```

If the output is:

```text
(300,)
```

it means that the vector contains **300 dimensions**.

Conceptually:

```text
Word
 ↓
Vector
 ↓
[ x₁, x₂, x₃, ..., x₃₀₀ ]
```

The actual dimensionality depends on the model being used.

---

# 🔗 5. Measuring Word Similarity

One of the most useful applications of word embeddings is measuring the similarity between words.

The notebook uses:

```python
base_token = nlp("bread")
```

and compares it with multiple words:

```python
doc = nlp(
    "bread sandeich burger car triger human wheat"
)

for token in doc:
    print(
        f"{token.text} <-> {base_token.text}:",
        token.similarity(base_token)
    )
```

The key method is:

```python
token.similarity(base_token)
```

This calculates a similarity score between the two token vectors.

### 💡 Concept

```text
Word A
  ↓
Vector A

Word B
  ↓
Vector B

Vector A ↔ Vector B
       ↓
 Similarity Score
```

The score provides an indication of how closely the model represents the two words.

---

# ⚙️ 6. Creating a Reusable Similarity Function

Instead of repeatedly writing the same comparison logic, the notebook creates a reusable function:

```python
def print_similarity(base_word, words_to_compare):

    base_token = nlp(base_word)
    doc = nlp(words_to_compare)

    for token in doc:
        print(
            f"{token.text} <-> {base_token.text}: ",
            token.similarity(base_token)
        )
```

Now we can compare different groups of words easily.

### Example

```python
print_similarity(
    "iphone",
    "apple samsung iphone dog kitten"
)
```

Another example:

```python
print_similarity(
    "car",
    "bus bike train apple banana"
)
```

This makes the experiment reusable without changing the main similarity logic.

---

# ➕ 7. Word Vector Arithmetic

The notebook also demonstrates **mathematical operations on word vectors**.

Vectors are obtained for:

```python
king = nlp.vocab["King"].vector
man = nlp.vocab["man"].vector
women = nlp.vocab["women"].vector
queen = nlp.vocab["queen"].vector
```

Then:

```python
result = king - man + women
```

Conceptually:

```text
King - Man + Women
```

The resulting vector is then compared with the vector representation of:

```text
Queen
```

This demonstrates how relationships between words can sometimes appear as patterns in an embedding space.

> **Note:** This should be understood as a vector-space experiment rather than literal reasoning performed by the model.

---

# 📊 8. Cosine Similarity

To compare the resulting vector with the `queen` vector, the notebook uses scikit-learn:

```python
from sklearn.metrics.pairwise import cosine_similarity
```

Then:

```python
cosine_similarity([result], [queen])
```

### What is Cosine Similarity?

Cosine similarity measures how similar two vectors are based on the **direction** they point in vector space.

```text
Similar direction
       ↓
Higher similarity
```

```text
Different direction
       ↓
Lower similarity
```

In this notebook, cosine similarity is used to compare:

```text
King - Man + Women
```

with:

```text
Queen
```

---

# 🔄 Notebook Workflow

The complete workflow can be summarized as:

```text
                  ┌──────────────────────┐
                  │     Load spaCy       │
                  └──────────┬───────────┘
                             ↓
                  ┌──────────────────────┐
                  │  Load en_core_web_lg │
                  └──────────┬───────────┘
                             ↓
                  ┌──────────────────────┐
                  │   Process Text       │
                  └──────────┬───────────┘
                             ↓
                  ┌──────────────────────┐
                  │ Check Word Vectors   │
                  └──────────┬───────────┘
                             ↓
                  ┌──────────────────────┐
                  │     Check OOV        │
                  └──────────┬───────────┘
                             ↓
                  ┌──────────────────────┐
                  │ Vector Dimensions    │
                  └──────────┬───────────┘
                             ↓
                  ┌──────────────────────┐
                  │  Word Similarity     │
                  └──────────┬───────────┘
                             ↓
                  ┌──────────────────────┐
                  │ Similarity Function  │
                  └──────────┬───────────┘
                             ↓
                  ┌──────────────────────┐
                  │ Vector Arithmetic    │
                  └──────────┬───────────┘
                             ↓
                  ┌──────────────────────┐
                  │ Cosine Similarity    │
                  └──────────────────────┘
```

---

# 📚 Key Concepts

| Concept               | Meaning                                                           |
| --------------------- | ----------------------------------------------------------------- |
| **Word Vector**       | Numerical representation of a word                                |
| **Word Embedding**    | Vector representation used to capture relationships between words |
| **Vocabulary**        | Words known to the NLP model                                      |
| **OOV**               | Out Of Vocabulary                                                 |
| **`has_vector`**      | Checks whether a token has a vector                               |
| **`is_oov`**          | Checks whether a token is outside the vocabulary                  |
| **Vector Shape**      | Represents the number of dimensions in a vector                   |
| **Similarity**        | Measures similarity between word vectors                          |
| **Vector Arithmetic** | Mathematical operations performed on vectors                      |
| **Cosine Similarity** | Compares vectors based on their direction                         |
| **`en_core_web_lg`**  | spaCy's large English model used in this notebook                 |

---

# ▶️ Running the Notebook

After installing the dependencies and model, open:

```text
Werd2vec.ipynb
```

You can use:

* **Jupyter Notebook**
* **JupyterLab**
* **Google Colab**
* **VS Code + Jupyter**

Run the cells from top to bottom.

Start with:

```python
import spacy

nlp = spacy.load("en_core_web_lg")
```

and continue through the notebook.

---

# ⚠️ Troubleshooting

### Model Not Found

If you see:

```text
OSError: [E050] Can't find model 'en_core_web_lg'
```

install the model:

```bash
python -m spacy download en_core_web_lg
```

Then restart the notebook kernel and execute the cells again.

---

# 🎯 Learning Outcomes

After completing this notebook, you will have a practical understanding of:

* What word vectors are
* How pretrained word embeddings are used
* How spaCy represents words as vectors
* How to check vector availability
* How to identify OOV words
* How to inspect vector dimensions
* How word similarity is calculated
* How to build a reusable similarity function
* How vector arithmetic works
* How cosine similarity is used to compare vectors

---

# ⚠️ Scope

This notebook focuses on **using pretrained word vectors with spaCy**.

It does **not** implement the complete Word2Vec training process from scratch.

Topics such as:

* **CBOW**
* **Skip-gram**
* **Negative Sampling**

are outside the scope of this particular notebook.

---

# 📌 Final Takeaway

The central idea behind this notebook is simple:

```text
Text
  ↓
Words / Tokens
  ↓
Numerical Vectors
  ↓
Vector Representation
  ↓
Similarity & Mathematical Operations
  ↓
Explore Relationships Between Words
```

Word embeddings allow NLP systems to represent words numerically and work with their relationships in a vector space.

This notebook provides a hands-on introduction to that concept using **spaCy's pretrained word vectors**.

---

## 👨‍💻 Author

**Ayush Pandey**

B.Tech Student | NLP & Machine Learning Enthusiast

---

## ⭐ If You Found This Useful

If this notebook helped you understand word embeddings, consider giving the repository a ⭐ on GitHub.

