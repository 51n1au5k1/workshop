# Step-by-Step Tutorial: Creating a Telegram ChatGPT Bot with PythonAnywhere #

## Step 1: Sign up for a PythonAnywhere account 

Go to the PythonAnywhere project website:
  `https://www.pythonanywhere.com`

Click on "Start running Python..."
Click "Create a Beginner Account."
Fill in all the required fields with your information.


## Step 2: Verify your account

Check your email and click the link to remove the warning.
Log in to your PythonAnywhere account.

## Step 3: Create a new 'bash' console

Click the "Bash" button in the 'Consoles' section.

## Step 4: Clone the bot repository

Copy the bot files from the GitHub repository using the command:

  ```git clone https://github.com/51n1au5k1/simplest_chatgpt_telegram_bot.git```
  
Go to the folder where the script is located: 
 ```cd simplest_chatgpt_telegram_bot```
 
## Step 5: Install required libraries

Run the command: 
```pip install -r requirements.txt```

## Step 6: Edit the settings file

Open the settings file with the command: 
```nano private/tokens.env```

Get the Telegram bot token: Log in to Telegram, find "BotFather", click "Start," give your bot a name and username, copy the token, and paste it in the file.
Get your OpenAI API key: Use the link `https://platform.openai.com/account/api-keys`, click "Create new secret key," copy and paste it in the file.
Press `Control-X` to save changes.

## Step 7: Secure sensitive files

Change the access rights to sensitive files using the following commands:
```
chmod 600 private/tokens.env
chmod 600 private/allowed_users.txt
chmod 600 private/config.env
```

## Step 8: Run the bot

Start your bot using the command: 
```python bot.py```

## Step 9: Test the bot

Go back to Telegram and click on the link in the message from your BotFather.

Start chatting with your ChatGPT bot!

## Congratulations! You have successfully created and set up your Telegram ChatGPT bot using PythonAnywhere. ##
