# Cube 🧊

### Breaking the ice in finance one cube at a time

<div align="center">
<img 
  src="https://github.com/usecube/.github/blob/main/assets/png/cube-banner.png?raw=true" 
  style="width:50%; height:50%;"
/>
</div>

## Introduction 🎬

Cube is a Seamless Interoperable QR Payments Solution that aims to onboard millions of TradFi merchants onto the onchain economy.

Imagine a place where you can access Merchants Food / Goods / Services all onchain. That's where Cube breaks the ice in!

Following Jesse Pollak's vision of an Onchain Economy, Cube aims to be a part of the movement to bring users onchain, and stay onchain.

## How it works 👷🏻‍♂️

1. Click on the `Sign Up` Button and create a Coinbase Smart Wallet.
2. Head to [Thirdweb Faucet](https://thirdweb.com/base-sepolia-testnet) to get Base Sepolia ETH Funds (this is required for Basenames registration).
3. Once you have Base Sepolia ETH in your Coinbase Smart Wallet, proceed to register for an account.
4. Head to [Circle Faucet](https://faucet.circle.com/) to get Base Sepolia USDC Funds (this is required to transact on Cube).
5. Once you have Base Sepolia USDC in your Coinbase Smart Wallet, you are ready to Scan & Pay! Scan the following QR Code and enter the amount in SGD that you would like to pay.

<div align="center">
<img 
  src="https://github.com/usecube/.github/blob/main/assets/png/333-carrot-cake-qr.jpeg?raw=true" 
  style="width:30%; height:30%;"
/>
</div>

## Features 🦶🏻
1. 🧢 Basenames: Users can personalize their identity with unique custom basenames.

2. 🏘️ Paymaster: Gas and other on-chain operations are abstracted from the user.

3. 😌 Onchainkit: User Experience streamlined and 10x because of Onchainkit SDK.

4. 💳 ERC4626: Aave USDC Vault Strategy Valt on Base for merchants to generate onchain yield.

5. ⛴️ Merchant Registry: Registry of onchain merchants to provide food / good / services onchain.

## Architecture 🏛️
<img 
  src="https://github.com/usecube/.github/blob/main/assets/png/cube-architecture-bg.png?raw=true" 
  style="width:100%; height:100%;"
/>
</div>

## Stack 🌐
- **Frontend Stack**: NextJS, Typescript, Wagmi, Viem
- **Backend Stack**: Supabase, PostgreSQL, DrizzleORM
- **Smart Contracts**: Foundry, Solidity

## Limitations 🦁
1. **Basenames cannot be completely gasless** for the user due to `_validatePayment` function in `RegistrarController.sol`
```
/// @notice Enables a caller to register a name.
    ///
    /// @dev Validates the registration details via the `validRegistration` modifier.
    ///     This `payable` method must receive appropriate `msg.value` to pass `_validatePayment()`.
    ///
    /// @param request The `RegisterRequest` struct containing the details for the registration.
    function register(RegisterRequest calldata request) public payable validRegistration(request) {
        uint256 price = registerPrice(request.name, request.duration);

        _validatePayment(price);

        _register(request);

        _refundExcessEth(price);
    }
```
2. Coinbase Smart Wallet bug (using wagmi hooks will always default to Ethereum mainnet despite setting ChainId). [Video Link](https://drive.google.com/file/d/1QzVvOUiQeuPghsglc4HkGfMtyCE7d_Sp/view?usp=sharing)

```
const hash = await writeContracts(wagmiConfig, {
          contracts: [
            {
              address: BASE_SEPOLIA_REGISTRAR_CONTROLLER_ADDRESS,
              abi: RegistrarControllerAbi,
              functionName: "register",
              args: [
                {
                  name: registrationArgs.name,
                  owner: registrationArgs.owner,
                  duration: registrationArgs.duration,
                  resolver: registrationArgs.resolver,
                  data: registrationArgs.data,
                  reverseRecord: registrationArgs.reverseRecord,
                },
              ],
            },
          ],
          capabilities: {
            paymasterService: {
              chainId: BASE_SEPOLIA_CHAIN_ID,
              url: process.env
                .NEXT_PUBLIC_CDP_PAYMASTER_AND_BUNDLER_ENDPOINT as string,
            },
          },
          chainId: BASE_SEPOLIA_CHAIN_ID,
        });
```
## Improvements 🔨
1. Stablecoins Price Feeds for more accurate conversions.
2. Integrate more stablecoins into Cube (EURC).
3. More ERC4626 Choices (Aave + Morpho).
4. Integrate RIP-7755 by Onchainkit

## Links 🔗
- [Frontend + Backend Repository](https://github.com/usecube/cube-dapp) - NextJS + Typescript Frontend <> Supabase + DrizzleORM Backend
- [Smart Contracts](https://github.com/usecube/cube-contracts) - Foundry + Solidity


