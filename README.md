<h1>
  <img src="https://play-lh.googleusercontent.com/xBMmaATox_2z_rb76UCJjh89iWITz6Ivqq4FyguM6bpi7429suZHIoB-exrAAJkyrQ=w480-h960-rw" width="28" style="vertical-align:middle;" />
  checkers_online.py
</h1>

> Mobile-API for [CheckersOnline](https://play.google.com/store/apps/details?id=com.rstgames.checkers) automate and interact with the popular mobile checkers game via its TCP socket API.

---

## Quick Start

```python
from checkers_online import CheckersOnline

# Connects and handshakes automatically on init
client = CheckersOnline()

# Login with your access token
client.login_with_access_token(access_token="your_token_here")
```

> On instantiation, `CheckersOnline` automatically opens a TCP socket, performs the session handshake, and verifies the session — no extra setup needed.

---

## Features

- 🔌 **Connection** — automatic TCP socket connection and session verification on init
- 🔐 **Auth** — login with access token
- 🎮 **Games** — create, join, leave, and search games
- 🏳️ **In-game actions** — ready up, surrender, draw requests, send emotes
- 👥 **Friends** — send/accept/decline/delete friend requests
- 💬 **Messaging** — send and delete private messages, invite to game
- 👤 **Users** — search users, view profiles, save notes
- 🏆 **Assets & Achievements** — select skins, achievements
- 💎 **Shop** — view prices, buy premium and points
- 📋 **Lobby** — browse available games with filters

---

## Usage

### Auth

```python
client = CheckersOnline(debug=True)  # enable debug logging
client.login_with_access_token(access_token="your_token_here")
```

### Games

```python
# Create a game (type 1 = standard, fast mode, 100 bet)
client.create_game(type=1, bet=100, fast=True)

# Create a private game with password
client.create_game(type=1, bet=500, password="secret")

# Join a game by ID
client.join_to_game(game_id=12345)

# Join a private game
client.join_to_game(game_id=12345, password="secret")

# Leave current game
client.leave_from_game()
```

### In-Game Actions

```python
# Signal ready
client.ready()

# Surrender
client.surrender()

# Request a draw
client.send_draw_request()

# Send an emote/smile
client.send_smile_in_game(smile_id=3)
```

### Lobby Browser

```python
# Browse open games with filters
client.lookup_start(
    type=[1, 2],
    bet_min=100,
    bet_max=10000,
    fast=[True, False]
)

# Stop browsing
client.lookup_stop()
```

### Friends

```python
# Search for a user
client.search_user(nickname="PlayerOne")

# Send / accept / cancel / delete
client.send_friend_request(user_id=123)
client.accept_friend(user_id=123)
client.cancel_friend_request(user_id=123)
client.delete_friend(user_id=123)

# Get your friends list
client.get_friends_list()
```

### Messaging

```python
# Send a private message
client.send_user_message(user_id=123, message="Good game!")

# Delete a message
client.delete_messege(message_id=456)

# Invite a user to your game
client.invite_to_game(user_id=123)
```

### Users & Notes

```python
# Get user profile
client.get_user_info(user_id=123)

# Save a note on a user (color 0–5)
client.save_note(user_id=123, note="Cheater", color=1)
```

### Profile

```python
# Change your nickname
client.update_nickname(nickname="NewName")

# Select an asset/skin
client.select_asset(asset_id=7)

# Select an achievement to display
client.select_achieve(achieve_id=3)

# Get all available assets
client.get_assets()
```

### Shop

```python
# View prices
client.get_premium_price()
client.get_points_price()

# Buy premium or points (id = product tier)
client.buy_premium(id=1)
client.buy_points(id=2)
```

---

## API Reference

| Method                      | Returns | Description                              |
|-----------------------------|---------|------------------------------------------|
| `login_with_access_token`   | `dict`  | Authenticate with token                  |
| `create_game`               | —       | Create a new game room                   |
| `join_to_game`              | —       | Join a game by ID                        |
| `leave_from_game`           | —       | Leave the current game                   |
| `ready`                     | —       | Signal ready to start                    |
| `surrender`                 | —       | Surrender the current game               |
| `send_draw_request`         | —       | Offer a draw to opponent                 |
| `send_smile_in_game`        | —       | Send an emote in-game                    |
| `lookup_start`              | —       | Start browsing open games                |
| `lookup_stop`               | —       | Stop browsing open games                 |
| `search_user`               | `dict`  | Search users by nickname                 |
| `get_user_info`             | `dict`  | Get a user's profile                     |
| `get_friends_list`          | `dict`  | List your friends                        |
| `send_friend_request`       | —       | Send a friend request                    |
| `accept_friend`             | —       | Accept a friend request                  |
| `cancel_friend_request`     | —       | Decline a friend request                 |
| `delete_friend`             | —       | Remove a friend                          |
| `send_user_message`         | —       | Send a private message                   |
| `delete_messege`            | —       | Delete a message                         |
| `invite_to_game`            | —       | Invite a user to your game               |
| `save_note`                 | —       | Save a note on a user                    |
| `update_nickname`           | —       | Change your display name                 |
| `select_asset`              | —       | Equip an asset/skin                      |
| `select_achieve`            | —       | Display an achievement                   |
| `get_assets`                | `dict`  | List all available assets                |
| `get_friends_list`          | `dict`  | Get your friends list                    |
| `get_bets`                  | `dict`  | Get available bet options                |
| `get_premium_price`         | `dict`  | Get premium subscription prices          |
| `get_points_price`          | `dict`  | Get points package prices                |
| `buy_premium`               | —       | Purchase a premium subscription          |
| `buy_points`                | —       | Purchase a points package                |
| `get_captcha`               | `dict`  | Request a captcha challenge              |
| `get_purchase_ids`          | `dict`  | Get available in-app purchase IDs        |

---

## Constructor Options

```python
CheckersOnline(
    platform="android",  # platform identifier sent to server
    debug=False,         # enable verbose debug logging
    language="ru",       # language code
)
```
