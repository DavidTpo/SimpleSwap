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


2. Mappings
pairs: Stores all token pairs using a hash of sorted addresses

State Variables
Variable	Type	Description
pairs	mapping	All registered token pairs
Core Functionality
1. Liquidity Provision
addLiquidity()
Creates or updates a token pair pool

Mints LP tokens proportional to deposit amounts

Enforces minimum deposit requirements

Emits LiquidityAdded event

removeLiquidity()
Burns LP tokens and returns proportional assets

Verifies minimum output amounts

Emits LiquidityRemoved event

2. Token Swaps
swapExactTokensForTokens()
Executes trades using constant product formula (x*y=k)

Applies 0.3% swap fee

Requires minimum output amount

Emits TokensSwapped event

3. Price Calculations
getPrice()
Returns price ratio between tokens (TokenA/TokenB)

Calculated as (reserveB * 1e18) / reserveA

getAmountOut()
Computes output amount using:

solidity
amountOut = (amountIn * 997 * reserveOut) / 
            (reserveIn * 1000 + amountIn * 997)
Key Mechanisms
1. Constant Product Market Maker
Maintains invariant: reserveA * reserveB = k

Prices adjust automatically based on pool ratios

2. Liquidity Calculations
Initial liquidity: sqrt(amountA * amountB)

Subsequent deposits: Min of proportional shares

3. Security Features
Deadline enforcement for transactions

Reentrancy protection via CEI pattern

Input validation for all parameters

Workflow
Pool Creation
User deploys two ERC-20 tokens (TokenA/TokenB)

Calls addLiquidity() with initial deposits

Receives LP tokens representing share

Token Swap
User approves token spending

Calls swapExactTokensForTokens()

Receives output tokens minus fee

Liquidity Removal
User approves LP token spending

Calls removeLiquidity()

Receives underlying tokens

Events
Event	Description
LiquidityAdded	Logs new liquidity provision
LiquidityRemoved	Records liquidity withdrawal
TokensSwapped	Tracks completed swaps
