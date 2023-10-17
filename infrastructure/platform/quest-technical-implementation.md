# Quest Technical Implementation

In order for us to set up a Quest for a game within the Treasure Platform, the following details will need to be collected:

1. **Quest Name**
2. **Name of the associated Game**
3. **Quest Description:** A non-technical definition of what a player needs to do to achieve this quest (73 character limit is preferred).
4. **Technical Quest Criteria:** Technical information and definition of criteria. Please provide quest status info for a `walletAddress` using one of the following methods:
   1. **\[Option 1]** Provide us contract info (contract address + function call parameters) to indicate whether a user with `walletAddress` has completed the quest.
   2. **\[Option 2]** Provide us an API endpoint
      1. Example API endpoint
      2. [`https://example.com/api/quest?address={walletAddress]&questId={questId}&startDate={starteDate}&endDate={endDate}`](https://example.com/api/quest?address={walletAddress]\&questId={questId}\&startDate={starteDate}\&endDate={endDate})
      3. You choose the `questId` (we'll make sure there are no naming collisions). A good convention is to name your quest after your game, like `the-beacon-0001` .

```
  // Response format.
interface Response {
  walletAddress: string;
  completed: boolean;
  numerator: number;
  denominator: number;
}

// Example response JSON.
{
  "walletAddress": "0x1234....",
  "completed": false,
  "numerator": 4,
  "denominator": 10
}
```

Here, `numerator` and `denominator` are used by our frontend to display partial progress (e.g., defeat 10 bosses, where the current `walletAddress` has defeated 4 /10 so far).

5. **Required Items:** (an optional field as some quests might not require that the user own a specific token/gamepiece to complete the quest) will display via tool tip with link to required asset
6. **CTA Link:** The URL that the player will need to navigate to to work on said quest
7. **Badge (optional):** to accompany this specific quest. See the Badge [Design Guide](https://drive.google.com/file/d/11598qNNmqoapSIUplgmtzPm-XsJOzTU9/view?usp=sharing) and the [Technical Implementation Guide](https://docs.treasure.lol/infrastructure/player-identity-and-progression/badges-and-achievements/badge-technical-implementation) for more details.
8. **Quest Mechanics:** To help us normalize rewards please provide approximate scores in the following categories:
   1. **Friction Score:** On a scale of 1-10 with 10 being most friction, how much friction does a player need to go through in order to complete this quest?
   2. **Difficulty Score:** On a scale of 1-10 with 10 being most difficult, how much skill does a player need to complete this quest?
   3. **Time Required:** On average, how much time (in hrs) will a player need to commit to complete this quest?
