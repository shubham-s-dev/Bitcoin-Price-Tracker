#  Bitcoin Price Tracker

A Python automation bot that monitors live Bitcoin prices using the CoinGecko API.
When the price drops below your target, it sends an instant alert to your Telegram.

##  Tech Stack
* **Python** (Requests, Time)
* **API:** CoinGecko (No Key Required)
* **Notification:** Telegram Bot API

##  How it Works
1. Fetches real-time BTC/USD price.
2. Compares it with your `target_price`.
3. Sends a "BUY NOW" alert if the price is low.
4. Runs 24/7 with error handling.

##  Author
**Shubham S** (shubham-s-dev)
