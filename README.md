# Robo Advisor

## Overview

In this project, we will build a Robo Advisor using Amazon Lex and Amazon Lambda.  

  * Configure the initial robo advisor

  * Build and test the robo advisor

  * Enhance the robo advisor with an Amazon Lambda function

## Process

First we configure the initial Robo Advisor with these characteristics:

    Bot name: RoboAdvisor
    Language: English (US)
    Output voice: Salli
    Session timeout: 5 minutes
    Sentiment analysis: No
    COPPA: No
    Advanced options: No
    All other options: The default value
    
Then we add a new intent named recommendPortfolio and begin configuring sample utterances such as "I want to save money for my retirement".

We create four slots:

  * firstName - AMAZON.US_FIRST_NAME - prompt: "Thank you for trusting me to help, could you please give me your name?"

  * age - AMAZON.NUMBER - prompt: "How old are you?"
 
  * investmentAmount - AMAZON.NUMBER - prompt: "How much do you want to invest?"

  * riskLevel - AMAZON.AlphaNumeric - prompt: "What level of investment risk would you like to take? (None, Low, Medium, High)"

And we add confirmation prompts:
    
  * Confirm: Thanks, now I will look for the best investment portfolio for you.
    
  * Cancel: I will be pleased to assist you in the future.
 
Here is the build and initial test:

![Amazon Lex - Initial build and test](https://github.com/kevin-mau/robo_advisor/blob/main/Resources/Amazon%20Lex%20-%20Initial%20build%20and%20test.gif?raw=true)




Next, we will split the data into training and testing datasets with `X` as the `SMA_Fast` and the `SMA_Slow` columns and `y` as the `Signal` column.
With the training and testing datasets ready, we can first try training the baseline model.

Our baseline model will use the `SVC` classifier model from SKLearn's support vector machine (SVM) learning method to fit the training data and make
predictions based on the testing data.
```python
    # From SVM, instantiate SVC classifier model instance
    svm_model = svm.SVC()
 
    # Fit the model to the data using the training data
    svm_model = svm_model.fit(X_train_scaled, y_train)
 
    # Use the testing data to make the model predictions
    svm_pred = svm_model.predict(X_test_scaled)
```
In the next section, I will display the baseline model's classification report and a cumulative return plot that shows the actual returns vs. the strategy
returns.  But before that I will discuss how we will modify the windows to try to optimize the trading algorithm.  For this trial, I will adjust to a 
shorter windows strategy, with the using short- and long-window SMA values set at 1 as the short window and 5 as the long window.  

We will also use a second machine learning model.  To try and get more accuracy from our trading algorithm.  On the second ML model, we will use 
`LogisticRegression`.  We backtest the new model with the same training and testing datasets to evaluate its performance. 


## Data:

The "emerging_markets_ohlcv.csv" file is a CSV file of historical OHLCV market data.  OHLCV is an aggregated form of market data standing for Open, High, Low, Close and Volume.

---

## Contributors

kevin-mau

---

## License

MIT