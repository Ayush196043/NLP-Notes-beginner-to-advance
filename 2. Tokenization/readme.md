# 🔤 Tokenization with spaCy

> **Tokenization is the foundation of NLP.**
> It converts raw text into meaningful units called **tokens**, which can then be analyzed and processed by different NLP techniques.

This notebook provides a practical introduction to **Tokenization using spaCy**. It starts with the basics of `Doc`, `Token`, and `Span` objects and gradually moves toward token attributes, multilingual tokenization, custom tokenization, sentence segmentation, URL extraction, and practical information-extraction exercises.

---

## 📌 Overview

In Natural Language Processing, computers cannot directly understand raw human language.

A text such as:

```text
Tony gave two $ to Peter.
```

needs to be broken into smaller units before further NLP processing.

spaCy tokenizes it approximately as:

```text
Tony | gave | two | $ | to | Peter | .
```

Each of these units becomes a **Token object** that can be inspected using different attributes.

This notebook focuses on understanding **how spaCy performs this process and how token-level information can be used in real NLP tasks.**

---

## 🎯 Learning Objectives

After completing this notebook, you will understand:

* What tokenization is and why it is important.
* How spaCy creates a `Doc` object.
* How to access individual `Token` objects.
* What a `Span` represents.
* How token indexes work.
* How to inspect useful token attributes.
* How spaCy detects numbers and currency.
* How to detect email addresses and URLs.
* How to tokenize text in Hindi.
* How to create a blank language pipeline.
* How to customize spaCy's tokenizer.
* Why tokenizer special cases cannot arbitrarily modify text.
* How sentence tokenization works.
* How `sentencizer` can be added to a pipeline.
* How a pretrained pipeline handles sentence boundaries.
* How token information can be used for information extraction.

---

# 🧠 1. What is Tokenization?

**Tokenization** is the process of splitting text into smaller units called **tokens**.

Consider:

```text
Tony gave two $ to Peter.
```

After tokenization:

```text
Tony
gave
two
$
to
Peter
.
```

Tokens don't have to be only words.

They can include:

* Words
* Numbers
* Punctuation
* Currency symbols
* URLs
* Email addresses
* Other meaningful text units

Tokenization is an important preprocessing step because many NLP operations work on individual tokens.

---

# ⚙️ 2. spaCy NLP Pipeline

The notebook uses spaCy's pretrained English pipeline:

```python
import spacy

nlp = spacy.load("en_core_web_sm")
```

Here:

* `spacy.load()` loads a trained language pipeline.
* `en_core_web_sm` is the pretrained English model.
* `nlp` is used to process raw text.

Example:

```python
doc = nlp("Tony gave two $ to Peter.")
```

The result is a `Doc` object.

---

# 📦 3. Understanding the `Doc` Object

A `Doc` represents the complete processed document.

```python
doc = nlp("Tony gave two $ to Peter.")
```

You can check its type:

```python
type(doc)
```

You can also inspect the pipeline components:

```python
nlp.pipe_names
```

The `Doc` acts as the main container for the tokens produced by spaCy.

---

# 🔤 4. Understanding the `Token` Object

Each individual token inside a `Doc` is represented by a `Token` object.

For example:

```python
token = doc[0]
```

Here:

```text
doc[0] → Tony
```

You can check:

```python
type(token)
```

A token provides access to many useful linguistic and lexical properties.

---

# 🔢 5. Token Indexing

Tokens can be accessed using normal Python indexing.

```python
doc[0]
doc[1]
doc[2]
```

For example:

```text
doc[0] → Tony
doc[1] → gave
doc[2] → two
```

This makes it easy to work with individual tokens.

---

# 📐 6. Understanding the `Span` Object

A **Span** is a continuous sequence of tokens from a `Doc`.

Example:

```python
span = doc[:5]
```

This selects the first five tokens.

You can check its type:

```python
type(span)
```

### `Doc` vs `Token` vs `Span`

| Object  | Represents                      |
| ------- | ------------------------------- |
| `Doc`   | Complete processed document     |
| `Token` | One individual token            |
| `Span`  | A continuous sequence of tokens |

Understanding these three objects is fundamental when working with spaCy.

---

# 🔍 7. Token Attributes

spaCy provides several attributes that allow us to inspect tokens.

The notebook demonstrates attributes such as:

```python
token.is_alpha
token.is_punct
token.like_num
token.is_currency
token.like_email
token.like_url
```

These attributes can be extremely useful during NLP preprocessing and information extraction.

---

## 🔤 `is_alpha`

Checks whether the token contains alphabetic characters.

```python
token.is_alpha
```

For example:

```text
Tony → True
```

while punctuation or numeric tokens will not be alphabetic.

---

## 🔢 `like_num`

Checks whether a token resembles a number.

```python
token.like_num
```

For example:

```text
two → True
5000 → True
```

This is useful when numbers may appear in different forms.

---

## 💰 `is_currency`

Checks whether a token represents a currency symbol.

```python
token.is_currency
```

For example:

```text
$ → True
₹ → True
€ → True
```

This property becomes particularly useful when extracting financial information from text.

---

## ✏️ `is_punct`

Checks whether a token is punctuation.

```python
token.is_punct
```

For example:

```text
. → True
! → True
```

This can be useful when preprocessing text for downstream NLP tasks.

---

# 📧 8. Detecting Email Addresses

spaCy provides:

```python
token.like_email
```

to identify tokens that look like email addresses.

Example:

```python
for token in doc:
    if token.like_email:
        print(token.text)
```

This can be used to extract email addresses from documents automatically.

### Practical use cases

* Resume parsing
* Contact extraction
* Customer-data processing
* Document analysis
* Information extraction

---

# 🌍 9. Multilingual Tokenization

spaCy is not limited to English.

The notebook demonstrates tokenization using Hindi:

```python
nlp = spacy.blank("hi")
```

Example:

```python
doc = nlp("भैया जी! 5000 ₹ उधार थे वो वापस देदो")

for token in doc:
    print(token, token.is_currency)
```

This demonstrates that spaCy can tokenize text written in other languages as well.

For example, the currency symbol:

```text
₹
```

is detected as a currency token.

> **Important:** A blank language pipeline primarily provides language-specific tokenization. Full linguistic features depend on the availability and use of an appropriate trained pipeline.

---

# 🧩 10. Customizing the Tokenizer

Sometimes the default tokenizer does not split a particular expression according to our requirement.

spaCy allows us to add **special tokenization rules**.

Consider:

```python
doc = nlp("gimme double cheese extra large healthy pizza")

tokens = [token.text for token in doc]
```

The default tokenization treats:

```text
gimme
```

as one token.

We can customize this behavior.

First:

```python
from spacy.symbols import ORTH
```

Then:

```python
nlp.tokenizer.add_special_case(
    "gimme",
    [
        {ORTH: "gim"},
        {ORTH: "me"}
    ]
)
```

Now the result becomes:

```text
gim
me
double
cheese
extra
large
healthy
pizza
```

---

# ⚠️ 11. Important Tokenizer Error — `ValueError [E997]`

The notebook intentionally demonstrates an important tokenizer rule.

This attempt:

```python
nlp.tokenizer.add_special_case(
    "gimme",
    [
        {ORTH: "Give"},
        {ORTH: "me"}
    ]
)
```

produces:

```text
ValueError: [E997]
Tokenizer special cases are not allowed to modify the text.
```

### Why?

The original text is:

```text
gimme
```

but the proposed tokenization produces:

```text
Give + me
```

which changes the original text.

spaCy's tokenizer special cases are intended to change **how the original text is split**, not to rewrite the text itself.

A valid approach demonstrated in the notebook is:

```python
nlp.tokenizer.add_special_case(
    "gimme",
    [
        {ORTH: "gim"},
        {ORTH: "me"}
    ]
)
```

This preserves the original characters while changing the token boundaries.

---

# 📝 12. Sentence Tokenization

Tokenization can also be performed at the sentence level.

Example:

```python
doc = nlp(
    "Dr. Strange loves pav bhaji of mumbai. "
    "Hulk loves chat of delhi"
)
```

We can iterate through sentences using:

```python
for sentence in doc.sents:
    print(sentence)
```

However, when using a blank pipeline without sentence-boundary information, spaCy can raise:

```text
ValueError: [E030] Sentence boundaries unset.
```

This is demonstrated in the notebook.

---

# 🔧 13. Using `sentencizer`

To add rule-based sentence segmentation:

```python
nlp.add_pipe("sentencizer")
```

Check the pipeline:

```python
nlp.pipe_names
```

Then process the text again:

```python
doc = nlp(
    "Dr. Strange loves pav bhaji of mumbai. "
    "Hulk loves chat of delhi"
)

for sentence in doc.sents:
    print(sentence)
```

The `sentencizer` adds sentence-boundary information without requiring a full trained pipeline.

---

# 🚀 14. Pretrained Pipeline vs Blank Pipeline

The notebook demonstrates an important difference between:

```python
spacy.blank("en")
```

and:

```python
spacy.load("en_core_web_sm")
```

### Blank Pipeline

```python
nlp = spacy.blank("en")
```

A blank pipeline starts with minimal language-specific functionality.

If sentence boundaries are required, you may need to add:

```python
nlp.add_pipe("sentencizer")
```

### Pretrained Pipeline

```python
nlp = spacy.load("en_core_web_sm")
```

A pretrained pipeline contains trained NLP components.

The notebook demonstrates that:

```python
doc.sents
```

works directly with the pretrained English pipeline for the example text.

### Comparison

| Feature                | Blank Pipeline                  | Pretrained Pipeline                   |
| ---------------------- | ------------------------------- | ------------------------------------- |
| Basic Tokenization     | ✅                               | ✅                                     |
| Trained NLP Components | ❌                               | ✅                                     |
| Sentence Boundaries    | Need appropriate component      | Available through pipeline components |
| Customization          | High                            | High                                  |
| Model Download         | Not required for blank pipeline | Required                              |

---

# 🌐 15. URL Extraction

The notebook contains a practical URL extraction exercise.

Example text includes URLs such as:

```text
http://www.data.gov/
http://www.science.gov/
http://data.gov.uk/
```

spaCy provides:

```python
token.like_url
```

to detect URL-like tokens.

Example:

```python
urls = []

for token in doc:
    if token.like_url:
        urls.append(token.text)

print(urls)
```

This demonstrates how token attributes can be used for simple information extraction.

---

# 💰 16. Extracting Money Transactions

The notebook also includes a practical exercise:

```text
Tony gave two $ to Peter, Bruce gave 500 € to Steve
```

The required output is:

```text
two $

500 €
```

The exercise specifically uses:

```python
token.i
```

and:

```python
token.is_currency
```

### Concept

`token.is_currency` helps identify the currency symbol.

`token.i` provides the token's position in the document.

By combining token positions with currency detection, we can identify the amount associated with a currency symbol.

---

# 🔄 Complete Learning Flow

The concepts covered in this notebook follow this progression:

```text
                    Raw Text
                       │
                       ▼
               spaCy NLP Pipeline
                       │
                       ▼
                  Tokenization
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
         Doc Object          Token Object
                                 │
                    ┌────────────┼────────────┐
                    ▼            ▼            ▼
                Attributes     Indexing      Span
                    │
       ┌────────────┼────────────┐
       ▼            ▼            ▼
    Numbers      Currency      URLs/Emails
       │
       ▼
 Information Extraction
       │
       ▼
 Custom Tokenization
       │
       ▼
 Sentence Tokenization
```

---

# 📚 Important spaCy APIs Used

| API / Attribute                | Purpose                             |
| ------------------------------ | ----------------------------------- |
| `spacy.load()`                 | Load a pretrained pipeline          |
| `spacy.blank()`                | Create a blank language pipeline    |
| `nlp()`                        | Process raw text                    |
| `nlp.pipe_names`               | View pipeline components            |
| `doc[i]`                       | Access a token                      |
| `doc[start:end]`               | Create a span                       |
| `token.text`                   | Get original token text             |
| `token.i`                      | Get token index                     |
| `token.is_alpha`               | Check alphabetic token              |
| `token.is_punct`               | Check punctuation                   |
| `token.like_num`               | Detect number-like tokens           |
| `token.is_currency`            | Detect currency symbols             |
| `token.like_email`             | Detect email-like tokens            |
| `token.like_url`               | Detect URL-like tokens              |
| `doc.sents`                    | Access sentence spans               |
| `nlp.add_pipe()`               | Add a pipeline component            |
| `tokenizer.add_special_case()` | Customize tokenization              |
| `ORTH`                         | Define token text in a special case |

---

# 🧪 Practical Exercises

The notebook contains two practical exercises.

### Exercise 1 — URL Extraction

Extract all URLs from a given paragraph using spaCy.

Key attribute:

```python
token.like_url
```

---

### Exercise 2 — Money Transaction Extraction

Extract monetary transactions from:

```text
Tony gave two $ to Peter, Bruce gave 500 € to Steve
```

Expected output:

```text
two $
500 €
```

Key attributes:

```python
token.i
token.is_currency
```

---

# 🎯 Why Tokenization Matters

Tokenization is not just about splitting a sentence into words.

A good tokenizer needs to understand different types of text:

```text
Words       → Tony
Numbers     → 5000
Currency    → ₹
Punctuation → !
Email       → example@gmail.com
URL         → https://example.com
```

This makes tokenization an essential foundation for later NLP tasks such as:

* POS Tagging
* Lemmatization
* Named Entity Recognition
* Text Classification
* Sentiment Analysis
* Information Extraction
* Text Similarity
* Question Answering
* Search and Retrieval

---

# 💡 Key Takeaways

After completing this notebook, you should be comfortable with:

* Creating spaCy NLP pipelines.
* Understanding `Doc`, `Token`, and `Span`.
* Accessing tokens using indexes.
* Inspecting important token attributes.
* Detecting numbers and currencies.
* Detecting email addresses and URLs.
* Working with Hindi tokenization.
* Creating blank language pipelines.
* Adding custom tokenizer rules.
* Understanding the `E997` tokenizer error.
* Performing sentence segmentation.
* Using `sentencizer`.
* Understanding the difference between blank and pretrained pipelines.
* Applying tokenization to practical information-extraction problems.

---

# 📂 Notebook Structure

```text
Tokenization with spaCy
│
├── 01. spaCy Introduction
│
├── 02. NLP Pipeline
│
├── 03. Doc Object
│
├── 04. Token Object
│
├── 05. Token Indexing
│
├── 06. Span Object
│
├── 07. Token Attributes
│   ├── is_alpha
│   ├── is_punct
│   ├── like_num
│   └── is_currency
│
├── 08. Email Detection
│
├── 09. Multilingual Tokenization
│
├── 10. Custom Tokenizer
│   └── Special Cases
│
├── 11. Sentence Tokenization
│   ├── sentencizer
│   └── Pretrained Pipeline
│
├── 12. URL Extraction
│
└── 13. Money Transaction Extraction
```

---

# 🛠️ Requirements

Install spaCy:

```bash
pip install spacy
```

Download the English model:

```bash
python -m spacy download en_core_web_sm
```

Then:

```python
import spacy
```

---

# 📖 References

* [spaCy Documentation](https://spacy.io/)
* [spaCy Models & Languages](https://spacy.io/usage/models)
* [spaCy Tokenizer Documentation](https://spacy.io/usage/linguistic-features#tokenization)

---

# 👨‍💻 Author

## Ayush Pandey

This notebook is part of my **Natural Language Processing learning repository**, where I am documenting NLP concepts from fundamentals to advanced techniques using **Python and spaCy**.

The goal is to build a structured reference that is useful for:

* 📚 Learning NLP
* 💻 Practicing Python
* 🧠 Understanding NLP concepts
* 🚀 Building NLP projects
* 🎯 Preparing for technical interviews

---

### 📜 Sanskrit Thought

> **अभ्यासेन तु कौन्तेय वैराग्येण च गृह्यते।**

**Meaning:** Consistent practice and dedication are the foundation of mastery.
