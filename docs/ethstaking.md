---
title: ETH Solo Staking
layout: default
nav_order: 2
last_modified_date: 2023/09/24
---

# ETH Solo Staking
{: .no_toc }

ETH Staking is the action of committing ETH to the Beacon chain in order to run a validator for the Ethereum network. When you commit ETH to the Beacon chain, you no longer have direct control on it (ie, you cannot spend it). However, it's possible to request for your validator to be removed from the network, in which case the associated 32 ETH will be returned to an address you control. You can exit whenever you like.

During the whole process, no one can mess with your 32 ETH unless they gain access to your validator credentials **and** your withdrawal address.

As a reward for running a validator, you receive ETH from two streams:
- **Execution**: receive tips from transactions.
- **Issuance**: receive rewards for proposing a new block and participating in Sync committees. These rewards are much higher but happen rarely, as just a few validators are chosen to participate in committees for each block.

This tutorial is primarily based on the excellent [CoinCashew's Guide](https://www.coincashew.com/coins/overview-eth/guide-or-how-to-setup-a-validator-on-eth2-mainnet). I really recommend going through this guide if you want to solo stake. My tutorial is a small addition to it, with some tips on steps for which the guide is lacking details.

Note that there are other ways to stake ETH, but they all involve giving up at least some control to a third party over your validator credentials or your ETH. You can check the options on the [official Ethereum page](https://ethereum.org/en/staking/#how-to-stake-your-eth).

**Disclaimer**: I am neither an employee of, nor associated in any way with any company or product mentioned on this page. The content of this page is not an investment advice.

## Table of contents
{: .no_toc .text-delta .fs-6 }
- TOC
{:toc}

# Requirements

In order to solo stake ETH, you need:
- Control of an ETH address with at least 32 ETH (in practice, 32 + some change for gas fees when transfering your 32 ETH to the Beacon Deposit Contract).
- Hardware powerful enough to run the ETH execution/consensus/validator software, and that can stay up almost 24/7. You can either use your own (see [Hardware](#hardware-setup) for recommendations), or use cloud based solutions such as AWS.
- Fast and reliable Internet connection.
- Some know-how with Linux and the command line. Some execution/consensus clients provide MacOS or Windows versions of their software, but most resources are for Linux. This tutorial covers Linux tools only.

# Hardware Setup

Ideally, you want to have a machine that is dedicated to ETH staking. Contrarily to PoW mining, PoS staking is not massively computationally consuming, and there is no need for a GPU. However, you still need a decent CPU, quite a lot of RAM, and a lot of disk space. Using an NVMe SSD is advised.

[Intel NUC](https://www.intel.fr/content/www/fr/fr/products/details/nuc.html) or similar hardware is a reasonable choice. Personally, I built my own machine with the following components:
- **Motherboard & CPU**: [Intel NUC13ANBi7](https://www.intel.fr/content/www/fr/fr/products/sku/233114/intel-nuc-13-pro-board-nuc13anbi7/specifications.html). This is probably overkill as my CPU is underused. An i5 would certainly do just fine.
- **RAM**: [Crucial 32GB Kit (2 x 16GB) DDR4-3200 SODIMM](https://www.crucial.fr/memory/ddr4/ct2k16g4sfra32a). I recommend having 32 GB of RAM. With a single validator running, my RAM usage is typically around 20GB.
- **SSD**: [FireCuda 530 4 TB](https://www.seagate.com/fr/fr/products/gaming-drives/pc-gaming/firecuda-530-ssd/). Again, 4TB is probably overkill, but the blockchain does grow fast, typically 1GB/day. At the time of writing this, I have not fully explored options in the execution client to prune the database, but it seems like it's possible, at the cost of going offline for a day or two. Anyhow, I recommend having at least 2TB.
- **AC Power Adapter**: [Delippo 120W 19V 6.32A](https://www.amazon.fr/dp/B07MV6C89N?psc=1&ref=ppx_yo2ov_dt_b_product_details).
- **Case**: [Maxwell Pro Fanless Mini-ITX case](https://akasa.co.uk/update.php?tpl=product/product.detail.tpl&model=A-ITX48-M1B). CPU and disk usage can be pretty heavy when running the validator, so you need some cooling. As my machine is sitting in my living room, I didn't want to have constant fan noise, so I chose this fanless case that dissipates heat with copper tubes and various thermal modules. You can buy it [here](https://www.cartft.com/catalog/il/3459).

# Linux installation

The easiest way to go is to install Ubuntu. You can follow the official installation guide. At this step I recommend choosing `Minimal installation`, and leaving `Install third party software` option unchecked. Running your staking node will not require any of this additional software, and you can always install additional software later if needed.

![Ubuntu install options](/assets/images/ubuntu_install_options.png)

# Setting up your node

Follow the steps from CoinCashew's guide, from [Step 2](https://www.coincashew.com/coins/overview-eth/guide-or-how-to-setup-a-validator-on-eth2-mainnet/part-i-installation/step-2-configuring-node) to [Step 4](https://www.coincashew.com/coins/overview-eth/guide-or-how-to-setup-a-validator-on-eth2-mainnet/part-i-installation/step-4-installing-consensus-client). You will have to choose an *execution client* and a *consensus client*. There are a few options for each. It is recommended to use a *minority client*, ie one that is used by a small percentage of nodes. Theoretically, this helps with ETH network resilience as an issue with a minority client would impact a smaller part of the network than an issue on a client everyone uses.

You can check current client distribution estimates [here](https://clientdiversity.org/). Personally, I chose *Besu* as execution client and *Teku* as consensus. So far, they have been running fine, although Besu database seems to be growing quite fast.

## Port forwarding

It is recommended to set up port forwarding on your router for your execution and consensus clients. To my understanding, it is not mandatory for your clients to run correctly, but it will help you have optimal connectivity to peers on the ETH network.

What does port forwarding mean? Your clients communicate with the external world through specific ports (you should have gone through this at [Step 2](https://www.coincashew.com/coins/overview-eth/guide-or-how-to-setup-a-validator-on-eth2-mainnet/part-i-installation/step-2-configuring-node)). By default, your home router will typically block traffic from the external world to your home network through these ports. You need to explicitly allow relevant ports in your router interface. My router is a Orange Livebox 5, if you have a different one, refer to your Internet provider instructions to adapt the steps below.

### DHCP Setup

toto

### NAT Setup

toto

# Adding a validator to your node

**This is the most critical step, be extra careful**.

# Monitoring your node

## NoIP

# Setting up downtime alerts for your node

# Further fail-safing your setup

## Uninterruptible Power Supply

## Automatic reboot
