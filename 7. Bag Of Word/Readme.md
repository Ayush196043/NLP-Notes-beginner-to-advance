# 🧠 NLP Tutorial: Text Representation — Bag of Words

This project demonstrates how to convert text data into numerical features using the **Bag of Words (BoW)** technique and use those features to build a **Spam Email Classification** model.

The implementation uses **Scikit-learn's `CountVectorizer`** for text vectorization and **Multinomial Naive Bayes** for classification.

---

## 📌 Project Overview

Machine Learning algorithms cannot directly understand raw text. Therefore, text needs to be converted into a numerical representation.

In this project, we use:

**Text → Bag of Words → Numerical Features → Naive Bayes → Spam/Not Spam Prediction**

The project uses an SMS/email dataset containing two categories:

* `ham` → Normal message
* `spam` → Spam message

---

## 🧠 What is Bag of Words?

**Bag of Words (BoW)** is a simple technique used in Natural Language Processing (NLP) to represent text as numerical vectors.

It creates a vocabulary containing unique words from the training documents and represents each document based on the number of times each word appears.

### Example

Suppose we have two sentences:

```text
I love machine learning
I love Python
```

Vocabulary:

```text
[I, love, machine, learning, Python]
```

Their Bag of Words representation can be:

```text
Sentence 1 → [1, 1, 1, 1, 0]
Sentence 2 → [1, 1, 0, 0, 1]
```

Here, each number represents the frequency of a word in the sentence.

---

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Jupyter Notebook / Google Colab
* NLP
* Bag of Words
* CountVectorizer
* Multinomial Naive Bayes
* Scikit-learn Pipeline

---

## 📂 Dataset

The project uses a `spam.csv` dataset containing messages and their corresponding categories.

The dataset contains:

```text
Category
Message
```

The `Category` column contains:

```text
ham
spam
```

The target variable is converted into numerical form:

```python
df["spam"] = df["Category"].apply(
    lambda x: 1 if x == "spam" else 0
)
```

Therefore:

```text
spam → 1
ham  → 0
```

---

## 🔄 Project Workflow

```text
                Raw Dataset
                     │
                     ▼
              Load CSV File
                     │
                     ▼
             Data Exploration
                     │
                     ▼
          Convert Target to 0/1
                     │
                     ▼
             Train/Test Split
                     │
                     ▼
            CountVectorizer
                     │
                     ▼
          Bag of Words Matrix
                     │
                     ▼
        Multinomial Naive Bayes
                     │
                     ▼
                Prediction
                     │
                     ▼
          Classification Report
```

---

## 1️⃣ Import Required Libraries

```python
import pandas as pd
import numpy as np
```

Pandas is used for handling the dataset, while NumPy is used for numerical operations.

---

## 2️⃣ Load the Dataset

```python
df = pd.read_csv("spam.csv")
df.head()
```

This loads the spam message dataset into a Pandas DataFrame.

---

## 3️⃣ Explore the Dataset

To check the distribution of categories:

```python
df.Category.value_counts()
```

This helps us understand how many `spam` and `ham` messages are present.

---

## 4️⃣ Convert Labels into Numerical Values

Machine Learning models work with numerical labels, so we convert:

```text
spam → 1
ham  → 0
```

Using:

```python
df["spam"] = df["Category"].apply(
    lambda x: 1 if x == "spam" else 0
)
```

---

## 5️⃣ Train-Test Split

The dataset is divided into training and testing sets.

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    df.Message,
    df.spam,
    test_size=0.2
)
```

### Why Train-Test Split?

The training data is used to train the model, while the testing data is used to evaluate how well the model performs on unseen messages.

Here:

```text
80% → Training Data
20% → Testing Data
```

---

# 🔤 6️⃣ Bag of Words using CountVectorizer

The main part of this project is the `CountVectorizer`.

```python
from sklearn.feature_extraction.text import CountVectorizer

v = CountVectorizer()
```

Now we fit the vectorizer on the training messages:

```python
X_train_cv = v.fit_transform(X_train.values)
```

### What happens here?

`CountVectorizer` performs two major tasks:

1. Creates a vocabulary from the training text.
2. Converts each message into a numerical vector based on word counts.

For example:

```text
"I love Python"
"I love Machine Learning"
```

The vectorizer creates a vocabulary such as:

```text
I
love
Python
Machine
Learning
```

Then every sentence is represented numerically.

---

## 🔍 Vocabulary

The vocabulary can be accessed using:

```python
v.vocabulary_
```

And the feature names can be obtained using:

```python
v.get_feature_names_out()
```

The vocabulary represents the unique words learned from the training dataset.

---

## 📊 Sparse Matrix

After vectorization:

```python
X_train_cv
```

returns a **sparse matrix**.

We can convert it into a NumPy array using:

```python
X_train_np = X_train_cv.toarray()
```

This allows us to see the numerical representation of the text.

---

# 🤖 7️⃣ Train Multinomial Naive Bayes

For classification, the project uses:

```python
from sklearn.naive_bayes import MultinomialNB

model = MultinomialNB()
model.fit(X_train_cv, y_train)
```

### Why Multinomial Naive Bayes?

Multinomial Naive Bayes is commonly used for text classification because it works well with discrete features such as word counts.

The model learns patterns from the Bag of Words representation and learns to distinguish between:

```text
0 → ham
1 → spam
```

---

# 🔄 8️⃣ Transform Test Data

The test data must be transformed using the **same vectorizer**:

```python
X_test_cv = v.transform(X_test)
```

Notice that we use:

```python
transform()
```

instead of:

```python
fit_transform()
```

because the vocabulary should be learned only from the training data.

---

# 📈 9️⃣ Model Evaluation

Predictions are generated using:

```python
y_pred = model.predict(X_test_cv)
```

The classification performance is evaluated using:

```python
from sklearn.metrics import classification_report

print(classification_report(y_test, y_pred))
```

The classification report provides metrics such as:

* Precision
* Recall
* F1-score
* Support

---

# 🧪 🔟 Test with Custom Emails

The trained model can also predict new messages.

Example:

```python
emails = [
    "Hey mohan, can we get together to watch footbal game tomorrow?",
    "Upto 20% discount on parking, exclusive offer just for you. Dont miss this reward!"
]
```

Convert the messages into Bag of Words vectors:

```python
emails_count = v.transform(emails)
```

Then make predictions:

```python
model.predict(emails_count)
```

The model predicts whether each message belongs to the `ham` or `spam` category.

---

# 🚀 1️⃣1️⃣ Using Scikit-learn Pipeline

The notebook also demonstrates how to combine the vectorization and classification steps using a **Pipeline**.

```python
from sklearn.pipeline import Pipeline

clf = Pipeline([
    ("vectorizer", CountVectorizer()),
    ("nb", MultinomialNB())
])
```

The complete pipeline can then be trained using:

```python
clf.fit(X_train, y_train)
```

And predictions can be generated with:

```python
y_pred = clf.predict(X_test)
```

Finally:

```python
print(classification_report(y_test, y_pred))
```

---

## ⭐ Why Use Pipeline?

Without a pipeline, we need separate steps:

```text
Text
 ↓
CountVectorizer
 ↓
Numerical Features
 ↓
Naive Bayes
 ↓
Prediction
```

With Pipeline, these steps are combined into one workflow:

```text
Raw Text
   ↓
CountVectorizer
   ↓
MultinomialNB
   ↓
Prediction
```

This makes the code:

* Cleaner
* Easier to maintain
* Easier to reuse
* Less error-prone

---

## 📁 Project Structure

```text
Bag-Of-Words/
│
├── Bag Of Words.ipynb
├── spam.csv
└── README.md
```

---

## 🎯 Concepts Covered

This project covers the following NLP and Machine Learning concepts:

* Natural Language Processing
* Text Representation
* Bag of Words
* CountVectorizer
* Vocabulary Creation
* Sparse Matrix
* Train-Test Split
* Multinomial Naive Bayes
* Text Classification
* Spam Detection
* Classification Report
* Scikit-learn Pipeline

---

## 💡 Real-World Applications

Bag of Words can be used in applications such as:

* 📧 Spam Email Detection
* 📝 Text Classification
* 💬 Sentiment Analysis
* 📰 News Classification
* 🔍 Document Classification
* 🗂️ Document Categorization

---

## ⚠️ Limitations of Bag of Words

Although Bag of Words is simple and useful, it has some limitations:

1. It does not understand the meaning of words.
2. It ignores the order of words.
3. It can create a very large vocabulary.
4. It produces high-dimensional feature vectors.
5. It does not understand context.
6. Words with similar meanings are treated as completely different words.

For example:

```text
"I love Python"
"Python loves me"
```

BoW mainly focuses on word occurrence rather than understanding the complete meaning or relationship between words.

---

## 🔮 What to Learn Next?

After Bag of Words, the next important text representation techniques are:

```text
Bag of Words
      ↓
TF-IDF
      ↓
Word2Vec
      ↓
GloVe
      ↓
FastText
      ↓
BERT
      ↓
GPT
```

These techniques progressively provide richer ways of representing and understanding text.

---

## 📚 Conclusion

This project demonstrates how raw text can be converted into numerical features using **Bag of Words** and `CountVectorizer`.

The resulting numerical representation is then used with **Multinomial Naive Bayes** to perform spam message classification.

The project also demonstrates the use of **Scikit-learn Pipeline** to combine text vectorization and machine learning into a single workflow.

---

## 👨‍💻 Author

**Ayush Pandey**

B.Tech Student | AI/ML & NLP Enthusiast

---

## 📜 Sanskrit Motivation

> **कर्मण्येवाधिकारस्ते मा फलेषु कदाचन।**
> **मा कर्मफलहेतुर्भूर्मा ते सङ्गोऽस्त्वकर्मणि॥**

**Meaning:**
You have the right to perform your actions, but not to the fruits of your actions.

---

⭐ **If you found this project useful, consider giving the repository a Star ⭐**

