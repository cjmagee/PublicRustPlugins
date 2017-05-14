# What is this?

This repo isn't properly organized. It is more of an online backup of some important public plugins, that people can look through and check out.



# Plugins


## BlueprintsRevived (The Blueprint System)

Bringing back the original blueprint system into current rust. Trying to keep the original feel while bringing in all the new features.

**Many changes and balances were made:**

Blueprints (fragments, pages, books, librarys)  
Revealing a blueprint gives a random item blueprint from the respective tier  
Accurate loot tables to July 2016 branch (with current items added on top)  
Accurate blueprint tiers (balanced with current items)  
Recycle blueprints to down-convert them (pages to fragments for example)  
Research tables work extremely similar to original version (had to use a custom UI to have accuracte research percentage)  
Research tables appear in all monuments (will be loaded in and removed when the plugin is loaded / unloaded)  
Arrow raiding (Only on wood, and extremely slow on stone)  
Softsiding doors and ladder hatches  
Old raid towers / building privledge (irrelivant now that you can build twig inside building blocked)  
No heavy armour  
Spears un-nerfed (headshot damage x1.5)  
Crossbows and bows un-nerfed (headshot damage x1.5)  
Radiation disabled (by default)  
Hemp gives 20 cloth and no seeds (as per original system)  
P250 and revolver back to original clip size (revolver 6 bullets, p250 8 bullets)  
Configurable blueprint fragment rate (for modded servers)  
And more I forgot about!  

### Details:

There were many hacky solutions I had to use. This mod was decievingly simple: there was a bunch of stuff going around in the background to make it look as normal and unmodded as possible for the player.

The research table on it's own did absolutely nothing. I had to add a custom monobehavior to each one, that would add a sphere collider. When players entered the sphere collider, it would raycast 4m in front of the player 4x a second to see if they were looking at the research table. If so, it would show the icons and "Open" text just like the original table did, and allow the UI to open when the player pressed "E".

Since blueprint fragments were completely out of the game, I had to upload custom workshop skins and reskin an existing item to look 
like fragments. 

When uploading a workshop skin, you disconnect your internet, find the folder in %TEMP%, replace the icon.png with your custom icon, and reconnect your internet to upload your custom workshop item. Forget how I figured that out, but that was the spark that got me to actually take this mod on.

Luckily, presents had an "unwrap" and "combine" option, which was good enough to use as the base item. After a bunch of code to have them behave as seperate items based on the skin ID, the "blueprint fragments" were back in the game.

## Combatlog

A SUPER simple plugin, that grabs the combatlog of a player based on steamID. Eventually the plugin will change the way combatlog works, by filtering hits on players, animals, building blocks, heli, etc. (Would only display player attacks, the rest are irrelivant 99% of the time)

## NoDespawning

Could also be called "PersistantItems". A super cool plugin I wrote over a random weekend: it optimizes dropped items on a server, while also allowing them to stay around way longer. 

Originially all items had super long despawn times, but it was soon discovered that the only way players get rid of trash is by dropping it on the ground and letting it despawn. As it currently stands, items such as burlap clothing only stick around for 15 minutes, while an assault rifle will stay around for 3 days, and an m249 will stay around for an entire week!

### Details:

The optimization was to disable any inactive items, so that we wouldn't hit the collider limit by having a bunch of entities just sitting around on the ground, plus the more items with physics, the more the server is stressed.

I split the world into a grid with 20m X 20m cells, and assigned all items into their own cells. Once all items inside a grid stopped moving, the rigidbodies would all be disabled. Once a new item is dropped in the grid OR an entity with dropped items on it was destroyed, all items in that grid will be reactivated, and would stay active until an minimum timout and they stop moving.

Since items would be sticking around for a lot longer than 5 minutes and people would still try to despawn, I made multiple of the same item stack. This means that when destroying a chest filled up with wood, instead of dropping 30 individual stacks, it drops one stack of 30,000. When picking up the wood, you will only take 1 stack at a time, until it is all gone. 

Despawn time also scales with the over-stack amount: 10k wood despawns in 10x the time.

This had the side-effect of making it very difficult to crash a server by dropping a bunch of pumkins or rocks in one place, though you could still still use the much less effective method of "running around and dropping them one by one in different locations".

[Non-stackable items stack on the ground as well, while preserving attachment, ammo, etc.](https://www.youtube.com/watch?v=uCsUEroNQ3o)

## RecycleTweaks

Another simple plugin that allows empty cans to be recycled. It was also going to take care of other items in the blueprint system like the old hazmat gear, but that was taken out before I had the chance to add it in.

## ShorterNights

This one was written by audi (i_love_code), it made night shorter while making it very hard for the player to tell we skipped it. It switches between equal daylight levels (22:00 -> 5:00). Unless the player watches the sky and sees the moon jump, they won't notice the "magic" as it happens. 

## Visual Debug

[Preview](https://gyazo.com/0758809fb4e5d55bf32e48194571356a)

Allows you to look around at all the variables, and call functions inside any running plugin. 

I am actually super proud of this plugin: it was my first real dive into reflection, and it is really cool all the debugging and fun stuff you can do with it :)

Was super useful to see what funky stuff was going on when our modded server was really laggy. Perhaps there was an edge case causing a dictionary not to be cleared, or you wanted to call a reset function, but couldn't reload the plugin to add a chat command.
