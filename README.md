# Alfonso Alonzo

scratchy ichimoku trading bot

Peaceful trading in the background

# Requirements

- git
- docker

# Installation

```bash

# cloning freqtrade & alfonso repositories
git clone https://github.com/freqtrade/freqtrade
git clone http://github.com/michakfromparis/alfonsoalonzo
cd freqtrade

# linking freqtrade folders to alfonso
rm -rf user_data/strategies
cp -r ../alfonsoalonzo/strategies user_data/strategies 
rm -rf Dockerfile
cp ../alfonsoalonzo/Dockerfile .
cp ../alfonsoalonzo/config.json .
```

# Build

```bash
docker build . -t alfonso
./setup.sh --install
```

# Alias

```bash
# creating a docker run alias with mounted directory
alias bot='docker run -v $PWD:/freqtrade alfonso'
```

# Set API Keys & Telegram Bot ID

- edit config.json in the freqtrade directory and set your API keys

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

# Run

```bash
bot
```


# Sample Output

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
