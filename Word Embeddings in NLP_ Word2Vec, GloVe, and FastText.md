**Title :** Understanding Word Embeddings in NLP: Word2Vec, GloVe, and FastText

**Introduction:**

Before diving into the concept of word embeddings, it’s important to understand **why** we need them. Computers don't understand human language the way we do, they understand only numbers. So, to process and analyze text data, we must convert words into a numerical format.

**Word embeddings** are techniques in Natural Language Processing (NLP) that represent words as **dense numerical vectors**. These vectors are designed in such a way that **semantically similar words** are located closer to each other in the vector space.

For example, the word *"bank"* can refer to either a **financial institution** or the **side of a river**. Word embeddings capture these **contextual meanings** by placing the word in a vector space based on the surrounding words in the text and helping models understand such variations in meaning.

**Types of Word Embedding:**

There are three widely used word embedding techniques in NLP:

·        **Word2Vec**

·        **GloVe**

·        **FastText**

 

**1.Word2Vec:**

**Word2Vec** is a popular word embedding technique developed by **Tomas Mikolov** and his team at **Google** in 2013\. It learns vector representations of words from large-scale text data and captures semantic relationships between them.

One famous example that shows how Word2Vec understands meaning:

King – Man \+ Women \= Queen

This illustrates that Word2Vec captures relationships such as gender, roles, and analogies in the vector space.

**Word2Vec Architecture:**

Word2Vec has two main architectures:

·       CBOW ( Continuous Bag of Words )

·       Skip-Gram

**CBOW (Continuous Bag of Words):**

* **Objective**: Predict the target word based on its surrounding context words.  
* **Direction**: Context → Target  
* It averages the vectors of context words to predict the central word.

**Example:**

Sentence: *"The cat sat on the mat"*

| Target | Context Word |
| :---: | :---: |
| cat | The , sat |
| sat | cat , on |
| on | sat , the |
| the | on , Mat |

 

In this approach, the model looks at a window of surrounding words and tries to guess the middle word.

#### **Skip-Gram:**

·        **Objective**: Predict the context words given the target word.

·        **Direction**: Target → Context

·        It works better for infrequent or rare words because it focuses on learning how a word relates to many different contexts.

Using the same sentence:

| Target | Predict Context Word |
| :---: | :---: |
| cat | The , sat |
| sat | cat , on |
| on | sat , the |
| the | on , Mat |

 

Skip-Gram is more computationally expensive but usually gives better results on smaller datasets or rare words.

**Pros:**

·       Fast to train and capture Semantic relationships.

**Cons:**

·       Don’t handle out of vocabulary words

·       Don’t consider sub-words information ( ex : play , played , playing )

·       Cannot distinguish between polysemy ( ex: bank : river bank / financial bank) , (one vector per word).

 

**2\. GloVe (Global Vectors for Word Representation)**

**GloVe** is a word embedding technique developed by **Stanford University** that blends the best of **local context learning** (like Word2Vec) and **global statistical information** (like matrix factorization).

**How GloVe Works:**

While Word2Vec learns from the local context of words (small windows), **GloVe builds a giant co-occurrence matrix** from the entire corpus — essentially turning every word into a tally sheet that tracks how frequently it appears near every other word.

Think of it like this:

Each word “makes friends” with others it commonly appears near, and the matrix records those friendships.

GloVe then applies **matrix factorization** and some mathematical transformations (like taking the logarithm of the counts) to derive **dense vector representations**. These vectors are positioned so that **semantically related words** are close together in the vector space.

**Famous Example:**

king \- man \+ woman ≈ queen

**Co-occurrence Matrix:**

GloVe builds a matrix **X**, where each element **X(i, j)** represents:

How often **word j** appears in the context of **word i**  
 Context could mean a sentence, paragraph, or a fixed-size sliding window.

**Formula:**

GloVe uses below formula to learned using matrix factorization

So, why take the **log** of the co-occurrence counts in GloVe?

Raw co-occurrence counts can vary wildly:

* Common words like **“the”** or **“and”** might appear **millions** of times.  
* Rare words like **“fjord”** or **“quasar”** might appear just a few times.

If we used the raw counts directly, the model would be **dominated by high-frequency words**, and the learning would be skewed

This makes the training **more stable** and helps the model learn **meaningful relationships** without being biased toward super common words

**Highlights:**

·        Unlike Word2Vec, which only uses local context (predictive)

·        Unlike pure matrix factorization approaches, which only use global counts

·        **GloVe merges both** to learn word vectors that are rich in meaning and grounded in usage patterns

Think of it like this: \> Word2Vec is like learning by overhearing short conversations. \> Pure matrix factorization is like reading a giant dictionary. \> **GloVe is both — it listens *and* reads.**

 

**Pros:**

·        Combines **global co-occurrence** and **local context**. ( like Combining listening and reading )

**Cons:**

·        Still one vector per word (polysemy not handled).

·        Memory intensive (large co-occurrence matrix).

·        Still no out of vocabulary handling

 

3.FastText:

**FastText**, developed by **Facebook AI Research (FAIR)**, improves upon Word2Vec by incorporating **subword information** into word embeddings.

Instead of treating a word as a single unit, FastText **represents each word as a collection of character n-grams** (subword units). This allows it to **understand internal word structure** like prefixes, suffixes, and roots — making it much more powerful for handling rare or unseen words.

**How It Works:**

Each word is broken down into overlapping **character-level n-grams**, and the word vector is computed as the **sum of its n-gram vectors**.

**Example:**

Word: **"king"**  
 Character n-grams (for n=3): "kin", "ing", "ki", "ng"

 

**Why it is powerful:**

·        Can generate vectors for **Out-of-Vocabulary (OOV)** words — even if the full word was never seen during training.

·        Understands **morphology** — the structure of words.  
 Example:

o   "play", "playing", "played" → similar vectors due to shared subwords.

·        Works well for **morphologically rich languages** like **Tamil, Hindi, Finnish**, etc.

**Architectures:**

·  FastText uses the **same architecture as Word2Vec**:

·        **CBOW** (predict target word from context)

·        **Skip-Gram** (predict context from target)

·  The key difference is: it operates on **subword units**, not just whole words.

 

 **Output:**

FastText generates **more robust** word vectors:

·        Better for **rare or misspelled words**

·        More contextually aware due to morphological patterns

**Pros:**

·        Handles **out-of-vocabulary** words.

·        Captures **morphological** relationships.

·        Better for morphologically rich languages (like Tamil, Hindi).

**Cons:**

·        Slightly slower to train than Word2Vec.

·        More complex vector structure.

 

### **Conclusion:**

Word embeddings have fundamentally changed how machines process human language by transforming words into rich, dense vector representations. Techniques like **Word2Vec**, **GloVe**, and **FastText** offer distinct advantages—whether it’s capturing local context, leveraging global statistics, or understanding the internal structure of words.

* **Word2Vec** is fast and efficient for common tasks.

* **GloVe** captures broader co-occurrence patterns across a corpus.

* **FastText** excels in handling rare, misspelled, or morphologically rich words.

Selecting the right embedding method depends on your data and task complexity. As NLP continues to evolve, these foundational methods remain crucial building blocks for developing context-aware, intelligent language models.

