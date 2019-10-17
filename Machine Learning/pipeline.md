Pipeline gives you a single interface for all 3 steps of transformation and resulting estimator. It encapsulates transformers and predictors inside, and now you can do something like:


```python
vect = CountVectorizer()
    tfidf = TfidfTransformer()
    clf = SGDClassifier()

    vX = vect.fit_transform(Xtrain)
    tfidfX = tfidf.fit_transform(vX)
    predicted = clf.fit_predict(tfidfX)

    # Now evaluate all steps on test set
    vX = vect.fit_transform(Xtest)
    tfidfX = tfidf.fit_transform(vX)
    predicted = clf.fit_predict(tfidfX)
```
## With just:

```python
pipeline = Pipeline([
    ('vect', CountVectorizer()),
    ('tfidf', TfidfTransformer()),
    ('clf', SGDClassifier()),
])
predicted = pipeline.fit(Xtrain).predict(Xtrain)
# Now evaluate all steps on test set
predicted = pipeline.predict(Xtest)
```

 ### All steps except last one must be transforms, last step can be transformer or predictor.
