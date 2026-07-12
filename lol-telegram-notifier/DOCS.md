# LoL Telegram Notifier

The app checks configured EUW Riot IDs and sends a Telegram message when one or more
tracked players start a game.

## Configuration

- **Telegram bot token**: create the bot through @BotFather.
- **Riot API key**: use a Personal Riot API key for a persistent installation.
- **Telegram group chat ID**: the negative group ID returned by `discover-telegram`.
- **Players**: add each player as `GameName#TAG`. Telegram IDs are not needed unless a
  future version enables direct mentions.

Keep **Repeat notifications for testing** disabled outside local testing. Enable
**Start on boot** after the first successful test so Home Assistant starts the app after
every reboot.

## Installation

1. Push the private source repository to GitHub and wait for the image publishing
   workflow to complete.
2. Keep the `telegram-notification-bot-addon` GHCR package private. Configure the
   Home Assistant `ghcr.io` registry credential with a GitHub token that has
   `read:packages` access.
3. Add the separate public manifest repository to **Settings → Apps → App store → menu
   → Repositories**. The manifest repository contains only Home Assistant metadata;
   it does not expose this source repository or the image contents.
4. Install **LoL Telegram Notifier**, fill in the options, start it, and verify its logs.
5. Enable **Start on boot** and **Auto update** in the app settings.

The source publishing workflow needs GitHub Actions workflow permissions set to **Read
and write permissions**. The private-image workflow and manifest synchronization should
use a dedicated token with the minimum required access to their respective repositories.
