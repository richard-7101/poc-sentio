# poc-sentio

### Pool.NewImplementation
```js
NewImplementation(address newImplementation)
```
1. Pool info
    ```js
    emit PoolInfo {
        poolAddress: event.address
        vaultTemplate: pool.vaultTemplate()
        vaultImplementation: pool.vaultImplementation()
        tokenB0: pool.tokenB0()
        tokenWETH: pool.tokenWETH()
        vTokenB0: pool.vTokenB0()
        vTokenETH: pool.vTokenETH()
        lToken: pool.lToken()
        pToken: pool.pToken()
        oracleManager: pool.oracleManager()
        swapper: pool.swapper()
        symbolManager: pool.symbolManager()
        privileger: pool.privileger()
        rewardVault: pool.rewardVault()
        decimalsB0: pool.decimalsB0()
        reserveRatioB0: pool.reserveRatioB0()
        minRatioB0: pool.minRatioB0()
        poolInitialMarginMultiplier: pool.poolInitialMarginMultiplier()
        protocolFeeCollectRatio: pool.protocolFeeCollectRatio()
        minLiquidationReward: pool.minLiquidationReward()
        maxLiquidationReward: pool.maxLiquidationReward()
        liquidationRewardCutRatio: pool.liquidationRewardCutRatio()
    }
    ```

### Pool.AddMarket
```js
AddMarket(address indexed market)
```
1. Market info
    ```js
    emit MarketInfo {
        pool: event.address
        asset: market.underlying()
        market: market.address
        assetSymbol: asset.symbol()
        marketSymbol: market.symbol()
    }
    ```

### SymbolManager.AddSymbol
```js
AddSymbol(bytes32 indexed symbolId, address indexed symbol)
```
1. Indexed symbols change
    ```js
    symbolManager = event.address
    emit IndexedSymbols {
        pool: symbolManager.pool()
        indexedSymbols: symbolManager.indexedSymbols()
    }

    // Instantiate new Symbol contract, and monitor Symbol.NewImplementation event
    ```

### SymbolManager.RemoveSymbol
```js
RemoveSymbol(bytes32 indexed symbolId, address indexed symbol)
```
1. Indexed symbols change
    ```js
    symbolManager = event.address
    emit IndexedSymbols {
        pool: symbolManager.pool()
        indexedSymbols: symbolManager.indexedSymbols()
    }
    ```

### Symbol.NewImplementation
```js
NewImplementation(address newImplementation)
```
1. Symbol info
    ```js
    symbol = event.address
    symbolName = symbol.symbol()
    if symbolName.endswith('-C') or symbolName.endswith('-P'): // Option
        emit SymbolInfo {
            symbolAddress: symbol
            symbol: symbolName
            symbolManager: symbol.manager()
            pool: symbolManager.pool()
            oracleManager: symbol.oracleManager()
            symbolId: symbol.symbolId()
            priceId: symbol.priceId()
            volatilityId: symbol.volatilityId()
            feeRatioNotional: symbol.feeRatioNotional()
            feeRatioMark: symbol.feeRatioMark()
            strikePrice: symbol.strikePrice()
            alpha: symbol.alpha()
            fundingPeriod: symbol.fundingPeriod()
            minTradeVolume: symbol.minTradeVolume()
            initialMarginRatio: symbol.initialMarginRatio()
            maintenanceMarginRatio: symbol.maintenanceMarginRatio()
            pricePercentThreshold: symbol.pricePercentThreshold()
            timeThreshold: symbol.timeThreshold()
            startingPriceShiftLimit: symbol.startingPriceShiftLimit()
            minInitialMarginRatio: symbol.minInitialMarginRatio()
            initialOpenVolume: symbol.initialOpenVolume()
            isCall: symbol.isCall()
            isCloseOnly: symbol.isCloseOnly()
        }
    elif '^2' in symbolName: // Power
        emit SymbolInfo {
            symbolAddress: symbol
            symbol: symbolName
            symbolManager: symbol.manager()
            pool: symbolManager.pool()
            oracleManager: symbol.oracleManager()
            symbolId: symbol.symbolId()
            priceId: symbol.priceId()
            volatilityId: symbol.volatilityId()
            feeRatio: symbol.feeRatio()
            alpha: symbol.alpha()
            fundingPeriod: symbol.fundingPeriod()
            minTradeVolume: symbol.minTradeVolume()
            initialMarginRatio: symbol.initialMarginRatio()
            maintenanceMarginRatio: symbol.maintenanceMarginRatio()
            pricePercentThreshold: symbol.pricePercentThreshold()
            timeThreshold: symbol.timeThreshold()
            startingPriceShiftLimit: symbol.startingPriceShiftLimit()
            jumpLimitRatio: symbol.jumpLimitRatio()
            initialOpenVolume: symbol.initialOpenVolume()
            isCloseOnly: symbol.isCloseOnly()
        }
    elif symbolName.endswith('-Gamma'): // Gamma
        emit SymbolInfo {
            symbolAddress: symbol
            symbol: symbolName
            symbolManager: symbol.manager()
            pool: symbolManager.pool()
            oracleManager: symbol.oracleManager()
            symbolId: symbol.symbolId()
            priceId: symbol.priceId()
            volatilityId: symbol.volatilityId()
            feeRatio: symbol.feeRatio()
            powerAlpha: symbol.powerAlpha()
            futuresAlpha: symbol.futuresAlpha()
            fundingPeriod: symbol.fundingPeriod()
            minTradeVolume: symbol.minTradeVolume()
            initialMarginRatio: symbol.initialMarginRatio()
            maintenanceMarginRatio: symbol.maintenanceMarginRatio()
            isCloseOnly: symbol.isCloseOnly()
        }
    else: // Futures
        emit SymbolInfo {
            symbolAddress: symbol
            symbol: symbolName
            symbolManager: symbol.manager()
            pool: symbolManager.pool()
            oracleManager: symbol.oracleManager()
            symbolId: symbol.symbolId()
            priceId: symbol.priceId()
            feeRatio: symbol.feeRatio()
            alpha: symbol.alpha()
            fundingPeriod: symbol.fundingPeriod()
            minTradeVolume: symbol.minTradeVolume()
            initialMarginRatio: symbol.initialMarginRatio()
            maintenanceMarginRatio: symbol.maintenanceMarginRatio()
            pricePercentThreshold: symbol.pricePercentThreshold()
            timeThreshold: symbol.timeThreshold()
            startingPriceShiftLimit: symbol.startingPriceShiftLimit()
            jumpLimitRatio: symbol.jumpLimitRatio()
            initialOpenVolume: symbol.initialOpenVolume()
            isCloseOnly: symbol.isCloseOnly()
        }
    ```

### Pool.AddLiquidity
```js
AddLiquidity(uint256 indexed lTokenId, address indexed underlying, uint256 amount, int256 newLiquidity)
```
1. Pool state
    ```js
    emit PoolState {
        poolAddress: event.address
        liquidity: pool.liquidity()
        lpsPnl: pool.lpsPnl()
        cumulativePnlPerLiquidity: pool.cumulativePnlPerLiquidity()
    }
    ```
1. LP state and markets
    ```js
    lpInfo = pool.lpInfos(lTokenId)
    emit LpState {
        pool: event.address
        lTokenId: lTokenId
        vault: lpInfo.vault
        amountB0: lpInfo.amountB0
        liquidity: lpInfo.liquidity
        cumulativePnlPerLiquidity: lpInfo.cumulativePnlPerLiquidity
        vaultLiquidity: vault.getVaultLiquidity()
        marketsIn: vault.getMarketsIn()
    }

    // vault balance for `underlying` changes
    def __getMarket(underlying):
        if underlying == address(0):
            return pool.vTokenETH()
        elif underlying == pool.tokenB0():
            return pool.vTokenB0()
        else:
            return pool.markets(underlying)

    emit MarketState {
        pool: event.address
        lTokenId: lTokenId
        vault: vault.address
        asset: underlying
        market: __getMarket(underlying)
        marketBalance: market.balanceOf(vault.address)
        exchangeRateStored: market.exchangeRateStored()
    }
    ```
1. All symbols states, since all symbols with positions will be settled on `AddLiquidity` activity
    ```js
    pool = event.address
    symbolManager = pool.symbolManager()

    emit SymbolManagerState {
        pool: pool
        symbolManagerAddress: symbolManager
        initialMarginRequired: symbolManager.initialMarginRequired()
    }

    symbolLength = symbolManager.getSymbolsLength()
    for i in range(symbolLength):
        symbol = symbolManager.indexedSymbols(i)
        symbolName = symbol.symbol()
        if not symbolName.endswith('-Gamma'):
            // Futures, Option, Power
            netVolume = symbol.netVolume()
            if netVolume != 0: // only symbols with positions will be settled
                emit SymbolState {
                    pool: pool
                    symbol: symbolName
                    symbolAddress: symbol.address
                    indexPrice: symbol.indexPrice()
                    fundingTimestamp: symbol.fundingTimestamp()
                    cumulativeFundingPerVolume: symbol.cumulativeFundingPerVolume()
                    tradersPnl: symbol.tradersPnl()
                    initialMarginRequired: symbol.initialMarginRequired()
                }
        else:
            // Gamma
            netPowerVolume = symbol.netPowerVolume()
            if netPowerVolume != 0: // only symbols with positions will be settled
                emit SymbolState {
                    pool: pool
                    symbol: symbolName
                    symbolAddress: symbol.address
                    indexPrice: symbol.indexPrice()
                    fundingTimestamp: symbol.fundingTimestamp()
                    cumulaitveFundingPerPowerVolume: symbol.cumulaitveFundingPerPowerVolume()
                    cumulativeFundingPerRealFuturesVolume: symbol.cumulativeFundingPerRealFuturesVolume()
                    tradersPnl: symbol.tradersPnl()
                    initialMarginRequired: symbol.initialMarginRequired()
                }
    ```

### Pool.RemoveLiquidity
```js
RemoveLiquidity(uint256 indexed lTokenId, address indexed underlying, uint256 amount, int256 newLiquidity)
```
Same processes as `Pool.AddLiquidity`.

### Pool.AddMargin
```js
AddMargin(uint256 indexed pTokenId, address indexed underlying, uint256 amount, int256 newMargin)
```
1. Trader state and markets
    ```js
    tdInfo = pool.tdInfos(pTokenId)
    emit TdState {
        pool: event.address
        pTokenId: pTokenId
        vault: tdInfo.vault
        amountB0: tdInfo.amountB0
        vaultLiquidity: vault.getVaultLiquidity()
        marketsIn: vault.getMarketsIn()
    }

    emit MarketState {
        pool: event.address
        pTokenId: pTokenId
        vault: vault.address
        asset: underlying
        market: __getMarket(underlying)
        marketBalance: market.balanceOf(vault.address)
        exchangeRateStored: market.exchangeRateStored()
    }
    ```

### Pool.RemoveMargin
```js
RemoveMargin(uint256 indexed pTokenId, address indexed underlying, uint256 amount, int256 newMargin)
```
1. Pool state
    ```js
    emit PoolState {
        poolAddress: event.address
        lpsPnl: pool.lpsPnl()
        cumulativePnlPerLiquidity: pool.cumulativePnlPerLiquidity()
    }
    ```
1. Trader state and markets
    ```js
    tdInfo = pool.tdInfos(pTokenId)
    emit TdState {
        pool: event.address
        pTokenId: pTokenId
        vault: tdInfo.vault
        amountB0: tdInfo.amountB0
        vaultLiquidity: vault.getVaultLiquidity()
        marketsIn: vault.getMarketsIn()
    }

    emit MarketState {
        pool: event.address
        pTokenId: pTokenId
        vault: vault.address
        asset: underlying
        market: __getMarket(underlying)
        marketBalance: market.balanceOf(vault.address)
        exchangeRateStored: market.exchangeRateStored()
    }
    ```
1. All settled symbols states
    ```js
    pool = event.address
    symbolManager = pool.symbolManager()

    symbols = symbolManager.getActiveSymbols(pTokenId) // symbols this trader has position with
    for symbol in symbols:
        symbolName = symbol.symbol()
        if not symbolName.endswith('-Gamma'):
            // Futures, Option, Power
            emit SymbolState {
                pool: pool
                symbol: symbolName
                address: symbol.address
                indexPrice: symbol.indexPrice()
                fundingTimestamp: symbol.fundingTimestamp()
                cumulativeFundingPerVolume: symbol.cumulativeFundingPerVolume()
                tradersPnl: symbol.tradersPnl()
                initialMarginRequired: symbol.initialMarginRequired()
            }
        else:
            // Gamma
            emit SymbolState {
                pool: pool
                symbol: symbolName
                address: symbol.address
                indexPrice: symbol.indexPrice()
                fundingTimestamp: symbol.fundingTimestamp()
                cumulaitveFundingPerPowerVolume: symbol.cumulaitveFundingPerPowerVolume()
                cumulativeFundingPerRealFuturesVolume: symbol.cumulativeFundingPerRealFuturesVolume()
                tradersPnl: symbol.tradersPnl()
                initialMarginRequired: symbol.initialMarginRequired()
            }
    ```

### SymbolManager.Trade
```js
Trade(uint256 indexed pTokenId, bytes32 indexed symbolId, int256 indexPrice, int256 tradeVolume, int256 tradeCost, int256 tradeFee)
```
1. Pool state
    ```js
    emit PoolState {
        poolAddress: symbolManager.pool()
        lpsPnl: pool.lpsPnl()
        cumulativePnlPerLiquidity: pool.cumulativePnlPerLiquidity()
        protocolFeeAccrued: pool.protocolFeeAccrued()
    }
    ```
1. Trader state
    ```js
    symbolManager = event.address
    pool = symbolManager.pool()
    tdInfo = pool.tdInfos(pTokenId)
    emit TdState {
        pool: pool
        pTokenId: pTokenId
        vault: tdInfo.vault
        amountB0: tdInfo.amountB0
        vaultLiquidity: vault.getVaultLiquidity()
        marketsIn: vault.getMarketsIn()
    }
    ```
1. Symbols settled
    ```js
    symbolManager = event.address
    pool = symbolManager.pool()

    // symbols this trader has position with
    symbols = symbolManager.getActiveSymbols(pTokenId)
    // the current traded symbol maybe removed from active symbols if position is closed with this trade
    // so we include the current symbol anyway
    symbols = set(symbols + [symbolManager.symbols(symbolId)])

    for symbol in symbols:
        symbolName = symbol.symbol()
        if not symbolName.endswith('-Gamma'):
                // Futures, Option, Power
                emit SymbolState {
                    pool: pool
                    symbol: symbolName
                    symbolAddress: symbol.address
                    netVolume: symbol.netVolume()
                    netCost: symbol.netCost()
                    indexPrice: symbol.indexPrice()
                    fundingTimestamp: symbol.fundingTimestamp()
                    cumulativeFundingPerVolume: symbol.cumulativeFundingPerVolume()
                    tradersPnl: symbol.tradersPnl()
                    initialMarginRequired: symbol.initialMarginRequired()
                    nPositionHolders: symbol.nPositionHolders()
                    lastNetVolume: symbol.lastNetVolume()
                    lastNetVolumeBlock: symbol.lastNetVolumeBlock()
                    openVolume: symbol.openVolume()
                }

                position = symbol.positions(pTokenId)
                emit PositionState {
                    pool: pool
                    symbol: symbolName
                    symbolAddress: symbol.address
                    pTokenId: pTokenId
                    volume: position.volume
                    cost: position.cost
                    cumulativeFundingPerVolume: position.cumulativeFundingPerVolume
                }

            else:
                // Gamma
                emit SymbolState {
                    pool: pool
                    symbol: symbolName
                    symbolAddress: symbol.address
                    indexPrice: symbol.indexPrice()
                    fundingTimestamp: symbol.fundingTimestamp()
                    cumulaitveFundingPerPowerVolume: symbol.cumulaitveFundingPerPowerVolume()
                    cumulativeFundingPerRealFuturesVolume: symbol.cumulativeFundingPerRealFuturesVolume()
                    tradersPnl: symbol.tradersPnl()
                    initialMarginRequired: symbol.initialMarginRequired()
                    netPowerVolume: symbol.netPowerVolume()
                    netRealFuturesVolume: symbol.netRealFuturesVolume()
                    netCost: symbol.netCost()
                    nPositionHolders: symbol.nPositionHolders()
                }

                position = symbol.positions(pTokenId)
                emit PositionState {
                    pool: pool
                    symbol: symbolName
                    symbolAddress: symbol.address
                    powerVolume: position.powerVolume
                    realFuturesVolume: position.realFuturesVolume
                    cost: position.cost
                    cumulaitveFundingPerPowerVolume: position.cumulaitveFundingPerPowerVolume
                    cumulativeFundingPerRealFuturesVolume: position.cumulativeFundingPerRealFuturesVolume
                }
    ```
