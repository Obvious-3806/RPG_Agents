# RPG_Agents
This is my preset and character cards to run a long form RPG in Silly Tavern.

I use 14 separate narrator characters in a group chat, each with distinct functions to ensure extremely high prompt adherence and token efficiency.

Why: Giving a lot of different instructions confuses the AI. It tries to do everything in one reply, doing a poor job of each. Explaining both a combat calculation sequence and narration style in the same guidance results in rubbish. Asking a blacksmith what he has for sale gives a long narration about the thing the AI thinks you want to buy instead of a proper list with weapon stats. The instructions should be filtered to exactly what it is doing in that message.

## Example Session
Your party is traveling along an unknown road. Run the **Travel** char which randomly says you discover a hidden path to a hostile fort. Run the **NewLoc** char to map out the location and populate it with characters. Run **NewChar** to build detailed personalities. You try to spy on the fort, run **SkillCheck** to see if you are successful and what you can see. Now say something as user to talk with your party members about it for several turns, using the **Narrator** char. Your group decides to attack. Run **SkillCheck** again to attempt sneaking up to the fort. Then shout some shit and start combat. Keep running the **Battle** char which resolves one combat action at a time, writing your own message only when your turn is called or until the battle is resolved. You find their hoard, run **Loot** to populate the chest which has zero junk loot to keep track of. One of the bandits survived as a prisoner so I copy that NewChar entry to a lorebook for later. After all that, run **XP** to total experience gains and possibly level up for each character in the party. Then run **Tracker** to record everything - time of day, inventory, present characters, quest status, open threads. Now switch back to chat with your party with **Narrator**. You make camp and fall asleep, run the **Sleep** char to see if any events happened.

## The Approach
The preset is extremely light and static, containing only the lorebook entries, persona and chat history -- zero AI guidance. All setting lore and NPC profiles should be stored as lorebook entries. The guidance for the AI's behavior are in each character card. Each character card is an agent that only contains a Character Note placing the guidance as system at depth 0. The instructions are brief enough the AI never forgets what was going on in the story's last message.

I recommend to leave main NPC and location lorebook entries as Constant (blue dot). Normal (triggered) reduces tokens, but static ensures an extremely high cache hit rate. When NPCs are gone for a while I manually turn off their entry. I run 100k tokens on average but it's cheap given >95% cache hit rate and the AIs don't struggle picking up old details.

I use Inline Summary to summarize sessions from the prior XP/Tracker calculations to right before the new ones - usually about 100-150 messages at a time.

## The Agents

Here are the agents that I use. The cards are extremely easy to customize to any game system.

**Narrator** - your typical prose and dialog with no distracting instructions. I don't run a separate turn-by-turn tracker. Each message prepends the time, nothing else.
**Spicy** - gooner narration to hit the right notes and keep the session more interactive, shorter messages, less full sentence conversation. Not having this in the main narrator prevents certain AIs from turning everything horny.
**Battle** - runs one combat action with a small amount of dialog, random rolls, and deciding the next action. Run repeatedly to cycle through NPCs until it is User's turn called.
**SkillCheck** - checks if a user/character action succeeds. Use when open to fail. Random{} options include "fails horribly", "fails humorously", "succeeds in unexpected way" which keeps things remarkably entertaining.
**XP** - calculates and tracks XP earned by character. If leveled up then processes the improvements, including giving options of skills to choose from.
**Trainer** - a deliberate approach to skills at level up. Instantly obtaining skills makes protagonists treated as godlike. This normalizes it. You need to train a skill from a trainer or manual. You start at a base level of effectiveness and this grows by a percentage day of practice.
**Tracker** - typical tracker of present characters, clothes, inventory, quests, open threads, etc.. I find with decent models this only needs to run once every 100 messages. I do not run a turn-by-turn tracker, but you can if you want, it wouldn't break anything here.
**NewLoc** - develops the history, layout and NPCs present at a new location. The AI is instructed to be fully omniscient. Copy to a lorebook entry if a recurring place or let it fall off into summaries.
**NewChar** - creates a detailed character profile. In the user message say which character(s) you want. I copy each ongoing character to a new lorebook entry. Temporary characters can roll off into summaries (this helps make even temporary enemies vastly more interesting and equips them properly). As characters evolve you can ask the NewChar to update existing profiles and then replace their lorebook entry. Run on main NPCs after major events or leveling up.
**Travel** - randomly decides if travel is uneventful or what happens. Different outcomes if the path is safe or dangerous.
**Sleep** - randomly decides if sleep is uneventful or what happens. Different outcomes if the location is safe or dangerous.
**Plot** - develops a scenario for a major story arc. This creates motivations of other characters and a suggested event that pull the User in.
**Shop** - generates items for sale at a merchant, avoiding a massively text heavy conversation to talk about (always) three things the AI thinks you want to buy.
**Loot** - generates content of chest or other stash. Keeps it relatively simple. No junk to take for sale - coins and maybe better equipment, maybe something lore/quest related.

Before calling the secondary characters you can give it some guidance in the user message, then delete the user message after completing.

## Installation

1. Load the preset.
2. Import all of the character cards.
3. Load all the characters into a group chat. They are tagged with 'RPG Agent' to make this easy.
4. Mute all characters except for Narrator (or Battle or Spicy for those scenes)
5. Import lorebook and enable - or write your own RPG systems for stats, equipment, etc.
6. Enable your lorebook of choice for the setting.
7. Write your Persona.
8. Start the chat.

