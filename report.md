# **Origami Audit Competition on Hats.finance** 


## Introduction to Hats.finance


Hats.finance builds autonomous security infrastructure for integration with major DeFi protocols to secure users' assets. 
It aims to be the decentralized choice for Web3 security, offering proactive security mechanisms like decentralized audit competitions and bug bounties. 
The protocol facilitates audit competitions to quickly secure smart contracts by having auditors compete, thereby reducing auditing costs and accelerating submissions. 
This aligns with their mission of fostering a robust, secure, and scalable Web3 ecosystem through decentralized security solutions​.

## About Hats Audit Competition


Hats Audit Competitions offer a unique and decentralized approach to enhancing the security of web3 projects. Leveraging the large collective expertise of hundreds of skilled auditors, these competitions foster a proactive bug hunting environment to fortify projects before their launch. Unlike traditional security assessments, Hats Audit Competitions operate on a time-based and results-driven model, ensuring that only successful auditors are rewarded for their contributions. This pay-for-results ethos not only allocates budgets more efficiently by paying exclusively for identified vulnerabilities but also retains funds if no issues are discovered. With a streamlined evaluation process, Hats prioritizes quality over quantity by rewarding the first submitter of a vulnerability, thus eliminating duplicate efforts and attracting top talent in web3 auditing. The process embodies Hats Finance's commitment to reducing fees, maintaining project control, and promoting high-quality security assessments, setting a new standard for decentralized security in the web3 space​​.

## Origami Overview

Origami is a folding protocol designed to boost returns with higher token exposure and efficiency.

## Competition Details


- Type: A public audit competition hosted by Origami
- Duration: 2 weeks
- Maximum Reward: $70,000
- Submissions: 63
- Total Payout: $50,400 distributed among 24 participants.

## Scope of Audit

* Users deposit into the OrigamiInvestmentVault (ovToken) and are minted a share of the ovToken
* Origami deploys the deposited capital into the underlying protocol
* Origami auto compounds underlying protocol yield and the value of the ovToken share increases as new reserve tokens are added

| File                                                                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| contracts/common/access/OrigamiElevatedAccess.sol                            | (abstract) Inherit to add Owner roles for DAO elevated access.                                                                                                                                                                                                                                                                                                                                                                                                              |
| contracts/common/access/OrigamiElevatedAccessBase.sol                        | (abstract) Inherit to add Owner roles for DAO elevated access.                                                                                                                                                                                                                                                                                                                                                                                                              |
| contracts/common/access/Whitelisted.sol                                      | (abstract) Functionality to deny non-EOA addresses unless whitelisted.                                                                                                                                                                                                                                                                                                                                                                                                      |
| contracts/common/circuitBreaker/OrigamiCircuitBreakerAllUsersPerPeriod.sol   | Circuit Breaker implementation which tracks total volumes (across all users) in a rolling period window, and reverts if over a cap                                                                                                                                                                                                                                                                                                                                          |
| contracts/common/circuitBreaker/OrigamiCircuitBreakerProxy.sol               | Client contract issues circuit breaker requests to this proxy, which maps queries to the pre-mapped underlying implementation.                                                                                                                                                                                                                                                                                                                                              |
| contracts/common/flashLoan/OrigamiAaveV3FlashLoanProvider.sol                | A flashloan wrapper over an Aave/Spark flashloan pool                                                                                                                                                                                                                                                                                                                                                                                                                       |
| contracts/common/interestRate/BaseInterestRateModel.sol                      | An abstract base contract to calculate the interest rate derived from the current utilization ratio (UR) of debt.                                                                                                                                                                                                                                                                                                                                                           |
| contracts/common/interestRate/LinearWithKinkInterestRateModel.sol            | An interest rate curve derived from the current utilization ratio (UR) of debt. This is represented as two separate linear slopes, joined at a 'kink' - a particular UR.                                                                                                                                                                                                                                                                                                    |
| contracts/common/MintableToken.sol                                           | (abstract) An ERC20 token which can be minted/burnt by approved accounts                                                                                                                                                                                                                                                                                                                                                                                                    |
| contracts/common/oracle/OrigamiCrossRateOracle.sol                           | A derived cross rate oracle price, by dividing baseOracle / quotedOracle                                                                                                                                                                                                                                                                                                                                                                                                    |
| contracts/common/oracle/OrigamiOracleBase.sol                                | (abstract) Common base logic for Origami Oracle's                                                                                                                                                                                                                                                                                                                                                                                                                           |
| contracts/common/oracle/OrigamiStableChainlinkOracle.sol                     | An Origami oracle wrapping a spot price lookup from Chainlink, and a fixed expected historic price (eg 1 for DAI/USD)                                                                                                                                                                                                                                                                                                                                                       |
| contracts/common/oracle/OrigamiWstEthToEthOracle.sol                         | The Lido wstETH/ETH oracle price, derived from the wstETH/stETH \* stETH/ETH                                                                                                                                                                                                                                                                                                                                                                                                |
| contracts/common/RepricingToken.sol                                          | (abstract) A re-pricing token which implements the ERC20 interface.                                                                                                                                                                                                                                                                                                                                                                                                         |
| contracts/common/swappers/OrigamiDexAggregatorSwapper.sol                    | An on chain swapper contract to integrate with the 1Inch router | 0x proxy                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                                                                                                                                                                       |
| contracts/investments/lending/idleStrategy/OrigamiAaveV3IdleStrategy.sol     | Assets are supplied into aave v3 for yield                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| contracts/investments/lending/idleStrategy/OrigamiAbstractIdleStrategy.sol   | (abstract) The common logic for an Idle Strategy, which can allocate and withdraw funds in 3rd party protocols for yield and capital efficiency.                                                                                                                                                                                                                                                                                                                            |
| contracts/investments/lending/idleStrategy/OrigamiIdleStrategyManager.sol    | Manage the allocation of idle capital, allocating to an underlying protocol specific strategy.                                                                                                                                                                                                                                                                                                                                                                              |
| contracts/investments/lending/OrigamiDebtToken.sol                           | A rebasing ERC20 representing debt accruing at continuously compounding interest rate.                                                                                                                                                                                                                                                                                                                                                                                      |
| contracts/investments/lending/OrigamiLendingClerk.sol                        | Manage the supply/withdraw | borrow/repay of a single asset                                                                                                                                                                                                                                                                                                                                                                                                                 |
| contracts/investments/lending/OrigamiLendingRewardsMinter.sol                | Periodically mint new oToken rewards for the Origami lending vault based on the cummulatively accrued debtToken interest.                                                                                                                                                                                                                                                                                                                                                   |
| contracts/investments/lending/OrigamiLendingSupplyManager.sol                | Manages the deposits/exits into an Origami oToken vault for lending purposes, eg oUSDC. The supplied assets are forwarded onto a 'lending clerk' which manages the collateral and debt                                                                                                                                                                                                                                                                                      |
| contracts/investments/lovToken/managers/OrigamiAbstractLovTokenManager.sol   | (abstract) The delegated logic to handle deposits/exits, and borrow/repay (rebalances) into the underlying reserve token                                                                                                                                                                                                                                                                                                                                                    |
| contracts/investments/lovToken/managers/OrigamiLovTokenFlashAndBorrowManager.sol | The \`reserveToken\` is deposited by users and supplied into Aave/Spark as collateral. Upon a rebalanceDown (to decrease the A/L), \`debtToken\` is borrowed (via a flashloan), swapped into \`reserveToken\` and added back in as more collateral.                                                                                                                                                                                                                         |
| contracts/investments/lovToken/managers/OrigamiLovTokenErc4626Manager.sol    | A lovToken which has reserves as ERC-4626 tokens. This will rebalance by borrowing funds from the Origami Lending Clerk, and swapping to the origami deposit tokens using a DEX Aggregator.                                                                                                                                                                                                                                                                                 |
| contracts/investments/lovToken/OrigamiLovToken.sol                           | Users deposit with an accepted token and are minted lovTokens. Origami will rebalance to lever up on the underlying reserve token, targeting a specific A/L (assets / liabilities) range                                                                                                                                                                                                                                                                                    |
| contracts/investments/OrigamiInvestment.sol                                  | (abstract) A non-repricing Origami Vault base contract.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| contracts/investments/OrigamiInvestmentVault.sol                             | A repricing ERC20 Origami Vault which wraps an underlying non-repricing Origami Vault. When users deposit they are allocated shares. Origami will apply the supplied token into the underlying protocol in the most optimal way. The reservesPerShare() will increase over time as upstream rewards are harvested by the protocol and new underlying reserves are added (spread over time to avoid frontrunning). This makes the Origami Investment Vault auto-compounding. |
| contracts/investments/OrigamiOToken.sol                                      | Users deposit with an accepted token and are minted oTokens. Generally speaking this oToken will represent the underlying protocol it is wrapping, 1:1. Origami will apply the accepted investment token into the underlying strategy in the most optimal way. Users won’t ordinarily interact with this vault directly, as it will be wrapped by a repricing OrigamiInvestmentVault. This design does allow for future AMO integration on this token.                      |
| contracts/investments/util/OrigamiManagerPausable.sol                        | (abstract) A mixin to add pause/unpause for Origami manager contracts                                                                                                                                                                                                                                                                                                                                                                                                       |
| contracts/libraries/Chainlink.sol                                            | (library) A helper library to safely query prices from Chainlink oracles and scale them                                                                                                                                                                                                                                                                                                                                                                                     |
| contracts/libraries/CommonEventsAndErrors.sol                                | A collection of common events and errors thrown within the Origami contracts                                                                                                                                                                                                                                                                                                                                                                                                |
| contracts/libraries/CompoundedInterest.sol                                   | A maths library to calculate compounded interest                                                                                                                                                                                                                                                                                                                                                                                                                            |
| contracts/libraries/DynamicFees.sol                                          | A helper to calculate dynamic entry and exit fees based off the difference between an oracle historic vs spot price                                                                                                                                                                                                                                                                                                                                                         |
| contracts/libraries/OrigamiMath.sol                                          | Utilities to operate on fixed point math multiplication and division taking rounding into consideration                                                                                                                                                                                                                                                                                                                                                                     |
| contracts/libraries/Range.sol                                                | A helper library to track a valid range from floor <= x <= ceiling                                                                                                                                                                                                                                                                                                                                                                                                          |
| contracts/libraries/SafeCast.sol                                             | A helper library for safe uint downcasting                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## Medium severity issues


- **OrigamiOToken circulating supply underflows when users burn their tokens**

  A vulnerability has been identified in OrigamiOToken, specifically in the `circulatingSupply` function, which can underflow when users burn their tokens. In a proof of concept (PoC), an exploiter can trigger this underflow by minting tokens using `amoMint` and then burning them using `burn` instead of the intended `amoBurn`. This results in the `circulatingSupply` becoming a max uint256 value, which impacts the `globalUtilisationRatio` and subsequently, the interest calculations in the OrigamiLendingClerk contract. Although this does not affect user funds directly, it could lead to a minor manipulation of the interest rate. The issue highlights the need for reviewing how token minting and burning functions are handled to prevent such underflows.


  **Link**: [Issue #7](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/7)


- **Flash Loan Attack Can Temporarily Block USDC Exits via Circuit Breaker Cap**

  The circuitBreaker contract, designed to limit abnormal ovUSDC exits, is susceptible to abuse through a flash-loan attack. An attacker can exploit the `preCheck` function by using flash-loaned USDC to both invest in and exit oUSDC within a single transaction. This manipulation allows the attacker to fill the rolling period's cap artificially, leading to a denial-of-service (DoS) situation. Legitimate users would be unable to exit ovUSDC as the cap would be reached. To mitigate this vulnerability, recommended solutions include implementing a cooldown period between investment and exit actions or introducing an exit fee, preventing rapidly repeated transactions that could exploit the cap.


  **Link**: [Issue #27](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/27)


- **OrigamiAaveV3FlashLoanProvider Hardcodes AAVE Pool Address Against Protocol Recommendations**

  The `OrigamiAaveV3FlashLoanProvider` contract implements a permissionless flash loan wrapper over an Aave/Spark pool, but it hardcodes the AAVE pool address in an immutable variable. This approach conflicts with Aave protocol guidelines, as the pool address should always be dynamically fetched from the PoolAddressProvider contract. If the AAVE pool address changes (for instance, if it's deprecated or updated by Aave admins), the flash loan calls in `OrigamiAaveV3FlashLoanProvider` would fail because the immutable address cannot be updated. This recommendation is essential to avoid breaks in the contract's functionality. A reasonable mitigation step is to fetch the pool address before each flash loan call, ensuring the usage of the current valid address.


  **Link**: [Issue #58](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/58)


- **Inaccurate historic data in `stETH` oracle allows bypassing dynamic fees in lovStEth vault**

  The Origami team implemented a vault where users deposit wstETH and receive lovStEth tokens. Currently, the system uses the SPOT price to determine the value of reserves and calculate exchange rates, particularly penalizing or rewarding deposits and withdrawals based on this rate. The flaw identified is that the method for determining these rates always returns SPOT values, even when HISTORIC values are needed, potentially allowing users to exploit market fluctuations to extract more value from the vault than they deposited.

If the price of wstETH increases and then returns to normal, a user can deposit when the price is high and withdraw when it stabilizes, receiving more wstETH than initially deposited, at the expense of other users. Proposed solutions involve adopting a more adaptive fee structure based on a moving average or using Chainlink’s price feed for more accurate HISTORIC data.


  **Link**: [Issue #62](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/62)

## Low severity issues


- **Addressing Inconsistency in DynamicFees Library Due to Price Difference Calculation**

  In the DynamicFees library, the relative price difference calculation is inconsistent. Currently, it calculates the difference using different denominators based on the scenario, leading to an imbalance in fee multipliers. It is recommended to use a consistent approach by dividing `delta` by the minimum value to standardize the calculation. However, existing safeguards prevent this issue from having a significant impact.


  **Link**: [Issue #9](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/9)


- **Fee Collection in OrigamiLovToken Fails to Accrue Correct Amount Overtime**

  The fee collection mechanism in the `OrigamiLovToken` contract can only operate every 7 days. If attempted earlier, the function `collectPerformanceFees()` reverts. The current fee calculation assumes exactly 7 days between collections, leading to potential under-collection if delayed. A recommended fix is to base fee calculation on the actual elapsed time since the last collection.


  **Link**: [Issue #10](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/10)


- **Rounding Mode in SubtractBps Function Causes Slippage Protection Issues**

  The `investQuote` function calculates `quoteData.minInvestmentAmount` using a hardcoded rounding down mode in `subtractBps`, which may lead to an actual slippage percentage lower than what the user specifies. This misalignment can cause users to enter a minimum investment amount that doesn't match their expectations. Suggested fix: allow different rounding modes.


  **Link**: [Issue #16](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/16)


- **Incorrect debtTokenRepaid amount in RebalanceUp event during full deleveraging scenario**

  When the `OrigamiLovTokenFlashAndBorrowManager::_rebalanceUpFlashLoanCallback()` function is called, the `RebalanceUp` event emits an incorrect `debtTokenRepaid` value if the remaining debt is lower than the `flashLoanAmount`. This discrepancy arises because `totalDebtRepaid` is not updated correctly, potentially leading to misleading data for tracking purposes.


  **Link**: [Issue #31](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/31)


- **Rounding Behavior in LovTokenManager Deviates from Protocol Design Guidelines**

  In LovTokenManager, the rounding behavior deviates from its intended design of rounding down values. The function `_reservesToShares()` should round down the amount of lovTokens a user receives, but it does not consistently adhere to this rule. This discrepancy needs correction to ensure proper rounding down of all transfer assets/tokens.


  **Link**: [Issue #32](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/32)


- **maxExit function does not account for circuit breaker limits leading to misleading values**

  The `OrigamiLendingSupplyManager::maxExit()` function in the oUSDC system returns higher values than the circuit breaker allows for withdrawals within a 24-hour period. This misleads users about the amount they can withdraw. A suggested fix involves comparing the available amount with the circuit breaker limit to avoid reverted transactions.


  **Link**: [Issue #39](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/39)


- **Potential Revenue Loss Due to Inaccurate Performance Fee Calculation Adjustment**

  The current performance fee calculation risks potential revenue loss as it relies on the last recorded fee before collection. If the performance fee value is altered mid-period, the protocol may overlook previously accumulated fees, leading to smaller collected amounts. An improved design for fee accrual or provisional performance fee values is suggested.


  **Link**: [Issue #40](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/40)


- **Potential Manipulation Risk in LovDSR Vault's A/L Ratio, Causing Protocol Freeze**

  The `LovDSR` vault faces a risk of manipulation that could disrupt its stability by altering the `A/L` ratio, leading to a protocol freeze. A user could repay USDC without access checks, changing the ratio and preventing future borrowing. Restricting unauthorized repayments could mitigate this issue.


  **Link**: [Issue #41](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/41)


- **Add Validation to Ensure Correct Slope Relationship in Interest Rate Curve**

  The documentation states that interest rates should rise more steeply after the kink, but current input validation doesn't ensure this. If misconfigured, interest rates wouldn't increase as intended beyond the kink. It’s recommended to add a requirement to validate that the slope after the kink is steeper.


  **Link**: [Issue #42](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/42)


- **Circuit Breaker Cap Not Checked in _availableToBorrow() Leading to borrowMax() Failures**

  The `_borrow()` function includes a circuit breaker to limit USDC borrowing within 24 hours, but the `_availableToBorrow()` function does not account for this cap. Consequently, `borrowMax()` may attempt to borrow more than allowed, causing the circuit breaker to revert. This makes `borrowMax()` unusable and returns unreliable values from `availableToBorrow()`. A fix is suggested to account for the circuit breaker cap in `_availableToBorrow()`.


  **Link**: [Issue #44](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/44)


- **Risk of Recovering BorrowTokens with Outstanding Debt and Elevated Access**

  In `OrigamiAaveV3BorrowAndLend`, two token recovery functions exist: `reclaimSurplusDebt` and `recoverToken`. The former recovers `borrowToken` when there's no outstanding debt, while the latter can recover any token, even with outstanding debt, which poses a risk. Elevated access users can recover tokens, but additional checks are recommended to prevent potential issues.


  **Link**: [Issue #47](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/47)


- **Incorrect rounding direction in maxUserReserves calculation for maximum investment amount**

  The maximum investment amount calculation uses incorrect rounding. The `_maxUserReserves` function rounds down when converting debt to deposit assets, while the `liabilities` function rounds up. This discrepancy leads to inaccurate asset-to-liability (A/L) ratios. Fixing this improves code simplicity and correctness. The proposed revision ensures consistent rounding, preventing the A/L ratio from mistakenly reaching its ceiling.


  **Link**: [Issue #48](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/48)


- **Implementing checks to prevent stale prices in L2 Chains like Arbitrum**

  When using Chainlink in Layer 2 (L2) chains like Arbitrum, it's crucial to ensure prices aren’t mistakenly perceived as fresh if the sequencer is down, which may lead to stale prices. This can cause serious issues such as incorrect liquidations or borrowing. Implement a sequencer check in the L2 contract to prevent this.


  **Link**: [Issue #49](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/49)


- **maxInvest Function Returns Non-Zero Even When investWithToken Would Revert**

  The `maxInvest()` function should return the maximum amount of `fromTokens` that can be invested, and if `investWithToken()` reverts, `maxInvest()` should return 0. However, if `_userRedeemableReserves()` is 0, `maxInvest()` still returns a non-zero value, causing `investWithToken()` to revert. It is recommended to include a check in `maxInvest()` to return 0 when `_userRedeemableReserves() == 0`.


  **Link**: [Issue #50](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/50)


- **Potential Invariant Violation in Origami Protocol Due to Imbalanced Balance Tracking**

  The `Origami protocol` should maintain the invariant that `suppliedBalance` in `OrigamiAaveV3BorrowAndLend` should not be less than the actual balance. The issue arises because of discrepancies caused by donated tokens and the calculation of balances which can lead to reverted transactions. Proposed fixes include adjusting `recoverToken` function to ensure this invariant.


  **Link**: [Issue #52](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/52)


- **Lack of Input Validation in OrigamiIdleStrategyManager Threshold Settings Causes Inefficient Fund Movement**

  The `setThresholds()` function in `OrigamiIdleStrategyManager` lacks input validation for the relationship between `depositThreshold` and `withdrawalBuffer`. If `withdrawalBuffer` exceeds `depositThreshold`, it results in unnecessary fund movements between the idle strategy and the manager. It is recommended to ensure `withdrawalBuffer` is not higher than `depositThreshold` within the function's logic.


  **Link**: [Issue #53](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/53)


- **Potential DoS Attack in `Repricing Token` Due to Infrequent Reserve Checkpoints**

  In the `Repricing Token`, `vested reserves` are only updated when the `_checkpointAndAddReserves` function is called. This can result in scenarios where a user's redemption amount exceeds the `vestedReserves`, leading to a DoS issue. A proposed mitigation involves checking and updating `vestedReserves` before redemption.


  **Link**: [Issue #55](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/55)


- **Dynamic Fee Calculation Rounding Issue Reduces Protocol Fees Under Certain Conditions**

  The `DynamicFees` library calculates dynamic fees by comparing SPOT and HISTORIC prices. Currently, SPOT prices are always rounded up, and HISTORIC prices are always rounded down, leading to lower protocol fees when SPOT < HISTORIC. A recommended fix is to round both prices in the same direction. Overall impact is minimal.


  **Link**: [Issue #56](https://github.com/hats-finance/Origami-0x998f1b716a5022be026ca6b919c0ddf45ca31abd/issues/56)



## Conclusion

The Origami Audit Competition conducted by Hats.finance on the Origami protocol identified multiple security vulnerabilities, categorized as medium and low severity issues. Significant medium-level issues included vulnerabilities in token burning functions that could cause underflows, potential flash loan attacks exploiting the circuit breaker cap, and hardcoded AAVE pool addresses conflicting with protocol recommendations. These findings emphasize the need for dynamic and secure handling of token minting, flash loan operations, and address configurations. Several low-severity issues were identified, such as inconsistencies in dynamic fee calculations, inaccurate performance fee collections, and rounding errors in various contract functions. The report suggests multiple improvements, like implementing cooldown periods, better input validation, and consistent rounding methods. Overall, the audit demonstrates the benefits of decentralized security competitions, fostering a proactive bug-hunting environment, and leading to more robust and scalable web3 security solutions.

## Disclaimer


This report does not assert that the audited contracts are completely secure. Continuous review and comprehensive testing are advised before deploying critical smart contracts.


The Origami audit competition illustrates the collaborative effort in identifying and rectifying potential vulnerabilities, enhancing the overall security and functionality of the platform.


Hats.finance does not provide any guarantee or warranty regarding the security of this project. Smart contract software should be used at the sole risk and responsibility of users.

