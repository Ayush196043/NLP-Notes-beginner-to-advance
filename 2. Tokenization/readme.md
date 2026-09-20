# 🧠 Part of Speech (POS) Tagging with spaCy

> **Part of Speech (POS) Tagging** is an important Natural Language Processing (NLP) technique used to identify the grammatical category of each word in a sentence.

This notebook demonstrates how to perform **POS Tagging using spaCy**, understand the difference between **POS tags and detailed grammatical tags**, identify grammatical information such as **verb tense**, remove unwanted tokens, and analyze the frequency of different POS categories in a text.

---

## 📌 What is Part of Speech?

In Natural Language Processing, **Part of Speech (POS)** tells us what role a word plays in a sentence.

For example:

```text
Elon flew to Mars yesterday.
```

The words can be classified approximately as:

| Word      | POS         |
| --------- | ----------- |
| Elon      | Proper Noun |
| flew      | Verb        |
| to        | Adposition  |
| Mars      | Proper Noun |
| yesterday | Adverb      |

POS tagging helps a machine understand the **grammatical structure and role of words** in natural language.

---

# 🚀 What This Notebook Covers

This notebook covers the following concepts:

* Installing and importing spaCy
* Loading the English language pipeline
* Tokenization
* POS Tagging
* Understanding `token.pos_`
* Understanding `token.tag_`
* Using `spacy.explain()`
* Identifying verb tense
* Removing unwanted tokens
* Filtering `SPACE`, `PUNCT`, and `X`
* Counting POS categories
* Understanding `doc.count_by()`
* Working with real-world text

---

# 🛠️ Technologies Used

* **Python**
* **spaCy**
* **Natural Language Processing (NLP)**

---

# 📦 Installation

First, install spaCy:

```bash
pip install spacy
```

Then download the English language model:

```bash
python -m spacy download en_core_web_sm
```

Import spaCy:

```python
import spacy
```

---

# 🔤 Loading the English NLP Pipeline

The notebook uses spaCy's small English language model:

```python
nlp = spacy.load("en_core_web_sm")
```

Here:

* `spacy.load()` loads a trained NLP pipeline.
* `en_core_web_sm` is spaCy's small English language model.
* `nlp` becomes the NLP processing pipeline.

We can then process text using:

```python
doc = nlp("A Person Elon flew to mars yesterday.")
```

The resulting `doc` contains processed tokens along with linguistic information.

---

# 🏷️ POS Tagging

POS tagging assigns a grammatical category to every token.

Example:

```python
doc = nlp("A Person Elon flew to mars yesterday.")

for word in doc:
    print(word, "|", word.pos_, "|", spacy.explain(word.pos_))
```

### Important attributes

### `word.text`

Returns the actual text of the token.

```python
word.text
```

Example:

```text
Elon
```

### `word.pos_`

Returns the **coarse-grained Part of Speech**.

```python
word.pos_
```

Examples include:

```text
NOUN
PROPN
VERB
ADJ
ADV
PRON
ADP
DET
```

### `spacy.explain()`

Provides a human-readable explanation of a spaCy tag.

```python
spacy.explain(word.pos_)
```

For example:

```text
PROPN → proper noun
VERB  → verb
ADV   → adverb
```

---

# 🔎 POS Tagging Example

The notebook also processes:

```python
doc = nlp("Wow! Dr. Strange made 265 million $ on the very first day")

for token in doc:
    print(
        token,
        "|",
        token.pos_,
        "|",
        spacy.explain(token.pos_)
    )
```

This example demonstrates that spaCy can assign grammatical information not only to normal words but also to:

* punctuation
* numbers
* symbols
* proper nouns
* determiners
* prepositions/adpositions

---

# 🏷️ POS vs Detailed TAG

One of the important concepts demonstrated in this notebook is the difference between:

```python
token.pos_
```

and

```python
token.tag_
```

### `token.pos_`

Provides a **coarse-grained POS category**.

Example:

```text
VERB
NOUN
PROPN
ADJ
ADV
```

### `token.tag_`

Provides a **more detailed grammatical tag**.

For example, different forms of verbs can receive different detailed tags.

The notebook demonstrates this using:

```python
print(
    token,
    "|",
    token.pos_,
    "|",
    spacy.explain(token.pos_),
    "|",
    token.tag_,
    "|",
    spacy.explain(token.tag_)
)
```

This allows us to inspect both the general POS category and its more specific grammatical information.

---

# ⏳ Understanding Verb Tense

The notebook demonstrates how spaCy can distinguish different grammatical forms of the same verb.

### Example 1

```python
doc = nlp("He quits the job")

print(
    doc[1].text,
    "|",
    doc[1].tag_,
    "|",
    spacy.explain(doc[1].tag_)
)
```

### Example 2

```python
doc = nlp("he quit the job")

print(
    doc[1].text,
    "|",
    doc[1].tag_,
    "|",
    spacy.explain(doc[1].tag_)
)
```

Although the words are closely related:

```text
quits
quit
```

spaCy assigns different detailed grammatical tags based on their usage.

This demonstrates why `token.tag_` can provide more detailed information than `token.pos_`.

---

# 🧹 Removing Unwanted Tokens

Real-world text contains many tokens that may not be useful for certain NLP tasks.

For example:

* Spaces
* Punctuation
* Unknown or other tokens

The notebook demonstrates how to remove:

```text
SPACE
PUNCT
X
```

The filtering condition is:

```python
filtered_tokens = []

for token in doc:
    if token.pos_ not in ["SPACE", "PUNCT", "X"]:
        filtered_tokens.append(token)
```

After processing, `filtered_tokens` contains only the tokens that satisfy our filtering condition.

We can inspect them using:

```python
filtered_tokens[:20]
```

This technique can be useful during **text preprocessing**.

---

# 📊 Counting POS Categories

spaCy provides a convenient method for counting POS categories:

```python
count = doc.count_by(spacy.attrs.POS)
```

The result is a dictionary-like structure where:

```text
key   → POS attribute ID
value → number of occurrences
```

Example:

```python
count
```

To convert the POS IDs into readable names:

```python
for k, v in count.items():
    print(doc.vocab[k].text, "|", v)
```

This gives output conceptually similar to:

```text
NOUN  | 10
VERB  | 8
PROPN | 6
ADJ   | 4
ADV   | 3
```

The exact counts depend on the input text.

---

# 🧠 Understanding `doc.count_by()`

The following code:

```python
doc.count_by(spacy.attrs.POS)
```

asks spaCy to count tokens according to their POS attribute.

This is useful when we want to perform simple linguistic analysis on a large document.

For example, we can determine:

* How many nouns are present?
* How many verbs are present?
* How many adjectives are present?
* How many adverbs are present?

---

# 🔢 Understanding `doc.vocab`

The notebook also demonstrates:

```python
doc.vocab[96].text
```

spaCy internally represents many linguistic attributes using integer IDs.

`doc.vocab` provides access to spaCy's vocabulary, allowing these IDs to be mapped back to their corresponding string representations.

For example:

```python
doc.vocab[k].text
```

converts a vocabulary ID into a readable text representation.

---

# 🔄 Overall NLP Pipeline

The basic workflow demonstrated in this notebook can be represented as:

```text
Raw Text
   ↓
spaCy NLP Pipeline
   ↓
Tokenization
   ↓
POS Tagging
   ↓
Detailed Grammatical Tagging
   ↓
Token Filtering
   ↓
POS Frequency Analysis
```

---

# 📚 Important spaCy Attributes Used

| Attribute / Function | Purpose                      |
| -------------------- | ---------------------------- |
| `spacy.load()`       | Loads an NLP model           |
| `nlp()`              | Processes text               |
| `doc`                | Processed document           |
| `token`              | Individual token             |
| `token.text`         | Original token text          |
| `token.pos_`         | Coarse POS category          |
| `token.tag_`         | Detailed grammatical tag     |
| `spacy.explain()`    | Explains a tag               |
| `doc.count_by()`     | Counts linguistic attributes |
| `doc.vocab`          | Accesses spaCy vocabulary    |

---

# 🎯 Why POS Tagging is Important in NLP

POS tagging is a fundamental NLP technique and is used in many applications such as:

* Text classification
* Information extraction
* Named Entity Recognition
* Question answering
* Sentiment analysis
* Chatbots
* Text summarization
* Grammar analysis
* Machine translation
* Search engines
* Linguistic analysis

It provides machines with information about **how words function inside sentences**.

---

# 💡 Key Takeaways

After completing this notebook, you should understand:

1. What Part of Speech means.
2. How spaCy performs POS tagging.
3. How to use `token.pos_`.
4. How `token.tag_` provides more detailed grammatical information.
5. How `spacy.explain()` helps understand tags.
6. How spaCy can distinguish different grammatical forms of verbs.
7. How to remove `SPACE`, `PUNCT`, and `X` tokens.
8. How to count POS categories using `doc.count_by()`.
9. How spaCy's vocabulary IDs can be mapped to readable labels.
10. How POS tagging fits into an NLP preprocessing pipeline.

---

# 📖 References

The notebook uses the following references for understanding POS categories and linguistic concepts:

* spaCy Annotation Documentation
* Wikipedia — Part of Speech
* Wikipedia — Preposition and Postposition

---

# 👨‍💻 Author

**Ayush Pandey**

This repository is part of my **NLP learning journey**, where I am documenting important NLP concepts and preprocessing techniques using Python and spaCy.

---

> **अभ्यासेन तु कौन्तेय वैराग्येण च गृह्यते।**
>
> *Practice and consistent effort are the foundation of mastery.*
