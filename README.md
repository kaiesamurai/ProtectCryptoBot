# ProtectCryptoBot

ProtectCryptoBot is a Telegram Mini App that demonstrates the integration of the ProtectCryptoBot Passkey Wallet, enabling users to interact with decentralized wallets seamlessly. This bot is designed for developers to showcase how to embed ProtectCryptoBot Passkey Wallet functionality into a Telegram Mini App.

## Vision

Empower developers to integrate decentralized wallet services into Telegram Mini Apps, providing users with seamless and secure access to DeFi services.

## Quick Start

### Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/botfi-app/protectcryptobot && cd protectcryptobot
   ```

2. Install dependencies:
   ```sh
   pnpm install
   ```

3. Update the configuration file:
   - Open and update `CALLBACK_SERVER_URL` and `ProtectCryptoBot_APP_URL` in `env/index.ts`.
     ```ts
     // env/index.ts
     export const CALLBACK_SERVER_URL = 'https://api.example.com/bot/api/v1/';
     export const ProtectCryptoBot_APP_URL = 'https://testnet.ProtectCryptoBot.dev'; // use https://app.joy.id for production
     ```

### Build and Test

1. Build the project:
   ```sh
   pnpm build
   ```

2. Run tests:
   ```sh
   pnpm test
   ```

### Build Your Own Telegram Mini App

#### ProtectCryptoBot URL

The ProtectCryptoBot Passkey Wallet requires an external browser to implement WebAuthn registration and login. Use the following functions to build URLs to connect the wallet, sign messages, and send Ethereum transactions:

- `buildConnectTokenAndUrl`
- `buildSignMsgTokenAndUrl`
- `buildSignTxTokenAndUrl`
- `buildSendTxTokenAndUrl`

#### Server Configuration

The ProtectCryptoBot Passkey Wallet interacts with your server to process messages and transactions. Implement the following APIs on your server:

1. **Receive message from ProtectCryptoBot Passkey Wallet:**
   - Route: `/messages`
   - Method: POST
   - Request:
     ```json
     {
       "token": "string",
       "message": "json string"
     }
     ```

2. **Telegram mini app gets message from server:**
   - Route: `/messages/:token`
   - Method: GET
   - Response:
     ```json
     {
       "message": "json string"
     }
     ```

### Message Format

The message format is a JSON string. Here are examples for different operations:

#### Connection
- **Approve:**
  ```json
  "message": "{\"address\":\"0x8ac36d0e764FF17dcF13b2465e77b4fe125EC2bC\"}"
  ```
- **Reject:**
  ```json
  "message": "{\"address\":\"rejected\"}"
  ```

#### Sign Message
- **Approve:**
  ```json
  "message": "{\"signature\":\"0xacf1fadf82f619fc5adc8bf956d0312a99f9915bf5b19e5c5e952485308d741347075a4a5d0c4fa8a8784b8ce79d6d68040e028aa1e7e7c5ee82c52bd1982e831b\"}"
  ```
- **Reject:**
  ```json
  "message": "{\"signature\":\"rejected\"}"
  ```

#### Sign Transaction
- **Approve:**
  ```json
  "message": "{\"signature\":\"0x02f87083aa36a7050b840e4d274a825208948ac36d0e764ff17dcf13b2465e77b4fe125ec2bc87038d7ea4c6800080c080a069d6956ba2d379cbefd02604f0f48628367cd1cf4a7a0408ac58309082d98faea065299a965bb80e8a18a678d83da1f2914aaa43ef235cb331d52c02b94860a54c\"}"
  ```
- **Reject:**
  ```json
  "message": "{\"signature\":\"rejected\"}"
  ```

#### Send Transaction
- **Approve:**
  ```json
  "message": "{\"txHash\":\"0x287ac8d53570799d102791781142539613d1468a08c4cdf33b264554ba8b3069\"}"
  ```
- **Reject:**
  ```json
  "message": "{\"txHash\":\"rejected\"}"
  ```

