# Reft
import requests

def get_bitcoin_price(currency='usd'):
    """Function to get the current Bitcoin price in the selected currency (default is USD)."""
    url = f'https://api.coingecko.com/api/v3/simple/price?ids=bitcoin&vs_currencies={currency}'
    response = requests.get(url)
    
    if response.status_code == 200:
        data = response.json()
        return data['bitcoin'][currency]
    else:
        print("Error getting Bitcoin price data.")
        return None

def btc_to_currency(btc_amount, currency='usd'):
    """Function to convert Bitcoin amount to the selected currency (e.g., USD)."""
    price = get_bitcoin_price(currency)
    if price is not None:
        return btc_amount * price
    else:
        return None

def calculator():
    print("Welcome to the Bitcoin calculator!")
    
    while True:
        print("\nMenu:")
        print("1. Convert Bitcoin to currency")
        print("2. Exit")
        
        choice = input("Choose an option: ")

        if choice == '1':
            try:
                btc_amount = float(input("Enter the amount of Bitcoin: "))
                currency = input("Enter the currency to convert to (e.g., usd, rub): ").lower()
                result = btc_to_currency(btc_amount, currency)
                
                if result is not None:
                    print(f"{btc_amount} BTC = {result} {currency.upper()}")
                else:
                    print("Conversion failed.")
            except ValueError:
                print("Please enter a valid Bitcoin amount.")
        
        elif choice == '2':
            print("Exiting the program.")
            break
        
        else:
            print("Invalid choice, please try again.")

if __name__ == '__main__':
    calculator()

