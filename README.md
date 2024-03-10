
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

![ss](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/a20e7ed1-d51a-4bef-9447-36a831949cd6)


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
![Screenshot 2024-03-10 220407](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/e52d0720-ac4b-426f-bbb0-22eb159c9cf9)

```
# Get Historical Data - Taken example is of Reliance as instrument_token =  738561
import datetime
instrument_token =  738561
from_datetime = datetime.datetime.now() - datetime.timedelta(days=7)     # From last & days
to_datetime = datetime.datetime.now()
interval = "5minute"
print(kite.historical_data(instrument_token, from_datetime, to_datetime, interval, continuous=False, oi=False))
```
![Screenshot 2024-03-09 070852](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/6411ac18-2a3b-44f1-9658-e096e9a5fb0b)
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
![Screenshot 2024-03-09 071148](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/ce3f4b12-415d-4ee2-aebb-4d9fd43ce16a)

![p](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/270510c4-f3f4-4b70-bc08-9dd165b72d6f)
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
![Screenshot 2024-03-09 071633](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/e3efce41-aa05-48b6-a938-b54df1a28ee1)
![Screenshot 2024-03-09 071741](https://github.com/Anubhavmalik1/Zerodha_Login_LiveOrderPLacement/assets/147001039/c4ea9dc3-2127-4f63-a2a2-31845223047d)
```

