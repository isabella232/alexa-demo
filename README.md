# Overview
---

For information on this, contact Andreas (@andreas)

This demo shows how Full Stack and feature management could be applied to an Amazon Alexa skill.

By following the steps in this guide you will be able to:

- Host your own Alexa Skill
- Use Optimizely Full Stack + Alexa
- Easily be able to customize this demo on the fly

**Initial Setup Time**
~ 1 hour

**Time to setup Demo**
~10 minutes per demo

### Interaction Model

1. Kick off skill + initiate Amazon "intent"
2. Alexa responds with a yes/no question (specific response string generated by Optimizely)
3. User then responds with affirmative or negative intent to the inital response
4. Affirmative or negaitve responses tracked in Optimizely

### Technologies Used

- AWS Lambda (for running the Alexa Skill code + Full Stack)
- Optimizely Node Full stack SDK
- Node ASK (Alex Skill Kit library)
- Amazon Developers - Alexa Skill
- Gulp to bundle zip file for Lambda

# Initial Setup
---

The most time consuming part of this demo is the inital setup to make sure your Amazon Developers + AWS accounts are properly linked.

## 1. Optimizely

Note: you can choose whether to create a new project per demo, or reuse an existing project

- Create an Optimizely Full Stack Project
- Create a feature flag called "alexaDemo", or otherwise (you will need to implment this in the code in step 2)
- Create a variable in the code for "response" [string]. Note: this will be the string that the Alexa skill responds with
- Create two events "respondedYes" and "respondedNo" (we'll track this from Alexa)
- Create an experiment using your Optimizely feature, and create one variation for each response that you want to demo (*NOTE* each response should end in a yes/no question)
	- *Recommendation* for best results, create 4 or more variation
	- Remember to start the experiment!

## 2. Amazon Setup

[Setup Guide from Amazon](https://developer.amazon.com/docs/custom-skills/host-a-custom-skill-as-an-aws-lambda-function.html)

- Create an [AWS account](https://aws.amazon.com/) (if you don't already have one) & an [Amazon Developer](https://www.amazon.com/ap/register?clientContext=134-7160800-6833942&openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&siteState=clientContext%3D147-1596174-2894532%2CsourceUrl%3Dhttps%253A%252F%252Fdeveloper.amazon.com%252Falexa%252Fconsole%252Fask%2Csignature%3Dnull&marketPlaceId=ATVPDKIKX0DER&language=en_US&pageId=amzn_developer_portal&openid.return_to=https%3A%2F%2Fdeveloper.amazon.com%2Falexa%2Fconsole%2Fask&prevRID=6VH2058CV2GEPNAPJAMD&openid.assoc_handle=mas_dev_portal&openid.mode=checkid_setup&prepopulatedLoginId=&failedSignInCount=0&openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0) (you'll need this to create an Alexa Skill)

### 1. Amazon Developers - Alexa

- Log into https://developer.amazon.com/ and click "amazon alexa"
- Click "Alexa Skills Kit" from the header, then click "Start a Skill"
- Click "Click Create a Skill", give your skill a name, and select "Custom"
- Click "Create Skill"
- From the Alexa Skill Console, click "Invocation" from the left hand menu and give your Skill an invocation (this is the phrase that will awaken the skill) then click "Save Model"

![Invocation](https://cdn.optimizely.com/img/8785893177/e2f9c4860f324b3caad8e608602dee64.png)

- Click the "+ Add" button next to "Intents" in the left hand menu and create a custom intent called "OptimizelyDemo"

![intent](https://cdn.optimizely.com/img/8785893177/cf6233e3d7a5480db956dc799f1c02a2.png)

- Add an few phrases you want Amazon to interpret for your demo Skill
- Click "Save Model" and then "Build Model"
- Click "Your Skills" in the header, and click "View Skill ID" below the skill you just created
- Take note of this skill ID... you will need it later!

### 2. AWS Lambda config

- Sign into the [AWS Console](https://aws.amazon.com/)
- Click "Services" from the menu and search for "Lambda"
- Click "Create Function"
- Give your function a name and select Node 6.10 or above for the Runtime
- Click "Designer" from the Lambda configuration panel to show the triggers 
![triggers](https://cdn.optimizely.com/img/8785893177/6f55bdb11855469685347fe16c6ed5a8.png) 
- From the triggers menu select Alexa Skills Kit and scroll down and paste your Alexa skill ID from before in the "Skill ID" field and click "Add"


### 3. Customize and upload your skill!

- Clone this repo to a local directory on your computer
- Run ```npm install```
- Copy your datafile from your Optimizely project and replace the datafile in line 5 of the ```index.js``` file
- Customize the confirmation and denied responses on line 12 and 13 (this is the responses that a user will receive when they confirm or deny the request from Alexa)
s
- In the projects terminal window, run ```gulp```
- Return to your Lambda Skill and in the Functional Code box, click the "Code entry type" and select "Upload a .ZIP file"
- Click Upload and search for the folder for this code repo on your computer, and select the zip file from the "/builds" folder
- Click "Save"

### 4. Testing your Skill

- Once you've uploaded your skills code (in the .zip) file, and connected your Lambda function to your Alexa skill, return to your Alexa Skill console in Amazon
- Click "Test" from the header navigation
- Enter the phrase to innvoke your skill + a phrase entered for the OptimizelyDemo intent, for example "ask Levi Strauss what jeans I should wear"

![test](https://cdn.optimizely.com/img/8785893177/9fb12667205f4a38a45fc57d20a70862.png)

YAY!

- Connecting this to a real Amazon Echo...
	- get your hands on an echo!
	- download the Amazon Alexa app
	- in the app log in using the same credentials used for your Amazon Developer account
	- You're now ready to use your skill on a real device!

### 5. Future Demos

Now that you've set this up, for future demos, all you need to do is...

- Change the feature variable strings in your Optimizely project
- Update the datafile in ```index.js```
- Run ```gulp``` and re-upload the new zip file in AWS Lambda
- Change the innvocation and any intent phrases in your Amazon Aleka Skills console
- That's it!



