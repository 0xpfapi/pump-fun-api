# What is Pump Fun API?

A 3rd-Party API secure endpoints that give you the opportunity to trade tokens, request liquidity information, implement stop loss and take profit strategies, and connect to streams

Our Trading API is gated by an API key and charges a 0.1% fee per trade. API keys can be created at [api-pump.fun](https://api-pump.fun)

Connect with us in [Discord](https://discord.com/invite/e3xGse42z7) to ask questions.

# Endpoints

* **API Endpoint** : [https://rpc.api-pump.fun](https://rpc.api-pump.fun) - Make API requests here
* **Documentation** : [https://docs.api-pump.fun](https://docs.api-pump.fun/) - Learn how to use our API
  
The following methods are available: 
 
 - Token trade (buy/sell).

 - Quote swap information (minimum output amount, bonding curve).

 - Token metatadata information (image, name, description).

 - Bonding curve information (virtual liquidity, reserves).
 
 - Wallet balance.

 - Pump.fun token creation (creation price less than 0.02SOL)

# Live stream

Stream real-time trading and token creation data by connecting to the PumpPortal Websocket at `wss://rpc.api-pump.fun/ws`. 

Once you connect, you can subscribe to different data streams. The following methods are available: 
 
 - `subscribeNewPools` For token creation events.

 - `subscribeToken` For all trades made on specific token(s).

 - `subscribeAccount` For all trades made by specific account(s).

 - `subscribeTrades` For all trades on pump.fun.

- `subscribePublications` For completed bonding curve events (publication on Raydium).

 ### Examples:

```js
import WebSocket from 'ws';

const ws = new WebSocket('wss://rpc.api-pump.fun/ws');  

ws.on('open', function open() {

      // Subscribing to all pump.fun trades
      payload = {
          method: "subscribeTrades",
          params: []
        }
      ws.send(JSON.stringify(payload));

      // Subscribing to new pools
      payload = {
          method: "subscribeNewPools",
          keys: []
        }
      ws.send(JSON.stringify(payload));

     // Subscribing to trades on specific mint
      payload = {
          method: "subscribeToken",
          params: ["8LPjGAPtCywvo51UACHxDg3ygzbrm9qi2XxhB2Ropump"]
        }
      ws.send(JSON.stringify(payload));
});

ws.on('message', function message(data) {
      console.log(JSON.parse(data));
});
```
# Fees

### GET endpoints/Live Stream 

There is no charge to use the Information/Stream API.

### Trading API

We take a 0.1% fee on each trade.

This does not include Solana network fees, or any fees charged by the Pump.fun bonding curve.
