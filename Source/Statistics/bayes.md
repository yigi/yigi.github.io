<img align="center" width="800" height="300" src="https://miro.medium.com/max/827/1*4_dSOG3F5qmjOFTGzA829Q.png">

The term on the left of the equal sign P(H |E )is the probability of having the disease (H) given that we have been diagnosed positive (E) in a test for such disease, which is what we actually want to calculate.

- P(H|E) = E olayı gerçekleştiğinde H olayının gerçekleşme olasılığı
- P(H) = H olayının gerçekleşme olasılığı
- P(E|H) = H olayı gerçekleştiğinde E olayının gerçekleşme olasılığı
- P(E) = E olayının gerçekleşme olasılığı


### Örnek: 
Bir araştırmaya göre her 43 çocuktan 1 tanesi, yetişkinlikte ortaya çıkan belli bir hastalığa yakalanmakta ve tam güvenilir olmamasına rağmen yapılan test sonuçlarına göre, hastalıklı bir çocuğun testi %80 pozitif, sağlıklı bir çocuğun testi ise %10 pozitif sonuç vermektedir. Bu bilgilere göre test sonucu pozitif olan bir çocuğun gerçekten hasta olma olasılığı nedir?

- P(A) : Çocuğun hasta olması olasılığı = 1/43
- P(B) : Testin pozitif çıkması olasılığı = 1/43 * 0.80 + 42/43 * 0.10 = 5/43
- P(A|B) : Pozitif çıkan testin hastalık çıkma olasılığı ( sorulan bu )
- P(B|A) : Hastalıklı çocuğun testinin pozitif çıkma olasılığı = 0.80


# Python Example 

## Pre-processing

```python
import pandas as pd

df = pd.read_table('SMSSpamCollection',
                   sep='\t', 
                   header=None,
                   names=['label', 'message'])
```
First, we have to convert the labels from strings to binary values for our classifier:

```python
df['label'] = df.label.map({'ham': 0, 'spam': 1})
```

Second, convert all characters in the message to lower case:

```python
df['message'] = df.message.map(lambda x: x.lower())
```

Third, remove any punctuation:

```python
df['message'] = df.message.str.replace('[^\w\s]', '')
```

Fourth, tokenize the messages into into single words using nltk. First, we have to import the tokenizer:

```python
import nltk
```

Now we can apply the tokenization:


```python
df['message'] = df['message'].apply(nltk.word_tokenize)
```

Fifth, we will perform some word stemming. The idea of stemming is to normalize our text for all variations of words carry the same meaning, regardless of the tense. One of the most popular stemming algorithms is the Porter Stemmer:

```python
from nltk.stem import PorterStemmer

stemmer = PorterStemmer()
 
df['message'] = df['message'].apply(lambda x: [stemmer.stem(y) for y in x])
```

Finally, we will transform the data into occurrences, which will be the features that we will feed into our model:

```python
from sklearn.feature_extraction.text import CountVectorizer

# This converts the list of words into space-separated strings
df['message'] = df['message'].apply(lambda x: ' '.join(x))

count_vect = CountVectorizer()
counts = count_vect.fit_transform(df['message'])
```

We could leave it as the simple word-count per message, but it is better to use Term Frequency Inverse Document Frequency, more known as tf-idf:

```python
from sklearn.feature_extraction.text import TfidfTransformer

transformer = TfidfTransformer().fit(counts)

counts = transformer.transform(counts)
```

## Training the Model

We will start by splitting our data into training and test sets:

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(counts, df['label'], test_size=0.1, random_state=69)
```

### Then, all that we have to do is initialize the Naive Bayes Classifier and fit the data. For text classification problems, the Multinomial Naive Bayes Classifier is well-suited:

```python
from sklearn.naive_bayes import MultinomialNB

model = MultinomialNB().fit(X_train, y_train)
```

## Evaluating the Model

```python
import numpy as np

predicted = model.predict(X_test)

print(np.mean(predicted == y_test))
```

Our simple Naive Bayes Classifier has 98.2% accuracy with this specific test set! But it is not enough by just providing the accuracy, since our dataset is imbalanced when it comes to the labels (86.6% legitimate in contrast to 13.4% spam). It could happen that our classifier is over-fitting the legitimate class while ignoring the spam class. To solve this uncertainty, let's have a look at the confusion matrix:

```python
from sklearn.metrics import confusion_matrix

print(confusion_matrix(y_test, predicted))
```

[[478   4]

[   6  70]]

As we can see, the amount of errors is pretty balanced between legitimate and spam, with 4 legitimate messages classified as spam and 6 spam messages classified as legitimate. Overall, these are very good results for our simple classifier
