# Payments

## Overview

The Payments module facilitates commerce within games. Developers can effortlessly process payments in a variety of ERC-20 currencies that leverage equivalent exchange rates for smooth transactions. For example, the payments module is used to define the cost of an asset to be, for example, the MAGIC equivalent of 10 USDC.&#x20;

## Key Features

1. **In-game Commerce Support:** The Payments module facilitates commerce within games, allowing developers to integrate a dynamic and engaging economy system within their gaming universe.
2. **Effortless Payments Processing:** Developers can easily process payments using the Payments module. It streamlines the usually complex process and allows for efficient and seamless transactions.
3. **Multiple Currency Support:** The module supports a variety of ERC-20 currencies, accommodating a diverse range of users and transactions. This feature broadens the scope of in-game purchases, making it more accessible for players around the globe.
4. **Equivalent Exchange Rates:** To ensure smooth transactions, the Payments module leverages equivalent exchange rates. This feature ensures fairness and consistency in transactions, making the trading process transparent and reliable.
5. **Asset Pricing:** The Payments module allows developers to define the cost of an asset in terms of another currency. This feature provides a flexible pricing mechanism that can cater to a wide range of pricing scenarios.
6. **Flexibility and Adaptability:** The Payments module allows developers to adapt to changing market conditions by adjusting asset prices or introducing new currencies. This flexibility allows for continual adaptation and improvement, ensuring the in-game economy remains engaging and dynamic.

## Integration Guide

1. The process of configuring a payment starts by calling a method on the game development suite. The method called depends on the payment currency and the currency used to determine the value.&#x20;

The methods are:

1. `makeStaticGasTokenPayment`: Accepts payment in ETH (gas token) with the price also in ETH. For instance, if you want exactly 1 ETH.
2. `makeStaticERC20Payment`: Takes payment in an ERC20 token, which is a flat amount. For example, if you want exactly 10 $MAGIC.
3. `makeGasTokenPaymentByPriceType`: Receives payment in ETH (gas token), priced in another currency. For instance, if you want ETH equivalent to $10 USD.
4. `makeERC20PaymentByPriceType`: Accepts payment in an ERC20 token, priced in another currency. For example, if you want $MAGIC equivalent to $10 USD.

These conversions are powered by ChainLink's [Price Feeds](https://docs.chain.link/data-feeds/price-feeds). Currently, our game development suite supports the following feeds:&#x20;

* $MAGIC <-> USD
* $ARB <-> USD
* ETH <-> USD.&#x20;

Refer to [IPayments.sol](https://github.com/TreasureProject/spellcaster-facets/blob/develop/src/interfaces/IPayments.sol) and [IPaymentsReceiver.sol](https://github.com/TreasureProject/spellcaster-facets/blob/develop/src/interfaces/IPaymentsReceiver.sol).&#x20;

If you want us to add another currency supported by ChainLink, please contact us via Discord or at [info@treasure.lol](mailto:info@treasure.lol).

2. To receive payments with the payment module, you need to deploy a contract for your project that implements the `IPaymentsReceiver`.

`IPaymentsReceiver` has two key methods: `acceptERC20` and `acceptGasToken`. These methods should verify all received parameters (price, token, etc.), and also act on the payment (like minting the user's NFT, emitting an event for external services to acknowledge the payment, recording the payment in the receiver contract, etc.). If you won't use a specific payment type, the method can revert safely.

An example of `IPaymentsReceiver` is available via [PaymentsReceiver](https://github.com/TreasureProject/spellcaster-facets/blob/develop/src/payments/PaymentsReceiver.sol). You can inherit directly from this contract or use it as a guide to create your own.

### Technical Cheat Sheet / Quick Reference

NOTE: See [#relevant-contract-addresses](payments.md#relevant-contract-addresses "mention") for the correct contract addresses to use for tokens / Payments Module. All addresses below will reflect **Arbitrum Mainnet**

#### Calculating Payment Amounts

**Get $10 USD worth of MAGIC:**\
`calculatePaymentAmountByPriceType(0x539bdE0d7Dbd336b79148AA742883198BBF60342, 1000000000, 2, 0x0000000000000000000000000000000000000000)`

_Example cast:_\
`cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "calculatePaymentAmountByPriceType(address,uint256,uint8,address)(uint256)" 0x539bdE0d7Dbd336b79148AA742883198BBF60342 1000000000 2 0x0000000000000000000000000000000000000000 --rpc-url https://arb1.arbitrum.io/rpc`

_Example cast formatted (assumes you have bc command):_\
`echo "scale=18; $(cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "calculatePaymentAmountByPriceType(address,uint256,uint8,address)(uint256)" 0x539bdE0d7Dbd336b79148AA742883198BBF60342 1000000000 2 0x0000000000000000000000000000000000000000 --rpc-url https://arb1.arbitrum.io/rpc | awk '{print $1;}') / 1000000000000000000" | bc`

**Get $10 USD worth of ARB:**\
`calculatePaymentAmountByPriceType(0x912CE59144191C1204E64559FE8253a0e49E654, 1000000000, 2, 0x0000000000000000000000000000000000000000)`

**Get $10 USD worth of ETH:**\
`calculatePaymentAmountByPriceType(0x0000000000000000000000000000000000000000, 1000000000, 2, 0x0000000000000000000000000000000000000000)`

_Example cast:_\
`cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "calculatePaymentAmountByPriceType(address,uint256,uint8,address)(uint256)" 0x0000000000000000000000000000000000000000 1000000000 2 0x0000000000000000000000000000000000000000 --rpc-url https://arb1.arbitrum.io/rpc`

_Example cast formatted (assumes you have bc command):_\
`echo "scale=18; $(cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "calculatePaymentAmountByPriceType(address,uint256,uint8,address)(uint256)" 0x0000000000000000000000000000000000000000 1000000000 2 0x0000000000000000000000000000000000000000 --rpc-url https://arb1.arbitrum.io/rpc | awk '{print $1;}') / 1000000000000000000" | bc`

#### Making Payments

For these I will use a dummy contract address (`0x1337000000000000000000000000000000001337`) that is assumed to implement the IPaymentsReceiver interface and otherwise be a valid receiver.

For the example casts I will use a dummy bob address (`0x0000000000000000000000000000000000000b0b`)

**Make a 10 $MAGIC payment:**\
`makeStaticERC20Payment(0x1337000000000000000000000000000000001337, 0x539bdE0d7Dbd336b79148AA742883198BBF60342, 10000000000000000000)`

_Example cast:_\
`cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "makeStaticERC20Payment(address,address,uint256)" 0x1337000000000000000000000000000000001337 0x539bdE0d7Dbd336b79148AA742883198BBF60342 10000000000000000000 --rpc-url https://arb1.arbitrum.io/rpc --from 0x0000000000000000000000000000000000000b0b --trace --verbose`

**Make a MAGIC payment equal to $10 USD:**\
`makeERC20PaymentByPriceType(0x1337000000000000000000000000000000001337, 0x539bdE0d7Dbd336b79148AA742883198BBF60342, 1000000000, 2, 0x0000000000000000000000000000000000000000)`

_Example cast:_\
`cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "makeERC20PaymentByPriceType(address,address,uint256,uint8,address)" 0x1337000000000000000000000000000000001337 0x539bdE0d7Dbd336b79148AA742883198BBF60342 1000000000 2 0x0000000000000000000000000000000000000000 --rpc-url https://arb1.arbitrum.io/rpc --from 0x0000000000000000000000000000000000000b0b --trace --verbose`

**Make an ARB payment equal to $10 USD:**\
`makeERC20PaymentByPriceType(0x1337000000000000000000000000000000001337, 0x912CE59144191C1204E64559FE8253a0e49E654, 1000000000, 2, 0x0000000000000000000000000000000000000000)`

**Make a 0.01 ETH payment (note different function than erc20):**\
`makeStaticGasTokenPayment(0x1337000000000000000000000000000000001337, 10000000000000000)`

_Example cast:_\
`cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "makeStaticGasTokenPayment(address,uint256)" 0x1337000000000000000000000000000000001337 10000000000000000 --rpc-url https://arb1.arbitrum.io/rpc --value 10000000000000000 --from 0x0000000000000000000000000000000000000b0b --trace --verbose`

**Make an ETH payment equal to $10 USD (note different function than erc20):**\
`makeGasTokenPaymentByPriceType(0x1337000000000000000000000000000000001337, 1000000000, 2, 0x0000000000000000000000000000000000000000)`

_Example cast (assuming $10 USD is_ .006 ETH)_:_\
`cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "makeGasTokenPaymentByPriceType(address,uint256,uint8,address)" 0x1337000000000000000000000000000000001337 1000000000 2 0x0000000000000000000000000000000000000000 --rpc-url https://arb1.arbitrum.io/rpc --value 6000000000000000 --from 0x0000000000000000000000000000000000000b0b --trace --verbose`

### Example CLI Commands

The following are scripts to assist in ensuring your contract is set up correctly and can use the Payments module. It is assumed that you have [Foundry/Cast](https://book.getfoundry.sh/getting-started/installation) installed.

#### Check if your contract supports the `IPaymentsReceiver` interface:

`cast call {your_contract_address} "supportsInterface(bytes4)(bool)" 0x298508df --rpc-url {your_network_rpc_url}`

NOTE: `0x298508df` is the value of `type(IPaymentsReceiver).interfaceId`

_Working example_:&#x20;

`cast call 0xb2e806a80D9328b3dC3787313588CE18A44B8653 "supportsInterface(bytes4)(bool)" 0x298508df --rpc-url https://arb1.arbitrum.io/rpc`

#### Check if making a payment through your contract will succeed

1. Get the necessary payment amount if you are pinning your payment to USD/some other second token:\
   `cast call {spellcaster_address} "calculatePaymentAmountByPriceType(address,uint256,uint8,address)(uint256)" {payment_token} {price} {price_type} {priced_token} --rpc-url {your_network_rpc_url}`\
   \
   _Working example for getting $25 worth of ETH:_\
   `cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "calculatePaymentAmountByPriceType(address,uint256,uint8,address)(uint256)" 0x0000000000000000000000000000000000000000 2500000000 2 0x0000000000000000000000000000000000000000 --rpc-url https://arb1.arbitrum.io/rpc`
2. Use `cast call` to simulate the makePayment transaction with your preferred payment token. To follow the example in #1 above, I will continue the gas token pinned to USD example (note --value XXXXX must match the output from #1 or you will get `IncorrectPaymentAmount`:\
   `cast call {spellcaster_address} "makeGasTokenPaymentByPriceType(address,uint256,uint8,address)" {your_contract_address} {price} {price_type} {priced_token} --from {your_sender} --value {value_from_step_1} --rpc-url {your_network_rpc_url} --trace --verbose`\
   \
   _Working example for seeing if an address with sufficient eth can mint a kaiju card pack during their event (will NOT work in the future when minting disabled / eth changes price):_\
   `cast call 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 "makeGasTokenPaymentByPriceType(address,uint256,uint8,address)" 0xb2e806a80D9328b3dC3787313588CE18A44B8653 2500000000 2 0x0000000000000000000000000000000000000000 --from 0x9b56E90e52070e307B66f8777d7FD572cF2FE464 --value 15214238096918503 --rpc-url https://arb1.arbitrum.io/rpc --trace --verbose`\
   \
   NOTE: If you get `IncorrectPaymentAmount` after plugging in the correct value from step #1 you may have hit a price feed update change, rerunning #1 to get the new value will fix this. This is only remotely likely to happen with gas token price feeds as they are more real-time and require precise value matching vs erc20 tokens only taking what is calculated.\


### Relevant Contract Addresses

#### Arbitrum Mainnet

| Contract        | Address                                    |
| --------------- | ------------------------------------------ |
| Payments Module | 0xF325aC5c9dc74A3c3b7F2474A709154E9F6bc194 |
| MAGIC           | 0x539bdE0d7Dbd336b79148AA742883198BBF60342 |
| ARB             | 0x912CE59144191C1204E64559FE8253a0e49E6548 |

#### Arbitrum Goerli

| Contract        | Address                                    |
| --------------- | ------------------------------------------ |
| Payments Module | 0x366A17839a625b87B114bE0aB5a45A979959702B |
| MAGIC           | 0x88f9eFB3A7F728fdb2B8872fE994c84b1d148f65 |
| ARB             | 0xF861378B543525ae0C47d33C90C954Dc774Ac1F9 |

Arbitrum Sepolia

| Contract        | Address                                    |
| --------------- | ------------------------------------------ |
| Payments Module | 0x06E308c2ED6168AfD158A4B495b084E9677F4E1D |
| MAGIC           | 0x55d0CF68a1Afe0932Aff6F36C87eFa703508191C |
| ARB             | N/A                                        |
