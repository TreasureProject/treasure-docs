---
description: Guide for games to integrate badges into Treasure
---

# Badge Technical Implementation

## Step 1: Design Your Badge

Before determining which use case suits your needs, please review the [**Treasure Badge Design Guide**](https://drive.google.com/open?id=11598qNNmqoapSIUplgmtzPm-XsJOzTU9\&usp=drive\_fs) for how to prepare the image assets for your badge.

## Step 2: Identify Your Use Case

Choose one of the three use cases that best suits your needs.

### (1) Host Badges on the [TreasureBadges contract](https://arbiscan.io/address/0x0d2e10774abbd54bbffb1cc4c44fe6a66e82d196), Treasure app handles claiming/display

For spinning up a badge quickly without your own Badge infra:

* Provide us a way to check "is wallet address `X` is eligible to claim your badge `B`?".\
  Some options: (a) static list of addresses (WL) \[examples: plaintext list, or JSON array of strings], (b) API call, (c) contract method, (d) whether the user possesses a particular ERC721/ERC1155/ERC20 token.
* Send us the image assets designed according to the guidelines in Treasure Badge Guide.
* Provide us the metadata in the `REQUIRED` section described below in **Metadata**.

### (2) Host Badges tracking + claiming yourself, display on Treasure app

Best for decentralization:

* Send us the image assets designed according to the guidelines in Treasure Badge Guide.
* Provide us the metadata in **both** the `REQUIRED` + `OPTIONAL` sections described in **Metadata**.

### (3) Host Badge tracking yourself, allow claiming/display of Badge from Treasure app

For decentralized hosting of badges w/ possibility to let users claim from Treasure app:

* Provide us a way to check "is wallet address `X` is eligible to claim your badge `B`?".\
  Some options: (a) static list of addresses (WL) \[examples: plaintext list, or JSON array of strings], (b) API call, (c) contract method, (d) whether the user possesses a particular ERC721/ERC1155/ERC20 token.
* Send us the image assets designed according to the guidelines in Treasure Badge Guide.
* Provide us the metadata in **both** the `REQUIRED` + `OPTIONAL` sections described in **Metadata**.
* Tell us input parameters needed to call your badge contract to claim a badge.\
  Example: for Treasure badges, eligible users are given a struct (`ClaimInfo`) and a signature to the `TreasureBadges` contract to claim the badge on-chain.

## Step 3: Provide Us Metadata About Your Badge

The following is a subset of the TypeScript schema we use for representing Badge configurations in our backend.

<pre class="language-tsx"><code class="lang-tsx"><strong>interface BadgeInfo {
</strong>    // REQUIRED: Basic info for the badge.
    displayName: string; // Example: 'Socializer'
    description?: string; // Example: 'Connect all socials'
    descriptionGerund?: string; // Example: 'connecting my socials'
    imageUri: string; // Send to us and we can host. Or provide your own URI.
    externalUrl?: string; // Example: 'https://yourgame.io'

    // OPTIONAL: If you are managing your own badge contract, these fields let
    // Treasure check whether the badge has been claimed.
    claimConfig?: {
        // Supported chains:
        // 'arb' (Arbitrum)
        // 'arbnova' (Arbitrum Nova)
        // 'eth' (Ethereum mainnet)
        // 'arbgoerli' (Arbitrum Goerli)
        // 'sepolia' (Sepolia)
        chain: string;
        // Contract address for your self-managed badge contract.
        badgeAddress: string;
        // Token ID within your badge contract.
        badgeTokenId: string;
        // And any other metadata relevant to checking your badge status.
    }; 
}
</code></pre>

## External Links

* TreasureBadges contract: [https://arbiscan.io/address/0x0d2e10774abbd54bbffb1cc4c44fe6a66e82d196](https://arbiscan.io/address/0x0d2e10774abbd54bbffb1cc4c44fe6a66e82d196)
