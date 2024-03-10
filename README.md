
# Python Code for Kite Zerodha Platform

### Prerequisites

Python using 3.12.2

### Python Code Example
Import
```python

from kite_trade import *

```
Log In Method
```python
# # First Way to Login
# # You can use your Kite app in mobile
# # But You can't login anywhere in 'kite.zerodha.com' website else this session will disconnected

user_id = ""       # Login Id
password = ""      # Login password
twofa = ""         # Login Pin or TOTP - It is a pin which you get in APP code section

enctoken = get_enctoken(user_id, password, twofa)
kite = KiteApp(enctoken=enctoken)
```
Log In Method
```python
# # Second way is provide 'enctoken' manually from 'kite.zerodha.com' website
# # Than you can use login window of 'kite.zerodha.com' website Just don't logout from that window

enctoken = ""
kite = KiteApp(enctoken=enctoken)
```

![Screenshot 2024-03-10 230443](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/bed9498a-6673-4b8b-b6ce-8198eca4287f)


Other Methods
```python
# Basic calls
print(kite.margins())
print(kite.orders())
print(kite.positions())
```
```
# Get instrument or exchange
print(kite.instruments())
print(kite.instruments("NSE"))
print(kite.instruments("NFO"))

# Get Live Data or last traded data
print(kite.ltp("NSE:RELIANCE"))
print(kite.ltp(["NSE:NIFTY 50", "NSE:NIFTY BANK"]))
print(kite.quote(["NSE:NIFTY BANK", "NSE:ACC"]))
```

![Screenshot 2024-03-10 230553](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/30201f3f-19b6-4c69-b901-d46a56eecef7)

```
# Get Historical Data - Taken example is of Reliance as instrument_token =  738561
import datetime
instrument_token =  738561
from_datetime = datetime.datetime.now() - datetime.timedelta(days=7)     # From last & days
to_datetime = datetime.datetime.now()
interval = "5minute"
print(kite.historical_data(instrument_token, from_datetime, to_datetime, interval, continuous=False, oi=False))
```

![Screenshot 2024-03-10 230722](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/06db6bf2-a3e2-466b-840c-648df05cc645)

```
# Place Order
order = kite.place_order(variety=kite.VARIETY_AMO,
                         exchange=kite.EXCHANGE_NSE,
                         tradingsymbol="RELIANCE",
                         transaction_type=kite.TRANSACTION_TYPE_BUY,
                         quantity=10,
                         product=kite.PRODUCT_CNC,
                         order_type=kite.ORDER_TYPE_MARKET,
                         price=None,
                         validity=None,
                         disclosed_quantity=None,
                         trigger_price=None,
                         squareoff=None,
                         stoploss=None,
                         trailing_stoploss=None,
                         )

print(order)
```
![Screenshot 2024-03-10 230855](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/84da0449-2392-472f-b24f-ee9f13a38493)

![Screenshot 2024-03-10 230947](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/70f3b4a6-3640-47e0-88c2-a2a63422d3a3)

```
# Modify order
kite.modify_order(variety=kite.VARIETY_AMO,
                  order_id="order_id",
                  parent_order_id=None,
                  quantity=5,
                  price=200,
                  order_type=kite.ORDER_TYPE_LIMIT,
                  trigger_price=None,
                  validity=kite.VALIDITY_DAY,
                  disclosed_quantity=None)

# Cancel order
kite.cancel_order(variety=kite.VARIETY_AMO,
                  order_id="order_id",
                  parent_order_id=None)
```
![Screenshot 2024-03-10 231236](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/1061ddf3-6fba-48ca-97d9-bb1e0ce316d5)

![Screenshot 2024-03-10 231323](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/15557e3d-4af9-4756-8f69-2530857c94cf)

```

