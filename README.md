import requests
import time

# --- CONFIGURATION ---
crypto_url = "https://api.coingecko.com/api/v3/simple/price"
tele_key = "YOUR_TELEGRAM_BOT_TOKEN_HERE"
chat_id = "YOUR_CHAT_ID_HERE"
tele_url = f"https://api.telegram.org/bot{tele_key}/sendMessage"

target_price = 95000

headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/91.0.4472.124 Safari/537.36"
}

params = {
    "ids": "bitcoin",
    "vs_currencies": "usd"
}


print("-----BTC PRICE TRACKER STARTED-----")

while True:
    try:
        response = requests.get(crypto_url , params=params, headers=headers)

        if response.status_code == 200: 
            request = response.json()
            data = request['bitcoin']['usd']
            current_price = data

            print(f"Current BTC: ${current_price} | Target: ${target_price}")

            if current_price < target_price:
                    print("🚨 PRICE DROP! Sending Alert...")

                    message_params = {
                        "chat_id": chat_id, 
                        "text": f"BUY NOW! BTC is {current_price}"
                    }
                
                    requests.get(tele_url, params=message_params)
                    print("✅ Alert Sent!")

                    # Alert bhejne ke baad thoda lamba break lo taaki spam na ho
                    time.sleep(60)
            else:
                print("price still high") 
        else:
            print(f"API Error: {response.status_code}")

        
    except Exception as e:
        print(f"Error: {e}")
        
    
    # CoinGecko Free API limit: 10-30 requests per minute.
    # 60 Seconds is safe. 20s me Block ho sakte ho.
    print("⏳ Waiting 60 seconds...")
    time.sleep(60)
