# Robo Advisor

## Overview

In this project we will build a Robo Advisor using Amazon Lex and Amazon Lambda.  Below are the action items we take to build the Robo Advisor. 

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
    
Next we add a new intent named `recommendPortfolio` and begin configuring sample utterances such as "I want to save money for my retirement" and "I want the best option to invest for my retirement".

We create four slots:

  * firstName - AMAZON.US_FIRST_NAME - prompt: "Thank you for trusting me to help, could you please give me your name?"

  * age - AMAZON.NUMBER - prompt: "How old are you?"
 
  * investmentAmount - AMAZON.NUMBER - prompt: "How much do you want to invest?"

  * riskLevel - AMAZON.AlphaNumeric - prompt: "What level of investment risk would you like to take? (None, Low, Medium, High)"

And we add the following confirmation prompts:
    
  * Confirm: Thanks, now I will look for the best investment portfolio for you.
    
  * Cancel: I will be pleased to assist you in the future.
 
Here is a recording of the build and initial test:

![Amazon Lex - Initial build and test](https://github.com/kevin-mau/robo_advisor/blob/main/Resources/Amazon%20Lex%20-%20Initial%20build%20and%20test.gif?raw=true)



Next, we will enhance the Robo Advisor with an Amazon Lambda Function using Python 3.7 as the runtime programming language.

In the lambda function we will add the following validation rules:

  * The value of `age` should be greater than zero and less than 65.
  
  * The value of `investment_amount` should be greater than or equal to 5000.

After slots are validated, the bot will respond with an investment recommendation based on the selected risk levels, as follows:

   * None: “100% bonds (AGG), 0% equities (SPY)”
   
   * Low: “60% bonds (AGG), 40% equities (SPY)”
   
   * Medium: “40% bonds (AGG), 60% equities (SPY)”
   
   * High: “20% bonds (AGG), 80% equities (SPY)”

Finally we test the Lambda function with the four provided test events that you can find in the Test_Events folder in github.

Here is the final Robo Advisor enhanced with the Lambda function showcasing both dialogs with valid and invalid data for the slots (please view in entirety, dialogs with valid data are showcased at the end.)

![Amazon Lex - Enhanced with Lambda Function](https://github.com/kevin-mau/robo_advisor/blob/main/Resources/Amazon%20Lex%20-%20Enhanced%20with%20Lambda%20Function.gif?raw=true)

---




## Contributors

kevin-mau

---

## License

MIT