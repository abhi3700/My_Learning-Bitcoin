## Installation Guide
Follow the steps: 
* Step-1: Install the Python directly via [Anaconda](https://anaconda.org/)
* Step-2: Now, pip library is installed. If not, use ```conda install pip``` in your command prompt (for Windows).
* Step-3: Use the command ```pip install bitcoin``` to install bitcoin in your system. 
![Bitcoin-python installation.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513422930/gslcqj6fnnx94p9xqtn0.png)
In my case, the **Bitcoin** is already installed.
#### NOTE: The best part in this installation is that we can fetch the Bitcoin related data w/o being a full node i.e. downloading the entire **Bitcoin-blockchain** (approx. 150 GB size till date). Please find [here](https://blockchain.info/charts/blocks-size) for recent size.
![bitcoin-blockchain size _ Dec 2017.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513423362/de4g4ojwporlyedinpcb.png)
This Py-bitcoin fetches the data from "Blockchain.info" API.

## Demo
Here, Python coding can be done in 2 ways: - 
* Command prompt - 
![bticoin python_coding in cmd.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513423812/q5mt4gbov29ggonyh6em.png)

* Jupyter notebook - 
![bticoin python_coding in jupyter notebook.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513423958/bqejrjn4j5ui6berv71w.png)

Now, the notebook opens in the browser as follows: 
![bticoin python_coding in jupyter notebook_2.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513424123/djyhtsscviy2eict5c6m.png)

use commands in the notebook - 
![bticoin python_coding in jupyter notebook_3.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513424218/bs6tblxwkcxlyuplqhmo.png)

Please, find the code below:
```python
# import bitcoin 
from bitcoin import*

# Generate private key
my_private_key = random_key()
print("My private key: " + my_private_key)

# Generate public key
my_public_key = privtopub(my_private_key)
print("My public key: " + my_public_key) 
```

## Basic commands
Here, are a few basic commands to use Bitcoin protocol. 
First, we need to import the bitcoin library like this -
```python
# import bitcoin 
from bitcoin import*
```
* Generate private key
```python
my_private_key = random_key()
print("My private key: " + my_private_key)
```
![bitcoin_private_key.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513427632/lq65ly92wmcs0wcfmupy.png)

* Generate public key
```python
my_public_key = privtopub(my_private_key)
print("My public key: " + my_public_key) 
```
![bitcoin_public_key.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513427648/xyjohyhngimrxalkh4zj.png)

* Create a bitcoin wallet address. Unlike Email id - Each time bitcoin address can be generated for each transaction.
```python
my_address = pubtoaddr(my_public_key)
print("My address: " + my_address)
```
![bitcoin_address.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513427666/wlxnxpevdicbiz7spzr3.png)

### Multi-signature wallet
This require multiple private-public keys.
**Application**: In organizations, suppose there is a account accessed by multiple members. Suppose, someone wants to make any transaction using that wallet address. In this case, we can use multi-signature wallet in order to unanimously decide on transactions happening from the company's wallet address. Hence, it would requrie the signature of each member. Therefore, account security is enhanced.

* Generate private keys
```python
# Create private keys
private_key1 = random_key()
private_key2 = random_key()
private_key3 = random_key()
```

* Generate public keys
```python
# Create public keys
public_key1 = privtopub(private_key1)
public_key2 = privtopub(private_key2)
public_key3 = privtopub(private_key3)
```

* Create Multi signature wallet
```python
my_multi_sig = mk_multisig_script(public_key1, public_key2, public_key3, 2, 3)
my_multi_address = scriptaddr(my_multi_sig)
print("My multi signature wallet address: " + my_multi_address)
```
![bitcoin_multi-sig_address.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513434322/qdd8pnrsqun8xwnv8zjw.png)

### History of a transaction
Through this function, we will see the bitcoin received (unit is in satoshi)
* Here, a valid address has few transactions. For more click [here](https://blockchain.info/address/13bUJhSbGLvkLK2xHf3mUqR7eXhQ1Uzg8Z).
![blockchain_info_tx_1.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513437450/wpugfmremdvg44idai6r.png)

**Code ** - 
```python
# a valid address 
valid_address = "13bUJhSbGLvkLK2xHf3mUqR7eXhQ1Uzg8Z"
print(history(valid_address))
```
![bitcoin_tx_history_1.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513437543/eb5xeyebvtjreugpw7pt.png)

* Here, another valid address has nearly 380 transactions. For more click [here](https://blockchain.info/address/1Nh7uHdvY6fNwtQtM1G5EZAFPLC33B59rB).
![blockchain_info_tx_380.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513437341/wwemk1a3qrsnec3as5pu.png)

**Code ** - 
```python
# a valid address 
valid_address = "1Nh7uHdvY6fNwtQtM1G5EZAFPLC33B59rB"
print(history(valid_address))
```
![bitcoin_tx_history_380.png](https://res.cloudinary.com/hpiynhbhq/image/upload/v1513437702/vdyoja1u7milhwezvmwz.png)

### Reference:
* https://www.youtube.com/watch?v=um9omi943jw&list=PLTgRMOcmRb3NGr6RA_mhSWvg6BSXI8hjN&index=2
