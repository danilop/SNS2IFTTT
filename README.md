# SNS2IFTTT

A sample [AWS Lambda](https://aws.amazon.com/lambda/) function to push [Amazon SNS](https://aws.amazon.com/sns/) notifications to [IFTTT](https://ifttt.com) via the [Maker](https://ifttt.com/maker) channel.

Here's a few customizations of this project to better handle specific events via SNS:
- [CloudWatchAlarm2IFTTT](https://github.com/danilop/CloudWatchAlarm2IFTTT) for [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) alarms
- [AutoScaling2IFTTT](https://github.com/danilop/AutoScaling2IFTTT) for [EC2 Auto Scaling](https://aws.amazon.com/autoscaling/) notifications

## License

Copyright (c) 2015 Danilo Poccia, http://danilop.net

This code is licensed under the The MIT License (MIT). Please see the LICENSE file that accompanies this project for the terms of use.

## Installation

### On IFTTT

1. Go to [https://ifttt.com/maker](https://ifttt.com/maker) and write down your secret key

### On AWS

2. Create a new Amazon SNS topic, e.g. `ifttt-maker`
3. Create a new AWS Lambda function, e.g. `sns-2-ifttt`
  1. Use Node.js as runtime
  2. Paste the code inline from the `index.js` file included in this repository
  3. Replace the `iftttMakerSecretKey` with the one you wrote down at step 1
  4. (Optional) Replace the `iftttMakerEventName` with the one you want to use
  5. Leave the default handler
  6. Use a basic execution role
  7. Leave the default memory (128MB) and timeout (3s)
4. Add SNS as an event source to the Lambda function
  1. Choose the SNS topic created at step 1
  2. In the options, enable the event source now (not later)

### On IFTTT

5. Select My Recipes
6. Create a Recipes
7. Choose Maker as Trigger ('this')
8. Select Receive a Web Request
9. Write the Event Name exacly as is the `iftttMakerEventName` variable of the Lambda function (step 3.4 on AWS)
10. Select Create Trigger
11. `Value1` contains the body of the SNS message
12. Choose whatever you want as Action ('that'), for example:
  1. iOS or Android Notifications to receive it on your mobile (you need the IF app from IFTTT installed on the device), e.g. you can set the notification to `SNS {{Value1}}`
  2. A Channel from the Connected Home category to have a *visible* effect, e.g. [Philips Hue](https://ifttt.com/hue) to change the color of your lights to blue
  3. Slack to send a message to your team
  4. Trello to create a new card
  5. GitHub to create a new issue

### On AWS (optional)

13. You can test the setup from the SNS web console
  1. Select the topic
  2. Publish a test message

## Feedback

Please give me your feedback [here](https://twitter.com/danilop).
