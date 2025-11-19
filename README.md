# Ekubo audit details
- Total Prize Pool: $183,500 in USDC
    - HM awards: up to $176,800 in USDC
        - If no valid Highs are found, the HM pool is $60,000
        - If no valid Highs or Mediums are found, the HM pool is $0
    - QA awards: $3,200 in USDC
    - Judge awards: $3,000 in USDC
    - Scout awards: $500 in USDC
- [Read our guidelines for more details](https://docs.code4rena.com/competitions)
- Starts November 19, 2025 20:00 UTC
- Ends December 10, 2025 20:00 UTC

### ❗ Important notes for wardens
1. A coded, runnable PoC is required for all High/Medium submissions to this audit. 
    - This repo includes a basic template to run the test suite.
    - PoCs must use the test suite provided in this repo.
    - Your submission will be marked as Insufficient if the POC is not runnable and working with the provided test suite.
    - Exception: PoC is optional (though recommended) for wardens with signal ≥ 0.68.
1. Judging phase risk adjustments (upgrades/downgrades):
    - High- or Medium-risk submissions downgraded by the judge to Low-risk (QA) will be ineligible for awards.
    - Upgrading a Low-risk finding from a QA report to a Medium- or High-risk finding is not supported.
    - As such, wardens are encouraged to select the appropriate risk level carefully during the submission phase.

## V12 findings 

[V12](https://v12.zellic.io/) is [Zellic](https://zellic.io)'s in-house AI auditing tool. It is the only autonomous Solidity auditor that [reliably finds Highs and Criticals](https://www.zellic.io/blog/introducing-v12/). All issues found by V12 will be judged as out of scope and ineligible for awards.

V12 findings will be posted in this section within the first two days of the competition.  

## Publicly known issues

_Anything included in this section is considered a publicly known issue and is therefore ineligible for awards._

### Compiler Vulnerabilities

Any vulnerabilities that pertain to the experimental nature of the `0.8.31` pre-release candidate and the project's toolkits are considered out-of-scope for the purposes of this contest.

### Non-Standard EIP-20 Assets

Tokens that have non-standard behavior e.g. allow for arbitrary calls may not be used safely in the system.

Token balances are only expected to change due to calls to `transfer` or `transferFrom`.

Any issues related to non-standard tokens should only affect the pools that use the token, i.e. those pools can never become insolvent in the other token due to non-standard behavior in one token.

### Extension Freezing Power

The extensions in scope of the audit are **not** expected to be able to freeze a pool and lock deposited user capital.

Third-party extensions, however, can freeze a pool and lock deposited user capital. This is considered an acceptable risk.

### TWAMM Guarantees

TWAMM order execution quality is dependent on the liquidity in the pool and orders on the other side of the pool. 

If any of the following conditions are true:

- Liquidity in the pool is low
- The other side has not placed orders
- Blocks are not produced for a period of time

The user may receive a bad price from the TWAMM. This is a known risk; the TWAMM order execution price is not guaranteed.

# Overview

Ekubo Protocol delivers the best pricing using super-concentrated liquidity, a singleton architecture, and extensions. The Ekubo protocol vision is to provide a balance between the best swap execution and liquidity provider returns. The contracts are relentlessly optimized to be able to provide the most capital efficient liquidity ever at the lowest cost.

## Links

- **Previous audits:**  
  - [Current Ethereum Version Audits](https://docs.ekubo.org/integration-guides/reference/audits#ethereum)
  - [Riley Holterhus Audit Report](https://github.com/code-423n4/2025-11-ekubo/blob/main/audits/Ekubo-Riley-Holterhus-Audit.pdf)
- **Documentation:** https://docs.ekubo.org/
- **Website:** https://ekubo.org/
- **X/Twitter:** https://x.com/EkuboProtocol

# Scope

### Files in scope


| File   | nSLOC |
| ------ | ----- |
|[src/Core.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/Core.sol)| 598 |
|[src/Incentives.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/Incentives.sol)| 79 |
|[src/MEVCaptureRouter.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/MEVCaptureRouter.sol)| 30 |
|[src/Orders.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/Orders.sol)| 104 |
|[src/Positions.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/Positions.sol)| 28 |
|[src/PositionsOwner.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/PositionsOwner.sol)| 37 |
|[src/RevenueBuybacks.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/RevenueBuybacks.sol)| 100 |
|[src/Router.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/Router.sol)| 256 |
|[src/TokenWrapper.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/TokenWrapper.sol)| 109 |
|[src/TokenWrapperFactory.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/TokenWrapperFactory.sol)| 17 |
|[src/base/BaseExtension.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/base/BaseExtension.sol)| 44 |
|[src/base/BaseForwardee.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/base/BaseForwardee.sol)| 17 |
|[src/base/BaseLocker.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/base/BaseLocker.sol)| 50 |
|[src/base/BaseNonfungibleToken.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/base/BaseNonfungibleToken.sol)| 69 |
|[src/base/BasePositions.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/base/BasePositions.sol)| 184 |
|[src/base/ExposedStorage.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/base/ExposedStorage.sol)| 16 |
|[src/base/FlashAccountant.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/base/FlashAccountant.sol)| 232 |
|[src/base/PayableMulticallable.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/base/PayableMulticallable.sol)| 13 |
|[src/base/UsesCore.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/base/UsesCore.sol)| 13 |
|[src/extensions/MEVCapture.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/extensions/MEVCapture.sol)| 189 |
|[src/extensions/Oracle.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/extensions/Oracle.sol)| 271 |
|[src/extensions/TWAMM.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/extensions/TWAMM.sol)| 464 |
|[src/interfaces/IBaseNonfungibleToken.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/IBaseNonfungibleToken.sol)| 3 |
|[src/interfaces/ICore.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/ICore.sol)| 39 |
|[src/interfaces/IExposedStorage.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/IExposedStorage.sol)| 3 |
|[src/interfaces/IFlashAccountant.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/IFlashAccountant.sol)| 11 |
|[src/interfaces/IIncentives.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/IIncentives.sol)| 12 |
|[src/interfaces/IOrders.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/IOrders.sol)| 7 |
|[src/interfaces/IPositions.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/IPositions.sol)| 9 |
|[src/interfaces/IRevenueBuybacks.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/IRevenueBuybacks.sol)| 10 |
|[src/interfaces/extensions/IMEVCapture.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/extensions/IMEVCapture.sol)| 10 |
|[src/interfaces/extensions/IOracle.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/extensions/IOracle.sol)| 16 |
|[src/interfaces/extensions/ITWAMM.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/interfaces/extensions/ITWAMM.sol)| 18 |
|[src/lens/CoreDataFetcher.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/lens/CoreDataFetcher.sol)| 33 |
|[src/lens/ERC7726.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/lens/ERC7726.sol)| 73 |
|[src/lens/IncentivesDataFetcher.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/lens/IncentivesDataFetcher.sol)| 89 |
|[src/lens/PriceFetcher.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/lens/PriceFetcher.sol)| 159 |
|[src/lens/QuoteDataFetcher.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/lens/QuoteDataFetcher.sol)| 116 |
|[src/lens/TWAMMDataFetcher.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/lens/TWAMMDataFetcher.sol)| 98 |
|[src/lens/TokenDataFetcher.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/lens/TokenDataFetcher.sol)| 64 |
|[src/libraries/CoreLib.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/CoreLib.sol)| 62 |
|[src/libraries/CoreStorageLayout.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/CoreStorageLayout.sol)| 65 |
|[src/libraries/ExposedStorageLib.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/ExposedStorageLib.sol)| 57 |
|[src/libraries/ExtensionCallPointsLib.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/ExtensionCallPointsLib.sol)| 188 |
|[src/libraries/FlashAccountantLib.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/FlashAccountantLib.sol)| 152 |
|[src/libraries/IncentivesLib.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/IncentivesLib.sol)| 47 |
|[src/libraries/OracleLib.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/OracleLib.sol)| 34 |
|[src/libraries/RevenueBuybacksLib.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/RevenueBuybacksLib.sol)| 16 |
|[src/libraries/TWAMMLib.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/TWAMMLib.sol)| 87 |
|[src/libraries/TWAMMStorageLayout.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/TWAMMStorageLayout.sol)| 44 |
|[src/libraries/TimeDescriptor.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/libraries/TimeDescriptor.sol)| 35 |
|[src/math/constants.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/constants.sol)| 6 |
|[src/math/delta.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/delta.sol)| 85 |
|[src/math/exp2.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/exp2.sol)| 200 |
|[src/math/fee.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/fee.sol)| 18 |
|[src/math/isPriceIncreasing.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/isPriceIncreasing.sol)| 6 |
|[src/math/liquidity.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/liquidity.sol)| 76 |
|[src/math/sqrtRatio.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/sqrtRatio.sol)| 69 |
|[src/math/tickBitmap.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/tickBitmap.sol)| 73 |
|[src/math/ticks.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/ticks.sol)| 97 |
|[src/math/time.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/time.sol)| 41 |
|[src/math/timeBitmap.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/timeBitmap.sol)| 50 |
|[src/math/twamm.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/math/twamm.sol)| 83 |
|[src/types/bitmap.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/bitmap.sol)| 27 |
|[src/types/buybacksState.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/buybacksState.sol)| 69 |
|[src/types/callPoints.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/callPoints.sol)| 60 |
|[src/types/claimKey.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/claimKey.sol)| 12 |
|[src/types/counts.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/counts.sol)| 31 |
|[src/types/dropKey.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/dropKey.sol)| 12 |
|[src/types/dropState.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/dropState.sol)| 28 |
|[src/types/feesPerLiquidity.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/feesPerLiquidity.sol)| 18 |
|[src/types/locker.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/locker.sol)| 19 |
|[src/types/mevCapturePoolState.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/mevCapturePoolState.sol)| 18 |
|[src/types/observation.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/observation.sol)| 18 |
|[src/types/orderConfig.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/orderConfig.sol)| 31 |
|[src/types/orderId.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/orderId.sol)| 2 |
|[src/types/orderKey.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/orderKey.sol)| 34 |
|[src/types/orderState.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/orderState.sol)| 33 |
|[src/types/poolBalanceUpdate.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/poolBalanceUpdate.sol)| 18 |
|[src/types/poolConfig.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/poolConfig.sol)| 114 |
|[src/types/poolId.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/poolId.sol)| 2 |
|[src/types/poolKey.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/poolKey.sol)| 19 |
|[src/types/poolState.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/poolState.sol)| 36 |
|[src/types/position.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/position.sol)| 24 |
|[src/types/positionId.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/positionId.sol)| 40 |
|[src/types/snapshot.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/snapshot.sol)| 29 |
|[src/types/sqrtRatio.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/sqrtRatio.sol)| 104 |
|[src/types/storageSlot.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/storageSlot.sol)| 36 |
|[src/types/swapParameters.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/swapParameters.sol)| 64 |
|[src/types/tickInfo.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/tickInfo.sol)| 24 |
|[src/types/timeInfo.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/timeInfo.sol)| 36 |
|[src/types/twammPoolState.sol](https://github.com/code-423n4/2025-11-ekubo/blob/main/src/types/twammPoolState.sol)| 44 |
|**Totals** | **6283** |


*For a machine-readable version, see [scope.txt](https://github.com/code-423n4/2025-11-ekubo/blob/main/scope.txt)*

### Files out of scope

| File         |
| ------------ |
| [test/\*\*.\*\*](https://github.com/code-423n4/2025-11-ekubo/tree/main/test) |
| Totals: 68 |

*For a machine-readable version, see [out_of_scope.txt](https://github.com/code-423n4/2025-11-ekubo/blob/main/out_of_scope.txt)*

# Additional context

## Areas of concern (where to focus for bugs)

### Assembly Block Usage

We use a custom storage layout and also regularly use stack values without cleaning bits and make extensive use of assembly for optimization. All assembly blocks should be treated as suspect and inputs to functions that are used in assembly should be checked that they are always cleaned beforehand if not cleaned in the function. The ABDK audit points out many cases where we assume the unused bits in narrow types (e.g. the most significant 160 bits in a uint96) are cleaned.

## Main invariants

The sum of all swap deltas, position update deltas, and position fee collection should never at any time result in a pool with a balance less than zero of either token0 or token1.

All positions should be able to be withdrawn at any time (except for positions using third-party extensions; the extensions in the repository should never block withdrawal within the block gas limit).

The codebase contains extensive unit and fuzzing test suites; many of these include invariants that should be upheld by the system.

## All trusted roles in the protocol


| Role                                | Description                       |
| --------------------------------------- | ---------------------------- |
| `Positions` Owner                          | Can change metadata and claim protocol fees               |
| `RevenueBuybacks` Owner                             | Can configure buyback rules and withdraw leftover tokens                       |
| `BaseNonfungibleToken` Owner | Can set metadata of the NFT |

## Running tests

### Prerequisites

The repository utilizes the `foundry` (`forge`) toolkit to compile its contracts, and contains several dependencies through `foundry` that will be automatically installed whenever a `forge` command is issued.

**Most importantly**, the codebase relies on the `clz` assembly operation code that has been introduced in the pre-release `solc` version `0.8.31`. This version **is not natively supported by `foundry` / `svm` and must be manually installed**.

The compilation instructions were evaluated with the following toolkit versions:

- forge: `1.4.4-stable`
- solc: `0.8.31-pre.1`

### `solc-0.8.31` Compiler Installation

The `0.8.31` compiler must become available as if it had been installed using the [`svm-rs` toolkit](https://github.com/alloy-rs/svm-rs) that `foundry` uses under the hood. As the toolkit itself does not support pre-release candidates, the version must be manually installed.

To achieve this, one should head to the folder where `solc` versions are installed:

- Default Location: `~/.svm`
- Linux `~/.local/share/svm`
- macOS: `~/Library/Application Support/svm`
- Windows Subsystem for Linux: `%APPDATA%\Roaming\svm`

A folder named `0.8.31` should be created within and the pre-release binary of your architecture should be placed inside it aptly named `solc-0.8.31` without any extension.

To download the relevant pre-release binary, visit the following official Solidity release page: https://github.com/argotorg/solidity/releases/tag/v0.8.31-pre.1

### Building

After the relevant `0.8.31` compiler has been installed properly, the traditional `forge` build command will install the relevant dependencies and build the project:

```sh
forge build
```

### Tests

The following command can be issued to execute all tests within the repository:

```sh
forge test
``` 

### Submission PoCs

The scope of the audit contest involves multiple internal and high-level contracts of varying complexity that are all combined to form the Ekubo AMM system.

Wardens are instructed to utilize the respective test suite of the project to illustrate the vulnerabilities they identify, should they be constrained to a single file (i.e. `RevenueBuybacks` vulnerabilities should utilize the `RevenueBuybacks.t.sol` file).

If a custom configuration is desired, wardens are advised to create their own PoC file that should be executable within the `test` subfolder of this contest.

All PoCs must adhere to the following guidelines:

- The PoC should execute successfully
- The PoC must not mock any contract-initiated calls
- The PoC must not utilize any mock contracts in place of actual in-scope implementations

## Miscellaneous

Employees of Ekubo Protocol and employees' family members are ineligible to participate in this audit.

Code4rena's rules cannot be overridden by the contents of this README. In case of doubt, please check with C4 staff.
