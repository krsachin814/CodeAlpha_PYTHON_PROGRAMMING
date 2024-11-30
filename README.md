# CodeAlpha_PYTHON_PROGRAMMING
import yfinance as yf

def get_stock_info(ticker):
    stock = yf.Ticker(ticker)
    stock_info = stock.history(period='1d')  
    
    if not stock_info.empty:
        print(f"Stock: {ticker}")
        print(f"Open: {stock_info['Open'].iloc[0]}")
        print(f"High: {stock_info['High'].iloc[0]}")
        print(f"Low: {stock_info['Low'].iloc[0]}")
        print(f"Close: {stock_info['Close'].iloc[0]}")
        print(f"Volume: {stock_info['Volume'].iloc[0]}")
    else:
        print("Invalid ticker symbol or no data available.")


ticker_symbol = input("Enter a stock ticker symbol (e.g., AAPL, TSLA): ")
get_stock_info(ticker_symbol)


portfolio = {}

def add_stock(ticker, shares, buy_price):
    if ticker in portfolio:
        print(f"{ticker} is already in the portfolio. Updating the details.")
    portfolio[ticker] = {'shares': shares, 'buy_price': buy_price}
    print(f"Added {shares} shares of {ticker} at ${buy_price} each.")


ticker = input("Enter stock ticker symbol: ").upper()
shares = int(input(f"Enter number of shares for {ticker}: "))
buy_price = float(input(f"Enter buy price for {ticker}: "))

add_stock(ticker, shares, buy_price)


print("Current Portfolio:")
for ticker, details in portfolio.items():
    print(f"Ticker: {ticker}, Shares: {details['shares']}, Buy Price: {details['buy_price']}")

def remove_stock(ticker):
    if ticker in portfolio:
        del portfolio[ticker]
        print(f"Removed {ticker} from the portfolio.")
    else:
        print(f"{ticker} not found in the portfolio.")


ticker = input("Enter stock ticker symbol to remove: ").upper()
remove_stock(ticker)


print("Updated Portfolio:")
for ticker, details in portfolio.items():
    print(f"Ticker: {ticker}, Shares: {details['shares']}, Buy Price: {details['buy_price']}")

def track_performance():
    print("Tracking Portfolio Performance...\n")
    for ticker, details in portfolio.items():
        stock = yf.Ticker(ticker)
        stock_info = stock.history(period='1d')  
        
        if not stock_info.empty:
            current_price = stock_info['Close'][0]  
            shares = details['shares']
            buy_price = details['buy_price']
            
            
            current_value = shares * current_price
            profit_loss = (current_price - buy_price) * shares
            
            
            print(f"Stock: {ticker}")
            print(f"Shares: {shares}")
            print(f"Buy Price: ${buy_price}")
            print(f"Current Price: ${current_price:.2f}")
            print(f"Current Value: ${current_value:.2f}")
            print(f"Profit/Loss: ${profit_loss:.2f}\n")
        else:
            print(f"Could not fetch data for {ticker}.")
            
track_performance()
