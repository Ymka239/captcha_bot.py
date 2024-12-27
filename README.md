# captcha_bot.py
# Telegram CAPTCHA Bot
This repository contains a Python-based bot that protects Telegram groups from spam and bots by requiring new members to solve a CAPTCHA before participating in the chat. It uses the **pyTelegramBotCAPTCHA** library to manage CAPTCHA creation, validation, and user restrictions.
## Features
1. **Custom Greetings and CAPTCHAs Per Group:**
    - The bot supports custom CAPTCHA greetings, messages, and validation settings for each group it manages.
    - New members are greeted with group-specific welcome messages and asked to solve a CAPTCHA.

2. **Multiple Supported Groups (Whitelist):**
    - Only works in groups specified in a whitelist (`custom_greetings` dictionary).
    - Settings can be customized for each group (e.g., CAPTCHA length, language, messages).

3. **User Restrictions:**
    - New members are restricted from chatting until they solve the CAPTCHA.
    - If they fail or ignore the CAPTCHA, they are removed (kicked) from the group.

4. **Advanced CAPTCHA Options:**
    - Custom settings include:
        - Numeric-only CAPTCHA.
        - Adjustable CAPTCHA code length.
        - Custom error messages for incorrect input or timeout.

5. **Bot Interaction Feedback:**
    - For successful CAPTCHA completion: A congratulatory message is sent, and the user gains full access to the group.
    - For failed CAPTCHA attempts: Warnings are sent, followed by removal from the group after multiple failures or timeout.

## Requirements
- **Python 3.7+**
- Required Libraries:
    - `pyTelegramBotAPI` (TeleBot)
    - `pyTelegramBotCAPTCHA`

Install dependencies with pip:
``` bash
pip install pyTelegramBotAPI pyTelegramBotCAPTCHA
```
## Setup
1. **Telegram Bot Token:**
    - Obtain your bot token from [BotFather]() on Telegram.
    - Replace `Your_API_Key` in the script with your bot's token.

2. **Group Whitelist and Settings:**
    - Add your group IDs to the `custom_greetings` dictionary.
    - Customize CAPTCHA messages, welcome texts, and error responses for each group.
    - Example settings for different groups:
``` python
     custom_greetings = {
         -1001594010258: CustomLanguage(
             text='Welcome to the Pineapple chat room, #USER!\nPlease enter code to confirm you are human.',
             try_again='Please try again!',
             your_code='Your captcha: ',
             wrong_user='❌: This captcha is not for you!',
             too_short='❌: The entered code is too short!'
         )
     }
```
1. **Run the Bot:**
    - Start the bot and it will monitor new members in the specified groups.

## How It Works
1. **New Members:**
    - When a new member joins a whitelisted group, they are greeted with a CAPTCHA message.
    - The member is temporarily restricted from interacting with the group until they solve the CAPTCHA.

2. **CAPTCHA Handling:**
    - **Correct Input:**
        - The bot unrestricts the member and congratulates them.

    - **Incorrect Input:**
        - The bot warns the user and provides another CAPTCHA attempt (up to two retries).

    - **Timeout or Multiple Failures:**
        - The user is automatically removed (kicked) from the group.

3. **Error Messages:**
    - The bot provides clear feedback for incorrect CAPTCHA attempts (e.g., invalid input or mismatched user).

## Example Configuration
Replace placeholder group IDs and bot token with real data:
``` python
custom_greetings = {
    -1001234567890: CustomLanguage(
        text='Welcome to Test Group #1, #USER!\nTo confirm you are human, please solve this CAPTCHA.',
        try_again='Try again, please!',
        your_code='Your captcha: ',
        wrong_user='This captcha is not for you!',
        too_short='The entered code is too short!'
    )
}

bot = TeleBot("123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11")
```
## Notes
- To share group IDs and showcase how the bot works, it is okay to keep **public group IDs**. However, if the groups are private, consider replacing the actual IDs with placeholders and provide instructions in the README so others can test it in their own groups.
- Example replacements for group IDs:
``` python
  custom_greetings = {
      -1001111111111: CustomLanguage(...),
      -1002222222222: CustomLanguage(...),
  }
```
In the README, mention, "_Replace `-1001111111111` with your group's actual chat ID._"
## License
This project is licensed under the MIT License. You may use, modify, and distribute it freely as long as this license is retained.
