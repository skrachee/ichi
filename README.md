# Alfonso Alonzo

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

# Back Testing

```bash
bot -s ichis backtesting
```

# Run

```bash
bot
```


