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
rm -rf Dockerfile
ln -s user_data/strategies ../alfonsoalonzo/strategies
ln -s Dockerfile ../alfonsoalonzo/Dockerfile
ln -s config.json ../alfonsoalonzo/config.json
```

# Build

```bash
docker build . -t alfonso
```

# Alias

```bash
# creating a docker run alias with mounted directory
alias bot='docker run -v $PWD:/freqtrade alfonso'
```

# Download Cache

```bash
bot download-data
```

# Back Testing

```bash
bot -s ichis backtesting
```


