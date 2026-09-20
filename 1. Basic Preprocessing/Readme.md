# 🧠 Text Preprocessing in NLP

<p align="center">

## 🚀 From Raw Text to Machine-Ready Text

**A beginner-friendly practical guide to cleaning, normalizing, and preparing text for NLP**

</p>

---

## 🌟 Overview

**Text Preprocessing** is one of the most important steps in **Natural Language Processing (NLP)**.

Real-world text is usually **messy, inconsistent, and noisy**.

For example:

```text
"OMG!!! I LOVED this movie 😍😍 <br> Visit https://example.com ASAP!!!"
```

A machine cannot always work effectively with such raw text.

So, before applying Machine Learning or Deep Learning models, we usually clean and transform the text.

### 🔄 Basic NLP Workflow

```text
📝 Raw Text
     ↓
🔤 Lowercasing
     ↓
🧹 Remove HTML Tags
     ↓
🔗 Remove URLs
     ↓
✂️ Remove Punctuation
     ↓
💬 Chat/Slang Conversion
     ↓
📝 Spelling Correction
     ↓
🚫 Stopword Removal
     ↓
😀 Emoji Handling
     ↓
🔪 Tokenization
     ↓
🌱 Stemming
     ↓
🌿 Lemmatization
     ↓
🤖 Machine Learning / NLP Model
```

---

# 🎯 What You'll Learn

This notebook covers **11 important text preprocessing techniques**:

| #  | 🔧 Technique           | 🎯 Purpose                     |
| -- | ---------------------- | ------------------------------ |
| 01 | 🔡 Lowercasing         | Convert text into lowercase    |
| 02 | 🧹 HTML Tag Removal    | Remove HTML markup             |
| 03 | 🔗 URL Removal         | Remove website links           |
| 04 | ✂️ Punctuation Removal | Remove unnecessary punctuation |
| 05 | 💬 Chat Word Treatment | Convert slang/short forms      |
| 06 | 📝 Spelling Correction | Correct spelling mistakes      |
| 07 | 🚫 Stopword Removal    | Remove common words            |
| 08 | 😀 Emoji Handling      | Remove or convert emojis       |
| 09 | 🔪 Tokenization        | Split text into tokens         |
| 10 | 🌱 Stemming            | Reduce words to stems          |
| 11 | 🌿 Lemmatization       | Convert words to base forms    |

---

# 🛠️ Technologies & Libraries

This notebook uses:

```text
🐍 Python
📊 Pandas
🔢 NumPy
🔤 Regular Expressions
📚 NLTK
🧠 spaCy
📝 TextBlob
😀 Emoji
```

### Import Libraries

```python
import numpy as np
import pandas as pd
import re
import string
import nltk
import spacy
```

---

# 📊 Dataset

The notebook works with an **IMDB Dataset**, which contains movie reviews.

The dataset is loaded using:

```python
df = pd.read_csv(
    'Copy of IMDB Dataset.csv'
)
```

We can inspect the dataset using:

```python
df.shape
```

and:

```python
df.head()
```

---

# 🔡 1. Lowercasing

## 🤔 What is Lowercasing?

Lowercasing means converting all characters into **small letters**.

### Before

```text
"I LOVE THIS MOVIE"
```

### After

```text
"i love this movie"
```

This helps reduce unnecessary differences between words.

For example:

```text
Movie
movie
MOVIE
```

can be normalized to:

```text
movie
```

---

## 🧪 Example

```python
df['review'][3].lower()
```

To apply it to the complete dataset:

```python
df['review'] = df['review'].str.lower()
```

---

# 🧹 2. Removing HTML Tags

Online reviews often contain HTML tags.

Example:

```html
<p>This is a great movie</p>
```

We don't want:

```text
<p>
</p>
```

inside our NLP data.

---

## 🧪 Example

```python
import re

def remove_html_tags(text):
    pattern = re.compile('<.*?>')
    return pattern.sub(r'', text)
```

Input:

```html
<html>
<body>
<p>Movie 1</p>
<p>Actor - Aamir Khan</p>
</body>
</html>
```

Output:

```text
Movie 1
Actor - Aamir Khan
```

---

## 📌 Apply on Dataset

```python
df['review'] = df['review'].apply(
    remove_html_tags
)
```

---

# 🔗 3. Removing URLs

URLs often don't provide useful information for certain NLP tasks.

Example:

```text
Check out my notebook
https://www.kaggle.com/example
```

After preprocessing:

```text
Check out my notebook
```

---

## 🧪 Function

```python
def remove_url(text):
    pattern = re.compile(
        r'https?://\S+|www\.\S+'
    )
    
    return pattern.sub(r'', text)
```

---

## 🔍 It Can Detect

```text
https://example.com
http://example.com
www.example.com
```

### Example

```python
text = """
Check out my notebook
https://www.kaggle.com/example
"""

remove_url(text)
```

---

# ✂️ 4. Removing Punctuation

Punctuation includes characters such as:

```text
! " # $ % & ' ( ) * + , - . / : ; < = > ? @
```

Depending on the NLP task, punctuation may be unnecessary.

### Example

```text
"Hello!!! How are you?"
```

After removal:

```text
"Hello How are you"
```

---

## 🧪 Method 1 — Loop Based

```python
import string

exclude = string.punctuation

def remove_punc(text):
    for char in exclude:
        text = text.replace(char, '')
    
    return text
```

---

# ⚡ Method 2 — `translate()`

The notebook also demonstrates a more efficient approach:

```python
def remove_punc1(text):
    return text.translate(
        str.maketrans('', '', exclude)
    )
```

Example:

```python
text = 'string. With. Punctuation?'

remove_punc1(text)
```

Output:

```text
string With Punctuation
```

The notebook compares the execution time of the two approaches.

---

# 💬 5. Chat Word / Slang Treatment

In social media and messaging, people often use short forms.

For example:

```text
IMHO → In My Humble Opinion
LOL  → Laughing Out Loud
BTW  → By The Way
```

These short forms can be converted into their full forms.

---

## 📥 Loading Slang Dictionary

The notebook downloads a `slang.txt` file:

```python
!wget -O slang.txt \
"https://raw.githubusercontent.com/rishabhverma17/sms_slang_translator/master/slang.txt"
```

The file is then converted into a Python dictionary.

```python
chat_words = {}

with open("slang.txt", "r",
          encoding="utf-8") as file:

    for line in file:
        line = line.strip()

        if "=" in line:
            short, full = line.split("=", 1)

            chat_words[
                short.strip().upper()
            ] = full.strip()
```

---

## 🔄 Chat Conversion Function

```python
def chat_conversion(text):

    new_text = []

    for w in text.split():

        if w.upper() in chat_words:
            new_text.append(
                chat_words[w.upper()]
            )

        else:
            new_text.append(w)

    return " ".join(new_text)
```

### Example

```python
chat_conversion(
    'IMHO he is the best'
)
```

Conceptually:

```text
IMHO
 ↓
In My Humble Opinion
```

---

# 📝 6. Spelling Correction

Real-world text often contains spelling mistakes.

Example:

```text
ceertain
conditionas
duriing
seveal
ggenerations
```

A spelling correction tool can help convert them into more standard words.

---

## 🧪 Using TextBlob

Install/import TextBlob:

```python
from textblob import TextBlob
```

Example:

```python
incorrect_text = """
ceertain conditionas duriing
seveal ggenerations aree
moodified in the saame maner.
"""
```

Create a `TextBlob`:

```python
textBlb = TextBlob(
    incorrect_text
)
```

Then:

```python
textBlb.correct().string
```

returns a corrected version.

---

# 🚫 7. Stopword Removal

## 🤔 What are Stopwords?

Stopwords are common words that often contribute limited information for certain NLP tasks.

Examples:

```text
the
is
am
are
a
an
of
to
in
for
```

---

## 📚 NLTK Stopwords

```python
from nltk.corpus import stopwords
```

Download the stopword dataset:

```python
import nltk

nltk.download('stopwords')
```

Check English stopwords:

```python
stopwords.words('english')
```

---

# 🧪 Stopword Removal Function

```python
def remove_stopwords(text):

    new_text = []

    for word in text.split():

        if word in stopwords.words('english'):
            new_text.append('')

        else:
            new_text.append(word)

    x = new_text[:]

    new_text.clear()

    return " ".join(x)
```

---

## Example

Input:

```text
"This is probably my favorite movie"
```

After stopword removal, some common words may be removed:

```text
"probably favorite movie"
```

> ⚠️ Stopword removal is **task-dependent**. Some NLP tasks may need words that are traditionally considered stopwords.

---

# 😀 8. Handling Emojis

Modern text contains lots of emojis:

```text
😍 😂 ❤️ 🔥 😘 👍
```

The notebook demonstrates two approaches:

### 1️⃣ Remove Emoji

```text
"I loved this movie 😍"
```

↓

```text
"I loved this movie"
```

### 2️⃣ Convert Emoji to Text

```text
🔥
```

↓

```text
:fire:
```

---

# 🧹 Removing Emojis

```python
import re

def remove_emoji(text):

    emoji_pattern = re.compile(
        "["
        u"\U0001F600-\U0001F64F"
        u"\U0001F300-\U0001F5FF"
        u"\U0001F680-\U0001F6FF"
        u"\U0001F1E0-\U0001F1FF"
        u"\U00002702-\U000027B0"
        u"\U000024C2-\U0001F251"
        "]+",
        flags=re.UNICODE
    )

    return emoji_pattern.sub(r'', text)
```

Example:

```python
remove_emoji(
    "Loved the movie. It was 😘😘"
)
```

---

# 🔥 Emoji → Text

Install:

```python
!pip install emoji
```

Import:

```python
import emoji
```

Then:

```python
emoji.demojize(
    'Python is 🔥'
)
```

Conceptually:

```text
Python is 🔥
       ↓
Python is :fire:
```

This can be useful when the **meaning of the emoji should be preserved** instead of simply deleting it.

---

# 🔪 9. Tokenization

## 🤔 What is Tokenization?

Tokenization means breaking text into smaller units called **tokens**.

Example:

```text
"I am learning NLP"
```

Word tokens:

```text
I
am
learning
NLP
```

---

# 🟢 Method 1 — Python `split()`

### Word Tokenization

```python
sent1 = 'I am going to delhi'

sent1.split()
```

Output:

```text
['I', 'am', 'going', 'to', 'delhi']
```

---

## Sentence Tokenization

```python
sent2 = """
I am going to delhi.
I will stay there for 3 days.
Let's hope the trip to be great
"""

sent2.split('.')
```

---

# ⚠️ Problem with `split()`

`split()` is simple but not always intelligent enough.

For example:

```python
sent4 = """
Where do you think I should go?
I have 3 day holiday
"""
```

Using:

```python
sent4.split('.')
```

will not properly handle `?`.

Therefore, more advanced tokenizers are often preferred.

---

# 🟡 Method 2 — Regular Expressions

Python's `re` module can be used for tokenization.

```python
import re

sent3 = 'I am going to delhi!'

tokens = re.findall(
    r"[\w']+",
    sent3
)

tokens
```

This provides more control over what should be considered a token.

---

## Sentence Tokenization with Regex

```python
sentences = re.compile(
    '[.!?] '
).split(text)
```

This can split text based on common sentence-ending punctuation.

---

# 🔵 Method 3 — NLTK

NLTK provides dedicated tokenization functions.

```python
from nltk.tokenize import (
    word_tokenize,
    sent_tokenize
)
```

---

## Word Tokenization

```python
sent1 = 'I am going to visit delhi!'

word_tokenize(sent1)
```

---

## Sentence Tokenization

```python
sent_tokenize(text)
```

NLTK tokenizers are more sophisticated than a basic `split()`.

---

# 🟣 Method 4 — spaCy

The notebook also demonstrates tokenization using spaCy.

Load the English model:

```python
import spacy

nlp = spacy.load(
    'en_core_web_sm'
)
```

Process text:

```python
doc = nlp(
    'I have a Ph.D in A.I'
)
```

Then:

```python
for token in doc:
    print(token)
```

spaCy can handle more complex text patterns and is useful for larger NLP pipelines.

---

# 🆚 Tokenization Methods

| Method    | 🧠 Complexity | 👍 Useful For                     |
| --------- | ------------- | --------------------------------- |
| `split()` | Easy          | Simple text                       |
| Regex     | Medium        | Custom tokenization               |
| NLTK      | Medium        | NLP learning & processing         |
| spaCy     | Advanced      | Production-oriented NLP pipelines |

---

# 🌱 10. Stemming

## 🤔 What is Stemming?

Stemming attempts to reduce related words to a common **stem**.

Example:

```text
walk
walks
walking
walked
```

may be reduced toward:

```text
walk
```

However, stemming can sometimes produce a form that is **not a proper dictionary word**.

---

# 🧪 Porter Stemmer

Import:

```python
from nltk.stem.porter import PorterStemmer
```

Create stemmer:

```python
ps = PorterStemmer()
```

Function:

```python
def stem_words(text):

    return " ".join(
        [ps.stem(word)
         for word in text.split()]
    )
```

---

## Example

```python
sample = """
walk walks walking walked
"""

stem_words(sample)
```

Conceptually:

```text
walk
walk
walk
walk
```

---

# 🌿 11. Lemmatization

## 🤔 What is Lemmatization?

Lemmatization converts words into their **base/dictionary form**, taking linguistic information into account.

For example:

```text
running → run
eating   → eat
swimming → swim
```

Unlike basic stemming, lemmatization aims to produce a valid linguistic base form.

---

# 🧪 WordNet Lemmatizer

Download WordNet:

```python
import nltk

nltk.download(
    'wordnet'
)
```

Import:

```python
from nltk.stem import (
    WordNetLemmatizer
)
```

Create:

```python
wordnet_lemmatizer = \
    WordNetLemmatizer()
```

---

## Example

```python
sentence = """
He was running and eating at same time.
He has bad habit of swimming after
playing long hours in the Sun.
"""
```

Tokenize:

```python
sentence_words = nltk.word_tokenize(
    sentence
)
```

Then lemmatize:

```python
for word in sentence_words:

    print(
        word,
        wordnet_lemmatizer.lemmatize(
            word,
            pos='v'
        )
    )
```

The `pos='v'` tells WordNet to treat the word as a **verb**.

---

# 🌱 Stemming vs Lemmatization

This is one of the most important concepts in text preprocessing.

| Feature  | 🌱 Stemming            | 🌿 Lemmatization                       |
| -------- | ---------------------- | -------------------------------------- |
| Approach | Rule-based reduction   | Linguistic analysis                    |
| Output   | May not be a real word | Usually dictionary form                |
| Speed    | Generally faster       | Generally slower                       |
| Accuracy | Lower in many cases    | Usually more linguistically meaningful |
| Example  | `studies → studi`      | `studies → study`                      |
| Example  | `running → run`        | `running → run`                        |

### Easy Way to Remember

```text
🌱 STEMMING
"Cut the word"

🌿 LEMMATIZATION
"Understand the word"
```

---

# 🔄 Complete Text Preprocessing Pipeline

The complete notebook can be understood as:

```text
                 📝 RAW TEXT
                     │
                     ▼
              🔡 LOWERCASE
                     │
                     ▼
              🧹 HTML REMOVAL
                     │
                     ▼
                🔗 URL REMOVAL
                     │
                     ▼
             ✂️ PUNCTUATION
                     │
                     ▼
             💬 CHAT WORDS
                     │
                     ▼
            📝 SPELLING FIX
                     │
                     ▼
             🚫 STOPWORDS
                     │
                     ▼
                😀 EMOJI
                     │
                     ▼
              🔪 TOKENIZATION
                     │
                     ▼
                🌱 STEMMING
                     │
                     ▼
             🌿 LEMMATIZATION
                     │
                     ▼
               🤖 NLP MODEL
```

---

# 🧠 One Complete Example

Suppose our original text is:

```text
"OMG!!! I LOVED this movie 😍 <br>
Visit https://example.com ASAP!!!"
```

### Step 1 — Lowercase

```text
"omg!!! i loved this movie 😍 <br>
visit https://example.com asap!!!"
```

### Step 2 — Remove HTML

```text
"omg!!! i loved this movie 😍
visit https://example.com asap!!!"
```

### Step 3 — Remove URL

```text
"omg!!! i loved this movie 😍
visit asap!!!"
```

### Step 4 — Remove Punctuation

```text
"omg i loved this movie 😍
visit asap"
```

### Step 5 — Handle Emoji

Depending on the task:

```text
Remove:
"omg i loved this movie visit asap"
```

or:

```text
Convert:
"omg i loved this movie :heart_eyes:
visit asap"
```

### Step 6 — Tokenization

```text
[
  "omg",
  "i",
  "loved",
  "this",
  "movie",
  "visit",
  "asap"
]
```

### Step 7 — Further Processing

Depending on the NLP task:

```text
Stopword Removal
       ↓
Stemming / Lemmatization
       ↓
Machine Learning Model
```

---

# ⚠️ Important: Preprocessing is Task Dependent

There is **no single preprocessing pipeline that is perfect for every NLP problem**.

For example:

### 🟢 Sentiment Analysis

You may want to preserve:

```text
😍
!
not
```

because they can carry sentiment information.

### 🔵 Search / Information Retrieval

Removing punctuation and common words may be useful.

### 🟣 Chatbot / Social Media NLP

Slang and emojis can carry important meaning.

So always ask:

> **"What is my NLP task?"**

before removing information.

---

# 📚 Important Functions Used

| Function              | Purpose                     |
| --------------------- | --------------------------- |
| `.lower()`            | Lowercase text              |
| `.str.lower()`        | Lowercase Pandas column     |
| `re.compile()`        | Create regex pattern        |
| `re.sub()`            | Replace regex matches       |
| `string.punctuation`  | Get punctuation characters  |
| `str.translate()`     | Efficient character removal |
| `TextBlob.correct()`  | Spelling correction         |
| `stopwords.words()`   | Get stopword list           |
| `emoji.demojize()`    | Convert emoji to text       |
| `word_tokenize()`     | Word tokenization           |
| `sent_tokenize()`     | Sentence tokenization       |
| `PorterStemmer()`     | Stemming                    |
| `WordNetLemmatizer()` | Lemmatization               |
| `spacy.load()`        | Load spaCy model            |

---

# 🧪 Practice Questions

After completing this notebook, try these yourself:

### 🟢 Beginner

1. Convert a sentence to lowercase.
2. Remove HTML tags from a sentence.
3. Remove URLs.
4. Remove punctuation.
5. Tokenize a sentence using `split()`.

### 🟡 Intermediate

6. Create your own slang dictionary.
7. Remove English stopwords.
8. Remove emojis.
9. Convert emojis into text.
10. Tokenize using NLTK.

### 🔴 Advanced

11. Compare Regex, NLTK and spaCy tokenization.
12. Compare stemming and lemmatization.
13. Create a complete preprocessing function.
14. Apply preprocessing to the complete IMDB dataset.
15. Compare text before and after preprocessing.

---

# 📁 Suggested Repository Structure

```text
📦 NLP-Repository
│
├── 📁 01-Text-Preprocessing
│   ├── 📓 Text Preprocessing.ipynb
│   └── 📄 README.md
│
├── 📁 02-Tokenization
│   ├── 📓 Tokenization.ipynb
│   └── 📄 README.md
│
├── 📁 03-POS-Tagging
│
├── 📁 04-NER
│
├── 📁 05-Text-Representation
│
└── 📁 06-Machine-Learning-for-NLP
```

---

# 🚀 Learning Roadmap

```text
🐍 Python
   ↓
📊 NumPy + Pandas
   ↓
🧹 Text Preprocessing
   ↓
🔪 Tokenization
   ↓
🏷️ POS Tagging
   ↓
🌿 Lemmatization
   ↓
🏢 NER
   ↓
📦 Bag of Words
   ↓
📊 TF-IDF
   ↓
🧠 Word2Vec / GloVe
   ↓
🤖 Machine Learning
   ↓
🧬 Deep Learning
   ↓
🔥 Transformers
   ↓
🚀 LLMs
```

---

# 📦 Installation

Install the required libraries:

```bash
pip install numpy pandas nltk spacy textblob emoji
```

Download required NLTK resources:

```python
import nltk

nltk.download('stopwords')
nltk.download('punkt')
nltk.download('punkt_tab')
nltk.download('wordnet')
```

Install spaCy English model:

```bash
python -m spacy download en_core_web_sm
```

---

# 📌 Key Takeaways

After completing this notebook, you should understand:

### 🔡 Lowercasing

Normalizes text casing.

### 🧹 HTML Removal

Removes HTML markup from text.

### 🔗 URL Removal

Removes URLs when they are not useful for the task.

### ✂️ Punctuation Removal

Removes punctuation when required.

### 💬 Chat Word Treatment

Converts slang and short forms into meaningful text.

### 📝 Spelling Correction

Attempts to correct spelling errors.

### 🚫 Stopword Removal

Removes selected common words.

### 😀 Emoji Handling

Either removes emojis or converts them into text.

### 🔪 Tokenization

Breaks text into smaller units.

### 🌱 Stemming

Reduces words toward a common stem.

### 🌿 Lemmatization

Converts words into linguistically meaningful base forms.

---

# 👨‍💻 Author

## Ayush Pandey

This notebook is part of my **NLP Learning Repository**, where I am documenting Natural Language Processing concepts with practical Python implementations.

### 🎯 Goal

> **Learn NLP → Understand the Concepts → Implement Them → Build Real Projects**

---

# ⭐ If You Find This Useful

If this repository helps you in your NLP journey:

```text
⭐ Star the repository
🍴 Fork it
👨‍💻 Practice the notebooks
🚀 Build your own NLP projects
```

---

<div align="center">

## 🧠 Learn • Practice • Build • Repeat 🚀

### 📜 अभ्यासेन तु कौन्तेय वैराग्येण च गृह्यते।

**Consistent practice turns knowledge into mastery.**

</div>

