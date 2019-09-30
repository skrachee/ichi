# Skrachee Ichi

Trailing stop loss ichimoku trading bot. Peaceful mid-term trading...

# Requirements

- git
- docker
- python

# Installation

```bash

# cloning freqtrade & alfonso repositories
git clone https://github.com/freqtrade/freqtrade
git clone http://github.com/skrachee/ichi
cd freqtrade

# linking freqtrade folders to alfonso
rm -rf user_data/strategies
cp -r ../ichi/strategies user_data/strategies 
rm -rf Dockerfile
cp ../ichi/Dockerfile .
cp ../ichi/config.json .
```

# Build

```bash
docker build . -t ichi
./setup.sh --install
```

# Alias

```bash
# creating a docker run alias with mounted directory
alias bot='docker run -v $PWD:/freqtrade ichi'
```

# Set API Keys & Telegram Bot ID

- edit config.json in the freqtrade directory and set your API keys
- look for the following strings:

```bash
"SET-YOUR-BINANCE-API-KEY-HERE"
"SET-YOUR-BINANCE-API-SECRET-HERE"
"SET-YOUR-TELEGRAM-TOKEN-HERE"
"SET-YOUR-TELEGRAM-CHAT-ID-HERE"
```
# Download Cache

```bash
bot download-data
```
To customize your ticker intervals and number of days of data to collect

```bash
bot download-data -t 5m 30m 1h 4h 12h 1d 1w --days 120
```

# Back Testing

```bash
bot -s ichis backtesting
```

# Create the trades db

The bot uses it to track current trading positions

```bash
touch tradesv3.sqlite
```

# Run

```bash
bot --strategy ichis
```

# Auto Start

```bash
docker run -d \
  --restart unless-stopped \
  --name bot-ichis \
  -v $PWD:/freqtrade \
  ichi \
  --db-url sqlite:///tradesv3.sqlite \
  --strategy ichis
```

# Logs

```bash
docker logs -f bot-ichis
```

# Manual Restart

```bash
docker restart bot-ichis
```

# Sample Output

- Backtesting

```bash
====================================================== LEFT OPEN TRADES REPORT ======================================================
| pair     |   buy count |   avg profit % |   cum profit % |   tot profit BTC |   tot profit % | avg duration      |   profit |   loss |
|:---------|------------:|---------------:|---------------:|-----------------:|---------------:|:------------------|---------:|-------:|
| BTC/USDT |           1 |          -0.83 |          -0.83 |      -0.04178338 |          -0.08 | 7:45:00           |        0 |      1 |
| BNB/BTC  |           1 |          -0.27 |          -0.27 |      -0.01343118 |          -0.03 | 2 days, 1:10:00   |        0 |      1 |
| XRP/BTC  |           1 |          23.83 |          23.83 |       1.19253846 |           2.38 | 20 days, 22:10:00 |        1 |      0 |
| XLM/BTC  |           1 |          27.45 |          27.45 |       1.37404973 |           2.75 | 12 days, 10:15:00 |        1 |      0 |
| EOS/BTC  |           1 |           9.00 |           9.00 |       0.45056559 |           0.90 | 22 days, 23:05:00 |        1 |      0 |
| ATOM/BTC |           1 |          53.32 |          53.32 |       2.66883663 |           5.33 | 21 days, 12:40:00 |        1 |      0 |
| BAT/BTC  |           1 |          19.06 |          19.06 |       0.95383721 |           1.91 | 20 days, 18:15:00 |        1 |      0 |
| POWR/BTC |           1 |           6.07 |           6.07 |       0.30391867 |           0.61 | 2 days, 1:40:00   |        1 |      0 |
| TRX/BTC  |           1 |          13.25 |          13.25 |       0.66308511 |           1.32 | 21 days, 7:25:00  |        1 |      0 |
| TOTAL    |           9 |          16.76 |         150.88 |       7.55161684 |          15.09 | 13 days, 19:36:00 |        7 |      2 |
```

- Notmal Initialization

```bash

2019-09-30 00:55:17,874 - freqtrade.freqtradebot - INFO - Cleaning up modules ...
2019-09-30 00:55:17,874 - freqtrade.rpc.rpc_manager - INFO - Cleaning up rpc modules ...
2019-09-30 00:55:47,043 - freqtrade.configuration.configuration - INFO - Using config: config.json ...
2019-09-30 00:55:47,044 - freqtrade.configuration.configuration - INFO - Validating configuration ...
2019-09-30 00:55:47,047 - freqtrade.loggers - INFO - Verbosity set to 0
2019-09-30 00:55:47,047 - freqtrade.configuration.configuration - INFO - Dry run is disabled
2019-09-30 00:55:47,047 - freqtrade.configuration.configuration - INFO - Using DB: "sqlite:///tradesv3.sqlite"
2019-09-30 00:55:47,048 - freqtrade.configuration.configuration - INFO - Using max_open_trades: 5 ...
2019-09-30 00:55:47,048 - freqtrade.configuration.configuration - INFO - Using user-data directory: /freqtrade/user_data ...
2019-09-30 00:55:47,048 - freqtrade.configuration.configuration - INFO - Using data directory: /freqtrade/user_data/data/binance ...
2019-09-30 00:55:47,049 - freqtrade.configuration.configuration - INFO - Runmode set to RunMode.LIVE.
2019-09-30 00:55:47,049 - freqtrade.configuration.check_exchange - INFO - Checking exchange...
2019-09-30 00:55:47,049 - freqtrade.configuration.check_exchange - INFO - Exchange "binance" is officially supported by the Freqtrade development team.
2019-09-30 00:55:47,049 - freqtrade.configuration.configuration - INFO - Using pairlist from configuration.
2019-09-30 00:55:47,050 - freqtrade.freqtradebot - INFO - Starting freqtrade develop-704fea61
2019-09-30 00:55:47,051 - freqtrade.resolvers.iresolver - INFO - Using resolved strategy ichis from '/freqtrade/user_data/strategies/ichimoku.py'...
2019-09-30 00:55:47,052 - freqtrade.resolvers.strategy_resolver - INFO - Override strategy 'stake_currency' with value in config file: BTC.
2019-09-30 00:55:47,052 - freqtrade.resolvers.strategy_resolver - INFO - Override strategy 'stake_amount' with value in config file: 0.2.
2019-09-30 00:55:47,052 - freqtrade.resolvers.strategy_resolver - INFO - Override strategy 'use_sell_signal' with value in config file: False.
2019-09-30 00:55:47,052 - freqtrade.resolvers.strategy_resolver - INFO - Override strategy 'sell_profit_only' with value in config file: False.
2019-09-30 00:55:47,053 - freqtrade.resolvers.strategy_resolver - INFO - Override strategy 'ignore_roi_if_buy_signal' with value in config file: False.
2019-09-30 00:55:47,053 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using minimal_roi: {'0': 1}
2019-09-30 00:55:47,053 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using ticker_interval: 1m
2019-09-30 00:55:47,053 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using stoploss: -0.05
2019-09-30 00:55:47,053 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using trailing_stop: False
2019-09-30 00:55:47,053 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using trailing_stop_positive: -0.1
2019-09-30 00:55:47,054 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using trailing_stop_positive_offset: 0.05
2019-09-30 00:55:47,054 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using trailing_only_offset_is_reached: True
2019-09-30 00:55:47,054 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using process_only_new_candles: False
2019-09-30 00:55:47,054 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using order_types: {'buy': 'limit', 'sell': 'limit', 'stoploss': 'market', 'stoploss_on_exchange': False}
2019-09-30 00:55:47,054 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using order_time_in_force: {'buy': 'gtc', 'sell': 'gtc'}
2019-09-30 00:55:47,054 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using stake_currency: BTC
2019-09-30 00:55:47,054 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using stake_amount: 0.2
2019-09-30 00:55:47,055 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using use_sell_signal: False
2019-09-30 00:55:47,055 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using sell_profit_only: False
2019-09-30 00:55:47,055 - freqtrade.resolvers.strategy_resolver - INFO - Strategy using ignore_roi_if_buy_signal: False
2019-09-30 00:55:47,055 - freqtrade.rpc.rpc_manager - INFO - Enabling rpc.telegram ...
2019-09-30 00:55:48,056 - freqtrade.rpc.telegram - INFO - rpc.telegram is listening for following commands: [['status'], ['profit'], ['balance'], ['start'], ['stop'], ['forcesell'], ['forcebuy'], ['performance'], ['daily'], ['count'], ['reload_conf'], ['stopbuy'], ['whitelist'], ['blacklist'], ['edge'], ['help'], ['version']]
2019-09-30 00:55:48,207 - freqtrade.exchange.exchange - INFO - Applying additional ccxt config: {'enableRateLimit': True}
2019-09-30 00:55:48,210 - freqtrade.exchange.exchange - INFO - Applying additional ccxt config: {'enableRateLimit': True, 'rateLimit': 500}
2019-09-30 00:55:48,218 - freqtrade.exchange.exchange - INFO - Using Exchange "Binance"
2019-09-30 00:55:48,364 - freqtrade.resolvers.exchange_resolver - INFO - Using resolved exchange 'Binance'...
2019-09-30 00:55:48,749 - freqtrade.wallets - INFO - Wallets synced.
2019-09-30 00:55:48,750 - freqtrade.resolvers.iresolver - WARNING - Path "/freqtrade/user_data/pairlist" does not exist.
2019-09-30 00:55:48,751 - freqtrade.resolvers.iresolver - INFO - Using resolved pairlist StaticPairList from '/freqtrade/freqtrade/pairlist/StaticPairList.py'...
2019-09-30 00:55:48,755 - freqtrade.rpc.rpc_manager - INFO - Sending rpc message: {'type': status, 'status': 'config reloaded'}
2019-09-30 00:55:49,030 - freqtrade.rpc.rpc_manager - INFO - Sending rpc message: {'type': status, 'status': 'running'}
2019-09-30 00:55:49,304 - freqtrade.worker - INFO - Changing state to: RUNNING
2019-09-30 00:55:49,304 - freqtrade.rpc.rpc_manager - INFO - Sending rpc message: {'type': custom, 'status': "*Exchange:* `binance`\n*Stake per trade:* `0.2 BTC`\n*Minimum ROI:* `{'0': 1}`\n*Stoploss:* `-0.05`\n*Ticker Interval:* `1m`\n*Strategy:* `ichis`"}
2019-09-30 00:55:49,581 - freqtrade.rpc.rpc_manager - INFO - Sending rpc message: {'type': status, 'status': "Searching for BTC pairs to buy and sell based on StaticPairList: ['BNB/BTC', 'ETH/BTC', 'XRP/BTC', 'XLM/BTC', 'EOS/BTC', 'ATOM/BTC', 'ALGO/BTC', 'RVN/BTC', 'ZRX/BTC', 'BAT/BTC']"}
2019-09-30 00:55:49,866 - freqtrade.persistence - INFO - Found open trade: Trade(id=1, pair=BAT/BTC, amount=10138.66520000, open_rate=0.00001971, open_since=2019-09-29 22:58:11)
2019-09-30 00:55:54,288 - freqtrade.freqtradebot - INFO - Found no buy signals for whitelisted currencies. Trying again...
2019-09-30 00:55:55,113 - freqtrade.freqtradebot - INFO - Found no buy signals for whitelisted currencies. Trying again...
2019-09-30 00:56:00,109 - freqtrade.freqtradebot - INFO - Found no buy signals for whitelisted currencies. Trying again...

```
