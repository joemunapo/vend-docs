# Telegram Bot API Setup

To integrate the Telegram Bot API into your application, follow these steps:

## Step 1: Install Vendor Packages

Ensure you have all the required packages installed in your project.

To install Vendor Packages:

```bash
composer install
```

## Step 2: Generate a Telegram Bot Key
- **Open Telegram** : Launch the Telegram app on your device or access Telegram Web.

- **Search for BotFather** : Use the search bar to find the BotFather bot, which is the official Telegram bot for creating and managing other bots.

- **Start a Chat with BotFather** : Click on BotFather to start a chat.

- **Create a New Bot** : Type the command /newbot and send it to BotFather.
Follow the instructions provided by BotFather to set up your new bot.
Provide a Name:

BotFather will ask you to provide a name for your new bot. Enter a name, such as
```bash
NameBot
```

- **Receive the API Key**:

After successfully creating the bot, BotFather will provide you with a Telegram Bot API key.
Add the API Key: Add the following line to the .env file with your copied API key