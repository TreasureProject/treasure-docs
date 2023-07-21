---
description: Pluggable on-chain game features
---

# Game Development Suite

## Introduction

Treasure offers a collection of modular on-chain features and engaging game loops designed to empower game developers. By seamlessly connecting their games to Treasure's tooling, developers can leverage on-chain game features as if they were native to their projects, streamlining the development process and accelerating time to market.

## Key Features

We offer a comprehensive suite of interconnected on-chain game loops and features that can be easily plugged into your game. This modular design enables developers to choose the functionalities that best suit their game, while providing a seamless integration experience. We currently offer the following infrastructure functionalities for games and dApps:

* **Creating and managing guilds**: Build and oversee player communities, establish hierarchies, and set up communication channels.
* **Facilitating in-game commerce/payments**: Enable secure and seamless in-game payments, including trading, buying, and selling virtual goods or services.
* **Asset emissions**: Efficiently generate, distribute, and manage in-game assets, such as items, currencies, or resources.

## Benefits

By utilizing our game development suite's powerful set of features, developers can enjoy numerous benefits, such as accelerated and cost-effective game development, enhanced collaboration with game partners, simplified cross-game interactions, and the ability to create captivating gaming experiences.

**Customizable and Adaptable Functionalities -** The tool's flexible design allows for customization and adaptation to fit the unique requirements of your games and dApps. Developers can tailor the functionalities to match their game's theme, mechanics, or aesthetics, ensuring a cohesive and engaging player experience.

**Continuous Updates and Feature Expansions -** We are committed to ongoing development, with regular updates and feature expansions to ensure it stays at the forefront of gaming infrastructure technology. Developers can rely on a continuously evolving toolkit to help them stay ahead of the curve and meet the demands of a dynamic industry.

**Integration into the Treasure Ecosystem -** Our game development suite is an integral part of the Treasure ecosystem, a thriving network of games and applications. This integration offers developers access to a larger community of users and partners, enabling collaboration on shared game loops, cross-game interactions, and enhanced gaming experiences.

**API/SDK for Simplified Integration (coming soon) -** The user-friendly API and SDK provided by our suite will streamline the integration process, making it simple for developers to connect their games and dApps to the platform. Comprehensive documentation and code samples further support developers in leveraging the tool's capabilities to their fullest potential.

## Who is this for?

1. **Game Builders**: It's a perfect tool for those seeking to craft unique, engaging gaming experiences. We provide on-chain game features, simplifying the development process. This allows creators to focus more on innovative gameplay. It caters to both independent developers and larger game studios, helping them create standout games.
2. **Treasure Ecosystem Partners**: As a vital part of the Treasure ecosystem, our game development suite integrates effortlessly with various network games and applications. Partners can enjoy improved collaboration, shared game loops, and cross-game interactions. By using this, they can help foster a vibrant community of interconnected games and applications, enhancing user experiences.

## Architecture

Our game development suite's architecture is designed to be a universal contract for all games, divided into modules with distinct functions. It allows third-party developers to customize according to their needs. This on-chain component, managed and updated by Treasure, uses a [Diamond](https://eips.ethereum.org/EIPS/eip-2535) contract that can be upgraded, ensuring our suite can evolve and accommodate new on-chain demands. This saves third-party developers the hassle of modifying their code for new features.

However, an upgradable contract might disrupt existing integrations - if a function Contract A relies on is removed, transactions through Contract A could fail. To prevent this, Treasure will only add to the core contract, maintaining backwards compatibility.

## Getting Started

Our tooling operates on the concept of 'Organizations,' where each Organization symbolizes a game. To start working with our game development suite on either the testnet or mainnet, you'll need to establish an Organization for your project.&#x20;

Reach out to us on [Discord](https://discord.com/invite/treasuredao) or email [info@treasure.lol](mailto:info@treasure.lol) for assistance.

## Links&#x20;

* [Spellcaster Github](https://github.com/TreasureProject/spellcaster-facets)

##
