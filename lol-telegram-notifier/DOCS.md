# LoL Telegram Notifier

The app checks configured EUW Riot IDs and sends a Telegram message when one or more
tracked players start a game.

## Configuration

- **Telegram bot token**: create the bot through @BotFather.
- **Riot API key**: use a Personal Riot API key for a persistent installation.
- **Players**: add each player as `GameName#TAG`. Telegram IDs are not needed unless a
  future version enables direct mentions.
- **Teammate exclusion players**: optional Riot IDs in `GameName#TAG` format. A notification
  is suppressed only when one of these players is on the same team as a tracked player; an
  excluded opponent does not suppress the notification.
- **Weekly statistics**: enabled by default. The bot sends the previous Monday-to-Sunday
  recap at the configured Monday local time. It stores match history for the configured
  retention period.
- **Inline League profile icons**: optional. First send `/myid` to the bot in a private
  chat, enter that number as **Emoji set owner Telegram ID**, then enable the setting.
  The bot creates and maintains its own custom-emoji set; no manual sticker-pack setup is
  required. Leaving this ID blank is safe and keeps normal text notifications running.

After starting the app, add the bot to a group and send `/enable` there. The bot confirms
the subscription in that chat. Use `/test` to send a sample notification and `/disable` to
unsubscribe the group. `/enable@BotUsername`, `/test@BotUsername`, and
`/disable@BotUsername` work too.

Use `/stats_current` in an enabled chat to test the recap for the current calendar week,
or `/stats_last7` for the rolling seven-day window. The recap includes per-mode and solo
win rates, duos and recurring squads with at least the configured minimum number of games,
longest loss streaks, and shortest/longest games.

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
4. Install **LoL Telegram Notifier**, fill in the options, start it, add the bot to a group,
   then run `/enable` and `/test` in that group.
5. Enable **Start on boot** and **Auto update** in the app settings.

The source publishing workflow needs GitHub Actions workflow permissions set to **Read
and write permissions**. The private-image workflow and manifest synchronization should
use a dedicated token with the minimum required access to their respective repositories.
