
<img align="center" width="350" height="300" src="https://miro.medium.com/max/500/1*9GuW1tfc1DqQgztEa_W4Sg.png">
<img align="center" width="650" height="500" src="https://miro.medium.com/max/700/1*a7yzB7N1z44wgo5LEFq1Pw.png">
<img align="center" width="650" height="500" src="https://miro.medium.com/max/558/1*QVDrjSYU8Wl0nRfafNbr6Q.png">

Once you loaded in your data-set and took a quick look at it, it is a good idea to get more information about each column. This can be achieved by dragging in the Summarize Data module.
After pressing the RUN button it will give you access to some basic statistics of each column including the unique value count, mean and the standard deviation. The exact statistics will vary depending on the column type.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/517/1*jJc01BjWpRMF7kgzX5mD7Q.png">

For this data-set, we don’t need to do much preprocessing. The only significant thing we will do to increase the accuracy of our model is to transform categorical features to one-hot encoded features.
Because Azure ML Studio thinks that our categorical columns are numeric we first need to change their type to categorical using the Edit Metadata module.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/671/1*XSOrvNO6FIQorlYsW39-Ow.png">

By clicking on the Edit Metadata module we launch the Properties tab. Here we need to click on the Launch column selector button. This opens a new window where we can select all columns we want to transform from numerical to categorical.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/700/1*-TBjIV9Dits-uftOO_AK4A.png">

Now that we selected the columns we need to change the Data type from Unchanged to Integer and then select Make Categorical from the Categorical tab.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/700/1*f8qBdghlQXIgw0XPfiFbwA.png">

Similarly, to now convert the chosen columns to a one-hot encoding, drag the Convert to Indicator Values module onto the experiment canvas, click onto it to open the Properties tab and select the same columns you selected before. Also, check the Overwrite categorical columns checkbox so that the old columns will get deleted when the conversion happens.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/700/1*yqFMLXS3Qx2B7-mLI7JL3g.png">

If we now visualize the output data of the Convert to Indicator Values module we can see that instead of the 14 columns we started off with we now have 31 columns.
Now the data must be split into training and validation set. This can be achieved by dragging the Split Data module onto the experiment canvas, connecting its input to the output of the Convert to Indicator Values, and then navigating to the Properties tab and choosing a right split percentage.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/700/1*eDWONza_urfi6_0u6zo0_g.png">

## Choosing and applying an algorithm and training it
At this point, we are ready to add a machine learning algorithm of our choice. By expanding the Machine Learning>Initialize Model category on the left of the canvas we get all the available models (We can also create our own using Python or R as discussed at the end of the article).
In order to keep this article simple drag the Two-Class Logistic Regression module onto the canvas. Also, drag the Train Model module from the Machine Learning>Train category onto the canvas, connect the output of the Logistic Regression model to the left input of the Train Model module and the left output of the Split Data module (training data) to the right input of the Train Model module as shown below.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/684/1*KBZkD_MkRSYPenUWpMN7Uw.png">
Next we need to specify a label column by opening the Launch column selector of the Train Model module. In our case, the label column is called target.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/700/1*m9n2EnyaBtmsK-XLVqhVIw.png">

By right clicking on the Train Model module we can now access the trained model and have the option to save it for later usage as well as to visualize information about its settings and learned weights.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/651/1*yHAU3oyYjZqqopp8xhetKQ.png">

## Scoring and evaluating the model
Now that we have trained our model, we can use our validation set to see how well our model is doing. We can do this by first of making predictions using the Score Model module and then using the Evaluate Model module to get our accuracy and loss metrics.
### Making predictions
To make predictions on the validation set we connect the trained model to the left input of the Score Model Module and the right output node of the Split data module to the right input of the Score Model Module.
<img align="center" width="650" height="500" "src=https://miro.medium.com/max/678/1*N8XYbRx9UijYB2e4do8y9A.png">
When visualizing the output we can see that we have two new columns. The Scored Labels column contains the labels represented by integers of either 0 or 1. The other column called Scored Probabilities gives us the raw probabilities of the predictions.


<img align="center" width="650" height="500" src="https://miro.medium.com/max/590/1*sog8rS-Nc_21l8sAFhYBaQ.png">

## Evaluating the model
To now evaluate the model we drag in the Evaluate Model module and connect the output of the Score Model module to its left input node.
<img align="center" width="350" height="300" src="https://miro.medium.com/max/312/1*33fr_3iTlrADUQz1FDM6tQ.png">


<img align="center" width="650" height="500" src="https://miro.medium.com/max/700/1*5lJJgjfArudVzqNU3yA1vA.png">
## Tuning parameters
With over 84% accuracy our model does a decent job at predicting if a patient has or doesn’t have a heart disease but we can easily get a higher accuracy by tuning our models hyperparameters.
For this, we have two options. We can either left click on our model and tune it manually or we can replace the Train Model module with the Tune Model Hyperparameters module which not only trains the model but also tunes its hyperparameters whilst training.

<img align="center" width="650" height="500" src="https://miro.medium.com/max/612/1*Fw3GFOrpOE3dKMSOPYJyZQ.png">
The Tune Model Hyperparameters module boosts our accuracy up to over 85%.

## Deploying as an Azure Web Service
Probably the best thing about Azure ML Studio is the feature to deploy your experiment as a web service with only a few clicks. This not only allows you to deploy your model fast but also provides you with a service that you can scale to multiple consecutive requests without adding any complexity.
Azure ML Studio provides multiple ways to transform your experiment to a web service. The easiest one is to just use the SET UP WEB SERVICE button at the bottom of the experiment.
This option converts an experiment into a predictive experiment by eliminating data summary, splits, training and other steps not needed for production.
This will work fine for most projects but doesn’t work for our example. This is because when using the Convert to Indicator Values module with a web-service it must be directly connected to the Web service input.After running the predictive experiment to ensure it’s working you can deploy it by clicking on the DEPLOY WEB SERVICE button. This will open a new window with two tabs, the dashboard, and a configuration tab.
Using the dashboard you can test your web service, access the API Key and view some general information.

## Using Python/R Inside Azure ML Studio
Lastly, even though we don’t need it for this simple example I want to quickly mention that Azure ML Studio provides support for both Python and R as well as some chosen functionality of the OpenCV library.
Python or R can be used by either dragging in the Execute Python Script or Execute R Script module onto the canvas and connecting it to the data you want to access.


With these modules you can perform tasks not currently supported by Azure ML Studio like creating extensive visualizations or performing complex data manipulations.
For more information about the capabilities of the Execute Python Script module take a look at the documentation.
<img align="center" width="650" height="500" src="https://miro.medium.com/max/700/1*N0DMHx6PIdfF0cRVoWVhIg.png">
