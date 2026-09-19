# 🔤 Tokenization using spaCy

This project demonstrates **Tokenization in NLP using spaCy**. Tokenization is one of the most important preprocessing steps in Natural Language Processing (NLP), where a text is divided into smaller meaningful units called **tokens**.

In this project, we use the **spaCy NLP library** to tokenize a given text into words, punctuation marks, and other linguistic units.

---

## 📌 What is Tokenization?

**Tokenization** is the process of breaking a sentence or paragraph into smaller pieces called **tokens**.

For example:

```text
Input:
"Python is an amazing language!"

Tokens:
Python
is
an
amazing
language
!
```

Each individual word or punctuation mark is treated as a separate token.

### Why is Tokenization Important?

Tokenization is usually one of the first steps in an NLP pipeline.

It helps us to:

* Split text into words
* Identify punctuation
* Process individual words
* Perform text preprocessing
* Prepare text for Machine Learning models
* Perform tasks such as POS Tagging, NER and Lemmatization

---

## 🚀 Technologies Used

* **Python**
* **spaCy**
* **NLP (Natural Language Processing)**

---

## 📦 Installation

First, install spaCy using pip:

```bash
pip install spacy
```

Then download the English language model:

```bash
python -m spacy download en_core_web_sm
```

---

## 💻 Code

```python
import spacy

# Load English language model
nlp = spacy.load("en_core_web_sm")

# Input text
text = "Python is an amazing programming language!"

# Process the text
doc = nlp(text)

# Print tokens
for token in doc:
    print(token.text)
```

---

## 📤 Output

The above code produces output similar to:

```text
Python
is
an
amazing
programming
language
!
```

Here, spaCy automatically identifies individual tokens from the input text.

---

## 🔍 Understanding the Code

### 1. Import spaCy

```python
import spacy
```

This imports the spaCy library into our Python program.

---

### 2. Load the NLP Model

```python
nlp = spacy.load("en_core_web_sm")
```

`en_core_web_sm` is a small English language model provided by spaCy.

The `nlp` object is used to process text and create a `Doc` object.

---

### 3. Provide Input Text

```python
text = "Python is an amazing programming language!"
```

This is the text that we want to tokenize.

---

### 4. Process the Text

```python
doc = nlp(text)
```

spaCy processes the input text and creates a **Doc object**.

The `Doc` contains the linguistic information extracted from the text.

---

### 5. Access Individual Tokens

```python
for token in doc:
    print(token.text)
```

Here:

* `token` → represents one individual token
* `token.text` → gives the actual text of that token

For example:

```python
token.text
```

may return:

```text
Python
```

or:

```text
is
```

or:

```text
!
```

---

## 🧠 Important spaCy Concepts

### `Doc`

A `Doc` is the container that holds the processed text.

```python
doc = nlp(text)
```

---

### `Token`

A `Token` represents an individual unit of text.

```python
for token in doc:
    print(token)
```

---

### `token.text`

Returns the original text of the token.

```python
for token in doc:
    print(token.text)
```

---

### `token.is_alpha`

Checks whether the token contains alphabetic characters.

```python
for token in doc:
    print(token.text, token.is_alpha)
```

Example:

```text
Python True
is True
amazing True
! False
```

---

### `token.is_punct`

Checks whether a token is punctuation.

```python
for token in doc:
    print(token.text, token.is_punct)
```

Example:

```text
! True
```

---

### `token.is_stop`

Checks whether a token is a **stop word**.

```python
for token in doc:
    print(token.text, token.is_stop)
```

For example:

```text
is True
the True
Python False
```

---

## 🔬 Example with Multiple Token Properties

```python
import spacy

nlp = spacy.load("en_core_web_sm")

text = "Python is easy to learn!"

doc = nlp(text)

for token in doc:
    print(
        token.text,
        token.is_alpha,
        token.is_punct,
        token.is_stop
    )
```

Output:

```text
Python True False False
is True False True
easy True False False
to True False True
learn True False False
! False True False
```

---

## 📚 Tokenization in NLP Pipeline

Tokenization is generally performed at the beginning of an NLP pipeline.

```text
Raw Text
   ↓
Tokenization
   ↓
Text Preprocessing
   ↓
POS Tagging
   ↓
Lemmatization
   ↓
Named Entity Recognition
   ↓
Machine Learning / NLP Task
```

Tokenization provides the basic structure required for many downstream NLP tasks.

---

## 🎯 Learning Outcomes

After completing this project, you should understand:

* What Tokenization is
* Why Tokenization is important in NLP
* How to tokenize text using spaCy
* What `Doc` and `Token` objects are
* How to use `token.text`
* How to identify punctuation
* How to identify alphabetic tokens
* How to identify stop words
* How spaCy processes natural language text

---

## 🛠️ Project Structure

```text
Tokenization/
│
├── tokenization.py
├── README.md
└── requirements.txt
```

If you are using `requirements.txt`, you can add:

```text
spacy
```

Then install dependencies using:

```bash
pip install -r requirements.txt
```

---

## 🌱 Future Improvements

This project can be extended by implementing:

* Sentence Tokenization
* Stop Word Removal
* Lemmatization
* Stemming
* Part-of-Speech (POS) Tagging
* Named Entity Recognition (NER)
* Dependency Parsing
* Custom Tokenization Rules

---

## 👨‍💻 Author

**Ayush Pandey**

B.Tech Student | AI/ML & NLP Enthusiast

---

## ⭐ Conclusion

Tokenization is a fundamental concept in **Natural Language Processing**. Using spaCy, text can be efficiently divided into meaningful tokens while also providing useful linguistic information about each token.

This project is part of my **NLP learning journey**, where I am exploring different NLP concepts and implementing them using Python and spaCy.
