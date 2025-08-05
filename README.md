# Daily Swap for Portal Plume Mainnet ( Izumi DEX )
Update for daily auto swap Plume Portal (pUSD -> PLUME). Izumi DEX earn points.

![izumi](https://github.com/user-attachments/assets/0cce5907-4712-499e-97e5-a24da84fa548)

## Feature bot
- Automated wallet login and authentication.
- Auto approve.
- You can set how much you want per day. 

### Link :
https://portal.plume.org/?referrer=CornflowerResourcefulSort487

## Installation

Clone the project and install dependencies:

```bash
screen -S Izumi
```

```bash
git clone https://github.com/Espenzuyderwyk/Autoswap-plumeV2.git
```
```bash
cd Autoswap-plumeV2
```
```bash
npm install
```

## ⚙️ Environment Setup
Create a .env file in the root directory:

```bash
nano .env
```

Input your private key and wallet address

```bash
RPC_URL=https://rpc.plume.org
PRIVATE_KEY=0xYOUR_PRIVATE_KEY
WALLET_ADDRESS=0xYOUR_WALLET_ADDRESS

PUSD=0xdddD73F5Df1F0DC31373357beAC77545dC5A6f3F
WPLUME=0xEa237441c92CAe6FC17Caaf9a7acB3f953be4bd1
ROUTER=0x77aB297Da4f3667059ef0C32F5bc657f1006cBB0
```

## ▶️ Run the Bot
To run the automated PLUME ↔ pUSD swap bot:

```bash
node index.js
```

Set how much you want per day.

![plumepoints](https://github.com/user-attachments/assets/f2378ba1-c612-4deb-9967-6b848a9758b7)


### * If this bot doesn't work, you can swap manually first via Izumi DEX.

# The bot will:
1. Login wallet
2. Display information
3. Process transactions daily
4. Monitor and display user stats

# Disclaimer

This script is created for educational and personal experimentation purposes. It is not to be used for illegal activities, spam, or violations of GitHub rules.

- Use of this script is entirely the responsibility of the user.
- Do not use it to violate GitHub's Terms of Service.

#Plume #PortalPlume #dailybot #autoswap #Web3 #PlumeNetwork
