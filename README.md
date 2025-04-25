# Ark Wallet App with Coinflip

This project demonstrates a simple web application built on top of the Ark protocol. It includes a wallet interface for sending and receiving Bitcoin transactions through Ark, as well as a simple coinflip game.

## Features

- Create an Ark wallet
- Send on-chain and off-chain Bitcoin payments
- Receive Bitcoin payments
- Play a coinflip game using Ark transactions

## Architecture

The application consists of:
- Backend: Rust server using Axum and the Ark-rs library
- Frontend: React application with Cloudscape Design components

## Setup

### Prerequisites

- Docker and Docker Compose
- An Ark server running (see instructions below)

### Running an Ark Server

Follow these steps to run a local Ark server:

Install Nigiri Bitcoin
curl https://getnigiri.vulpem.com | bash

Start Nigiri
nigiri start

Run Ark Server
docker run -d --name arkd
-v ark:/app/wallet-data
-v arkd:/app/data
--network nigiri
-p 7070:7070
-e ARK_NETWORK=regtest
-e ARK_TX_BUILDER_TYPE=covenantless
-e ARK_ROUND_INTERVAL=5
-e ARK_MIN_RELAY_FEE=200
-e ARK_NEUTRINO_PEER=bitcoin:18444
-e ARK_ESPLORA_URL=http://chopsticks:3000
-e ARK_NO_TLS=true
-e ARK_NO_MACAROONS=true
ghcr.io/ark-network/ark:latest

Create and unlock the wallet
docker exec -it arkd arkd wallet create --password password
docker exec -it arkd arkd wallet unlock --password password

Get a funding address
docker exec -it arkd arkd wallet address
