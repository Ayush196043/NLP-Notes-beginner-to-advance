# 🧠 NLP Pipeline with spaCy

<p align="center">

### 🚀 Understanding How spaCy Processes Human Language

**From Raw Text → Tokenization → Linguistic Analysis → Named Entity Recognition**

</p>

---

## 🌟 What is this Notebook About?

If you are a **beginner in NLP**, this notebook is a good place to understand how **spaCy processes text internally**.

In simple words:

> 🧑‍💻 We give **raw human language** to spaCy, and spaCy processes that text through different **NLP components** to extract useful information.

For example:

```text
"Tesla is going to acquire Twitter for $45 billion."
```

An NLP pipeline can process this sentence and identify things like:

```text
Tesla       → Organization
Twitter     → Organization
$45 billion → Money
```

So instead of treating the entire sentence as plain text, the machine gets **structured linguistic information**.

---

# 🎯 What You Will Learn

This notebook covers the following concepts:

| #  | Concept                | What You Learn                           |
| -- | ---------------------- | ---------------------------------------- |
| 01 | 🔤 Blank Pipeline      | How to create an empty spaCy pipeline    |
| 02 | 🧩 Pipeline Components | How NLP components work                  |
| 03 | 📦 `Doc` Object        | How spaCy stores processed text          |
| 04 | 🏷️ Tokenization       | How text is converted into tokens        |
| 05 | 🧠 POS Tagging         | How words get grammatical information    |
| 06 | ✨ Lemmatization        | How words are reduced to their base form |
| 07 | 🏢 NER                 | How entities are identified              |
| 08 | 🔌 Component Reuse     | How trained components can be reused     |
| 09 | 🎨 displaCy            | How NLP results can be visualized        |
| 10 | 🌍 Multilingual NLP    | How French NLP pipelines work            |

---

# 🧠 1. First Understand: What is an NLP Pipeline?

Imagine an **NLP Pipeline like a factory** 🏭.

Raw text enters the factory:

```text
📝 Raw Text
     ↓
🔤 Tokenizer
     ↓
🏷️ POS Tagger
     ↓
🌱 Lemmatizer
     ↓
🔗 Dependency Parser
     ↓
🏢 Named Entity Recognizer
     ↓
📊 Structured Information
```

Each component performs a particular task.

### Example

Input:

```text
Tesla is going to acquire Twitter for $45 billion.
```

After processing:

```text
Tesla       → ORG
Twitter     → ORG
$45 billion → MONEY
```

The important thing to remember is:

> **An NLP pipeline is simply a sequence of NLP processing components.**

---

# 🧩 2. What is a Pipeline Component?

A **pipeline component** is a processing step inside the NLP pipeline.

Some common components are:

```text
🔤 Tokenizer
🏷️ Tagger
🧠 Lemmatizer
🔗 Parser
🏢 NER
```

Each component adds some kind of information to the document.

For example:

```text
Raw Text
   ↓
Tokenizer
   ↓
Tokens
   ↓
Tagger
   ↓
POS Information
   ↓
NER
   ↓
Named Entities
```

---

# 🐍 3. Installing spaCy

First install spaCy:

```bash
pip install spacy
```

Then import it:

```python
import spacy
```

---

# 🏗️ 4. Creating a Blank Pipeline

Let's create our first pipeline:

```python
nlp = spacy.blank("en")
```

Here:

| Part      | Meaning                 |
| --------- | ----------------------- |
| `spacy`   | spaCy library           |
| `blank()` | Create a blank pipeline |
| `"en"`    | English language        |

So:

```python
spacy.blank("en")
```

means:

> **Create a blank English NLP pipeline.**

---

# 🔍 5. Checking Pipeline Components

We can check which components exist inside our pipeline:

```python
nlp.pipe_names
```

For a blank pipeline, you may get:

```python
[]
```

### 🤔 Why is it empty?

Because we created:

```python
spacy.blank("en")
```

We did **not** load a pretrained model.

So there are no additional trained processing components in the pipeline.

---

# 🔤 6. But Can a Blank Pipeline Tokenize Text?

### YES! ✅

A blank pipeline still provides the language-specific tokenizer.

Example:

```python
nlp = spacy.blank("en")

doc = nlp(
    "Captain America ate 100$ of samosa."
)

for token in doc:
    print(token)
```

The text gets divided into tokens.

Conceptually:

```text
Captain
America
ate
100
$
of
samosa
.
```

So remember:

> 🟢 **Blank pipeline ≠ No functionality**

It still has basic tokenization.

---

# 📦 7. Understanding the `Doc` Object

When we write:

```python
doc = nlp("Hello world!")
```

spaCy returns a **Doc object**.

You can think of `Doc` as:

> 📦 A container that stores the processed document and its linguistic information.

Example:

```python
doc = nlp("Hello world!")
```

Conceptually:

```text
Doc
│
├── Token → Hello
├── Token → world
└── Token → !
```

---

# 🔤 8. What is a Token?

A **Token** is an individual unit of text.

Example:

```python
doc = nlp("Hello world!")
```

The tokens are:

```text
Hello
world
!
```

We can access them using indexes:

```python
doc[0]
doc[1]
doc[2]
```

Output:

```text
doc[0] → Hello
doc[1] → world
doc[2] → !
```

---

# 🏷️ 9. POS Tagging

**POS = Part of Speech**

POS tells us the grammatical role of a word.

For example:

```text
Apple is good.
```

A model can identify:

```text
Apple → Noun
is    → Verb
good  → Adjective
```

In spaCy:

```python
token.pos_
```

can be used to access POS information.

---

# 🌱 10. Lemmatization

Lemmatization converts a word into its **base or dictionary form**.

For example:

```text
running → run
ate     → eat
cars    → car
```

In spaCy:

```python
token.lemma_
```

is used to access the lemma.

Example:

```python
for token in doc:
    print(token.text, "|", token.lemma_)
```

Output conceptually:

```text
running | run
cars    | car
```

---

# ⚠️ Important: Blank Pipeline Limitation

If you create:

```python
nlp = spacy.blank("en")
```

you should not expect trained POS, lemma, or NER information automatically.

Why?

Because the blank pipeline does not contain the trained components required for those annotations.

This is one of the most important concepts demonstrated in this notebook.

---

# 🚀 11. Using a Pretrained Pipeline

Instead of creating a blank pipeline, we can load a pretrained English model.

First download it:

```bash
python -m spacy download en_core_web_sm
```

Then:

```python
nlp = spacy.load("en_core_web_sm")
```

Now we have a **trained NLP pipeline**.

---

# 🔍 12. Inspecting the Pretrained Pipeline

Run:

```python
nlp.pipe_names
```

Unlike the blank pipeline, the pretrained pipeline contains trained components.

You can also inspect:

```python
nlp.pipeline
```

### Difference

```text
Blank Pipeline
     ↓
Basic tokenizer

Pretrained Pipeline
     ↓
Tokenizer
   +
Trained NLP Components
```

---

# 🧠 13. Processing Text with the Pretrained Model

Example:

```python
nlp = spacy.load("en_core_web_sm")

doc = nlp(
    "Captain America ate 100$ of samosa."
)
```

Now we can inspect linguistic information:

```python
for token in doc:
    print(
        token.text,
        "|",
        token.pos_,
        "|",
        token.lemma_
    )
```

The pretrained model can provide trained linguistic annotations.

---

# 🆚 Blank Pipeline vs Pretrained Pipeline

This difference is extremely important.

| Feature               | 🟡 Blank Pipeline | 🟢 Pretrained Pipeline |
| --------------------- | ----------------- | ---------------------- |
| Tokenization          | ✅                 | ✅                      |
| Trained POS           | ❌                 | ✅                      |
| Trained Lemmatization | ❌                 | ✅                      |
| Trained NER           | ❌                 | ✅                      |
| Pretrained knowledge  | ❌                 | ✅                      |
| Customization         | ✅                 | ✅                      |

### Blank

```python
nlp = spacy.blank("en")
```

### Pretrained

```python
nlp = spacy.load("en_core_web_sm")
```

---

# 🏢 14. Named Entity Recognition — NER

Now let's move to one of the most useful NLP tasks:

## **Named Entity Recognition (NER)**

NER identifies important entities in text.

Consider:

```text
Tesla Inc is going to acquire Twitter for $45 billion.
```

A trained NLP model can identify:

```text
Tesla Inc      → ORG
Twitter        → ORG
$45 billion    → MONEY
```

This is extremely useful for extracting structured information from unstructured text.

---

# 🔎 15. Extracting Entities with spaCy

Load the model:

```python
nlp = spacy.load("en_core_web_sm")
```

Process text:

```python
doc = nlp(
    "Tesla Inc is going to acquire Twitter for $45 billion."
)
```

Now:

```python
for ent in doc.ents:
    print(ent.text, "|", ent.label_)
```

Example output:

```text
Tesla Inc | ORG
Twitter   | ORG
$45 billion | MONEY
```

---

# 🏷️ 16. Understanding `doc.ents`

The property:

```python
doc.ents
```

contains the entities recognized by the NER component.

Each entity has information such as:

```python
ent.text
ent.label_
```

Example:

```python
for ent in doc.ents:
    print(
        ent.text,
        "|",
        ent.label_,
        "|",
        spacy.explain(ent.label_)
    )
```

This helps us understand what each entity label means.

---

# 🔌 17. Reusing a Trained Component

One interesting concept demonstrated in the notebook is **component reuse**.

First load a pretrained pipeline:

```python
source_nlp = spacy.load("en_core_web_sm")
```

Then create a blank pipeline:

```python
nlp = spacy.blank("en")
```

Now add the trained NER component:

```python
nlp.add_pipe(
    "ner",
    source=source_nlp
)
```

Check:

```python
nlp.pipe_names
```

The NER component has now been added to the new pipeline.

---

# 💡 Why Would We Reuse a Component?

Sometimes we don't want the complete pretrained pipeline.

We may want only a specific component.

For example:

```text
Pretrained Pipeline
        │
        ├── Tagger
        ├── Parser
        ├── NER
        └── Other Components
```

We can reuse a particular component depending on our requirement.

In this notebook, the example focuses on:

```text
NER
```

---

# 🎨 18. Visualizing NER with displaCy

spaCy provides a visualization tool called:

```text
displaCy
```

Import it:

```python
from spacy import displacy
```

Then:

```python
displacy.render(
    doc,
    style="ent"
)
```

This creates a visual representation of recognized entities.

Conceptually:

```text
Tesla Inc        → ORG
Twitter          → ORG
$45 billion      → MONEY
```

This is very useful for:

* 👀 Understanding NER
* 🐞 Debugging
* 📊 Presenting NLP results
* 🎓 Learning NLP

---

# 🌍 19. Multilingual NLP

spaCy also supports multiple languages.

The notebook demonstrates a **French NLP pipeline**.

Load it using:

```python
nlp = spacy.load("fr_core_news_sm")
```

If it is not installed:

```bash
python -m spacy download fr_core_news_sm
```

---

# 🇫🇷 20. French NLP Example

Example:

```python
doc = nlp(
    "Tesla Inc va racheter Twitter "
    "pour $45 milliards de dollars"
)
```

We can extract entities:

```python
for ent in doc.ents:
    print(
        ent.text,
        "|",
        ent.label_,
        "|",
        spacy.explain(ent.label_)
    )
```

The same basic NLP concepts can therefore be applied using a trained pipeline for another language.

---

# 🔤 21. French POS & Lemmatization

We can also inspect tokens:

```python
for token in doc:
    print(
        token,
        "|",
        token.pos_,
        "|",
        token.lemma_
    )
```

This demonstrates how a trained multilingual pipeline can provide token-level linguistic information.

---

# 🏗️ 22. The Complete Pipeline

Now combine everything we learned.

```text
                 📝 RAW TEXT
                     │
                     ▼
              🔤 TOKENIZER
                     │
                     ▼
              📦 DOC OBJECT
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       🏷️ POS     🌱 LEMMA     🏢 NER
          │          │          │
          │          │          ▼
          │          │      Named Entities
          │          │
          └──────────┴──────────┐
                                 ▼
                       📊 Structured Data
```

This is the basic idea behind

