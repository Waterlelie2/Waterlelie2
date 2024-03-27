import requests
import time
import random
import matplotlib.pyplot as plt
API_KEY = 'YOUR_COINLAYER_API_KEY'
balances = []
timestamps = []
# Functie om de huidige prijs van een cryptocurrency op te halen vanuit Coinlayer
def get_crypto_price(symbol):
    url = f'https://api.coinlayer.com/convert?access_key={API_KEY}&from={symbol}&to=USD&amount=1'
    response = requests.get(url)
    data = response.json()
    return data['rates']['USD']
# Strategie 1: Simuleer de Bitvavo-exchange
def get_bitvavo_price():
    return random.uniform(30000, 60000)
# Strategie 2: Simuleer de Fetch.ai-exchange
def get_fetch_price():
    return random.uniform(0.10, 1.00)
# Strategie 3: Simuleer handelsbeslissingen met winst zonder verlies
def make_trade(balance, price, coins_owned):
    max_amount_to_trade = balance / 10
    if price < 35000:
        amount_to_buy = max_amount_to_trade
        balance -= amount_to_buy * price
        return balance, amount_to_buy, price, 'buy', coins_owned
    elif price < 0.50:
        amount_to_buy = max_amount_to_trade / price
        balance -= amount_to_buy * price
        coins_owned += amount_to_buy
        return balance, amount_to_buy, price, 'buy', coins_owned
    elif price > 50000:
        amount_to_sell = max_amount_to_trade
        balance += amount_to_sell * price
        return balance, amount_to_sell, price, 'sell', coins_owned
    elif price > 0.75:
        amount_to_sell = max_amount_to_trade / price
        balance += amount_to_sell * price
        coins_owned -= amount_to_sell
        return balance, amount_to_sell, price, 'sell', coins_owned
    else:
        return balance, 0, price, 'hold', coins_owned
# Hoofdloop van de bot
def crypto_bot():
    initial_balance = 1000
    balance = initial_balance
    fetch_coins_owned = 76
    iteration = 0
    while True:
        bitvavo_price = get_bitvavo_price()
        fetch_price = get_fetch_price()
        btc_price = get_crypto_price('BTC')
        balance, amount, price, action, fetch_coins_owned = make_trade(balance, btc_price, fetch_price, fetch_coins_owned)
        
        balances.append(balance)
        timestamps.append(iteration)
        
        print(f"Iteration: {iteration}, Balance: {balance}, Action: {action}, Amount: {amount}, Bitvavo Price: {bitvavo_price}, Fetch.ai Price: {fetch_price}, Fetch.ai Coins Owned: {fetch_coins_owned}, BTC Price: {btc_price}")
        
        if iteration % 10 == 0:
            plot_graph(timestamps, balances)
        
        iteration += 1
        time.sleep(5)
# Functie om de balans over de tijd te plotten
def plot_graph(timestamps, balances):
    plt.plot(timestamps, balances)
    plt.xlabel('Iteration')
    plt.ylabel('Balance')
    plt.title('Balance over Time')
    plt.show()
# Start de bot
if __name__ == "__main__":
    crypto_bot()- 👋 Hi, I’m @Waterlelie2
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Waterlelie2/Waterlelie2 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
