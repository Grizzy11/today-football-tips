#!/usr/bin/env python3
import requests
from telegram import Bot
import datetime

# Bot setup
TELEGRAM_TOKEN = "8436380315:AAGB4kldLn3-53v3T7heHHFvu2a5FGVCGK0"
CHANNEL_ID = "@Todayfootball_tips"

bot = Bot(token=TELEGRAM_TOKEN)

# Get today fixtures from SofaScore
def scrape_matches():
    today = datetime.datetime.now().strftime("%Y-%m-%d")
    url = f"https://www.sofascore.com/api/v1/sport/football/scheduled-events/{today}"
    headers = {"User-Agent": "Mozilla/5.0"}
    response = requests.get(url, headers=headers)
    if response.status_code != 200:
        return []

    data = response.json()
    matches = []
    for event in data.get("events", []):
        match = {
            "id": event["id"],
            "home": event["homeTeam"]["name"],
            "away": event["awayTeam"]["name"]
        }
        matches.append(match)
    return matches

# Get odds for a match
def get_odds(event_id):
    url = f"https://www.sofascore.com/api/v1/event/{event_id}/odds/1/all"
    headers = {"User-Agent": "Mozilla/5.0"}
    response = requests.get(url, headers=headers)
    if response.status_code != 200:
        return None

    data = response.json()
    markets = data.get("markets", [])
    for market in markets:
        if market["marketName"] == "Match Winner":
            outcomes = market["outcomes"]
            return {
                "home": outcomes[0]["value"],
                "draw": outcomes[1]["value"],
                "away": outcomes[2]["value"]
            }
    return None

# Pick predictions until ~20 odds
def pick_predictions(matches):
    predictions = []
    total_odds = 1.0

    for match in matches:
        odds = get_odds(match["id"])
        if not odds:
            continue

        # Pick safer option (lower odd)
        if odds["home"] <= odds["away"]:
            tip = f"⚽ <b>{match['home']} vs {match['away']}</b>\n👉 Tip: {match['home']} Win @ {odds['home']}"
            total_odds *= odds["home"]
        else:
            tip = f"⚽ <b>{match['home']} vs {match['away']}</b>\n👉 Tip: {match['away']} Win @ {odds['away']}"
            total_odds *= odds["away"]

        predictions.append(tip)

        if total_odds >= 20:
            break

    return predictions, total_odds

def post_to_telegram():
    matches = scrape_matches()
    if not matches:
        bot.send_message(chat_id=CHANNEL_ID, text="⚠️ No matches found today.")
        return

    tips, total_odds = pick_predictions(matches)
    today = datetime.datetime.now().strftime("%Y-%m-%d")

    message = f"🔥 <b>Today’s Football Tips ({today})</b> 🔥\n\n"
    message += "\n\n".join(tips)
    message += f"\n\n📊 <b>Total Odds ≈ {round(total_odds, 2)}</b>\n\n"
    message += "💡 Bet smart. Good luck! 🍀"

    # ✅ Unpin previous message (if any)
    try:
        bot.unpin_all_chat_messages(chat_id=CHANNEL_ID)
    except Exception as e:
        print("⚠️ No old pin to remove:", e)

    # ✅ Send today’s tips
    sent = bot.send_message(chat_id=CHANNEL_ID, text=message, parse_mode="HTML")

    # ✅ Pin today’s message
    bot.pin_chat_message(chat_id=CHANNEL_ID, message_id=sent.message_id, disable_notification=True)

if __name__ == "__main__":
    post_to_telegram()
    print("✅ Daily tips posted, old pin cleared, new pin set.")
