# Obvious's RPG Agents
This is my preset and character cards to run a long form TTRPG in Silly Tavern.
<img width="424" height="424" alt="Obvious Agents sq" src="https://github.com/user-attachments/assets/dab5a776-0384-445c-827f-8235a1628080" />


My last full session was 8k messages and 70 NPCs. The AI didn't forget details or mess up the plot. I had a battle of a goblin army of 68 attacking a town where my party helped the town defense with leaders plus 40 guards and everything followed the TTPRG rules with bonus actions, reactions, saving throws, etc..

How: I use **20** separate agent characters in a group chat, each with distinct functions to ensure extremely high prompt adherence and token efficiency. The preset is tiny, lorebooks are used for characters/setting and each character gets a unique set of instructions.

Why: Giving a lot of different instructions confuses the AI. It tries to do everything in one reply, doing a terrible job of each. Explaining both a combat calculation sequence and narration style in the same guidance results in rubbish. Asking a blacksmith what he has for sale gives a long narration about the thing the AI thinks you want to buy instead of a proper list with weapon stats. The instructions should be filtered to exactly what it is doing in that message. The AI is also extremely sycophantic in RPG settings, so forcing them to use an actual game system and make proper rolls creates an entirely different, solid experience. Basically the pacing feels like actually playing a proper roleplaying game while the options remain vast.

## Example Session
* Your party is traveling along an unknown road.
* Run the **Travel** agent which randomly says you discover a hidden path to a hostile fort.
* Run the **Location** agent to map out the location and populate it with characters.
* Run **Character** to build several detailed personalities (especially important for interesting bad guys!)
* You try to spy on the fort, say "the party tries to use stealth to scout the fort, DC 15" and run **SkillCheck** to see if you are successful and what you can see.
* Now say something as user to talk with your party members about it for several turns, using the **Narrator** char.
* Your group decides to attack. Run **SkillCheck** again to attempt sneaking up to the fort.
* Run **Initiative** to get the action order and everyone's stats laid out.
* Keep running the **Battle** char which resolves one combat action at a time, writing your own message only when your turn is called or until the battle is resolved. Use a fast model for this.
* You find their hoard, run **Loot** to populate the chest. Then take what you want and distribute.
* Run **XP** to total experience gains and possibly level up for each character in the party.
* Then run **Tracker** to record everything - time of day, inventory, present characters, quest status, open threads.
* Now switch back to chat with your party with **Narrator**.
* You make camp and fall asleep, run the **Sleep** char to see if any events happened.

Naturally there is more directing involved here, but it *works*.

## The Approach
The preset is extremely light and static, containing only the lorebook entries, persona and chat history -- zero AI guidance. All setting lore and NPC cards should be stored as lorebook entries. The guidance for the AI's behavior are in each character card. Each character card is an agent that only contains it's guidance. The preset moves that guidance to be at depth 0. The instructions are brief enough the AI does not forget what was going on in the story's last message.

I recommend to leave main NPC and location lorebook entries as Constant (blue dot). Normal (triggered) reduces tokens, but static ensures an extremely high cache hit rate. When NPCs are gone for a while I manually turn off their entry. I run 100k tokens on average but it's cheap given >95% cache hit rate and the AIs don't struggle picking up old details.

I use Inline Summary to summarize sessions from the prior XP/Tracker calculations to right before the new ones - usually about 100-150 messages at a time.

I have a Visual Novel element with 10 different images per character with highly consistent character look. Remove the line from the Narrator agent or create those as well, but the VN is *highly recommended!*

The whole thing is highly modifiable and forgiving. Switch things up to your liking.

## The Agents

Here are the agents!

1. **Narrator** - your typical prose and dialog with no distracting instructions. I don't run a separate turn-by-turn tracker. Each message prepends the time, nothing else. May append a skill check with DC for the party to discover more.
2. **CYOA** - presents four choices of what to do next. Includes DC checks where appropriate.
3. **SkillCheck** - checks if a user/character action succeeds against pre-rolled dice values. Best after Narrator or CYOA already set the DC of the role.
4. **Spicy** - gooner narration to hit the right notes and keep the session more interactive, shorter messages, less full sentence conversation. Not having this in the main narrator prevents certain AIs from turning everything horny.
5. **Initiative** - sets up a battle, describes the layout, generates missing stats/skills, groups identical characters into groups, rolls for initiative
6. **Battle** - runs one combat action with a small amount of dialog, calculates the outcomes. Run repeatedly to cycle through NPCs until it is User's turn called.
7. **Location** - develops the history, layout and NPCs present at a new location. The AI is instructed to be fully omniscient. Copy to a lorebook entry if a recurring place or let it fall off into summaries.
8. **Character** - creates a detailed character card. In the preceding user message say which character(s) you want. I copy each ongoing character to a new lorebook entry. Temporary characters can roll off into summaries - it is especially useful in making enemies more interesting. As characters evolve you can run the agent again to update existing cards and then replace their lorebook entry. Run on main NPCs after major events or leveling up.
9. **ImagePrompt** - crafts an image prompt to drop into comfyui or whatever tool you like. My workflow is included with the files.
10. **XP** - calculates and tracks XP earned by character. If leveled up then processes the improvements, including giving options of skills to choose from.
11. **Trainer** - a deliberate approach to skills at level up. Instantly obtaining skills makes can make protagonists treated as godlike unless this is brutally normalized in the lore. You need to train a skill from a trainer or manual. You start at a base level of effectiveness and this grows by a percentage day of practice.
12. **Loot** - generates content of chest or other stash. Keeps it relatively simple. No junk to take for sale - coins and maybe better equipment, maybe something lore/quest related.
13. **Tracker** - typical tracker of present characters, clothes, inventory, quests, open threads, etc.. I find with decent models this only needs to run once every 100 messages or after major changes. More frequent trackers I find need excessive babysitting.
14. **Quest** - prompts and NPC discussion or board readout to give an appropriate spread of correctly rewarded quests.
15. **Timeskip** - generates a montage from the current time until the requested point in the future.
16. **Travel** - decides if travel is uneventful or what happens as a DM would.
17. **Sleep** - decides if sleep is uneventful or what happens as a DM would.
18. **Shop** - generates items for sale at a merchant, avoiding a massively text heavy conversation to talk about the three things the AI thinks you want to buy.
19. **Plot** - develops a scenario for a major story arc. This creates motivations of other characters and a suggested event that pull the User in.
20. **Auditor** - scans the chat history and lorebooks for bad character cards, plot problems, lore conflicts, etc.. This is especially helpful if you are running a model like Kimi that will get stuck in a thinking loop if something doesn't fit.

Before calling the secondary characters you can give it some guidance in the user message, then delete the user message after completing.

## Installation

###Starting a Chat:
1. Load the preset.
2. Import all of the character cards.
3. Load all the characters into a group chat. They are tagged with 'RPG Agent' to make this easy.
4. Mute all characters (except for either Narrator, Battle or Spicy if you are on a roll).
5. Enable your lorebook of choice for the setting at set to always active (blue dot).
6. Include a variable in your lorebook for your setting like so: {{.lore=Basic Fantasy}}.
7. Create a CYOA Regex (Name="CYOA", Find Regex="&lt;cyoa>[\s\S]*&lt;/cyoa>\s\*", check AI Output, Run On Edit, Alter Chat Display, Alter Outgoing Prompt, Min Depth=6)
8. Create a Battle Regex (Name="Battle", Find Regex="&lt;battle>[\s\S]*&lt;/battle>\s\*", check AI Output, Run On Edit, Alter Chat Display, Alter Outgoing Prompt, Min Depth=6)
9. Call the Character card with a little guidance to generate your persona, edit as you like.
10. Start the chat.

###Visual Novel images:
1. Install Comfyui
2. Load the workflow ZIT Profile Set.json included here.
3. Download any nodes and models you need (or switch to your own favorite models).
4. Put the character's name in the green node named "NAME OF CHARACTER"
5. Put the image prompt into the green node named "IMAGE PROMPT"
6. Update the folder where your silly tavern images for this roleplay sits in the green node named "FOLDER FOR IMAGES"
7. Run the ImagePrompt character, editing to whatever visual style you want.
8. Run the image prompt, repeat for each NPC

Please do customize everything to your preferred TTRPG and enjoy!
