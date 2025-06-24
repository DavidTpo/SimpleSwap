# SimpleSwap DEX Implementation

[![Solidity Version](https://img.shields.io/badge/Solidity-^0.8.30-blue)](https://soliditylang.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Introduction
This document details the implementation of a decentralized exchange (DEX) smart contract called SimpleSwap, built on Ethereum using Solidity (v0.8.0). The contract facilitates automated token swaps and liquidity provision without relying on external protocols like Uniswap.

## Purpose
The SimpleSwap contract enables:
- Creation of token pair liquidity pools
- Non-custodial token swaps with 0.3% fees
- Transparent price calculations
- ERC-20 compatible operations
- Decentralized liquidity management

## Key Data Structures
### 1. Pair Structure
```solidity
struct Pair {
    address tokenA;         // First token address
    address tokenB;         // Second token address
    uint256 reserveA;       // Token A reserves
    uint256 reserveB;       // Token B reserves
    uint256 totalLiquidity; // Total LP tokens minted
    mapping(address => uint256) liquidity; // LP balances
}# SimpleSwap
