# 🧠 Natural Language Processing (NLP)

<p align="center">

<img src="https://img.shields.io/badge/NLP-Learning%20Repository-blue?style=for-the-badge">
<img src="https://img.shields.io/badge/Python-3.x-yellow?style=for-the-badge&logo=python">
<img src="https://img.shields.io/badge/AI%20%2F%20ML-Learning-green?style=for-the-badge">
<img src="https://img.shields.io/badge/Status-Learning%20%26%20Building-orange?style=for-the-badge">

</p>

<p align="center">

### 🚀 Learn NLP • Understand the Concepts • Implement • Build Real Projects

</p>

> **“चरैवेति चरैवेति — Keep learning, keep moving forward.”** 🚀

---

# 🌟 About This Repository

Welcome to my **Natural Language Processing (NLP)** learning repository.

This repository is created to document and implement **NLP concepts from fundamentals to advanced topics**, with a strong focus on **hands-on Python implementations**.

The goal is not just to learn *what* an NLP technique does, but also to understand:

* 🧠 **How** it works
* ❓ **Why** it is used
* 🎯 **When** it should be used
* 💻 **How to implement it**
* 🌍 **Where it is used in real-world applications**

This repository follows a **progressive learning approach**, starting from basic text processing and gradually moving toward **Machine Learning, Deep Learning, Transformers and modern NLP applications**.

---

# 📌 What is NLP?

**Natural Language Processing (NLP)** is a branch of Artificial Intelligence that enables computers to **understand, process, analyze and generate human language**.

In simple words:

> 🗣️ **NLP teaches computers how to work with human language.**

For example, when you write:

```text
"I really loved this movie!"
```

An NLP system can analyze it and understand that the sentence expresses a **positive sentiment**.

NLP combines multiple fields:

```text
🤖 Artificial Intelligence
        +
📊 Machine Learning
        +
🧠 Deep Learning
        +
📝 Linguistics
        +
💻 Computer Science
        ↓
     🧠 NLP
```

---

# 🌍 Real-World Applications of NLP

NLP is already being used in many real-world systems:

| Application              | Example                       |
| ------------------------ | ----------------------------- |
| 💬 Chatbots              | Conversational AI             |
| 🔍 Search Engines        | Google-like search            |
| 📧 Spam Detection        | Detecting unwanted emails     |
| 📄 Resume Classification | Categorizing resumes          |
| 😊 Sentiment Analysis    | Positive/negative reviews     |
| 🌐 Machine Translation   | Hindi → English               |
| 🎙️ Speech Processing    | Voice assistants              |
| 📰 Text Classification   | News categorization           |
| 🤖 Generative AI         | AI text generation            |
| 📚 Text Summarization    | Long text → short summary     |
| ❓ Question Answering     | Answering questions from text |

---

# 🗺️ NLP Learning Roadmap

The repository follows this learning path:

```text
                         🧠 NLP
                           │
          ┌────────────────┴────────────────┐
          │                                 │
   🧹 Text Processing                 📝 Linguistics
          │                                 │
          ├── Tokenization                 ├── POS Tagging
          ├── Normalization                ├── NER
          ├── Stop Words                   ├── Parsing
          ├── Stemming                     └── Chunking
          ├── Lemmatization
          └── Text Cleaning
                           │
                           ▼
                  📊 Text Representation
                           │
              ┌────────────┼────────────┐
              │            │            │
             BoW         TF-IDF     Embeddings
              │                         │
              │             ┌───────────┼───────────┐
              │             │           │           │
              │          Word2Vec     GloVe      FastText
              │
              ▼
                  🤖 Machine Learning
                           │
             ┌─────────────┼─────────────┐
             │             │             │
            NB            LR            SVM
             │             │             │
             └─────────────┼─────────────┘
                           │
                           ▼
                  🧠 Deep Learning
                           │
                 ┌─────────┼─────────┐
                 │         │         │
                RNN       LSTM       GRU
                           │
                           ▼
                    ⚡ Attention
                           │
                           ▼
                    🔥 Transformers
                           │
             ┌─────────────┼─────────────┐
             │             │             │
            BERT          GPT           T5
                           │
                           ▼
                    🚀 Generative AI
```

---

# 📚 Contents

## 1️⃣ NLP Fundamentals

* [ ] Introduction to NLP
* [ ] NLP vs ML vs AI
* [ ] NLP Pipeline
* [ ] Text Corpus
* [ ] Documents
* [ ] Sentences
* [ ] Words
* [ ] Vocabulary
* [ ] Tokens

---

# 2️⃣ Text Preprocessing

Text preprocessing is one of the **most important stages** of an NLP pipeline.

Real-world text is usually messy:

```text
"OMG!!! I LOVED this movie 😍 <br>
Visit https://example.com ASAP!!!"
```

Before giving this text to a Machine Learning model, we may need to clean and normalize it.

### 🔄 Typical Preprocessing Flow

```text
📝 Raw Text
    ↓
🔡 Lowercasing
    ↓
🧹 HTML Removal
    ↓
🔗 URL Removal
    ↓
✂️ Punctuation Removal
    ↓
💬 Slang Handling
    ↓
📝 Spelling Correction
    ↓
🚫 Stopword Handling
    ↓
😀 Emoji Handling
    ↓
🔪 Tokenization
    ↓
🌱 Stemming
    ↓
🌿 Lemmatization
    ↓
🤖 NLP Model
```

---

## 🔹 Tokenization

Tokenization means breaking text into smaller units called **tokens**.

Example:

```text
"I am learning NLP"
        ↓
["I", "am", "learning", "NLP"]
```

Topics:

* Word Tokenization
* Sentence Tokenization
* Character Tokenization
* Subword Tokenization

Tools:

* 🟢 NLTK
* 🔵 spaCy

---

## 🔹 Lowercasing

Converts text into lowercase.

```text
"Natural Language Processing"
              ↓
"natural language processing"
```

This helps reduce unnecessary differences between words.

---

## 🔹 Removing Punctuation

Removes punctuation when it is not useful for the task.

```text
"Hello, World!"
       ↓
"Hello World"
```

---

## 🔹 Removing Numbers

Numbers can be removed when they are not relevant to the NLP task.

Example:

```text
"I have 25 books"
        ↓
"I have books"
```

> ⚠️ Numbers should only be removed when they are not useful for the particular task.

---

## 🔹 Removing Special Characters

Special characters can be removed when they are not relevant.

```text
@ # $ % ^ & *
```

This is usually done using **Regular Expressions**.

---

## 🔹 Stopword Removal

Stopwords are common words that may provide limited information for some NLP tasks.

Examples:

```text
is
the
a
an
of
to
in
```

However:

> ⚠️ Stopword removal is **task-dependent**. Some tasks may need these words.

---

## 🔹 Stemming

Stemming reduces words toward a common root-like form.

Example:

```text
playing
played
plays
   ↓
 play
```

Popular stemmers:

* Porter Stemmer
* Snowball Stemmer
* Lancaster Stemmer

---

## 🔹 Lemmatization

Lemmatization converts a word into its meaningful dictionary base form.

Example:

```text
running → run
better  → good
studies → study
```

Libraries:

* spaCy
* NLTK

---

## 🔹 Handling URLs

URLs can be detected and removed when they are not useful.

```text
https://example.com
```

---

## 🔹 Handling Email Addresses

Email addresses can be detected and processed.

```text
example@gmail.com
```

---

## 🔹 Handling HTML

Web text often contains HTML tags.

```html
<p>Hello World</p>
```

↓

```text
Hello World
```

---

## 🔹 Handling Emojis

Emojis can either be removed or converted into text depending on the task.

```text
"I love this ❤️"
```

Possible approaches:

```text
Remove → "I love this"

Convert → "I love this :red_heart:"
```

---

## 🔹 Handling Slang

Informal language can be converted into standard language.

```text
brb → be right back
u   → you
```

---

## 🔹 Handling Contractions

Contractions can be expanded.

```text
don't → do not
can't → cannot
I'm   → I am
```

---

## 🔹 Spelling Correction

Spelling mistakes can be corrected.

```text
machne learning
       ↓
machine learning
```

---

# 3️⃣ Text Normalization

Text normalization makes text more **consistent and standardized**.

Topics include:

* 🔡 Lowercasing
* 🔤 Unicode normalization
* 🔄 Contraction expansion
* 📝 Spelling correction
* 💬 Slang conversion
* 🔤 Abbreviation handling
* 🔢 Number normalization
* 🧹 Special character handling

---

# 4️⃣ Regular Expressions for NLP

**Regular Expressions (Regex)** are extremely useful for text cleaning and pattern extraction.

Python provides Regex through:

```python
import re
```

### Common Applications

* 🔗 Removing URLs
* 📧 Removing emails
* 🧹 Removing HTML tags
* ✂️ Removing punctuation
* 🔢 Extracting numbers
* 🔍 Finding patterns
* 🧽 Text cleaning

### Example

```python
text = re.sub(
    r'[^a-zA-Z\s]',
    '',
    text
)
```

This can be used to keep alphabetic characters and spaces.

---

# 5️⃣ Linguistic Processing

Once text is cleaned, we can perform deeper linguistic analysis.

---

## 🔤 Part-of-Speech Tagging

POS Tagging assigns a grammatical category to each word.

Common categories include:

```text
Noun
Verb
Adjective
Adverb
Pronoun
Preposition
```

Example:

```text
Python → Proper Noun
is     → Verb
easy   → Adjective
```

---

## 🏷️ Named Entity Recognition — NER

NER identifies important entities in text.

Common entity types:

```text
👤 Person
🏢 Organization
📍 Location
📅 Date
💰 Money
📦 Product
```

Example:

```text
"Google was founded by Larry Page."
```

NLP system:

```text
Google     → Organization
Larry Page → Person
```

---

## 🌳 Dependency Parsing

Dependency parsing identifies grammatical relationships between words.

It helps identify:

* Subject
* Object
* Verb
* Modifier

Example:

```text
"Ayush learns NLP."

Ayush  → Subject
learns → Verb
NLP    → Object
```

---

## 🧩 Chunking

Chunking groups words into meaningful phrases.

Examples:

* Noun Phrase
* Verb Phrase
* Prepositional Phrase

---

# 6️⃣ Text Representation

Machine Learning algorithms cannot directly understand raw human language.

Therefore:

```text
Human Text
    ↓
Numerical Representation
    ↓
Machine Learning Model
```

Important techniques:

* 📦 Bag of Words
* 📊 TF-IDF
* 🧠 Word Embeddings

---

## 📦 Bag of Words — BoW

Bag of Words represents text based on **word frequency**.

Important concepts:

* Vocabulary creation
* Document-Term Matrix
* Word frequency
* CountVectorizer

Example:

```text
Document 1 → "I love NLP"
Document 2 → "I love AI"
```

Vocabulary:

```text
[I, love, NLP, AI]
```

Each document can then be represented numerically.

---

# 📊 TF-IDF

**TF-IDF = Term Frequency–Inverse Document Frequency**

It measures how important a word is within a document relative to a collection of documents.

Implementation:

```python
from sklearn.feature_extraction.text import TfidfVectorizer
```

---

# 🧠 Word Embeddings

Word embeddings represent words as **dense numerical vectors**.

Important techniques:

* Word2Vec
* GloVe
* FastText

The key idea is:

> Words that occur in similar contexts tend to have similar representations.

---

# 7️⃣ Word2Vec

Word2Vec learns word representations based on context.

It mainly uses two architectures:

### 🔵 CBOW

**Continuous Bag of Words**

Predicts the target word from surrounding words.

```text
Context → Target Word
```

### 🟣 Skip-Gram

Predicts surrounding words from a target word.

```text
Target Word → Context
```

---

# 8️⃣ GloVe

**GloVe = Global Vectors for Word Representation**

GloVe learns word vectors using **global word co-occurrence statistics**.

Important concepts:

* Word co-occurrence
* Vector representation
* Semantic similarity

---

# 9️⃣ FastText

FastText represents words using **character-level information**.

This makes it particularly useful for:

* Rare words
* Misspellings
* Morphologically rich languages
* Out-of-vocabulary words

---

# 🔟 NLP with Machine Learning

After preprocessing and text representation, traditional Machine Learning algorithms can be applied.

### 🤖 Algorithms

* Naive Bayes
* Logistic Regression
* Support Vector Machine
* K-Nearest Neighbors
* Decision Tree
* Random Forest
* XGBoost

### 🎯 Common NLP Applications

* Text Classification
* Sentiment Analysis
* Spam Detection
* Resume Classification
* News Classification

---

# 1️⃣1️⃣ Deep Learning for NLP

Important architectures:

### 🔵 RNN

**Recurrent Neural Network**

Designed to process sequential information.

### 🟢 LSTM

**Long Short-Term Memory**

Designed to handle longer-term dependencies.

### 🟡 GRU

**Gated Recurrent Unit**

A simpler gated recurrent architecture.

### 🔄 Bidirectional RNN

Processes information from both directions.

---

# 1️⃣2️⃣ Attention Mechanism

Attention allows a model to focus on the **most relevant parts of a sequence**.

Important concepts:

* Query
* Key
* Value
* Attention Scores
* Self-Attention

Conceptually:

```text
Input Sequence
      ↓
Attention
      ↓
Important Information
      ↓
Better Representation
```

---

# 1️⃣3️⃣ Transformers

Transformers changed the way modern NLP systems are built.

Important concepts:

* Self-Attention
* Multi-Head Attention
* Positional Encoding
* Encoder
* Decoder
* Feed Forward Network

Basic idea:

```text
Text
 ↓
Tokenization
 ↓
Embeddings
 ↓
Self-Attention
 ↓
Transformer Layers
 ↓
Output
```

---

# 1️⃣4️⃣ Transformer-Based Models

This repository will also explore modern NLP architectures and models such as:

* 🔵 BERT
* 🟣 RoBERTa
* 🟢 DistilBERT
* 🔴 GPT
* 🟡 T5
* 🟠 ALBERT

---

# 1️⃣5️⃣ NLP Tasks

Important NLP tasks include:

* 🏷️ Text Classification
* 😊 Sentiment Analysis
* 📚 Text Summarization
* 🌐 Machine Translation
* ❓ Question Answering
* ✍️ Text Generation
* 🏢 Named Entity Recognition
* 📰 Topic Classification
* 📧 Spam Detection
* 🌍 Language Detection
* 🔎 Information Extraction

---

# 🛠️ Technologies & Libraries

This repository mainly uses **Python** and popular NLP/ML libraries.

### 🐍 Programming

```text
Python
```

### 🧠 NLP

```text
NLTK
spaCy
```

### 🤖 Machine Learning

```text
Scikit-learn
```

### 🧬 Deep Learning

```text
TensorFlow
PyTorch
```

### 📊 Data Processing

```text
NumPy
Pandas
```

### 📈 Visualization

```text
Matplotlib
Seaborn
```

### 🔥 Transformers

```text
Hugging Face Transformers
```

---

# 📂 Repository Structure

The repository is organized topic-wise:

```text
NLP/
│
├── 01_NLP_Basics/
│
├── 02_Text_Preprocessing/
│   ├── Tokenization/
│   ├── Lowercasing/
│   ├── Stopwords/
│   ├── Stemming/
│   ├── Lemmatization/
│   ├── Regex/
│   ├── Spell_Correction/
│   ├── Slang_Handling/
│   └── Text_Cleaning/
│
├── 03_Linguistic_Processing/
│   ├── POS_Tagging/
│   ├── NER/
│   ├── Chunking/
│   └── Dependency_Parsing/
│
├── 04_Text_Representation/
│   ├── Bag_of_Words/
│   ├── TF_IDF/
│   ├── Word2Vec/
│   ├── GloVe/
│   └── FastText/
│
├── 05_ML_for_NLP/
│
├── 06_Deep_Learning_for_NLP/
│
├── 07_Attention/
│
├── 08_Transformers/
│
├── 09_Transformer_Models/
│
├── 10_NLP_Projects/
│
└── README.md
```

---

# 🎯 Goal of This Repository

The main goal of this repository is to build a **complete practical NLP knowledge base**.

Every topic is intended to follow this learning cycle:

```text
             💡 Concept
                ↓
             📖 Theory
                ↓
             🧪 Example
                ↓
          💻 Implementation
                ↓
             📊 Output
                ↓
          🌍 Real Use Case
```

This approach makes the repository useful not only for learning but also for **revision, placement preparation and practical project development**.

---

# 📈 Learning Approach

I am following a progressive learning path:

```text
🟢 NLP Basics
      ↓
🧹 Text Preprocessing
      ↓
🔤 Linguistic Processing
      ↓
📊 Text Representation
      ↓
🤖 Machine Learning
      ↓
🧠 Deep Learning
      ↓
⚡ Attention
      ↓
🔥 Transformers
      ↓
🚀 Modern NLP
      ↓
💻 Real-World Projects
```

---

# 🚀 Projects

The repository will gradually include practical NLP projects such as:

* 📧 Spam Detection
* 😊 Sentiment Analysis
* 📄 Resume Classification
* 📰 News Classification
* 💬 Chatbot
* 🔍 Text Similarity
* 🏷️ NER System
* 📚 Text Summarization
* 🤖 NLP-based AI Applications

---

# 📌 Why This Repository?

This repository is **not just a collection of code**.

It represents my **NLP learning journey** — where concepts, implementations, experiments and projects are documented step by step.

The objective is to create a resource that helps with:

```text
📖 Learning
      ↓
🧠 Understanding
      ↓
💻 Implementation
      ↓
🧪 Experimentation
      ↓
🚀 Project Building
```

It can also serve as a quick revision resource for **NLP, Machine Learning and AI**.

---

# 🤝 Completed a Notebook?

## 🎉 I Want to See Your Progress!

If you complete any notebook or topic from this repository, **don't just stop there — implement it yourself and share your learning journey!**

### 📢 Tag Me on LinkedIn

Once you complete a notebook:

```text
1️⃣ Complete the notebook
        ↓
2️⃣ Understand the concepts
        ↓
3️⃣ Try the examples yourself
        ↓
4️⃣ Share your learning/project on LinkedIn
        ↓
5️⃣ Tag me on LinkedIn
```

### 🔗 Mention Me

**Tag: ****`Ayush Pandey`**** on LinkedIn**

> 🚀 **Completed a topic from this repository? I'd love to see what you learned and built. Share your progress on LinkedIn and tag me!**

Learning becomes more meaningful when we **learn together, build together and share together.** 🤝

---

# ⭐ Support the Repository

If you find this repository useful:

```text
⭐ Star the Repository
🍴 Fork the Repository
👨‍💻 Practice the Notebooks
🚀 Build Your Own Projects
📢 Share Your Learning
🤝 Tag Me on LinkedIn
```

Every star, fork and contribution motivates me to keep expanding this repository. ❤️

---

# 👨‍💻 Author

## Ayush Pandey

**B.Tech Student | AI/ML & NLP Enthusiast**

Currently exploring:

```text
🤖 Artificial Intelligence
🧠 Machine Learning
📝 Natural Language Processing
🧬 Deep Learning
🔥 Transformers
🚀 Generative AI
```

---

# 🌱 Learning Philosophy

> **Learn the concept.**

> **Understand the reason.**

> **Implement it yourself.**

> **Build something with it.**

> **Share what you learned.**

```text
             LEARN
               ↓
           UNDERSTAND
               ↓
           IMPLEMENT
               ↓
             BUILD
               ↓
             SHARE
               ↓
             GROW 🚀
```

---

# 🕉️ प्रेरणा

> **कर्मण्येवाधिकारस्ते मा फलेषु कदाचन।**
> **मा कर्मफलहेतुर्भूर्मा ते सङ्गोऽस्त्वकर्मणि॥**

> *“You have a right to perform your duty, but not to the fruits of your actions.”*

### — श्रीमद्भगवद्गीता 2.47

---

<p align="center">

## 🚀 Learn • Practice • Build • Share • Grow

### ⭐ Keep Learning. Keep Building. Keep Moving Forward. ⭐

**चरैवेति चरैवेति।**

</p>
