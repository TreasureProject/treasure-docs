# Emissions

## Overview

The emission infrastructure is a system designed to allow users to emit any type of asset (ERC20 and ERC1155) with configurable parameters including the amount, frequency, and duration of the emission. The primary use case of this system is to emit assets to partner games or players automatically in a pre-defined frequency/duration.&#x20;

## Key Features

The emission infrastructure has the following features:

1. **Multi-Asset Support**: The system supports multiple types of assets, including ERC20 and ERC1155.
2. **Configurable Emission Parameters**: Users can set parameters such as the total amount of assets to be emitted, the frequency of emission, and the duration of emission.
3. **Time-based Emission Rate**: Emission rates can be tied to a unit of time, ensuring a consistent flow of assets over a period.
4. **Reliability and Accuracy**: The system ensures that the correct amount of assets is emitted according to the configured parameters.

## Integration Guide

Here's how to integrate with the emission infrastructure:

See [IEmitter.sol](https://github.com/TreasureProject/spellcaster-facets/blob/develop/src/interfaces/IEmitter.sol) for more details on each step of the process, such as the exact function parameters and the meaning of each.\
\
**1. Create an organization -** See [Getting Started](./#getting-started) for steps to setup an Organization.

#### 2. Create an EmissionInstance

**Create an EmissionInstance**: This can be achieved using the `createEmittingInstance` function. Here, you can set the initial parameters defining the EmissionInstance. For detailed and current information about each parameter, refer to [IEmitter.sol](https://github.com/TreasureProject/spellcaster-facets/blob/develop/src/interfaces/IEmitter.sol).&#x20;

```solidity
function createEmittingInstance(
    bytes32 _organizationId, 
    EmittingCollectionType _collectionType, 
    address _collection, 
    uint64 _emittingFrequencyInSeconds, 
    uint256 _amountToEmitPerSecond, 
    uint64 _startTime, 
    uint64 _endTime, 
    EmittingRateChangeBehavior _rateChangeBehavior, 
    uint256 _tokenId, 
    bytes4 _emitFunctionSelector
) external;
```

**Example**

Suppose you want to continuously send 10 $EXAMPLE tokens to an address. You'd like this to happen daily, at the end of each day.

```solidity
emitter.createEmittingInstance(
    ORG_ID,
    EmittingCollectionType.ERC20,
    EXAMPLE_COLLECTION_ADDRESS,
    1 days,
    (10 ether) / 1 days, // Amount per second
    block.timestamp, // Start immediately
    0, // Indefinite
    EmittingRateChangeBehavior.CLAIM_PARTIAL, // See EmittingRateChangeBehavior for more details
    0, // No tokenId for ERC20
    IExampleToken.mint.selector // The function that actually mints the token
);
```

#### 3. Approve Addresses to Claim

You can authorize one or more addresses to claim from the emission using the `changeEmittingInstanceCanClaim` method. Remember, you need to call `changeEmittingInstanceCanClaim` separately for each address.\


```solidity
emitter.changeEmittingInstanceCanClaim(
    EMITTING_ID,
    ADDRESS,
    CAN_CLAIM // true to allow ADDRESS to claim. False to revoke claiming privelages
);
```

#### 4. Approve the Emitter to Emit the Collection as a Collection Owner

You can accomplish this using the `changeEmittingInstanceApproval` method. The owner of a contract must approve any call from an external contract via the game development suite to prevent malicious activity.

_Note_: If your token's contract mint method has permissions, you must enable the game development suite to call this method.

#### 5. Claim

Use the `claim` function from an approved address to retrieve any accumulated tokens.



##
