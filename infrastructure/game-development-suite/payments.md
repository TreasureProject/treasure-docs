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





##
