
# PRDT Pro V2 Bot

This bot allows users to play on PRDT.FINANCE Pro v2 on their own computers / servers without the necessity of frontend.

## Install
```bash
git clone https://github.com/PRDTfinance/PRDT-PRO-BOT
```

```bash
npm install
```

## Setup
create .env file that inclused the private key of the account

example:
```bash
PRIVATE_KEY=62da64f3dd3090dcc0f154163878bb627a6c4c523c1b087322fb2a6c309fa4da
```

### Why Private Key?

PRDT.FINANCE PRO uses web3 authentication. User needs to connect to the system by signing a message with their wallets. When using the frontend, this signing is done through user wallets such as Metamask. As the bots are running on servers, they need to sign these messages using a private key.

PRDT.FINANCE PRO system uses the balances of already deposited amounts. This script does not send any transaction using the private key. User needs to deposit on front-end before using this bot.

## Usage

import newBet and authenticate functions from lib
```js
import { newBet, authenticate } from "./lib.js";
```

call authenticate to get access to the api
```js
await authenticate();
```

call newBet with your desired settings
```js
await newBet({
    network: "polygon",
    bettingToken: "matic",
    targetToken: "btc",
    interval: 180,
    amount: 7.3,
    position: 0,
  });
```

## Bet Options
```js
network can be "polygon", "bsc"
bettingToken can be "matic", "bnb", "usdt"
targetToken can be "btc", "eth", "matic", "ada", "doge", "sol"
interval is in seconds, 180 is 3 minutes
amount is betting amount in decimals. no need to convert to wei
position, 0 is up 1 is down
```

## Other Functions

getBalances() 

```js
import { getBalances } from "./lib.js";
```
returns balance amounts the bot. 

```js
  const balances = await getBalances();
```

Example output:

```js
  { network: 'polygon', token: 'matic', amount: 40.1849 },
  { network: 'bsc', token: 'bnb', amount: 0.018 },
```

getBets() 

```js
import { getBets } from "./lib.js";
```
returns latest bets of the user to follow up bet results.
requires network parameter

```js
  const bets = await getBets({network: "polygon"});
```
Example output:

```js
  {
    network: 'polygon',
    sender: '0xaddress',
    bettingToken: 'matic',
    targetToken: 'btc',
    currentEpoch: 393,
    closeTimestamp: '2023-03-13T14:04:08.898Z',
    amount: 10,
    calculated: true,
    startTimestamp: '2023-03-13T14:01:08.901Z',
    samePrice: false,
    won: true
  }
```

## Disclaimers

All investment strategies and investments involve risk of loss.

Nothing contained in this program, scripts, code or repository should be construed as investment advice. Any reference to an investment's past or potential performance is not, and should not be construed as, a recommendation or as a guarantee of any specific outcome or profit. By using this program you accept all liabilities, and that no claims can be made against the developers or others connected with the program.
