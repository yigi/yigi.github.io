True positive: Sick people correctly identified as sick
False positive: Healthy people incorrectly identified as sick
True negative: Healthy people correctly identified as healthy
False negative: Sick people incorrectly identified as healthy

<img align="center" width="500" height="300" src="https://miro.medium.com/max/446/0*HZBYBaOyXaeXWape.png">

### 1. Accuracy
It’s one of the most stereotypical metrics in Machine Learning. This metric evaluates all the correctly classified samples against the total number of samples.
Formula: Accuracy = (TP+TN)/(TP+FP+FN+TN)
In our illustration, considering Cats as the positive class, we get
TP: 80, TN:50, FP: 50 , FN:20
The above illustration of cats and dogs gives us the accuracy as (80+50)/(80+50+50+20)=0.65(65%)
The sklearn library has built-in functions for the same as follows

```python
From sklearn.metrics import accuracy_score
Accuracy = accuracy_score(y_true, y_pred, average=’weighted’)
```

### 2. Precision
The Oxford dictionary defines precision as “the quality, condition, or fact of being exact and accurate”. This metric basically calculates the exactness or accuracy of predicting a class in such a way there are less number of negative samples getting predicted as the positive class. It basically calculates the relevance of predicted samples in all the samples, hence called as the positive predicted value(PPV).
This metric finds its application in mainly the medical domain. When you build a binary classifier whether an X-ray has a pathology or is healthy, you need to be exact in your predictions which in turn helps in reducing the Radiologist effort.
Formula : TP/(TP+FP)
Considering our example the precision for Cats class is 80/(80+50)=0.615(61.5%)
Similarly, the precision for Dogs class will be 50/(50+20)=0.714(71.4%)
Now, in order to calculate the average precision of the model, you can take the Weighted average w.r.t number of samples.

```python
From sklearn.metrics import precision_score
Precision= precision_score(y_true, y_pred,  average=’weighted’)
```

### 3. Recall
Wikipedia defines Recall as “the fraction of relevant instances that have been retrieved over the total amount of relevant instances”. So, it is basically the predicted positive samples amongst the actual positives. This is also called as the Sensitivity or True Positive Rate. Hence, when all the positive samples are correctly predicted, the recall is 1.
Formula : TP/(TP+FN)
In our Cats vs Dogs Classification, the recall for Cats class is: 80/(80+20)=0.8(80%)

```python
From sklearn.metrics import recall_score
Recall = recall_score(y_true, y_pred,  average=’weighted’)
```

<img align="center" width="450" height="300" src="https://miro.medium.com/max/878/0*2oLmlEljiq6APneF.png">

### 4. Specificity
Specificity is the True Negative Rate. It measures the proportion of actual negatives that are correctly identified as such. Using the above use case of a patient having a pathology or being healthy, high specificity means that the model calling a actually healthy person healthy is high.
Formula: TN/(TN+FP)
The specificity of the model is 50/(50+50)=0.5 (50%).
