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

Extensions can freeze a pool and lock deposited user capital. This is considered an acceptable risk.

# Overview

Ekubo Protocol delivers the best pricing using super-concentrated liquidity, a singleton architecture, and extensions. The Ekubo protocol vision is to provide a balance between the best swap execution and liquidity provider returns. The contracts are relentlessly optimized to be able to provide the most capital efficient liquidity ever at the lowest cost.

## Links

- **Previous audits:**  
  - [Current Ethereum Version Audits](https://docs.ekubo.org/integration-guides/reference/audits#ethereum)
  - [Riley Holterhus Audit Report](https://github.com/code-423n4/2025-11-ekubo/blob/scout-changes/Ekub-Draft-Nov-14.pdf)
- **Documentation:** https://docs.ekubo.org/
- **Website:** https://ekubo.org/
- **X/Twitter:** https://x.com/EkuboProtocol

# Scope

*See [scope.txt](https://github.com/code-423n4/2025-11-ekubo/blob/main/scope.txt)*

### Files in scope


| File   | Logic Contracts | Interfaces | nSLOC | Purpose | Libraries used |
| ------ | --------------- | ---------- | ----- | -----   | ------------ |
| /src/Core.sol | 1| **** | 598 | |solady/utils/FixedPointMathLib.sol<br>solady/utils/SafeCastLib.sol<br>solady/utils/LibBit.sol|
| /src/Incentives.sol | 1| **** | 79 | |solady/utils/SafeTransferLib.sol<br>solady/utils/Multicallable.sol<br>solady/utils/MerkleProofLib.sol|
| /src/MEVCaptureRouter.sol | 1| **** | 30 | |solady/utils/SafeTransferLib.sol|
| /src/Orders.sol | 1| **** | 104 | |solady/utils/FixedPointMathLib.sol<br>solady/utils/SafeCastLib.sol<br>solady/utils/SafeTransferLib.sol|
| /src/Positions.sol | 1| **** | 28 | ||
| /src/PositionsOwner.sol | 1| **** | 37 | |solady/auth/Ownable.sol<br>solady/utils/Multicallable.sol|
| /src/RevenueBuybacks.sol | 1| **** | 100 | |solady/auth/Ownable.sol<br>solady/utils/Multicallable.sol<br>solady/utils/SafeTransferLib.sol|
| /src/Router.sol | 1| **** | 256 | |solady/utils/FixedPointMathLib.sol<br>solady/utils/SafeTransferLib.sol|
| /src/TokenWrapper.sol | 1| **** | 109 | |forge-std/interfaces/IERC20.sol<br>solady/utils/SafeCastLib.sol|
| /src/TokenWrapperFactory.sol | 1| **** | 17 | |forge-std/interfaces/IERC20.sol<br>solady/utils/EfficientHashLib.sol|
| /src/base/BaseExtension.sol | 1| **** | 44 | ||
| /src/base/BaseForwardee.sol | 1| **** | 17 | ||
| /src/base/BaseLocker.sol | 1| **** | 50 | ||
| /src/base/BaseNonfungibleToken.sol | 1| **** | 69 | |solady/tokens/ERC721.sol<br>solady/utils/LibString.sol<br>solady/auth/Ownable.sol|
| /src/base/BasePositions.sol | 1| **** | 184 | |solady/utils/SafeCastLib.sol<br>solady/utils/SafeTransferLib.sol|
| /src/base/ExposedStorage.sol | 1| **** | 16 | ||
| /src/base/FlashAccountant.sol | 1| **** | 232 | ||
| /src/base/PayableMulticallable.sol | 1| **** | 13 | |solady/utils/Multicallable.sol<br>solady/utils/SafeTransferLib.sol|
| /src/base/UsesCore.sol | 1| **** | 13 | ||
| /src/extensions/MEVCapture.sol | 1| **** | 189 | |solady/utils/FixedPointMathLib.sol<br>solady/utils/SafeCastLib.sol|
| /src/extensions/Oracle.sol | 1| **** | 271 | |solady/utils/FixedPointMathLib.sol|
| /src/extensions/TWAMM.sol | 1| **** | 464 | |solady/utils/FixedPointMathLib.sol<br>solady/utils/LibBit.sol|
| /src/interfaces/IBaseNonfungibleToken.sol | ****| 1 | 3 | ||
| /src/interfaces/ICore.sol | ****| 2 | 39 | ||
| /src/interfaces/IExposedStorage.sol | ****| 1 | 3 | ||
| /src/interfaces/IFlashAccountant.sol | ****| 3 | 11 | ||
| /src/interfaces/IIncentives.sol | ****| 1 | 12 | ||
| /src/interfaces/IOrders.sol | ****| 1 | 7 | ||
| /src/interfaces/IPositions.sol | ****| 1 | 9 | ||
| /src/interfaces/IRevenueBuybacks.sol | ****| 1 | 10 | ||
| /src/interfaces/extensions/IMEVCapture.sol | ****| 1 | 10 | ||
| /src/interfaces/extensions/IOracle.sol | ****| 1 | 16 | ||
| /src/interfaces/extensions/ITWAMM.sol | ****| 1 | 18 | ||
| /src/lens/CoreDataFetcher.sol | 1| **** | 33 | ||
| /src/lens/ERC7726.sol | 1| 1 | 73 | |solady/utils/FixedPointMathLib.sol|
| /src/lens/IncentivesDataFetcher.sol | 1| **** | 89 | ||
| /src/lens/PriceFetcher.sol | 1| **** | 159 | |solady/utils/FixedPointMathLib.sol|
| /src/lens/QuoteDataFetcher.sol | 1| **** | 116 | |solady/utils/DynamicArrayLib.sol|
| /src/lens/TWAMMDataFetcher.sol | 1| **** | 98 | ||
| /src/lens/TokenDataFetcher.sol | 1| **** | 64 | |solady/utils/SafeTransferLib.sol<br>solady/utils/DynamicArrayLib.sol<br>forge-std/interfaces/IERC20.sol|
| /src/libraries/CoreLib.sol | 1| **** | 62 | ||
| /src/libraries/CoreStorageLayout.sol | 1| **** | 65 | ||
| /src/libraries/ExposedStorageLib.sol | 1| **** | 57 | ||
| /src/libraries/ExtensionCallPointsLib.sol | 1| **** | 188 | ||
| /src/libraries/FlashAccountantLib.sol | 1| **** | 152 | ||
| /src/libraries/IncentivesLib.sol | 1| **** | 47 | ||
| /src/libraries/OracleLib.sol | 1| **** | 34 | ||
| /src/libraries/RevenueBuybacksLib.sol | 1| **** | 16 | ||
| /src/libraries/TWAMMLib.sol | 1| **** | 87 | |solady/utils/FixedPointMathLib.sol|
| /src/libraries/TWAMMStorageLayout.sol | 1| **** | 44 | ||
| /src/libraries/TimeDescriptor.sol | ****| **** | 35 | |solady/utils/DateTimeLib.sol<br>solady/utils/LibString.sol|
| /src/math/constants.sol | ****| **** | 6 | ||
| /src/math/delta.sol | ****| **** | 85 | |solady/utils/FixedPointMathLib.sol|
| /src/math/exp2.sol | ****| **** | 200 | ||
| /src/math/fee.sol | ****| **** | 18 | ||
| /src/math/isPriceIncreasing.sol | ****| **** | 6 | ||
| /src/math/liquidity.sol | ****| **** | 76 | |solady/utils/FixedPointMathLib.sol<br>solady/utils/LibBit.sol<br>solady/utils/SafeCastLib.sol|
| /src/math/sqrtRatio.sol | ****| **** | 69 | |solady/utils/FixedPointMathLib.sol|
| /src/math/tickBitmap.sol | ****| **** | 73 | ||
| /src/math/ticks.sol | ****| **** | 97 | |solady/utils/FixedPointMathLib.sol<br>solady/utils/LibBit.sol|
| /src/math/time.sol | ****| **** | 41 | |solady/utils/FixedPointMathLib.sol|
| /src/math/timeBitmap.sol | ****| **** | 50 | ||
| /src/math/twamm.sol | ****| **** | 83 | |solady/utils/FixedPointMathLib.sol|
| /src/types/bitmap.sol | ****| **** | 27 | ||
| /src/types/buybacksState.sol | ****| **** | 69 | ||
| /src/types/callPoints.sol | ****| **** | 60 | ||
| /src/types/claimKey.sol | ****| **** | 12 | ||
| /src/types/counts.sol | ****| **** | 31 | ||
| /src/types/dropKey.sol | ****| **** | 12 | ||
| /src/types/dropState.sol | ****| **** | 28 | ||
| /src/types/feesPerLiquidity.sol | ****| **** | 18 | ||
| /src/types/locker.sol | ****| **** | 19 | ||
| /src/types/mevCapturePoolState.sol | ****| **** | 18 | ||
| /src/types/observation.sol | ****| **** | 18 | ||
| /src/types/orderConfig.sol | ****| **** | 31 | ||
| /src/types/orderId.sol | ****| **** | 2 | ||
| /src/types/orderKey.sol | ****| **** | 34 | ||
| /src/types/orderState.sol | ****| **** | 33 | ||
| /src/types/poolBalanceUpdate.sol | ****| **** | 18 | ||
| /src/types/poolConfig.sol | ****| **** | 114 | ||
| /src/types/poolId.sol | ****| **** | 2 | ||
| /src/types/poolKey.sol | ****| **** | 19 | ||
| /src/types/poolState.sol | ****| **** | 36 | ||
| /src/types/position.sol | ****| **** | 24 | |solady/utils/FixedPointMathLib.sol|
| /src/types/positionId.sol | ****| **** | 40 | ||
| /src/types/snapshot.sol | ****| **** | 29 | ||
| /src/types/sqrtRatio.sol | ****| **** | 104 | ||
| /src/types/storageSlot.sol | ****| **** | 36 | ||
| /src/types/swapParameters.sol | ****| **** | 64 | ||
| /src/types/tickInfo.sol | ****| **** | 24 | ||
| /src/types/timeInfo.sol | ****| **** | 36 | ||
| /src/types/twammPoolState.sol | ****| **** | 44 | ||
| **Totals** | **39** | **15** | **6283** | | |

### Files out of scope

*See [out_of_scope.txt](https://github.com/code-423n4/2025-11-ekubo/blob/main/out_of_scope.txt)*

| File         |
| ------------ |
| ./script/DeployAndTestGas.s.sol |
| ./script/DeployCore.s.sol |
| ./script/DeployERC7726.sol |
| ./script/DeployIncentives.s.sol |
| ./script/DeployMEVCapture.sol |
| ./script/DeployRevenueBuybacks.s.sol |
| ./script/DeployStateful.s.sol |
| ./script/DeployStateless.s.sol |
| ./script/DeployTWAMMStateful.s.sol |
| ./script/DeployTWAMMStateless.sol |
| ./script/DeployTokenWrapper.s.sol |
| ./script/PrintCoreInitCodeHash.s.sol |
| ./test/Core.t.sol |
| ./test/FullTest.sol |
| ./test/Incentives.t.sol |
| ./test/MEVCaptureRouter.t.sol |
| ./test/MaxLiquidityPerTick.t.sol |
| ./test/Orders.t.sol |
| ./test/PositionExtraData.t.sol |
| ./test/Positions.t.sol |
| ./test/PositionsOwner.t.sol |
| ./test/RevenueBuybacks.t.sol |
| ./test/Router.t.sol |
| ./test/SolvencyInvariantTest.t.sol |
| ./test/SwapTest.t.sol |
| ./test/TWAMMInvariantTest.t.sol |
| ./test/TestToken.sol |
| ./test/TokenWrapper.t.sol |
| ./test/WithdrawMultiple.t.sol |
| ./test/base/ExposedStorage.t.sol |
| ./test/base/FlashAccountant.t.sol |
| ./test/base/FlashAccountantReturnData.t.sol |
| ./test/base/UsesCore.t.sol |
| ./test/extensions/MEVCapture.t.sol |
| ./test/extensions/Oracle.t.sol |
| ./test/extensions/TWAMM.t.sol |
| ./test/lens/ERC7726.t.sol |
| ./test/lens/OracleLib.t.sol |
| ./test/lens/PriceFetcher.t.sol |
| ./test/lens/QuoteDataFetcher.t.sol |
| ./test/lens/TWAMMDataFetcher.t.sol |
| ./test/lens/TokenDataFetcher.t.sol |
| ./test/libraries/CoreStorageLayout.t.sol |
| ./test/libraries/ExtensionCallPointsLib.t.sol |
| ./test/libraries/TWAMMStorageLayout.t.sol |
| ./test/libraries/TimeDescriptor.t.sol |
| ./test/math/delta.t.sol |
| ./test/math/exp2.t.sol |
| ./test/math/fee.t.sol |
| ./test/math/isPriceIncreasing.t.sol |
| ./test/math/liquidity.t.sol |
| ./test/math/sqrtRatio.t.sol |
| ./test/math/tickBitmap.t.sol |
| ./test/math/ticks.t.sol |
| ./test/math/time.t.sol |
| ./test/math/timeBitmap.t.sol |
| ./test/math/twamm.t.sol |
| ./test/types/bitmap.t.sol |
| ./test/types/buybacksState.t.sol |
| ./test/types/callPoints.t.sol |
| ./test/types/counts.t.sol |
| ./test/types/feesPerLiquidity.t.sol |
| ./test/types/locker.t.sol |
| ./test/types/mevCapturePoolState.t.sol |
| ./test/types/observation.t.sol |
| ./test/types/orderConfig.t.sol |
| ./test/types/orderKey.t.sol |
| ./test/types/orderState.t.sol |
| ./test/types/poolBalanceUpdate.t.sol |
| ./test/types/poolConfig.t.sol |
| ./test/types/poolKey.t.sol |
| ./test/types/poolState.t.sol |
| ./test/types/position.t.sol |
| ./test/types/positionId.t.sol |
| ./test/types/snapshot.t.sol |
| ./test/types/sqrtRatio.t.sol |
| ./test/types/swapParameters.t.sol |
| ./test/types/tickInfo.t.sol |
| ./test/types/timeInfo.t.sol |
| ./test/types/twammPoolState.t.sol |
| Totals: 80 |

# Additional context

## Areas of concern (where to focus for bugs)

### Assembly Block Usage

We use a custom storage layout and also regularly use stack values without cleaning bits and make extensive use of assembly for optimization. All assembly blocks should be treated as suspect and inputs to functions that are used in assembly should be checked that they are always cleaned beforehand if not cleaned in the function. The ABDK audit points out many cases where we assume the unused bits in narrow types (e.g. the most significant 160 bits in a uint96) are cleaned.

## Main invariants

The sum of all swap deltas, position update deltas, pand osition fee collection should never at any time result in a pool with a balance less than zero of either token0 or token1.

All positions should be able to be withdrawn at any time (except for positions using third party extensions; the extensions in the repository should never block withdrawal within the block gas limit).

The codebase contains extensive unit and fuzzing test suites; many of these include invariants that should be upheld by the system.

## All trusted roles in the protocol


| Role                                | Description                       |
| --------------------------------------- | ---------------------------- |
| `Positions` Owner                          | Can change metadata and claim protocol fees               |
| `RevenueBuybacks` Owner                             | Can configure buyback rules and withdraw leftover tokens                       |

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
