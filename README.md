# zeru assignment 2
Data Collection Method:
Transaction history for each wallet was fetched from the Covalent API, specifically using the transactions_v2 endpoint on Ethereum Mainnet. This endpoint provides detailed transaction data including logs and event information relevant to DeFi protocols like Compound V2 and V3.

Feature Selection Rationale:
Key features were derived from on-chain event logs to capture the wallet’s interaction with the Compound protocol:

Number of Borrow events: indicates the borrowing activity of the wallet.

Number of Repay events: reflects the wallet’s repayment behavior.

Number of Liquidations: shows if the wallet was liquidated, indicating potential risk.

Total Borrowed Amount: quantifies exposure to borrowed assets.

Borrow-to-Repay Ratio: serves as a repayment consistency indicator.

Days Since Last Activity: used as a proxy for wallet activeness.

Scoring Method:
Due to the absence of Compound-specific event data in the fetched transactions, the risk scoring was primarily based on the wallet’s recency of activity (last_activity_days). A simple linear scoring function was applied where more recent activity (lower last_activity_days) yields a higher risk score (up to 1000), assuming that active wallets present higher exposure or risk. Wallets with no recent activity received lower scores approaching zero.

Justification of Risk Indicators Used:
Active wallets engaging recently in lending and borrowing are more likely to carry risk exposure due to ongoing debt positions or potential for liquidation. The lack of event data limited direct assessment of borrow/repay behaviors, so wallet activity recency served as a practical proxy for risk. This approach ensures scalability and can be extended to include richer protocol-specific features when detailed logs are available.

