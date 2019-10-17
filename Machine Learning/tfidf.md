# Tfidftransformer Usage

### 1. Dataset and Imports

```python
import pandas as pd
 
from sklearn.feature_extraction.text import TfidfTransformer
from sklearn.feature_extraction.text import CountVectorizer
 
# this is a very toy example, do not try this at home unless you want to understand the usage differences
docs=["the house had a tiny little mouse",
      "the cat saw the mouse",
      "the mouse ran away from the house",
      "the cat finally ate the mouse",
      "the end of the mouse story"
     ]
```

### 2. Initialize CountVectorizer

```python
 #instantiate CountVectorizer()
cv=CountVectorizer()
 
# this steps generates word counts for the words in your docs
word_count_vector=cv.fit_transform(docs)
```

word_count_vector.shape
 
(5, 16)

### 3. Compute the IDF values

```python
tfidf_transformer=TfidfTransformer(smooth_idf=True,use_idf=True)
tfidf_transformer.fit(word_count_vector)
```

```python
# print idf values
df_idf = pd.DataFrame(tfidf_transformer.idf_, index=cv.get_feature_names(),columns=["idf_weights"])
 
# sort ascending
df_idf.sort_values(by=['idf_weights'])
```
<img align="center" width="200" height="600" src="http://kavita-ganesan.com/wp-content/uploads/307.png">

Notice that the words ‘mouse’ and ‘the’ have the lowest IDF values. This is expected as these words appear in each and every document in our collection. The lower the IDF value of a word, the less unique it is to any particular document.

### 4. Compute the TFIDF score for your documents

```python
# count matrix
count_vector=cv.transform(docs)
 
# tf-idf scores
tf_idf_vector=tfidf_transformer.transform(count_vector)
```

The first line above, gets the word counts for the documents in a sparse matrix form. We could have actually used word_count_vector from above. However, in practice, you may be computing tf-idf scores on a set of new unseen documents. When you do that, you will first have to do cv.transform(your_new_docs) to generate the matrix of word counts.

Then, by invoking tfidf_transformer.transform(count_vector) you will finally be computing the tf-idf scores for your docs. Internally this is computing the tf * idf  multiplication where your term frequency is weighted by its IDF values.


```python
feature_names = cv.get_feature_names()
 
#get tfidf vector for first document
first_document_vector=tf_idf_vector[0]
 
#print the scores
df = pd.DataFrame(first_document_vector.T.todense(), index=feature_names, columns=["tfidf"])
df.sort_values(by=["tfidf"],ascending=False)
```
<img align="center" width="200" height="600" src="http://kavita-ganesan.com/wp-content/uploads/266.png">


________________________________________________________________________________________________

# Tfidfvectorizer Usage

Now, we are going to use the same 5 documents from above to do the same thing as we did for Tfidftransformer – which is to get the tf-idf scores of a set of documents. But, notice how this is much shorter.

With Tfidfvectorizer you compute the word counts, idf and tf-idf values all at once. It’s really simple.

```python
from sklearn.feature_extraction.text import TfidfVectorizer 
 
# settings that you use for count vectorizer will go here
tfidf_vectorizer=TfidfVectorizer(use_idf=True)
 
# just send in all your docs here
tfidf_vectorizer_vectors=tfidf_vectorizer.fit_transform(docs)
```

### Here’s another way to do it by calling fit and transform separately and you’ll end up with the same results.


```python
tfidf_vectorizer=TfidfVectorizer(use_idf=True)
 
# just send in all your docs here
fitted_vectorizer=tfidf_vectorizer.fit(docs)
tfidf_vectorizer_vectors=fitted_vectorizer.transform(docs)
```


# Tfidftransformer vs. Tfidfvectorizer

In summary, the main difference between the two modules are as follows:

With Tfidftransformer you will systematically compute word counts using CountVectorizer and then compute the Inverse Document Frequency (IDF) values and only then compute the Tf-idf scores.

With Tfidfvectorizer on the contrary, you will do all three steps at once. Under the hood, it computes the word counts, IDF values, and Tf-idf scores all using the same dataset.

# When to use what?

So now you may be wondering, why you should use more steps than necessary if you can get everything done in two steps. Well, there are cases where you want to use Tfidftransformer over Tfidfvectorizer and it is sometimes not that obvious. Here is a general guideline:

If you need the term frequency (term count) vectors for different tasks, use Tfidftransformer.
If you need to compute tf-idf scores on documents within your “training” dataset, use Tfidfvectorizer
If you need to compute tf-idf scores on documents outside your “training” dataset, use either one, both will work.
