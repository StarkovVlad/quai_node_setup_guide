# quai_node_setup_guide

Here’s an adapted README for your GitHub repository based on the provided content:

```markdown
# Quai Node Setup Guide

## Run A Node

This guide will help you start and run a Quai Network node.

---

## Introduction

In this tutorial, we will install **go-quai**, the Go implementation of Quai Network. This guide is tailored for Linux distributions and MacOS systems.

---

## Requirements

Quai consists of various “slices,” or execution shards, working together to form an overarching network. A global node runs all slices, while a slice node operates a single slice. For most users, running a slice node is recommended.

### Global Node Requirements (Iron Age Testnet)

To run a global node, your MacOS or Ubuntu machine should meet the following specifications:

- Fast CPU with 16+ cores
- 64GB+ RAM
- Fast SSD with at least 3TB free space
- 10+ MBit/sec download Internet service

### Slice Node Requirements (Iron Age Testnet)

To run a slice node, your MacOS or Ubuntu machine should meet the following specifications:

- Fast CPU with 8+ cores
- 24GB+ RAM
- Fast SSD with at least 1TB free space
- 10+ MBit/sec download Internet service

---

## Install Dependencies

To run an instance of go-quai, you’ll need to install a few dependencies using your preferred package manager (apt, brew, etc.):

### 1. Go v1.22.0+

#### Linux Snap Install

Snap is not installed by default on all Linux distributions. To install snapd, run:

```bash
sudo apt install snapd
```

Then, install Go:

```bash
sudo snap install go --classic
```

For direct Go installation instructions, please refer to the [Golang installation page](https://golang.org/doc/install).

#### MacOS Install

For MacOS, you can use Homebrew:

```bash
brew install go
```

### 2. Git, Make, and G++

Install Git, Make, and G++ with the following command:

```bash
# Install git and make
sudo apt install git make g++
```

### 3. go-quai

Now that the dependencies are installed, clone the go-quai repository:

```bash
git clone https://github.com/dominant-strategies/go-quai
cd go-quai
```

This command installs the main branch to your local machine. If you're not developing, check out the latest release:

```bash
git checkout <latest-release-tag>
```

For example:

```bash
git checkout v1.2.3-rc.4
```

---

## Node Configuration

### Selecting a Node Type

There are two types of nodes in Quai: **Global** and **Slice nodes**.

- **Global nodes** validate every shard in the network. They are recommended for users with:
  - More available computing power
  - Desire to switch between shards for mining
  - Need to provide chain data as an RPC service

- **Slice nodes** validate a “slice” of all shards in the network. They are recommended for users with:
  - Less available computing power
  - No need to switch miners between shards
  - No requirement to provide chain data as an RPC service

### Environment Variables

After installing go-quai, configure your node using the `config.toml` file. If this is your first time running go-quai, build the node and populate the config file with:

```bash
# Build go-quai
make go-quai

# Populate config file
./build/bin/go-quai config
```

This command creates a `config.toml` file in:

- **Linux:** `~/.config/go-quai/config.toml`
- **MacOS:** `~/.config/go-quai/config.toml`

### Open the Config File

Open the `config.toml` file with your favorite text editor:

```bash
# Edit with nano
nano ~/.config/go-quai/config.toml

# Open in VSCode to edit
cd ~/.config/go-quai/
code .

# Edit with vim
vim ~/.config/go-quai/config.toml
```

### Set Environment

Set the environment variable for the network you plan to run. Available options can be found in the [network specifications page](#).

```toml
environment = 'colosseum'
```

### Set Mining Addresses

If mining, insert the coinbase addresses for the chains you intend to mine. Generate addresses for each shard using Pelagus Wallet or Koala Wallet.

```toml
[global node]
coinbases = '0x00a3e45aa16163F2663015b6695894D918866d19,0x01a3e45aa16163F2663015b6695894D918866d19,...'

[single slice node]
coinbases = '0x00a3e45aa16163F2663015b6695894D918866d19'
```

### Set Slices

Set the slices parameter to the slices you wish to run, ensuring the number matches the coinbases.

```toml
[global node]
slices = '[0 0],[0 1],[0 2],[1 0],[1 1],[1 2],[2 0],[2 1],[2 2]'
```

---

## Starting a Node

### Build

To start the node, first build the source if you haven't already:

```bash
make go-quai
```

### Start

To start your node, run:

```bash
./build/bin/go-quai start
```

Logs will begin printing to the terminal.

### Stop

To stop your node (especially before making changes to your config file or shutting down), use `CTRL+C`. If you're running a miner, you may need to kill the miner process before stopping the node.

---

Feel free to reach out for further assistance or clarification.
```

This README format follows GitHub conventions and presents the information clearly and systematically. Adjust any sections as needed!
