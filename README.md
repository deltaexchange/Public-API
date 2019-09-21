# Delta Exchange Public Rest API
You can use Delta Exchange API to build tickers, price comparison apps, or anything that helps the crypto community.

## General Information
1. Base API Endpoint: https://publicapi.deltaexchange.io
1. All public api will return either JSON or Array object.

### Public API Endpoints

1. #### MARKET STATUS
   GET `/v1/market-status`  [Live link](https://publicapi.deltaexchange.io/v1/market-status)

    > "Market Status" will give your an overview of markets and assets. This is helpful when you want to track the configuration of our markets, track fees or status of withdrawal deposit, market configuration and more. This response is not recommended for price polling because accurate realtime price is not guaranteed as there could be some delays. We recommend using price ticker API for all price tracking activity.
    
    Response object will have 2 keys `markets`(all market related configs will be in this key) and `assets`(all assets related configs will be here). 
    ### Response:
    ```
    {
        "markets": [
            {
                "baseMarket": "BTC",
                "quoteMarket": "USDT",
                "fee": 0.01,
                "basePrecision": 7,
                "quotePrecision": 7,
                "low": "9693.6717629",
                "high": "10431.4637213",
                "last": "9999.2529977",
                "open": "10295.4978845",
                "volume": "4732.7484362",
                "sell": "9999.2563541",
                "buy": "9999.2529977",
                "type": "SPOT",
                "Status": "active",
                "at": 1568486791
            },
            ...
        ],
        "assets": [
            {
                "type": "BTC",
                "name": "Bitcoin",
                "withdrawFee": "0.1",
                "minWithdrawAmount": "0.002",
                "deposit": "enabled",
                "withdrawal": "enabled"   
            },
            ...
        ]
    }
    ```
    
    
    1. **`markets` key has multiple market related configuration, and description of every field in market is as below:**
    
        1. `baseMarket`: ticker code of base asset
        1. `quoteMarket`: ticker code of quote asset
        1. `fee`: JSON Object consists of `bid` and `ask` order's maker-taker fee percentage
        1. `basePrecision`: Maximum precision of base asset, this the decimal point. 
        1. `quotePrecision`: Maximum  precision of quote asset
        1. `low`: 24 hrs lowest price of base asset
        1. `high`: 24 hrs highest price of base asset
        1. `last`: Last traded price in current market
        1. `open`: Market Open price 24hrs ago
        1. `volume`: Last 24hrs traded volume
        1. `sell`: Top ask order price
        1. `buy`: Top bid order price
        1. `type`: This defines the type of market, currently we have `SPOT` and `P2P`
        1. `status`: This defines the current state of the market. This can be `active` or `suspended`
        1. `at`: Last timestamp
    1. **`assets` key have multiple asset related configuration as described below:**
    
        1. `type`: asset code
        1. `name`: Display name of asset
        1. `withdrawFee`: Withdrawal fee of asset
        1. `minWithdrawAmount`: Minimum withdrawal amount in a single transaction
        1. `deposit`: Denotes whether deposit is enabled or disabled
        1. `withdrawal`: Denotes whether withdrawal is enabled or disabled
        


1. #### MARKET TICKER
   GET `/v1/tickers` [Live link](https://publicapi.deltaexchange.io/v1/tickers)
    > Get the latest market heart-beat for all the markets for the last 24hrs.
    
    Returns JSON response which has active market data with all ticker related values.
    ### Response:
    ```
    {
        "BTCUSDT": {
            "base_unit": "BTC",
            "quote_unit": "USDT",
            "low": "9693.6717629",
            "high": "10431.4637213",
            "last": "10008.4163763",
            "type": "SPOT",
            "open": "10295.9579369",
            "volume": "4737.8742200",
            "sell": "10017.9712866",
            "buy": "10008.4163763",
            "at": "1568486940",
            "name": "BTC/USDT"
        },
        ...
    }
    ```
    Response has multiple key which denotes market data, this is in JSON. Find all the fields below:
    
    1. `base_unit`: ticker code of base market
    1. `quote_unit`: ticker code of quote asset
    1. `low`: 24 hrs lowest price of base asset
    1. `high`: 24 hrs highest price of base asset
    1. `last`: Last traded price in current market
    1. `open`: Market Open price 24hrs ago
    1. `volume`: Last 24hrs traded volume
    1. `sell`: Top ask order price
    1. `buy`: Top bid order price
    1. `at`: Timestamp when ticker information is fetched
    1. `name`: Display text of market
    

1. #### MARKET DEPTH
   GET `/v1/depth` [Live link](https://publicapi.deltaexchange.io/v1/depth?market=BTCUSDT)
    > Get market orderbook of any market
    
    Returns JSON response which has order book of a perticular market
    ### Response:
    ```
    {
    "timestamp":1559561187,
    "asks":[
               ["9999.2563541","0.0000520"],
               ["9999.3111512","0.0001795"]
           ],
    "bids":[
               ["9936.5872237","0.0001540"],
               ["9936.5866086","0.0000863"]
           ]
    }
    ```
    1. `["9999.2563541","0.0000520"]` : [ PRICE, VOLUME ]
    1. URL param `market=BTCUSDT` : Replace this with any market to get the desired order book.
    
1. #### MARKET TRADE HISTORY
   GET `/v1/trades` [Live link](https://publicapi.deltaexchange.io/v1/trades?market=BTCUSDT)
    > Get trade history of a market
    
    Returns JSON response which has trade history of a perticular market
    ### Response:
    ```
    [
      {
          "price": "10017.6818188",
          "volume": "0.0001450",
          "funds": "1.4525639",
          "market": "BTCUSDT",
          "created_at": "2019-09-21T16:18:31.000Z"
       }  
   ...
   ]
    ```
    1. URL param `market=BTCUSDT` : Replace this with any market to get the desired order book.
    
    
If you have any questions regarding APIs, please reach out to us at support@deltaexchange.io
