# Guilds

### Overview

Guilds represent an on-chain feature that assembles wallets into groups. Owners and admins structure guilds, which function under specific rules that dictate guild creation and membership. Every guild issues a unique Soul Bound Token to its members, displaying the guild's name and emblem and indicating guild membership. Guilds aim to make wallet grouping more efficient and cultivate a sense of community and shared identity.

Guilds function under the wider organization, enabling substantial customization regarding governance and operations. Each organization can set who can form a guild and how they run. Following the establishment of a guild, the owner can invite wallets to join. Wallets can then accept these invitations, expanding the guild and fostering a collective within the organization.

## Key Features

1. **On-chain Wallet Grouping:** Guilds enable on-chain assembly of wallets into groups. This feature adds a layer of organization and community-building to the ecosystem.
2. **Customizable Structure:** Owners and admins have the power to structure guilds under specific rules that govern guild creation and membership. This allows for flexible and customized organizational design.
3. **Unique Soul Bound Tokens:** Each guild issues a unique Soul Bound Token to its members, representing their membership. The token carries the guild's name and emblem, fostering a sense of identity and belonging among members.
4. **Admin and Member Operations:** The guild system includes multiple features designed for managing guild members:
   * **Assign Admins:** The system allows for the assignment of administrative roles within the guild, empowering certain members with governance responsibilities.
   * **Kick Members:** Administrators have the power to remove members from the guild, ensuring they can maintain a positive and productive community environment.
   * **Invite Members / Join Guilds:** Guilds can extend invitations to wallets to join the guild, and wallets can accept these invitations, facilitating the expansion of the guild.
   * **Assign Member Levels:** The guild system allows for the definition of different levels or ranks for guild members, introducing a hierarchy or progression system within the guild.
   * **Invitation System:** Once a guild is established, the owner can invite other wallets to join. Wallets can accept these invitations, facilitating the expansion of the guild and fostering a sense of community within the organization.
5. **Enhanced Efficiency:** Guilds aim to streamline the process of wallet grouping, making it more efficient. This feature reduces complexity and facilitates smoother interactions within the ecosystem.
6. **Community Building:** Guilds promote a sense of community among members, fostering shared identity and encouraging collaboration. This enhances user engagement and satisfaction within the ecosystem.
7. **Customizable Governance and Operations:** Guilds operate under a wider organization, with substantial customization options for governance and operations. Each organization can set who can form a guild and how they run, allowing for varied and adaptable guild structures.

### Integration Guide

1. **Create an organization  -** Begin by setting up an Organization for your project. Refer to  [Getting Started](./#getting-started) for guidance on this process.
2. **Copy the Interface/ABI -** Check out [IGuildManager.sol](https://github.com/TreasureProject/spellcaster-facets/blob/develop/src/interfaces/IGuildManager.sol). If you're planning to call methods from another contract, import the interface file into your solidity project. If the intention is to call methods directly from the front end, copy the ABI.
3. **Call initializeForOrganization  -** Refer toe [IGuildManager.sol](https://github.com/TreasureProject/spellcaster-facets/blob/develop/src/interfaces/IGuildManager.sol) for information on the different parameters. his step is only necessary once.

```solidity
function initializeForOrganization(
        bytes32 _organizationId,
        uint8 _maxGuildsPerUser,
        uint32 _timeoutAfterLeavingGuild,
        GuildCreationRule _guildCreationRule,
        MaxUsersPerGuildRule _maxUsersPerGuildRule,
        uint32 _maxUsersPerGuildConstant,
        address _customGuildManagerAddress,
        bool _requireTreasureTagForGuilds
) external;
```

i.e.

```solidity
guildManager.initializeForOrganization(
    ORG_ID,
    1, // Users can only be in 1 guild at once
    1 days, // Have to wait 24 hours to join a new guild
    GuildCreationRule.ANYONE, // Anyone can create a guild in this organization
    MaxUsersPerGuildRule.CONSTANT, // Indicates to use the 200 parameter passed below
    200,
    address(0), // Only needed if doing custom interactions
    true // All users must have a Treasure Tag to join a guild
);
```

4. **Create Guilds -** You can permission the creation of guilds via `GuildCreationRules` setup in step 2. For example, you can allow anyone to create a guild within your organization or you can&#x20;
5. **Create Guilds**: Through `GuildCreationRules` set in step 2, you can control who can create guilds. For instance, you might allow anyone, or restrict it to just the organization admin. Use `createGuild` to establish a new guild in your organization.
6. **Configure Guild**: Use `updateGuildInfo` and `updateGuildSymbol` to change guild details like its name and symbol. These details appear with the soulbound token minted for users.
7. **Invite Users**: To invite users to a guild, use `inviteUsers`. To remove a user or retract an invitation, use `kickOrRemoveInvitation`.
8. **Set Up Guild Admins**: Use `changeGuildAdmins` to elevate or demote users to admin status. Admins can invite and remove users.
9. **Adjust Member Levels**: Each guild member has a level between 1-5. The significance of these levels is up to the guild, or this feature can be omitted. Guild admins can modify member levels.

For further reading, see  [IGuildManager.sol](https://github.com/TreasureProject/spellcaster-facets/blob/develop/src/interfaces/IGuildManager.sol).
