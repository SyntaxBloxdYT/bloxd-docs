# Bloxd Code API 最新版docs

取得日: 2026-11-09 / Changelog最新: 2026-11-05 / 全27 ページ

出典はすべて https://bloxd.io/docs (ブラウザで取得)。

## 目次

- Welcome to the Bloxd Code API (https://bloxd.io/docs)
- Getting started (https://bloxd.io/docs/getting-started)
- Snippets (https://bloxd.io/docs/snippets)
- Changelog (https://bloxd.io/docs/changelog)
- How-Tos (https://bloxd.io/docs/how-to)
- Variations (https://bloxd.io/docs/how-to-variations)
- Plugins (https://bloxd.io/docs/how-to-plugins)
- Building a SessionBasedGame (https://bloxd.io/docs/how-to-building-a-session-based-game)
- Interactable NPCs (https://bloxd.io/docs/how-to-interactable-npcs)
- Dialogue (https://bloxd.io/docs/how-to-dialogue)
- Project schematics (https://bloxd.io/docs/how-to-project-schematics)
- API Reference (https://bloxd.io/docs/api-reference)
- Callbacks (https://bloxd.io/docs/callbacks)
- Client Options (https://bloxd.io/docs/client-options)
- Types (https://bloxd.io/docs/types)
- Entity Settings (https://bloxd.io/docs/entity-settings)
- Mob Settings (https://bloxd.io/docs/mob-settings)
- Vehicle Settings (https://bloxd.io/docs/vehicle-settings)
- Mesh Entities, Throwables & Node Mesh Attachment (https://bloxd.io/docs/mesh-entities)
- Quick Time Events (QTEs) (https://bloxd.io/docs/qte)
- Dialogue Voices (https://bloxd.io/docs/dialogue-voices)
- Particles (https://bloxd.io/docs/particles)
- Sounds and Songs (https://bloxd.io/docs/sounds)
- Icons (https://bloxd.io/docs/icons)
- Skins and Poses (https://bloxd.io/docs/skins)
- Block Names (1466 blocks) (https://bloxd.io/docs/block-names)
- Item Names (1492 items) (https://bloxd.io/docs/item-names)

---

## Welcome to the Bloxd Code API

URL: https://bloxd.io/docs

Run JavaScript in Bloxd, from a single block to a whole custom game.

Getting started
Code blocks, boards and World Code, and the globals your code can use.
Snippets
Ready-made code for common jobs, from moving players to running code every second.
18 snippets
API Reference
Every method on the api object, with parameters and return types.
251 methods
Callbacks
Functions your world code defines to react to game events.
84 callbacks
How-Tos
Step-by-step guides for variations, plugins and full games.
Client Options
Per-player options such as speed, health and camera.
132 options

Write JavaScript that runs inside Bloxd: make a block launch players into the sky, give your world its own shop, or build a whole custom game with rounds, teams and a winner.

New to coding in Bloxd?#

Start with Getting started, which explains code blocks, boards and World Code, and where each one runs. Then copy something from Snippets into a code block and change it to see what happens.

Building a game#

Callbacks let your World Code react to players joining, chatting, breaking blocks and more. The How-Tos walk through bigger features step by step, from plugins to a complete team game.

Looking something up#

The API Reference lists every method on api. Settings for players, entities, mobs and vehicles each have their own page, and the Assets pages list every block, item, sound, particle, icon and skin name you can use. Press Ctrl K, or ⌘ K on a Mac, to search all of it.

What's new#

The Changelog lists what has changed in the Code API, newest first.

Get help#

Ask questions, report problems and suggest features on our Discord.

Next
Getting started

---

## Getting started

URL: https://bloxd.io/docs/getting-started

Code blocks, boards and World Code, and the globals your code can use.


There are three places to write JavaScript in Bloxd: code blocks, code boards and World Code. Code in any of them controls the game through api, in custom games and worlds. Only players who can edit code (the canEditCode client option) can write it, but anyone can run a code block or board.

Please use our Discord to report problems or suggest features.

Code Blocks#
Find the Code Block by searching in the creative menu.
Clicking a code block runs its code, unless you are crouching. Players who can edit code open its code by right clicking it.
Running a code block or board also runs the code blocks and boards touching it, so clicking a press to code board next to a code block runs it without opening the code editor.
A code block doesn't need a press to code line, and removes one if you add it.
Boards#
A board whose text starts with press to code on its own line runs the code below that line when someone clicks it.
Boards only hold a little text: use a code block for anything longer, or split the code across several boards.
World Code#

World Code runs for the whole world instead of when someone clicks. Open it with F8. It defines Callbacks, such as tick and onPlayerJoin, which the game calls when things happen. The How-Tos build whole games with it.

Globals#
Name	Value
api	The game API: every method in the API Reference
myId	The ID of the player running the code, or null when nobody is, as in most World Code
playerId	The same as myId
thisPos	The position of the code block or board running the code, as [x, y, z]
api.ownerDbId	The database ID of the world's owner, or null if it has none
Logs and results#
api.log and console.log do the same thing: each shows its values in chat as a Log: message.
When the last line of a code block or board has a value, the player who ran it sees that value as a Result: message.
Next steps#

Snippets has short pieces of code to copy into a code block and change.

Previous
Welcome
Next
Snippets

---

## Snippets

URL: https://bloxd.io/docs/snippets

Ready-made code for common jobs, from moving players to running code every second.

18 snippets

Short pieces of code to copy into a code block and change to suit your world. In a code block or board, myId is the player who ran it. In World Code, use the player ID a callback is given instead.

Make the player jump#

Sets the player's velocity straight up, whatever they were doing.

JavaScript
Copy
api.setVelocity(myId, 0, 9, 0)
Push the player#

Adds to the player's velocity, so the push carries on from how they were already moving.

JavaScript
Copy
api.applyImpulse(myId, 9, 0, 9)
Teleport the player onto this block#

thisPos is the position of the code block or board that is running.

JavaScript
Copy
api.setPosition(myId, thisPos[0] + 0.5, thisPos[1] + 1, thisPos[2] + 0.5)
Send yourself a coloured message#
JavaScript
Copy
api.sendMessage(myId, "Welcome to my world!", { color: "orange" })
Send a message to everyone#
JavaScript
Copy
api.broadcastMessage("The game starts in 10 seconds!", { color: "red" })
Show flying text#

Text that flies across the middle of the player's screen. The last number is how far away whatever caused it is, which sets how the text flies.

JavaScript
Copy
api.sendFlyingMiddleMessage(myId, ["You found the secret room!"], 100)
Say a line of dialogue#

Shows a line below the crosshair, revealed word by word in a voice, with the speaker's name above it. It stays up until you hide it with api.setClientOption(myId, "dialogue", null). In World Code, sayDialogue from @plugins/dialogue hides it for you after a while.

JavaScript
Copy
api.setClientOption(myId, "dialogue", { line: "Welcome to my world!", speakerName: "Guide", voice: "regular" })
Set the player's health#

Logs the health they had before.

JavaScript
Copy
const oldHealth = api.getHealth(myId)
api.setHealth(myId, 50)
api.log("Old health:", oldHealth)
Give the player an item#
JavaScript
Copy
api.giveItem(myId, "Diamond Sword", 1)
Place a block above this block#
JavaScript
Copy
api.setBlock(thisPos[0], thisPos[1] + 1, thisPos[2], "Block of Gold")
Give the player a speed boost#

An inbuilt effect, for 10 seconds.

JavaScript
Copy
api.applyEffect(myId, "Speed", 10000, { inbuiltLevel: 1 })
Make the player faster#

Client options change how the game behaves for one player.

JavaScript
Copy
api.setClientOption(myId, "speedMultiplier", 2)
Play a sound#
JavaScript
Copy
api.playSound(myId, "equip_leather1", 1, 1)
Find every other player#

A function assigned without const or let stays defined for later code blocks, until World Code is next saved or the world restarts.

JavaScript
Copy
getOtherIds = () => {
	const otherIds = []
	for (const id of api.getPlayerIds()) {
		if (id !== myId) {
			otherIds.push(id)
		}
	}
	return otherIds
}
Turn the other players into zombies#

Uses getOtherIds from the snippet above.

JavaScript
Copy
for (const otherId of getOtherIds()) {
	api.setPlayerPose(otherId, "zombie")
	api.changePlayerIntoSkin(otherId, "head", "zombie")
}
Make everyone a floating wizard#
JavaScript
Copy
for (const playerId of api.getPlayerIds()) {
	api.setPlayerPose(playerId, "driving")
	api.changePlayerIntoSkin(playerId, "head", "wizard")
}
Welcome players as they join#

World Code: onPlayerJoin runs each time a player joins, with their ID.

JavaScript
Copy
onPlayerJoin = (playerId) => {
	api.sendMessage(playerId, "Welcome! Type in chat if you need help.", { color: "green" })
}
Run code every second#

World Code: tick runs many times a second, and is given the time since the last one, in milliseconds.

JavaScript
Copy
let sinceLastSecond = 0
tick = (ms) => {
	sinceLastSecond += ms
	if (sinceLastSecond >= 1000) {
		sinceLastSecond -= 1000
		api.broadcastMessage("Another second has passed")
	}
}
Previous
Getting started
Next
Changelog

---

## Changelog

URL: https://bloxd.io/docs/changelog

What changed in the Code API, newest first.

37 updates

Here you can discover the latest changes to the API.

5th November 2026#
Added the gameCamera client option, to take over a player's camera for top-down games, map flyovers, security cameras, spectating and cutscenes. Set its mode:
"fixed" stands still at a position, e.g. { mode: "fixed", position: [0, 30, 0], lookAt: playerId }.
"follow" moves with the player or another entity at an offset, e.g. a top-down view with { mode: "follow", offset: [0, 20, 5] }, or { mode: "follow", target: otherPlayerId, offset: [0, 3, -6], offsetSpace: "target", avoidTerrain: true } to spectate from behind.
"path" flies through keyframes of { timeMs, position, lookAt }.
"frame" keeps several players or positions in view, e.g. { mode: "frame", targets: api.getPlayerIds().slice(0, 64) }.
"default" goes back to the player's own camera.
Every camera takes blendInMs to glide there from the current view, and the others take fov in degrees, playerLook to let the mouse look around, and playerFacing to choose which way the player turns while walking. To replay the same path, set another camera first.
For cutscenes, every camera also takes transition to fade through a colour instead of blending, letterbox: true for black bars at the top and bottom of the screen, and hideHud: true to hide the HUD, e.g. { mode: "path", keyframes, transition: { outMs: 500, holdMs: 250, inMs: 600 }, letterbox: true, hideHud: true }, then { mode: "default", transition: { outMs: 500, holdMs: 250, inMs: 600 } } to fade back to the player's own camera.
customButtons can now use "Space" as a button's keycode, shown as _ next to the button, e.g. { id: "dash", icon: "bolt", keycode: "Space" }. Space also jumps for players who have not changed their jump key.
2nd November 2026#
Colours in CustomTextStyling and text styles (color / colour, and a ProgressBar's colours and backgroundColour) must now be plain CSS colours: a name, hex or rgb()/hsl()-style colour, e.g. "red", "#ff0000" or "rgba(255, 0, 0, 0.5)", optionally followed by stop positions in a ProgressBar's colours, e.g. "red 30%". Values with other CSS functions, such as url(), are refused with an error.
26th October 2026#
Added the lockHeadToBody entity setting. Set it on a mob, player or Person mesh entity to make it turn as one piece, so api.setEntityRotation sets where its whole body faces rather than turning its head first, e.g. api.setTargetedPlayerSettingForEveryone(eId, "lockHeadToBody", true).
api.setMobAiState takes an optional { hold: true } to keep a mob in the state you set until you set another one: it won't time out, react to nearby players or fight back when hit. It still leaves the state if its target leaves the game or turns invisible, or if it is tamed. For example, api.setMobAiState(mobId, "watching", { targetId: playerId }, { hold: true }) keeps a mob watching a player.
23rd October 2026#
Added the @plugins/dialogue plugin, whose sayDialogue shows a player a line for a while, 6 seconds by default, and clearDialogue hides it early. See the dialogue how-to for examples.
The new Dialogue Voices page lists every voice preset and explains how to build a custom SpeechSynth. Its dialogue editor lets you start from a preset, tune the voice, type a line to hear it read out, and copy the code.
Each docs page can now be copied as Markdown, or opened in ChatGPT or Claude to ask about it, from the buttons in its header. AI tools can also read every page as Markdown at /docs/<page>.md, with an index of them all at bloxd.io/llms.txt.
22nd October 2026#
The docs have a new home at bloxd.io/docs, with a page for every reference, setting list, How-To and asset list, in light and dark themes and laid out for phones too.
New pages: Getting started explains code blocks, boards and World Code, Snippets collects short examples to copy, and Types, on the site, explains every type the reference mentions.
Press Ctrl K, or ⌘ K on a Mac, to search every method, callback, setting, guide and asset name, landing right on it.
Methods, callbacks and settings are cards you can filter and copy from. Hover a type in a signature to see what it is, and each card links to the guides that use it and the changelog entries that mention it. Deprecated methods are marked.
Asset pages show what each name looks like or sounds like: particle effects play live, sounds and songs play in a player with a scrubber and volume, NPC skins and poses are shown as the game draws them, and blocks and items show their textures.
The Icons page has a CustomTextStyling editor: add parts from a list, edit their styles and icons, and copy the code.
Every QTE can be played on the QTEs page, with its sensible defaults.
Added the dialogue client option! Set it to show a player a line of dialogue below the crosshair, revealed word by word in a voice, with the speaker's name above it, e.g. api.setClientOption(playerId, "dialogue", { line: "Welcome!", speakerName: "Guide", voice: "regular" }). Set it to null to hide the line.
voice takes a preset, "soft", "regular", "dark", "high-pitched", "gruff", "lively", "posh" or "mechanical", or a SpeechSynth that sets every parameter. Leave it out for a silent line.
[[Item Name]] in a line shows that item's icon inline.
16th October 2026#
The damage callbacks (onPlayerDamagingOtherPlayer, onPlayerDamagingMob, onMobDamagingPlayer, onMobDamagingOtherMob) now receive a last damageInfo argument whose cause says what dealt the hit: "Melee", "Projectile", "Gun", "Explosion", "Spikes", "Fall", "Stomp", "Thorns" or "Effect", or null when unknown. Use it to tell a swing of a held item from that item going off, e.g. a punch with a Mining Grenade in hand from a Mining Grenade's blast.
api.attemptApplyDamage takes an optional damageCause, passed on to those callbacks.
30th September 2026#
interactable now gives mobs the same interaction priority as mesh entities: onPlayerAltAction runs before held-item actions. Native harvesting, mounting and pet actions are disabled while the setting is true; leave it false for ordinary mob behaviour.
29th September 2026#
Added project schematics to World Code! Use the + beside "Schematics" in the Code Editor to upload a .bloxdschem file or choose a snapshot from your profile. Projects support up to five schematics.
Added api.setChunkAsSchematic to replace one complete chunk, including air and block data. Positions are block coordinates selecting their containing chunks, like copyChunk.
Added api.getSchematicDimensions() to read a schematic's stored [x, y, z] dimensions, including selection padding.
@plugins/sessionBasedGame maps and lobbies now accept source: { schematic: "maps/arena.bloxdschem" } as an alternative to a world rectangle. Maps are pasted directly and must fit the available placement and block-data budgets.
Schematic saved from profiles are snapshots - you must update the schematic in the world/custom game if you edit the linked schematic otherwise.
See the project schematics how-to for examples and details.
10th September 2026#
Added the interactable entity setting. Set it on a mesh entity or a mob (e.g. api.setTargetedPlayerSettingForEveryone(eId, "interactable", true)) to make alt actioning it count as an interaction: the alt action is consumed, so a held block isn't placed through the entity and a held throwable isn't used, and onPlayerAltAction fires with the entity as the target. Leave it off for decorative entities, or they will swallow player input. It also makes the entity pickable, so an entity can be interactable with canAttack off: the player's aim lands on it and interacting works, but swinging or shooting at it does nothing. On a mob it applies alongside the usual mounting and taming behaviour rather than replacing it, though there a held throwable or consumable is still used in preference to interacting.
Entities marked interactable now show an interaction prompt by the crosshair while a player is looking at them, showing the key bound to the interact action (E by default) so players can tell which input to use. Set the new interactionPrompt entity setting to replace the label beside that key, e.g. api.setTargetedPlayerSettingForEveryone(eId, "interactionPrompt", "Open Shop"), and leave it off for the default "Interact". It takes plain text or CustomTextStyling, and describes what interacting does rather than which button to press, since the engine draws the key itself. Not shown on touchscreens, where a tap needs no prompt.
8th September 2026#
Added first-party plugins!
You can import helper scripts to help you from @plugins
E.g. import { setTimeout } from "@plugins/helpers"
See the plugins how-to for more information.
The biggest example of this is Session-Based Game, a helper to help you create a game with mini-matches, like Bedwars/Skywars etc.
import { createGame } from "@plugins/sessionBasedGame" to check it out
See the SessionBasedGame how-to for more information.
28th August 2026#
Added vehicle spawn callbacks:
onPlayerAttemptSpawnVehicle
onWorldAttemptSpawnVehicle
onPlayerSpawnVehicle
onWorldSpawnVehicle
onVehicleDespawned
Added onEntityDeleted, called whenever any non-player entity is deleted.
27th August 2026#
Added api.attemptSpawnVehicle to spawn rideable vehicles (boats, karts, cars) which players can mount with an alt action.
18th August 2026#
Added TypeScript support to World Code!
Rename your file from index.js to index.ts to use TypeScript files!
Import some of our types from @bloxd
E.g. import type { PlayerId } from "@bloxd"
Use your own types!
Type Checking is supported and errors will show if you use incorrect types.
Multiple files are supported! Split your code across multiple files for better readability!
Create .js and .ts files
Use import / export syntax to be able to import files across between versions
index.js or index.ts MUST be where your callbacks are stored and cannot be imported anywhere else.
require() syntax technically works although isn't type-safe.
Increased total code size from 64k characters to 512k characters.
Added variations to custom games!
Each custom game can now have multiple variations, with default being the default variation.
api.getVariation
api.matchmakeToVariation
See the variations doc for more information.
11th August 2026#
Added currency API:
api.setCurrency
api.getCurrency
api.deleteCurrency
api.getCurrencyAmount
api.setCurrencyAmount
api.giveCurrencyAmount
These currencies can be used in the currency field in the Shop to automatically deduct currency on purchase.
These can also be persisted across sessions.
10th August 2026#
Added to the UI Request System:
api.addUiRequestPopup
7th August 2026#
Added UI Request System:
api.addUiRequest
api.deleteUiRequest
onUiRequestResponded
20th July 2026#
New mob settings:
runningJumpInfo
runningRandomFacingInfo
runningSlideInfo
walkingJumpInfo
walkingRandomFacingInfo
walkingSlideInfo
13th July 2026#
Added new bridgeInfo mob setting to make mobs build bridges or leave trails, e.g.:
JavaScript
Copy
bridgeInfo: {
    blockToPlace: "Bricks",
    mustBeGrounded: false,
    yOffset: -1,
},
26th June 2026#
Added new client options for custom game UI:
middleTextTop
headerChips
Added ProgressBar support to options that accept a CustomTextStyling
e.g. ["Loading", { type: "ProgressBar", progress: 0.5 }]
15th June 2026#
Added new client options for adjusting the third person camera:
cameraRotationOffset
cameraPositionOffset
11th June 2026#
Added the ability to get and set scale for lifeforms (players, mobs)
api.getLifeformScale
api.setLifeformScale
Added new block standing callbacks:
This is to prevent having to use onBlockStand, which eats into your runtime limit significantly due to its high frequency of being called
onBlockStandStart
onBlockStandStop
Added isReceiveDamageCooldownGlobal client option and mob setting
10th June 2026#
Added showChatBubbles client option
Added useRespawnButton client option
Added multilineTextBox entity setting
Added lobbyLeaderboardTags entity setting
18th May 2026#
Added the ability to change the gamemode of a player
api.setPlayerGamemode
api.getPlayerGamemode
Added the ability to queue text to be displayed in different places on the screen
api.queueMiddleTextLower
api.queueMiddleTextUpper
api.queueCrosshairText
api.getQueuedStatus
api.removeFromQueue
15th May 2026#
Significantly increased runtime limit - interrupts should be less frequent
Added api.isNearInterrupt
12th May 2026#
Added new client option groundArrowPath
11th May 2026#
Added Changelog
Added a bunch of new API Methods:
api.addCustomKillfeedMessage
api.deleteAllItems
api.findItem
api.findStandardChestItem
api.getEffectLevel
api.getItemDropName
api.getItemIDsOverlappingWithPlayer
api.getMobDbId
api.hasEffect
api.preventFallDamageNextGrounding
api.removeItemNameFromStandardChest
api.resetCanChangeBlock
api.resetCanPickUpItem
api.setOtherEntitySettingToDefault
api.updateMeshParticleSystems
7th May 2026#
Added api.copyChunk
Added onPlayerToggledShopMenu
28th April 2026#
Doubled code block size (16000 -> 32000)
'Hide World Code' option renamed to 'Hide Code' and also hides code of Code Blocks
New docs page!
23rd April 2026#
Added api.matchmakePlayer
Added per-item gun stats in customAttributes.gunStats
21st April 2026#
Added database methods to write persisted data to be saved between sessions.
There are two sections of database values:
Lobby
api.getLobbyDBValue
api.setLobbyDBValue
api.deleteLobbyDBValue
api.deleteAllLobbyDBValues
Writes data that is persisted to the *lobby*, whether it's a worlds lobby or a lobby within a custom game
Player
api.getDBValue
api.setDBValue
api.deletePlayerDBValue
api.deleteAllPlayerDBValues
Writes data that is persisted to the player. For custom games, this data persists *between* lobbies
16th April 2026#
Added api.setItemStat
11th April 2026#
The Code Editor now supports collaborative editing
You can now simultaneously code with your other fellow coders at the same time! Hop into a code block or World Code together to simultaneously create the best World or the best Custom Game ever!!
7th April 2026#
New Code Editor UI! Syntax Highlighting, Autocomplete, Error Checking, and more!
25th March 2026#
Increased world code size from 16000 to 64000 characters
24th March 2026#
Added mesh entities!
api.attemptCreateMeshEntity
api.updateMeshEntity
api.deleteMeshEntity
Added throwables!
api.attemptCreateThrowable
api.deleteThrowable
23rd March 2026#
Added the ability to open and close chests for players, going beyond reach distance to open chests from far away
api.openChestForPlayer
api.closeChestForPlayer
Previous Changes#
For previous changes, see the code-api repository or #dev-log in the Bloxd Discord server
Previous
Snippets
Next
How-Tos

---

## How-Tos

URL: https://bloxd.io/docs/how-to

Step-by-step guides for variations, plugins and full games.


This contains a quick list of tutorials for some features that may be harder to understand on first glance.

Variations
Alternate versions of a custom game, and matchmaking players between them.
Plugins
Reusable first-party World Code features, imported from @plugins.
Building a SessionBasedGame
A full team game: lobby, teams, map voting, rounds and a winner.
Interactable NPCs
Entities players talk to or use, such as shopkeepers and guards.
Dialogue
Lines of dialogue below the crosshair, read out a syllable at a time in a voice.
Project schematics
Build whole chunks from schematics stored with your project.
More coming soon!#

If you think there are any guides we should add to this page, let us know in Discord!

Previous
Changelog
Next
Variations

---

## Variations

URL: https://bloxd.io/docs/how-to-variations

Alternate versions of a custom game, and matchmaking players between them.


Custom games now support *variations*, which allow you to create your own alterations of gameplay.

Custom Games#

In custom games, you can use api.getVariation() to get the current variation. For the base game, this will be default.

You can use api.matchmakeToVariation(playerId, variation) to connect a player to a different variation of your custom game. Use default to matchmake back to the original

Variation names must be between 1 and 32 characters. They can only contain letters, numbers, hyphens and underscores.

You can set the variation title using api.setClientOption(playerId, "customVariationTitle", "My Variation"). View the docs for the api.setClientOption or the customVariationTitle for more information.

Player database values (set with api.setPlayerDbValue, including persistent currencies) are shared across all variations of your custom game, so progress a player earns in the hub carries into 1v1, 2v2, etc. If you want a value to differ per variation, include the variation name in the key (e.g. `wins_${api.getVariation()}`).

Example#

Here's an example inspired by the lobby arenas of games such as Clutch and Containment Breach. It creates a hub variation (default) and then variations for two different modes: Solos (1v1) and Duos (2v2)

JavaScript
Copy

let initialised = false
const variation = api.getVariation()

tick = () => {
    if (initialised) {
        return
    }

    if (api.getBlock(0, 0, 0) === "Unloaded") {
        // Wait for chunk to load
        return
    }


    if (variation === "default") {
        // Create platforms to matchmake players
        api.setBlockRect([0, 0, 0], [2, 0, 2], "Red Concrete") // 1v1
        api.setBlockRect([4, 0, 0], [6, 0, 2], "Blue Concrete") // 2v2
    }
    initialised = true
}

onPlayerJoin = (playerId) => {
    if (variation === "default") {
        api.setPosition(playerId, 3, 5, -3)
        api.setCameraDirection(playerId, [0, 0, 1])
    }
    else if (variation === "1v1") {
        api.setClientOption(playerId, "customVariationTitle", "Solos")
    } else if (variation === "2v2") {
        api.setClientOption(playerId, "customVariationTitle", "Duos")
    }
}

// Don't matchmake people if they've already been matchmade
/** @type {Record<PlayerId, boolean>} */
const playerHasMatchmade = {}

onBlockStandStart = (playerId, _x, _y, _z, blockName) => {
    if (variation !== "default") {
        return
    }
    if (playerHasMatchmade[playerId]) {
        return
    }

    if (blockName === "Red Concrete") {
        api.matchmakeToVariation(playerId, "1v1")
        playerHasMatchmade[playerId] = true
    } else if (blockName === "Blue Concrete") {
        api.matchmakeToVariation(playerId, "2v2")
        playerHasMatchmade[playerId] = true
    }
}
Show all 55 lines
Worlds#

Due to worlds being their own lobby, there is no possibility for variations. However, to test out custom games, you can reload lobby code as a specific variation. There are two main ways of doing this, however both require you to have at least Coder permissions or higher.

In the Code Editor, click the three dots on the right to open the More Options menu. Here, you can type in a variation and reload the lobby code to test as that variation
If your code runs api.matchmakeToVariation, it will ask you if you want to reload to that variation.
Previous
How-Tos
Next
Plugins

---

## Plugins

URL: https://bloxd.io/docs/how-to-plugins

Reusable first-party World Code features, imported from @plugins.


First-party plugins provide reusable World Code features. Import a plugin from @plugins/<name> in your entry file or another project file:

TypeScript
Copy
import { setTimeout, getRandomItem } from "@plugins/helpers"
import { debugLog } from "@plugins/debug"

Importing a plugin also loads its callbacks. Plugin callbacks run before callbacks with the same name in your own code, so both of these tick callbacks run:

TypeScript
Copy
import { setTimeout } from "@plugins/helpers"

tick = () => {
    /* Your tick code */
}

If callbacks return a value, your callback's return value takes precedence over the plugin's. Avoid replacing a useful plugin return by accident, particularly in callbacks such as onPlayerChat and onRespawnRequest.

Plugins may import other plugins. Their dependencies are loaded automatically, so importing @plugins/sessionBasedGame also loads the helpers it needs.

Available plugins#
@plugins/helpers exports setTimeout, setInterval, clearTimeout, clearInterval, forceLoadChunk, randomInt, shuffleArray, and getRandomItem.
@plugins/dialogue exports sayDialogue, which shows a player a line of dialogue for a while, and clearDialogue. See Dialogue.
@plugins/debug exports debugLog.
@plugins/sessionBasedGame provides a lobby-to-game lifecycle, teams, spectators, map loading, optional map voting, optional team choosing, and automatic game resets.

The editor's autocomplete and the read-only plugin source files are the reference for the latest exports and option types.

Previous
Variations
Next
Building a SessionBasedGame

---

## Building a SessionBasedGame

URL: https://bloxd.io/docs/how-to-building-a-session-based-game

A full team game: lobby, teams, map voting, rounds and a winner.


Use @plugins/sessionBasedGame for a team game that follows this loop:

Load a lobby and wait for players.
Optionally let players choose teams and vote for a map.
Copy the selected map into the play area and assign teams.
Run the game until one team remains or your code chooses a winner.
Show the result, reset the lobby, and start the next countdown.
World layout#

Build the lobby and each map in unused parts of the world. The plugin treats these areas as templates and copies one of them into playAreaRect.

playAreaRect is the destination where the current lobby or map is placed.
lobby.source.rect and each map.source.rect are absolute world coordinates for template builds.
Lobby spawns, map team spawns, and team-pad rectangles are offsets from the lowest corner of playAreaRect, not absolute world coordinates.
Source rectangles are rounded outwards to chunk boundaries. Keep template builds aligned to 32-block chunk boundaries so the copied area is predictable.
Every lobby and map source must fit inside playAreaRect.
At least two teams and one map are required.
Minimal setup#

Create the game once, at the top level of your entry file:

JavaScript
Copy
import { createGame } from "@plugins/sessionBasedGame"

const teams = [
    { name: "Red", maxPlayers: 4, colour: "#ff5555" },
    { name: "Blue", maxPlayers: 4, colour: "#5555ff" },
]

const game = createGame({
    teams,
    maps: [
        {
            name: "Castle",
            icon: "Stone Bricks",
            source: {
                rect: [
                    [320, 0, 0],
                    [351, 31, 31],
                ],
            },
            teams: {
                Red: {
                    spawn: [6, 2, 16],
                    spawnFacing: [1, 0, 0],
                },
                Blue: {
                    spawn: [26, 2, 16],
                    spawnFacing: [-1, 0, 0],
                },
            },
        },
    ],
    lobby: {
        source: {
            rect: [
                [256, 0, 0],
                [287, 31, 31],
            ],
        },
        spawn: [16, 2, 16],
        spawnFacing: [0, 0, 1],
    },
    playAreaRect: [
        [0, 0, 0],
        [31, 31, 31],
    ],
    emptyLobbyStartInSecs: 60,
    fullLobbyStartInSecs: 10,
    gameResetInSecs: 10,
    onStart: () => {
        game.giveColouredArmourToEveryone()
    },
})
Show all 52 lines

The plugin supplies default values for the optional settings. With the setup above, players are assigned to the smallest available team when the game starts.

Eliminating players and ending the game#

By default, players remain on their team after dying. For an elimination game, turn the victim into a spectator:

TypeScript
Copy
onPlayerKilledOtherPlayer = (_killerId, victimId) => {
    game.getPlayer(victimId).startSpectating()
}

onMobKilledPlayer = (_mobId, playerId) => {
    game.getPlayer(playerId).startSpectating()
}

startSpectating() checks whether only one team remains and finishes the game automatically. For games with another win condition, call game.makeTeamWin(team) when that condition is met.

Team choosing#

Add teamPads to the lobby to let players request a team before the game starts:

TypeScript
Copy
lobby: {
    source: {
        rect: [
            [256, 0, 0],
            [287, 31, 31],
        ],
    },
    spawn: [16, 2, 16],
    spawnFacing: [0, 0, 1],
    teamPads: {
        Red: {
            rect: [
                [4, 1, 14],
                [6, 1, 16],
            ],
            emptyBlock: "Red Concrete",
            fullBlock: "Red Ceramic",
        },
        Blue: {
            rect: [
                [25, 1, 14],
                [27, 1, 16],
            ],
            emptyBlock: "Blue Concrete",
            fullBlock: "Blue Ceramic",
        },
    },
}

Each key must exactly match a team name. The plugin changes a pad from emptyBlock to fullBlock when that team has enough requests.

Map voting#

Set mapVotingEnabled: true and provide multiple maps. Before each game, the plugin opens a shop containing up to four randomly selected maps. The icon on each map is used as its shop image.

Custom player state and behaviour#

Extend SessionBasedPlayer when each player needs additional state or customised lifecycle behaviour, then pass the class as playerConstructor. This example assumes teams, maps, lobby, and playAreaRect are top-level constants:

TypeScript
Copy
import { createGame, SessionBasedPlayer } from "@plugins/sessionBasedGame"

class GamePlayer extends SessionBasedPlayer<(typeof teams)[number], (typeof maps)[number]> {
    kills = 0

    startPlaying() {
        super.startPlaying()
        this.kills = 0
    }
}

const game = createGame({
    teams,
    maps,
    lobby,
    playAreaRect,
    playerConstructor: GamePlayer,
})

Call super.startPlaying() or super.startSpectating() when overriding those methods so the plugin still updates inventory, health, visibility, building permissions, and win detection.

Main session-based exports#
createGame(options) creates and returns the single game instance.
SessionBasedGame exposes the current gamePhase, selected map, getPlayer, getPlayers, getStartingInText, giveColouredArmourToEveryone, checkWin, and makeTeamWin.
SessionBasedPlayer exposes playerId, game, team, requestedTeam, isSpectating, startPlaying, startSpectating, onMessage, onRespawnRequest, and getPositionInPlayArea.
BaseTeamInfo, BaseMapInfo, and SessionBasedGameSetupOptions are exported TypeScript types.
Complete example: team deathmatch#

This combines team choosing, two-map voting, a custom player class, respawning equipment, personal kill counts, team scores, a round timer, sudden death, and automatic resets. Each enemy kill earns one team point. The first team to 10 points wins; after three minutes, the leading team wins. A tied round continues until a team takes the lead. Players who join mid-round spectate until the next round.

Build the templates first#

Use these absolute world coordinates, or change the corresponding rectangles in the code:

Area	Lowest block	Highest block
Play area (overwritten each round)	[0, 0, 0]	[31, 31, 31]
Lobby template	[256, 0, 0]	[287, 31, 31]
Castle template	[320, 0, 0]	[351, 31, 31]
Courtyard template	[384, 0, 0]	[415, 31, 31]

Build a floor at y = 1 in each template, with walls to keep players inside and clear space above each spawn. In the lobby, leave room for the spawn at [272, 2, 16] and the team pads at [260, 1, 14]–[262, 1, 16] and [281, 1, 14]–[283, 1, 16]. The plugin colours the pads in the copied lobby. Castle's spawns are [326, 2, 16] and [346, 2, 16]; Courtyard's are [400, 2, 6] and [400, 2, 26]. Add cover between the opposing spawns.

Enable PvP and health, disable spawn protection, and save the builds in your world. The code copies your templates; it does not build them. All spawn and pad coordinates inside the code are offsets within the copied area, which is why Castle's Red spawn is [6, 2, 16], not [326, 2, 16].

Paste the whole entry file#

Use index.js in the Code Editor. Replace the earlier examples with this entire block: it includes every constant and creates the game exactly once. Test with at least two players on opposing teams; team-pad requests are honoured, so choose different pads when testing.

JavaScript
Copy
import { createGame, SessionBasedPlayer } from "@plugins/sessionBasedGame"

/* Settings */
const SCORE_TO_WIN = 10
const ROUND_SECONDS = 180
const PLAYERS_PER_TEAM = 4

/* World layout */
/* This example's scoring and HUD are written for exactly two teams: Red and Blue. */
const teams = [
    { name: "Red", maxPlayers: PLAYERS_PER_TEAM, colour: "#ff5555" },
    { name: "Blue", maxPlayers: PLAYERS_PER_TEAM, colour: "#5555ff" },
]

const maps = [
    {
        name: "Castle",
        icon: "Stone Bricks",
        source: { rect: [[320, 0, 0], [351, 31, 31]] },
        teams: {
            Red: { spawn: [6, 2, 16], spawnFacing: [1, 0, 0] },
            Blue: { spawn: [26, 2, 16], spawnFacing: [-1, 0, 0] },
        },
    },
    {
        name: "Courtyard",
        icon: "Grass Block",
        source: { rect: [[384, 0, 0], [415, 31, 31]] },
        teams: {
            Red: { spawn: [16, 2, 6], spawnFacing: [0, 0, 1] },
            Blue: { spawn: [16, 2, 26], spawnFacing: [0, 0, -1] },
        },
    },
]

/* Round state */
const scores = { Red: 0, Blue: 0 }
let roundEndsAt = 0
let resultText = ""

class ArenaPlayer extends SessionBasedPlayer {
    kills = 0

    startPlaying() {
        super.startPlaying()
        this.kills = 0
        api.setClientOptions(this.playerId, {
            secsToRespawn: 3,
            respawnButtonText: "Respawn",
            usePlayAgainButton: false,
        })
    }

    onRespawnRequest() {
        const position = super.onRespawnRequest()
        if (this.team !== null) {
            /* Also runs at round start. Set slots so respawns cannot duplicate equipment. */
            api.setItemSlot(this.playerId, 0, "Iron Sword")
            api.setItemSlot(this.playerId, 46, `${this.team.name} Wood Helmet`)
            api.setItemSlot(this.playerId, 47, `${this.team.name} Wood Chestplate`)
            api.setItemSlot(this.playerId, 48, `${this.team.name} Wood Gauntlets`)
            api.setItemSlot(this.playerId, 49, `${this.team.name} Wood Leggings`)
            api.setItemSlot(this.playerId, 50, `${this.team.name} Wood Boots`)
        }
        return position
    }
}

const game = createGame({
    teams,
    maps,
    playerConstructor: ArenaPlayer,
    playAreaRect: [[0, 0, 0], [31, 31, 31]],
    lobby: {
        source: { rect: [[256, 0, 0], [287, 31, 31]] },
        spawn: [16, 2, 16],
        spawnFacing: [0, 0, 1],
        teamPads: {
            Red: {
                rect: [[4, 1, 14], [6, 1, 16]],
                emptyBlock: "Red Concrete",
                fullBlock: "Red Ceramic",
            },
            Blue: {
                rect: [[25, 1, 14], [27, 1, 16]],
                emptyBlock: "Blue Concrete",
                fullBlock: "Blue Ceramic",
            },
        },
    },
    mapVotingEnabled: true,
    maxSpectators: 4,
    emptyLobbyStartInSecs: 30,
    fullLobbyStartInSecs: 5,
    gameResetInSecs: 10,
    onStart: () => {
        scores.Red = 0
        scores.Blue = 0
        resultText = ""
        roundEndsAt = api.now() + ROUND_SECONDS * 1000
        api.broadcastMessage(`First team to ${SCORE_TO_WIN} kills wins!`)
        game.checkWin()
    },
    onFinish: (winningTeam) => {
        resultText = `${winningTeam.name} wins! Red ${scores.Red} - Blue ${scores.Blue}`
        api.broadcastMessage(resultText)
        /* Disable combat and clear equipment during the result screen. */
        for (const player of game.getPlayers()) {
            player.startSpectating()
        }
    },
    getRightInfoText: (player) => {
        if (game.gamePhase === "beforeGame") {
            return [
                "TEAM DEATHMATCH\nChoose a team on the coloured pads.\nVote for a map in the shop.\n",
                ...game.getStartingInText(),
            ]
        }
        if (game.gamePhase === "gameFinished") {
            return `${resultText}\nNext round soon!`
        }
        const secondsLeft = Math.max(0, Math.ceil((roundEndsAt - api.now()) / 1000))
        const clock = secondsLeft > 0 ? `${secondsLeft}s left` : "Sudden death: next team lead wins!"
        const role = player.team === null ? "Spectating until next round" : `${player.team.name} team`
        return `TEAM DEATHMATCH\n${role}\nRed ${scores.Red} - Blue ${scores.Blue}\nTarget: ${SCORE_TO_WIN}\n${clock}\nYour kills: ${player.kills}`
    },
})

function checkScoreWin() {
    if (game.gamePhase !== "inGame") {
        return
    }
    for (const team of teams) {
        const otherName = team.name === "Red" ? "Blue" : "Red"
        const reachedTarget = scores[team.name] >= SCORE_TO_WIN
        const leadsAfterTime = api.now() >= roundEndsAt && scores[team.name] > scores[otherName]
        if (reachedTarget || leadsAfterTime) {
            game.makeTeamWin(team)
            return
        }
    }
}

tick = () => {
    checkScoreWin()
}

onPlayerKilledOtherPlayer = (killerId, victimId) => {
    if (game.gamePhase === "inGame") {
        const killer = game.getPlayer(killerId)
        const victim = game.getPlayer(victimId)
        if (killer.team !== null && victim.team !== null && killer.team !== victim.team) {
            killer.kills++
            scores[killer.team.name]++
            checkScoreWin()
        }
    }
    return "keepInventory"
}

onMobKilledPlayer = () => {
    return "keepInventory"
}

onPlayerDropItem = () => {
    return "preventDrop"
}
Show all 167 lines
How the pieces connect#
Importing the plugin registers its join, leave, tick, team-pad, shop-voting, chat, and respawn callbacks. Do not call those plugin callbacks manually: your tick and kill callbacks run after theirs automatically.
startPlaying() runs once per round for each participant. It resets personal kills and calls the base implementation to restore health, team visibility, friendly-fire rules, and the spawn position. onStart resets shared scores and the deadline after players have started.
Deaths leave players on their teams, so the plugin respawns them at their map spawn. The player method onRespawnRequest() restores equipment and returns the base spawn position. Returning that position is essential; a separate global respawn callback could accidentally override it. Mob and environmental deaths do not award points.
getRightInfoText(player) builds the scoreboard for that player, including their personal kills count. The plugin refreshes this HUD once a second.
makeTeamWin changes the phase before calling onFinish, so converting everyone to spectators there cannot trigger another win. Scores remain visible during the result screen; the plugin reloads the lobby after ten seconds, then onStart clears them for the next match. The plugin also ends a round when only one team remains after disconnects.

To check the full loop, choose opposite pads, vote, score a kill, and confirm the victim respawns with a sword while the killer's team gains a point. Temporarily set SCORE_TO_WIN to 2 and ROUND_SECONDS to 15 to check a score victory, a timed victory, a tied round continuing into sudden death, and the next round starting with cleared scores. Join mid-round to check spectating.

Previous
Plugins
Next
Interactable NPCs

---

## Interactable NPCs

URL: https://bloxd.io/docs/how-to-interactable-npcs

Entities players talk to or use, such as shopkeepers and guards.


An interactable entity is one the player aims at and interacts with rather than attacks. Interacting fires onPlayerAltAction with the entity as the target, and the crosshair tells the player which key to press.

interactable makes the entity pickable on its own, so leave canAttack off unless being hit is meant to do something. Aim still lands on the entity; swinging or shooting at it does nothing.
The alt action is consumed, so a held block is not placed through the NPC and a held throwable is not spent.
interactionPrompt replaces the label beside the key. Leave it unset for the default Interact. Describe what interacting does rather than which button to press, since the engine draws the key itself.
It takes plain text or CustomTextStyling, so use a translationKey if your world is translated.
Works on mobs as well as mesh entities.
Nothing is drawn on touchscreens, where a tap needs no prompt. The interaction itself still works there.
A shopkeeper#
JavaScript
Copy
let shopkeeperId = null

tick = () => {
    if (shopkeeperId !== null) {
        return
    }

    if (api.getBlock(8, 4, 8) === "Unloaded") {
        // Wait for the chunk to load before placing the NPC
        return
    }

    shopkeeperId = api.attemptCreateMeshEntity("Person", {
        size: 1,
        pose: "standing",
        textures: { head: "trader_black" },
    }, "Blacksmith")

    if (shopkeeperId === null) {
        // The mesh entity limit was reached
        return
    }

    api.setPosition(shopkeeperId, 8, 5, 8)

    // interactable is what keeps the NPC pickable, so canAttack can stay off
    api.setTargetedPlayerSettingForEveryone(shopkeeperId, "canAttack", false)
    api.setTargetedPlayerSettingForEveryone(shopkeeperId, "interactable", true)
    api.setTargetedPlayerSettingForEveryone(shopkeeperId, "interactionPrompt", "Buy Gear")
}

onPlayerAltAction = (playerId, x, y, z, block, targetEId) => {
    if (targetEId === shopkeeperId) {
        // Toggle off, or holding the key would flicker the shop open and closed
        api.openShop(playerId, false)
    }
}
Show all 37 lines

Players now see the interact key and Buy Gear at the crosshair whenever they look at the Blacksmith, and pressing it opens the shop. Hitting the NPC does nothing at all.

Guarding a held key#

onPlayerAltAction keeps firing while the interact key is held down, roughly every 50-150ms. Reopening an already open shop does nothing, so the example above needs no guard. An interaction that grants an item, charges a currency or advances a conversation is not idempotent, and has to swallow the repeats itself:

JavaScript
Copy
const INTERACT_COOLDOWN_MS = 800
const lastInteractAt = {}

onPlayerAltAction = (playerId, x, y, z, block, targetEId) => {
    if (targetEId === questGiverId) {
        const now = api.now()
        if (now - (lastInteractAt[playerId] ?? 0) >= INTERACT_COOLDOWN_MS) {
            lastInteractAt[playerId] = now
            sayNextLine(playerId)
        }
    }
}

onPlayerLeave = (playerId) => {
    delete lastInteractAt[playerId]
}

800ms is long enough to swallow a held key and short enough that two deliberate presses still count twice. A quest giver fills in sayNextLine.

Previous
Building a SessionBasedGame
Next
Dialogue

---

## Dialogue

URL: https://bloxd.io/docs/how-to-dialogue

Lines of dialogue below the crosshair, read out a syllable at a time in a voice.


@plugins/dialogue shows a player a line of dialogue in the panel below the crosshair. The line is revealed word by word, and each syllable blips in the speaker's voice as its word appears.

JavaScript
Copy
import { sayDialogue, clearDialogue } from "@plugins/dialogue"

onPlayerJoin = (playerId) => {
    sayDialogue(playerId, "Welcome to the forge. Mind the sparks!", {
        speakerName: "Blacksmith",
        voice: "gruff",
    })
}
sayDialogue(playerId, text, opts) shows the line and hides it after opts.durationMs, 6 seconds by default, counted from when the line starts to appear. A new line replaces the one already up, and saying the same line again replays it.
clearDialogue(playerId) hides the line early.
text is plain text or a TranslatedText. [[Item Name]] in it shows that item's icon inline, e.g. "Bring me 3 [[Iron Bar]]".
speakerName is shown above the line, as plain text or CustomTextStyling, so it can carry a portrait icon.
voice is one of the presets "soft", "regular", "dark", "high-pitched", "gruff", "lively", "posh" and "mechanical", or a SpeechSynth that sets every parameter, such as its waveform, pitch and speaking rate. Leave it out for a silent line. Hear the presets and make a voice of your own in Dialogue Voices.

The plugin is built on the dialogue client option, which you can also set yourself with api.setClientOption, e.g. from a code block. A line set that way stays up until you set the option to null, and setting the same line again does not replay it. Set animateIn: false on it to show the line whole, without its reveal or voice.

A quest giver#

Create the quest giver as in A shopkeeper, keeping its ID in questGiverId, with interactionPrompt set to "Talk" and no shop. Each interaction says the next line, guarded as in Guarding a held key:

JavaScript
Copy
import { sayDialogue } from "@plugins/dialogue"

const QUEST_LINES = [
    "Ah, a new face! The mine has been quiet for days.",
    "Bring me 3 [[Iron Bar]] and I'll make it worth your while.",
    "Off you go, then!",
]
const INTERACT_COOLDOWN_MS = 800
const lastInteractAt = {}
const nextLineIndex = {}

function sayNextLine(playerId) {
    const index = nextLineIndex[playerId] ?? 0
    sayDialogue(playerId, QUEST_LINES[index], { speakerName: "Miner", voice: "lively" })
    nextLineIndex[playerId] = (index + 1) % QUEST_LINES.length
}

onPlayerAltAction = (playerId, x, y, z, block, targetEId) => {
    if (targetEId === questGiverId) {
        const now = api.now()
        if (now - (lastInteractAt[playerId] ?? 0) >= INTERACT_COOLDOWN_MS) {
            lastInteractAt[playerId] = now
            sayNextLine(playerId)
        }
    }
}

onPlayerLeave = (playerId) => {
    delete lastInteractAt[playerId]
    delete nextLineIndex[playerId]
}
Show all 31 lines

The plugin has its own onPlayerLeave, which runs before yours, so both forget the player.

Previous
Interactable NPCs
Next
Project schematics

---

## Project schematics

URL: https://bloxd.io/docs/how-to-project-schematics

Build whole chunks from schematics stored with your project.


In the Code Editor, click the + beside Schematics, enter a project path, then upload a .bloxdschem file or choose a snapshot from your profile. A project can contain up to five schematics. Open an existing schematic to rename or delete it. To replace it, delete it and add it again at the same path. Profile edits do not change an existing snapshot.

Call api.setChunkAsSchematic(schematicPath, srcCoords, destCoords) to replace one complete destination chunk, including air and block data. Both positions are block coordinates selecting their containing chunk, like copyChunk. Source coordinates use the stored chunk grid, including padding around the original selection; the Code Editor shows its dimensions.

JavaScript
Copy
// Place two neighbouring chunks, spreading the work over ticks.
let nextChunk = 0
tick = () => {
    if (nextChunk < 2) {
        api.setChunkAsSchematic("maps/arena.bloxdschem", [nextChunk * 32, 0, 0], [nextChunk * 32, 64, 0])
        nextChunk++
    }
}

The example requires an arena containing source chunks [0, 0, 0] and [32, 0, 0]. Placement uses the normal chunk-load and block-data budgets, so spread larger builds over time. Missing assets or source chunks throw an error. Placement replaces chunks without block-break drops or callbacks.

Use api.getSchematicDimensions("maps/arena.bloxdschem") to get its stored [x, y, z] dimensions, including selection padding. Like placement, this reads the active project snapshot.

The @plugins/sessionBasedGame plugin accepts source: { schematic: "maps/arena.bloxdschem" } for maps and the lobby, alongside source: { rect: [pos1, pos2] }. Dimensions are read automatically and rounded outwards to chunks when checking the play area. Spawn positions and team pads use offsets from the stored chunk grid's lowest corner. Schematics are pasted directly through the plugin's normal map-loading flow and must fit within the available placement and block-data budgets; large metadata-heavy maps need a custom loader that spreads work over ticks.

Loading an entire schematic#
JavaScript
Copy
function loadSchematic(schematicPath, destination) {
    const [width, height, depth] = api.getSchematicDimensions(schematicPath)
    const [destX, destY, destZ] = destination

    for (let x = 0; x < width; x += 32) {
        for (let y = 0; y < height; y += 32) {
            for (let z = 0; z < depth; z += 32) {
                api.setChunkAsSchematic(
                    schematicPath,
                    [x, y, z],
                    [destX + x, destY + y, destZ + z],
                )
            }
        }
    }
}

loadSchematic("maps/arena.bloxdschem", [0, 64, 0])
Previous
Dialogue
Next
API Reference

---

## API Reference

URL: https://bloxd.io/docs/api-reference

Every method on the api object, with parameters and return types.

251 methods
addCustomKillfeedMessage#
Copy call
api.addCustomKillfeedMessage(killer, victim, withItem)

Add a custom killfeed message to the killfeed

PARAMETERS
killer
{ eId: EntityId } | { name: string; colour: string }
The entity ID or a custom name and colour for the killer
victim
{ eId: EntityId } | { name: string; colour: string }
The entity ID or a custom name and colour for the victim
withItem
string
The item used
CHANGELOG
11th May 2026
addFollowingEntityToPlayer#
Copy call
api.addFollowingEntityToPlayer(playerId, eId, offset, followsPlayerRotation)

Add following entity to an entity

PARAMETERS
playerId
EntityId
eId
EntityId
offset
number[]
followsPlayerRotation
boolean
addQTE#
Copy call
api.addQTE(playerId, qteParameters)
→
QTERequestId

Create and register the UI for the requested quicktime event (QTE) to the screen.

Handle the result via the onPlayerFinishQTE engine callback.

PARAMETERS
playerId
PlayerId
qteParameters
QTEClientParameters<T>
includes type and parameters
RETURNS
QTERequestId

an id that can be passed to deleteQTE

USED IN
QTEs
addUiRequest#
Copy call
api.addUiRequest(playerId, parameters, timeoutAfterMs)
→
UiRequestId

Add a request for the player to answer in the top right corner. E.g. accepting or denying a tprequest.

Use onUiRequestResponded to handle the response.

Example Usage:

JavaScript
Copy
const myRequestId = api.addUiRequest(playerId, {
  type: "standard",
  title: "Do you want to join the game?",
}, 5000)

onUiRequestResponded = (playerId, uiRequestId, response) => {
  if (uiRequestId === myRequestId) {
    api.log(response)
  }
}
PARAMETERS
playerId
PlayerId
The ID of the player to add the request to.
parameters
UiRequestClientParameters
The parameters of the request.
timeoutAfterMs
number
The timeout after which the request will be automatically deleted. A response will not be given and onUiRequestResponded will not be called.
RETURNS
UiRequestId

The ID of the request. Pass into deleteUiRequest or cross-reference with onUiRequestResponded.

CHANGELOG
7th August 2026
addUiRequestPopup#
Copy call
api.addUiRequestPopup(playerId, requestText)
→
PNull<UiRequestId>

Add a request for the player to answer in the form of a popup. This blocks the player from doing anything else until they respond.

Use onUiRequestResponded to handle the response.

Example Usage:

JavaScript
Copy
const myRequestId = api.addUiRequestPopup(playerId, "Do you want to join the game?")

onUiRequestResponded = (playerId, uiRequestId, response) => {
  if (uiRequestId === myRequestId) {
    api.log(response)
  }
}
PARAMETERS
playerId
PlayerId
The ID of the player to add the request to.
requestText
string
The text of the request.
RETURNS
PNull<UiRequestId>

The ID of the request, or null if the request was rate limited. Pass into deleteUiRequest or cross-reference with onUiRequestResponded.

CHANGELOG
10th August 2026
animateEntity#
Copy call
api.animateEntity(entityId, animation, initialTimeFraction, animationSpeed)

Animates the given entity. Pass null for animation to stop the entity's current animation (the

initialTimeFraction and animationSpeed arguments are ignored in that case).

Pass a clip name instead (such as "animation.quadruped.head_wave", or just "head_wave") to play a clip of the texture pack's or

Bloxd's built-in animation on a mob or vehicle that has animation. It adds onto the entity's automatic animation,

as a head nod plays over a walk, or replaces the parts it moves if the clip sets override_previous_animation. It

blends back out when a one-shot clip ends or the animation is stopped; a looping or held clip plays until

stopped or replaced. An entity without animation, or a name no clip has (or several share: give the full name),

plays nothing. A name must be 1 to 128 characters long, or the call throws.

PARAMETERS
entityId
EntityId
animation
AnimationSchema | BlockbenchAnimationSchema | string | null
initialTimeFraction
number
animationSpeed
number
applyAuraChange#
Copy call
api.applyAuraChange(playerId, auraDiff)
→
number

Add (or remove if negative) aura to a player. Will not go over max level or under 0

PARAMETERS
playerId
PlayerId
auraDiff
number
RETURNS
number

The actual change in aura

applyEffect#
Copy call
api.applyEffect(lifeformId, effectName, duration, customEffectInfo)

Apply an effect to a lifeform.

Can be an inbuilt effect E.g. "Speed" (speed boost), "Damage" (damage boost).

For inbuilt just pass the name of the effect and the functionality is handled in-engine.

For custom effect, you pass customEffectInfo. The icon can be an InGameIconName or a bloxd item name.

The custom effect onEndCb is an optional helper within which you can undo the effect you applied.

Note that onEndCb will not work for press to code boards, code blocks or world code.

PARAMETERS
lifeformId
LifeformId
effectName
string
duration
number | null
customEffectInfo
{ icon?: IngameIconName | ItemName; onEndCb?: () => void; displayName?: string | TranslatedText } & Partial<InbuiltEffectInfo>
USED IN
Snippets
applyHealthChange#
Copy call
api.applyHealthChange(lifeformId, changeAmount, whoDidDamage, broadcastLifeformHurt)
→
boolean
PARAMETERS
lifeformId
LifeformId
changeAmount
number
Must be an integer. A positive amount will increase the entity's health. A negative amount will decrease the entity's shield first, then their health.
whoDidDamage
LifeformId | { lifeformId: LifeformId; withItem: string }
Optional - If damage done by another player
broadcastLifeformHurt
boolean
RETURNS
boolean
applyImpulse#
Copy call
api.applyImpulse(eId, xImpulse, yImpulse, zImpulse)

Apply an impulse to an entity

PARAMETERS
eId
EntityId
xImpulse
number
yImpulse
number
zImpulse
number
USED IN
Snippets
applyMeleeHit#
Copy call
api.applyMeleeHit(hittingEId, hitEId, dirFacing, bodyPartHit, overrides)
→
boolean

Make it as if hittingEId hit hitEId

PARAMETERS
hittingEId
LifeformId
hitEId
LifeformId
dirFacing
number[]
bodyPartHit
PNull<LifeformBodyPart>
overrides
{ damage?: PNull<number> heldItemName?: PNull<string> horizontalKbMultiplier?: number verticalKbMultiplier?: number }
RETURNS
boolean

whether the attack damaged the lifeform

attemptApplyDamage#
Copy call
api.attemptApplyDamage({ eId, hitEId, attemptedDmgAmt, withItem, bodyPartHit = undefined, attackDir = undefined, showCritParticles = false, reduceVerticalKbVelocity = true, horizontalKbMultiplier = 1, verticalKbMultiplier = 1, broadcastEntityHurt = true, attackCooldownSettings = null, hittingSoundOverride = null, ignoreOtherEntitySettingCanAttack = false, isTrueDamage = false, damagerDbId = null, damageCause = null, })
→
boolean

Apply damage to a lifeform.

eId is the player initiating the damage, hitEId is the lifeform being hit.

It is recommended to self-inflict damage when the game code wants to apply damage to a lifeform.

PARAMETERS
{ eId, hitEId, attemptedDmgAmt, withItem, bodyPartHit = undefined, attackDir = undefined, showCritParticles = false, reduceVerticalKbVelocity = true, horizontalKbMultiplier = 1, verticalKbMultiplier = 1, broadcastEntityHurt = true, attackCooldownSettings = null, hittingSoundOverride = null, ignoreOtherEntitySettingCanAttack = false, isTrueDamage = false, damagerDbId = null, damageCause = null, }
PlayerAttemptDamageOtherPlayerOpts
RETURNS
boolean

whether the attack damaged the lifeform

CHANGELOG
16th October 2026
attemptCreateAudioEntity#
Copy call
api.attemptCreateAudioEntity(x, y, z, soundName, volume, options)
→
PNull<EntityId>

Create an invisible audio entity at a world position that loops a sound to

nearby players (e.g. a waterfall or fireplace).

Audio entities count against the same budget as physics-less mesh entities; returns null

if that budget is exhausted.

PARAMETERS
x
number
y
number
z
number
soundName
string
The sound to loop.
volume
number
options
{ refDistance?: number maxHearDist?: number rate?: number }
: number, maxHearDist: number, rate: number} refDistance: higher means the sound decreases less in volume with distance. Defaults to 3. Hitting is 4. Guns are 10 maxHearDist: sound is not played if player is further than this. Defaults to 30 rate: The speed of playback. Also affects pitch. 0.5-4. Lower playback = lower pitch. Good for varying the sound. E.g. item pickup sound has a random rate between 1 and 1.5.
RETURNS
PNull<EntityId>

the audio entity ID, or null if the entity budget is exhausted

attemptCreateMeshEntity#
Copy call
api.attemptCreateMeshEntity(type, opts, name, physicsOptions, initiatorId)
→
PNull<EntityId>

Try to create a mesh entity. This creates an entity whose mesh position is synced with clients.

Set entity position using setPosition

There is a limit to the number of mesh entities and throwables that can be created, with an even smaller limit for mesh entities with physics.

PARAMETERS
type
MeshType
opts
MeshEntityOpts[MeshType]
name
string
The default name for the nametag
physicsOptions
MeshEntityPhysicsOpts
Physics Options
initiatorId
EntityId
The entity that initiated the creation of the mesh entity.
RETURNS
PNull<EntityId>

null if the entity creation failed, otherwise the entity ID.

USED IN
Interactable NPCs
Mesh Entities
CHANGELOG
24th March 2026
attemptCreateThrowable#
Copy call
api.attemptCreateThrowable(throwerEId, itemName, position, direction, velocityMult, damageMult, gravityMult, attributes)
→
string

Try to create a throwable entity.

Similar to creating a mesh entity and uses the same rate limiting.

However, this uses the predefined throwables system and physics used by throwable items with the game

Each throwable item has its own behaviour already, including default velocity, damage and gravity multipliers.

PARAMETERS
throwerEId
EntityId
itemName
ThrowableItem
Must be an Item that is usually throwable in-engine
position
[number, number, number]
Starting position
direction
[number, number, number]
velocityMult
number
Multiplier for the default velocity of the throwable item
damageMult
number
Multiplier for the default damage of the throwable item
gravityMult
number
Multiplier for the default gravity of the throwable item
attributes
ItemAttributes
item attributes (currently used only for the "Boomerag" item)
RETURNS
string

null if throwable creation failed, otherwise the entity ID.

USED IN
Mesh Entities
CHANGELOG
24th March 2026
attemptSpawnMob#
Copy call
api.attemptSpawnMob(mobType, x, y, z, opts)
→
PNull<MobId>

Try to spawn a mob into the world at a given position. Returns null on failure.

WARNING: Either the "onPlayerAttemptSpawnMob" or the "onWorldAttemptSpawnMob" game callback will be called

depending on whether "spawnerId" is provided. Calling this function inside those callbacks risks infinite recursion.

PARAMETERS
mobType
TMobType
x
number
y
number
z
number
opts
MobSpawnOpts<TMobType>
Includes: - mobHerdId The ID of this mob's herd. (A mob herd represents a collection of mobs that move together.) - spawnerId The ID of the player who tried to spawn this mob. - mobDbId A persistent ID for the mob. This can be useful when loading mob data from the database. If the DB ID is already taken, null will be returned. - name If set, gives the mob a name that will be displayed as a nametag above their head. - playSoundOnSpawn - variation - physicsOpts { width: number; height: number; collidesEntities: boolean }
RETURNS
PNull<MobId>

null if the mob could not be spawned. This can happen when there are too many mobs in the world for the current number of players in the lobby, or if the area is protected e.g. by spawn area protection.

attemptSpawnVehicle#
Copy call
api.attemptSpawnVehicle(vehicleType, x, y, z, opts)
→
PNull<EntityId>

Try to spawn a rideable vehicle, which players can mount with an alt action.

There is a limit to the number of mesh entities with physics that can be created.

WARNING: Either the "onPlayerAttemptSpawnVehicle" or the "onWorldAttemptSpawnVehicle" game callback will be called

depending on whether "spawnerId" is provided. Calling this function inside those callbacks risks infinite recursion.

PARAMETERS
vehicleType
MeshEntityVehicleType
x
number
y
number
z
number
opts
VehicleSpawnOpts
Includes: - spawnerId The ID of the player who spawned the vehicle. The vehicle faces away from them.
RETURNS
PNull<EntityId>

null if the vehicle could not be spawned, otherwise the entity ID of the vehicle.

CHANGELOG
27th August 2026
attemptWorldChangeBlock#
Copy call
api.attemptWorldChangeBlock(initiatorDbId, x, y, z, blockName, extraInfo)
→
"preventChange" | "preventDrop" | void

Initiate a block change "by the world".

Calls onWorldAttemptChangeBlock, then onWorldChangeBlock if allowed.

initiatorDbId is null if the change was initiated by the game code.

PARAMETERS
initiatorDbId
PNull<PlayerDbId>
x
number
y
number
z
number
blockName
BlockName
extraInfo
WorldBlockChangedInfo
RETURNS
"preventChange" | "preventDrop" | void

"preventChange" if the change was prevented, "preventDrop" if the change was allowed but without dropping any items, and undefined if the change was allowed with an item drop

blockCoordToChunkId#
Copy call
api.blockCoordToChunkId(pos)
→
string

Get the unique id of the chunk containing pos in the current map

PARAMETERS
pos
number[]
RETURNS
string
blockIdToBlockName#
Copy call
api.blockIdToBlockName(blockId)
→
BlockName

Goes from block id to block name. The reverse of blockNameToBlockId

PARAMETERS
blockId
BlockId
RETURNS
BlockName
blockNameToBlockId#
Copy call
api.blockNameToBlockId(blockName, allowInvalidBlock)
→
PNull<number>

Get the numeric id of a block used in the ndarrays returned from getChunk

I.e. chunk.blockData.set(x, y, z, api.blockNameToBlockId("Dirt"))

or chunk.blockData.get(x, y, z) === api.blockNameToBlockId("Dirt")

PARAMETERS
blockName
BlockName
allowInvalidBlock
boolean
Don't throw an error if the block name is invalid. Defaults false. If true and name is invalid, returns null.
RETURNS
PNull<number>
broadcastMessage#
Copy call
api.broadcastMessage(message, style)

Send a message to everyone

PARAMETERS
message
string | CustomTextStyling
The text contained within the message. Can use Custom Text Styling.
style
{ fontWeight?: number | string; color?: string; colour?: string }
An optional style argument. Can contain values for fontWeight and color of the message. style is ignored if message uses custom text styling (i.e. is not a string).
USED IN
Snippets
Building a SessionBasedGame
broadcastSound#
Copy call
api.broadcastSound(soundName, volume, rate, posSettings, exceptPlayerId)

See documentation for api.playSound

PARAMETERS
soundName
string
volume
number
rate
number
posSettings
{ playerIdOrPos: EntityId | number[] maxHearDist?: number refDistance?: number }
exceptPlayerId
PlayerId
USED IN
Sounds & Music
calcExplosionForce#
Copy call
api.calcExplosionForce(eId, explosionType, knockbackFactor, explosionRadius, explosionPos, ignoreProjectiles)
→
{ force: [number, number, number]; forceFrac: number; }
PARAMETERS
eId
EntityId
explosionType
ExplosionType
knockbackFactor
number
explosionRadius
number
explosionPos
number[]
ignoreProjectiles
boolean
RETURNS
{ force: [number, number, number]; forceFrac: number; }
canOpenStandardChest#
Copy call
api.canOpenStandardChest(playerId, chestX, chestY, chestZ)
→
PNull<boolean>

Checks if a player is able to open a chest at a given location,

as per the rules laid out by the "onPlayerAttemptOpenChest" game callback.

Returns true if the player can open the chest, false if they cannot, and void if the chest does not exist.

PARAMETERS
playerId
PlayerId
chestX
number
chestY
number
chestZ
number
RETURNS
PNull<boolean>
changePlayerIntoSkin#
Copy call
api.changePlayerIntoSkin(playerId, cosmeticType, cosmeticName)

Change a part of a player's skin.

UGC code is restricted to cosmetics from packs with ugcSelectable; internal code can use any cosmetics.

PARAMETERS
playerId
PlayerId
Player to change
cosmeticType
CosmeticType
Type of cosmetic
cosmeticName
CosmeticName
Chosen cosmetic, will be made lowercase automatically
USED IN
Snippets
Skins & Poses
checkValid#
Copy call
api.checkValid(entityId)
→
boolean

Check your game (and, optionally, a entity) is still valid and executing.

Useful if you're using async functions and await within your game.

If you use await/async or promises and do not check this, your game could have closed and then the rest of your

async code executes.

PARAMETERS
entityId
PNull<EntityId>
RETURNS
boolean
chunkIdToBotLeftCoord#
Copy call
api.chunkIdToBotLeftCoord(chunkId)
→
[number, number, number]

Get the co-ordinates of the block in the chunk with the lowest x, y, and z co-ordinates

PARAMETERS
chunkId
string
RETURNS
[number, number, number]
clearDirectionArrow#
Copy call
api.clearDirectionArrow(playerId, id)

Clear a directional arrow from the player's screen.

PARAMETERS
playerId
PlayerId
The player to clear the arrow for
id
PNull<string>
The arrow identifier to clear. If null, clears all arrows for this player.
clearInventory#
Copy call
api.clearInventory(playerId)

Clear the players inventory

PARAMETERS
playerId
PlayerId
clearKillstreak#
Copy call
api.clearKillstreak(playerId)

Clears the player's current killstreak

PARAMETERS
playerId
PlayerId
closeChestForPlayer#
Copy call
api.closeChestForPlayer(playerId)

Close a chest for a player.

If the player does not have a chest open, do nothing.

PARAMETERS
playerId
PlayerId
CHANGELOG
23rd March 2026
configureShopCategory#
Copy call
api.configureShopCategory(categoryKey, config)

Set properties of a shop category.

PARAMETERS
categoryKey
ShopCategoryKey
The key of the category to configure
config
ShopCategoryConfig
Category configuration properties
configureShopCategoryForPlayer#
Copy call
api.configureShopCategoryForPlayer(playerId, categoryKey, config)

Configure a shop category for a specific player.

PARAMETERS
playerId
PlayerId
The player to configure the category for
categoryKey
ShopCategoryKey
The key of the category to configure
config
ShopCategoryConfig
Category configuration properties
copyChunk#
Copy call
api.copyChunk(fromPos, toPos)

Copies chunk from one position to another.

A good use case for this is storing 'template' chunks that can be continuously copied to a new position.

In order to reset an area to the template, e.g. resetting a session-based game.

NOTE: Does nothing if the source chunk is not loaded.

PARAMETERS
fromPos
number[]
A block coordinate within the chunk to copy from.
toPos
number[]
A block coordinate within the chunk to copy to.
CHANGELOG
29th September 2026
7th May 2026
createEnchantmentAttributesForItem#
Copy call
api.createEnchantmentAttributesForItem(itemName, enchantmentLevel)
→
EnchantmentAttributes

Create enchantment attributes for an item at a given enchantment level. Same behaviour as if that level of enchant was selected for the item in an enchanting table.

PARAMETERS
itemName
ItemName
enchantmentLevel
number
RETURNS
EnchantmentAttributes
createItemDrop#
Copy call
api.createItemDrop(x, y, z, itemName, amount, mergeItems, attributes, timeTillDespawn, dropperId, options)
→
PNull<EntityId>

Create a dropped item.

PARAMETERS
x
number
y
number
z
number
itemName
ItemName
Name of the item. Any item name, including blocks and 'Air'
amount
PNull<number>
The amount of the item in the drop. Defaults to 1 when omitted. Use 0 for a collect-only trigger that does not add to inventory (fires onPlayerPickedUpItem with itemAmount 0).
mergeItems
boolean
Whether to merge the item into a nearby item of same type, if one exists. Defaults to false.
attributes
ItemAttributes
Attributes of the item being dropped
timeTillDespawn
number
Time till the item automatically despawns in milliseconds. Defaults to 5 mins, max of 1 hour.
dropperId
PNull<LifeformId>
Who dropped the item.
options
ItemDropOptions
Additional options, such as doPhysics and size.
RETURNS
PNull<EntityId>

the id you can pass to setCantPickUpItem, or null if the item drop limit was reached

createMobHerd#
Copy call
api.createMobHerd()
→
MobHerdId

Create a mob herd. A mob herd represents a collection of mobs that move together.

RETURNS
MobHerdId
createShopItem#
Copy call
api.createShopItem(categoryKey, itemKey, item)

Create a new shop item under the given category.

Will create a new category if it does not exist.

If the shop item already exists then it will be replaced.

If any per-player overrides exist under the same categoryKey and itemKey then they will be deleted.

PARAMETERS
categoryKey
ShopCategoryKey
The key of the category to create the item in
itemKey
ShopItemKey
The unique key for the item
item
ShopItem
The shop item to create (will be mutated)
createShopItemForPlayer#
Copy call
api.createShopItemForPlayer(playerId, categoryKey, itemKey, item)

Create a new shop item for a specific player.

Will create a new category if it does not exist.

Will replace any overrides this player already has for the same item.

PARAMETERS
playerId
PlayerId
The player to create the item for
categoryKey
ShopCategoryKey
The key of the category to create the item in
itemKey
ShopItemKey
The unique key for the item
item
ShopItem
The shop item to create (will be mutated)
deleteAllItems#
Copy call
api.deleteAllItems()

Deletes all items dropped in the world

CHANGELOG
11th May 2026
deleteAllLobbyDbValues#
Copy call
api.deleteAllLobbyDbValues()

Deletes all database values that are saved per lobby.

deleteAllPlayerDbValues#
Copy call
api.deleteAllPlayerDbValues(playerId)

Deletes all database values that are saved per player, including persisted currencies.

PARAMETERS
playerId
PlayerId
deleteAudioEntity#
Copy call
api.deleteAudioEntity(eId)

Delete an audio entity by its entity ID (returned by attemptCreateAudioEntity).

PARAMETERS
eId
EntityId
deleteCurrency#
Copy call
api.deleteCurrency(playerId, currencyId)

Delete a currency from a player. This will make the currency unknown to the player.

PARAMETERS
playerId
PlayerId
currencyId
string
CHANGELOG
11th August 2026
deleteEntity#
Copy call
api.deleteEntity(eId)
→
boolean

Delete any non-player entity (mesh entity, mob, audio entity, item drop, throwable, etc.) and dispose of their state.

PARAMETERS
eId
EntityId
RETURNS
boolean

whether the entity's replicated state existed and was deleted

deleteItemDrop#
Copy call
api.deleteItemDrop(itemId)

Delete an item drop by item drop entity ID

PARAMETERS
itemId
EntityId
deleteLobbyDbValue#
Copy call
api.deleteLobbyDbValue(key)

Deletes a database value that is saved per lobby.

PARAMETERS
key
string
deleteMeshEntity#
Copy call
api.deleteMeshEntity(eId)
→
boolean

Delete a mesh entity

PARAMETERS
eId
EntityId
RETURNS
boolean

whether the api successfully deleted the meshEntity

USED IN
Mesh Entities
CHANGELOG
24th March 2026
deletePlayerDbValue#
Copy call
api.deletePlayerDbValue(playerId, key)

Deletes a database value that is saved per player.

PARAMETERS
playerId
PlayerId
key
string
deleteQTE#
Copy call
api.deleteQTE(playerId, id)

Delete a quicktime event from the screen

PARAMETERS
playerId
PlayerId
id
QTERequestId
Returned from the addQTE request you want to cancel
USED IN
QTEs
deleteShopItem#
Copy call
api.deleteShopItem(categoryKey, itemKey)

Delete an existing shop item.

Throws an error if the item does not exist.

Will also delete all per-player overrides for the shop item.

PARAMETERS
categoryKey
ShopCategoryKey
The key of the category containing the item
itemKey
ShopItemKey
The unique key for the item
deleteThrowable#
Copy call
api.deleteThrowable(eId)
→
boolean

Delete a throwable entity before it automatically removes itself.

PARAMETERS
eId
EntityId
RETURNS
boolean

true if the entity was deleted, false if it was not a throwable entity

USED IN
Mesh Entities
CHANGELOG
24th March 2026
deleteUiRequest#
Copy call
api.deleteUiRequest(playerId, id)

Delete a request for a player.

PARAMETERS
playerId
PlayerId
id
UiRequestId
Returned from the addUiRequest call you want to cancel
CHANGELOG
7th August 2026
despawnMob#
Copy call
api.despawnMob(mobId)

Dispose of a mob's state and remove them from the world without triggering "on death" flows.

Always succeeds.

PARAMETERS
mobId
MobId
despawnVehicle#
Copy call
api.despawnVehicle(vehicleId)

Dispose of a vehicle's state and remove them from the world.

Always succeeds.

PARAMETERS
vehicleId
EntityId
editItemCraftingRecipes#
Copy call
api.editItemCraftingRecipes(playerId, itemName, recipesForItem)

Edit the crafting recipes for a player.

PARAMETERS
playerId
PlayerId
itemName
ItemName
recipesForItem
RecipesForItem
exitPlayerVehicle#
Copy call
api.exitPlayerVehicle(playerId)

Take a player off whatever they are riding, dropping them where it is. Does nothing if they are

not riding anything.

PARAMETERS
playerId
PlayerId
findItem#
Copy call
api.findItem(playerId, itemName)
→
PNull<number>

Finds the index of a particular item in a player's inventory.

PARAMETERS
playerId
PlayerId
itemName
ItemName
RETURNS
PNull<number>
CHANGELOG
11th May 2026
findStandardChestItem#
Copy call
api.findStandardChestItem(chestPos, itemName)
→
PNull<number>

Find the index of a particular item in a standard chest

PARAMETERS
chestPos
number[]
itemName
ItemName
RETURNS
PNull<number>
CHANGELOG
11th May 2026
forceRespawn#
Copy call
api.forceRespawn(playerId, respawnPos)

Force respawn a player

PARAMETERS
playerId
PlayerId
respawnPos
number[]
getAuraInfo#
Copy call
api.getAuraInfo(playerId)
→
{ level: number; totalAura: number; auraPerLevel: number }

Get the aura info for a player

PARAMETERS
playerId
PlayerId
RETURNS
{ level: number; totalAura: number; auraPerLevel: number }
getBlock#
Copy call
api.getBlock(x, y, z)
→
BlockName

Get the name of a block.

PARAMETERS
x
number | number[]
could be an array [x, y, z]. If so, the other params shouldn't be passed.
y
number
z
number
RETURNS
BlockName
USED IN
Variations
Interactable NPCs
getBlockCoordinatesPlayerStandingOn#
Copy call
api.getBlockCoordinatesPlayerStandingOn(playerId)
→
number[][]

Get the co-ordinates of the blocks the entity is standing on as a list. For example, if the centre of the entity is at 0,0,0

this function will return [[0, -1, 0], [-1, -1, 0], [0, -1, -1], [-1, -1, -1]]

If the entity is just standing on one block, the function would return e.g. [[0, 0, 0]]

If the entity is midair or has no physics body, returns an empty list [].

PARAMETERS
playerId
EntityId
RETURNS
number[][]
getBlockData#
Copy call
api.getBlockData(x, y, z)
→
any

Get stored data about a block in a performant manner. Data is cleared when block changes.

E.g. chest

Works well with blocks marked tickable (e.g. wheat)

PARAMETERS
x
number
y
number
z
number
RETURNS
any
getBlockId#
Copy call
api.getBlockId(x, y, z)
→
BlockId

Used to get the block id at a specific position.

Intended only for use in hot code paths - default to getBlock for most use cases

PARAMETERS
x
number
y
number
z
number
RETURNS
BlockId
getBlockSolidity#
Copy call
api.getBlockSolidity(x, y, z)
→
boolean

Returns whether a block is solid or not.

E.g. Grass block is solid, while water, ladder and water are not.

Will be true if the block is unloaded.

PARAMETERS
x
number | number[]
y
number
z
number
RETURNS
boolean
getBlockTypesPlayerStandingOn#
Copy call
api.getBlockTypesPlayerStandingOn(playerId)
→
any[]

Get the types of block the entity is standing on

For example, if an entity is standing on 4 dirt blocks, this will return ["Dirt", "Dirt", "Dirt", "Dirt"]

Returns an empty list if the entity is midair or has no physics body.

PARAMETERS
playerId
EntityId
RETURNS
any[]
getClientOption#
Copy call
api.getClientOption(playerId, option)
→
ClientOptions[PassedOption]

Returns the current value of a client option

PARAMETERS
playerId
PlayerId
option
PassedOption
RETURNS
ClientOptions[PassedOption]
getCraftingRecipesForPlayer#
Copy call
api.getCraftingRecipesForPlayer(playerId)
→
Record<string, RecipesForItem>

Read a player's current crafting recipe set, keyed by output item name. Includes any

per-player overrides set via editItemCraftingRecipes / removeItemCraftingRecipes.

PARAMETERS
playerId
PlayerId
RETURNS
Record<string, RecipesForItem>
getCurrencyAmount#
Copy call
api.getCurrencyAmount(playerId, currencyId)
→
PNull<number>

Get the amount of a given currency a player has.

PARAMETERS
playerId
PlayerId
currencyId
string
RETURNS
PNull<number>

The amount of the currency, or null if the currency is not defined.

CHANGELOG
11th August 2026
getCurrentKillstreak#
Copy call
api.getCurrentKillstreak(playerId)
→
number

Gets the player's current killstreak

PARAMETERS
playerId
PlayerId
RETURNS
number
getDefaultMobSetting#
Copy call
api.getDefaultMobSetting(mobType, setting)
→
MobSettings<TMobType>[TMobSetting]

Returns the current default value for a mob setting.

PARAMETERS
mobType
TMobType
setting
TMobSetting
RETURNS
MobSettings<TMobType>[TMobSetting]
getEffectLevel#
Copy call
api.getEffectLevel(lifeformId, name)
→
number

Get the level of an effect on a lifeform, or 0 if they don't have it.

PARAMETERS
lifeformId
LifeformId
name
string
RETURNS
number
CHANGELOG
11th May 2026
getEffects#
Copy call
api.getEffects(lifeformId)
→
string[]

Get all the effects currently applied to a lifeform.

PARAMETERS
lifeformId
LifeformId
RETURNS
string[]
getEmptyChunk#
Copy call
api.getEmptyChunk()
→
GameChunk

Use this to get a chunk ndarray you can edit and set in resetChunk.

Only use chunk helpers if you REALLY need the performance (i.e. you are iterating over tens of thousands of blocks)

ReturnedObject.blockData is a 32x32x32 ndarray of air.

(see https://www.npmjs.com/package/ndarray)

Each block id is a 16-bit number

RETURNS
GameChunk
getEntitiesInRect#
Copy call
api.getEntitiesInRect(minCoords, maxCoords)
→
EntityId[]

Get the entities in the rect between [minX, minY, minZ] and [maxX, maxY, maxZ]

PARAMETERS
minCoords
number[]
maxCoords
number[]
RETURNS
EntityId[]
getEntityHeading#
Copy call
api.getEntityHeading(entityId)
→
number
Deprecated: use getEntityRotation

Get the heading for a server-auth entity.

PARAMETERS
entityId
EntityId
RETURNS
number
getEntityName#
Copy call
api.getEntityName(entityId)
→
string

Get the in game name of an entity: a player's name, or "" for a mob nobody named. Use getEntityType for what kind of mob it is.

PARAMETERS
entityId
EntityId
RETURNS
string
getEntityRotation#
Copy call
api.getEntityRotation(entityId)
→
[number, number, number]

Get the rotation for a server-auth entity.

PARAMETERS
entityId
EntityId
RETURNS
[number, number, number]
getEntityType#
Copy call
api.getEntityType(entityId)
→
EntityType

What kind of entity it is: "Player", or a mob's type like "Draugr Zombie" or "Pig"

PARAMETERS
entityId
EntityId
RETURNS
EntityType
getHealth#
Copy call
api.getHealth(entityId)
→
number

Get the current health of an entity.

PARAMETERS
entityId
PlayerId
RETURNS
number
USED IN
Snippets
getHeldItem#
Copy call
api.getHeldItem(playerId)
→
PNull<InvenItem>

Get the currently held item of a player

Returns null if no item is being held

If an item is held, return an object of the format {name: itemName, amount: amountOfItem}

PARAMETERS
playerId
PlayerId
RETURNS
PNull<InvenItem>
getInitialItemMetadata#
Copy call
api.getInitialItemMetadata(itemName)
→
Partial<BlockMetadataItem & NonBlockMetadataItem>

Get the metadata about a block or item before stats have been modified by any client options

(i.e. its entry in the initial metadata object)

PARAMETERS
itemName
string
RETURNS
Partial<BlockMetadataItem & NonBlockMetadataItem>
getInventoryFreeSlotCount#
Copy call
api.getInventoryFreeSlotCount(playerId)
→
number

Get the amount of free slots in a player's inventory.

PARAMETERS
playerId
PlayerId
RETURNS
number

number

getInventoryItemAmount#
Copy call
api.getInventoryItemAmount(playerId, itemName)
→
number

The amount of an itemName a player has.

Returns 0 if the player has none, and a negative number if infinite.

PARAMETERS
playerId
PlayerId
itemName
ItemName
RETURNS
number

number

getItemAmount#
Copy call
api.getItemAmount(itemId)
→
number

Get the amount of an item in an item entity

PARAMETERS
itemId
EntityId
RETURNS
number

number

getItemDropName#
Copy call
api.getItemDropName(itemEId)
→
PNull<ItemName>

Gets the item name of a dropped item

PARAMETERS
itemEId
EntityId
The ID of the dropped item from createItemDrop
RETURNS
PNull<ItemName>
CHANGELOG
11th May 2026
getItemIDsOverlappingWithPlayer#
Copy call
api.getItemIDsOverlappingWithPlayer(playerId)
→
EntityId[]

Returns all items overlapping with the given player

PARAMETERS
playerId
PlayerId
RETURNS
EntityId[]

the overlapping item entity IDs

CHANGELOG
11th May 2026
getItemSlot#
Copy call
api.getItemSlot(playerId, itemSlotIndex)
→
PNull<InvenItem>

Get the item at a specific index

Returns null if there is no item at that index

If there is an item, return an object of the format { name: string; amount: PNull<number>; attributes: ItemAttributes; }

PARAMETERS
playerId
PlayerId
itemSlotIndex
number
RETURNS
PNull<InvenItem>
getItemStat#
Copy call
api.getItemStat(lifeformId, itemName, stat)
→
AnyMetadataItem[K]

Get stat info about a block or item

Either based on a client option for a player: (e.g. DirtTtb)

or its entry in the initial metadata object if no client option is set.

If null is passed for lifeformId, this is simply its entry in blockMetadata etc.

PARAMETERS
lifeformId
PNull<LifeformId>
itemName
ItemName
stat
K
RETURNS
AnyMetadataItem[K]
getLifeformScale#
Copy call
api.getLifeformScale(lifeformId)
→
number

Get the scale of a lifeform.

PARAMETERS
lifeformId
LifeformId
RETURNS
number
CHANGELOG
11th June 2026
getLobbyDbValue#
Copy call
api.getLobbyDbValue(key)
→
PNull<string | number>

Gets a database value that is saved per lobby.

PARAMETERS
key
string
RETURNS
PNull<string | number>
getLobbyName#
Copy call
api.getLobbyName()
→
string

Get the name of the lobby this game is running in.

RETURNS
string
getLobbyType#
Copy call
api.getLobbyType()
→
LobbyType

Returns if the current lobby the game is running in is special - e.g. a discord guild or dm, or simply a standard lobby

RETURNS
LobbyType
getMetaInfo#
Copy call
api.getMetaInfo(blockName)
→
ItemMetaInfo

Splits the block name by '|'. If no meta info, metaInfo is ''

PARAMETERS
blockName
BlockName | null | undefined
RETURNS
ItemMetaInfo
getMobAiState#
Copy call
api.getMobAiState(mobId)
→
{ state: MobAiState; params: MobAiStateParams<MobAiState> }

Gets the current AI state for the given mob.

PARAMETERS
mobId
MobId
RETURNS
{ state: MobAiState; params: MobAiStateParams<MobAiState> }
getMobDbId#
Copy call
api.getMobDbId(mobId)
→
PNull<MobDbId>

Gets the persistent database ID for the given mob.

This can be useful for reasoning about mobs that have been loaded from the database, such as owned mobs.

PARAMETERS
mobId
MobId
The ID of the mob from spawnMob
RETURNS
PNull<MobDbId>

The persistent database ID for the mob, or null if the mob is not persistent

CHANGELOG
11th May 2026
getMobIds#
Copy call
api.getMobIds()
→
MobId[]

Get the mob IDs of all mobs in the world.

RETURNS
MobId[]
getMobSetting#
Copy call
api.getMobSetting(mobId, setting, returnDefaultIfNotOverridden)
→
MobSettings<MobType>[TMobSetting]

Get the current value of a mob setting for a specific mob.

PARAMETERS
mobId
MobId
setting
TMobSetting
returnDefaultIfNotOverridden
boolean
If true, return the default setting if not overridden.
RETURNS
MobSettings<MobType>[TMobSetting]
getMoonstoneChestItems#
Copy call
api.getMoonstoneChestItems(playerId)
→
PNull<InvenItem>[]

Get all the items from a moonstone chest in order. Use this instead of repetitive calls to getMoonstoneChestItemSlot

Moonstone chests are a type of chest where a player accesses the same contents no matter the location of the moonstone chest

PARAMETERS
playerId
PlayerId
RETURNS
PNull<InvenItem>[]
getMoonstoneChestItemSlot#
Copy call
api.getMoonstoneChestItemSlot(playerId, idx)
→
PNull<InvenItem>

Get the item in a player's moonstone chest slot. Null if empty

Moonstone chests are a type of chest where a player accesses the same contents no matter the location of the moonstone chest

PARAMETERS
playerId
PlayerId
idx
number
RETURNS
PNull<InvenItem>
getNumMobs#
Copy call
api.getNumMobs()
→
number

Get the number of mobs in the world.

RETURNS
number
getNumPlayers#
Copy call
api.getNumPlayers()
→
number

Get the number of players in the room

RETURNS
number
getOtherEntitySetting#
Copy call
api.getOtherEntitySetting(relevantPlayerId, targetedEntityId, settingName)
→
OtherEntitySettings[Setting]

Get the value of a player's other-entity setting for a specific entity.

PARAMETERS
relevantPlayerId
PlayerId
targetedEntityId
EntityId
settingName
Setting
RETURNS
OtherEntitySettings[Setting]
getPlayerCosmetic#
Copy call
api.getPlayerCosmetic(playerId, cosmeticType)
→
CosmeticName

Get a single equipped cosmetic for a player.

PARAMETERS
playerId
PlayerId
cosmeticType
CosmeticType
Type of cosmetic
RETURNS
CosmeticName
getPlayerDbId#
Copy call
api.getPlayerDbId(playerId)
→
PlayerDbId

Given a player, get their permanent identifier that doesn't change when leaving and re-entering

PARAMETERS
playerId
PlayerId
RETURNS
PlayerDbId
getPlayerDbValue#
Copy call
api.getPlayerDbValue(playerId, key)
→
PNull<string | number>

Gets a database value that is saved per player.

PARAMETERS
playerId
PlayerId
key
string
RETURNS
PNull<string | number>
getPlayerFacingInfo#
Copy call
api.getPlayerFacingInfo(playerId)
→
{ camPos: [number, number, number]; dir: [number, number, number]; angleDir: AngleDir; moveHeading: number }

Get the position of a player's camera and the direction (both in Euclidean and spherical coordinates) they are attempting to use an item.

The camPos has the same limitations described in getPlayerTargetInfo

PARAMETERS
playerId
PlayerId
RETURNS
{ camPos: [number, number, number]; dir: [number, number, number]; angleDir: AngleDir; moveHeading: number }
USED IN
Mesh Entities
getPlayerGamemode#
Copy call
api.getPlayerGamemode(playerId)
→
WorldGamemode

Get the gamemode of a player.

PARAMETERS
playerId
PlayerId
The ID of the player to get the gamemode of.
RETURNS
WorldGamemode

The gamemode of the player.

CHANGELOG
18th May 2026
getPlayerId#
Copy call
api.getPlayerId(playerName)
→
PNull<PlayerId>

Given the name of a player, get their id

PARAMETERS
playerName
string
RETURNS
PNull<PlayerId>
getPlayerIdFromDbId#
Copy call
api.getPlayerIdFromDbId(dbId)
→
PNull<PlayerId>

Returns null if player not in lobby

PARAMETERS
dbId
PlayerDbId
RETURNS
PNull<PlayerId>
getPlayerIds#
Copy call
api.getPlayerIds()
→
PlayerId[]

Get all the player ids.

RETURNS
PlayerId[]
USED IN
Snippets
getPlayerPartyWhenJoined#
Copy call
api.getPlayerPartyWhenJoined(playerId)
→
PNull<{ partyCode: string; playerDbIds: PlayerDbId[] }>

Returns the party that the player was in when they joined the game. The returned object contains the playerDbIds, as well

as the playerIds if available, of the party leader and members.

PARAMETERS
playerId
PlayerId
RETURNS
PNull<{ partyCode: string; playerDbIds: PlayerDbId[] }>
getPlayerPhysicsState#
Copy call
api.getPlayerPhysicsState(playerId)
→
PlayerPhysicsState<PhysicsType>

Get physics state for player

PARAMETERS
playerId
PlayerId
RETURNS
PlayerPhysicsState<PhysicsType>
getPlayerTargetInfo#
Copy call
api.getPlayerTargetInfo(playerId)
→
{ position: [number, number, number]; normal: [number, number, number]; adjacent: [number, number, number] }

Get the position of a player's target block and the block adjacent to it (e.g. where a block would be placed)

Note: This position is a tick ahead of the client's block target info (noa.targetedBlock),

since the client updates the blocktarget before the entities tick (and since it uses the renderposition of the camera)

This normally doesn't matter but if you are client predicting something based on noa.targetedBlock

(currently only applicable to in-engine code), you should not verify using this

PARAMETERS
playerId
PlayerId
RETURNS
{ position: [number, number, number]; normal: [number, number, number]; adjacent: [number, number, number] }
getPosition#
Copy call
api.getPosition(entityId)
→
[number, number, number]

Get position of a player / entity.

PARAMETERS
entityId
EntityId
RETURNS
[number, number, number]
USED IN
Mesh Entities
getQueuedStatus#
Copy call
api.getQueuedStatus(id)
→
QueuedStatusString

Get the status of a queued command.

PARAMETERS
id
QueuedCommandId
The ID of the queued command to get the status of.
RETURNS
QueuedStatusString

NOT_IN_QUEUE, WAITING_TO_RUN, or CURRENTLY_RUNNING.

CHANGELOG
18th May 2026
getSchematicDimensions#
Copy call
api.getSchematicDimensions(schematicPath)
→
[number, number, number]

Get a project schematic's stored dimensions as [x, y, z], including selection padding.

Uses the active project snapshot. Missing schematic paths throw an error.

PARAMETERS
schematicPath
string
Project-relative path, including .bloxdschem.
RETURNS
[number, number, number]
USED IN
Project schematics
CHANGELOG
29th September 2026
getSelectedInventorySlotI#
Copy call
api.getSelectedInventorySlotI(playerId)
→
number

Get a player's currently selected inventory slot

PARAMETERS
playerId
PlayerId
RETURNS
number
getShieldAmount#
Copy call
api.getShieldAmount(entityId)
→
number

Get the current shield of an entity.

PARAMETERS
entityId
EntityId
RETURNS
number
getStandardChestFreeSlotCount#
Copy call
api.getStandardChestFreeSlotCount(chestPos)
→
PNull<number>

Get the amount of free slots in a standard chest

Returns null for non-chests

PARAMETERS
chestPos
number[]
RETURNS
PNull<number>

number

getStandardChestItemAmount#
Copy call
api.getStandardChestItemAmount(chestPos, itemName)
→
number

The amount of an itemName a standard chest has.

Returns 0 if the standard chest has none, and a negative number if infinite.

PARAMETERS
chestPos
number[]
itemName
ItemName
RETURNS
number

number

getStandardChestItems#
Copy call
api.getStandardChestItems(chestPos)
→
PNull<InvenItem>[]

Get all the items from a standard chest in order. Use this instead of repetitive calls to getStandardChestItemSlot

PARAMETERS
chestPos
number[]
RETURNS
PNull<InvenItem>[]
getStandardChestItemSlot#
Copy call
api.getStandardChestItemSlot(chestPos, idx)
→
PNull<InvenItem>

Get the item at a chest slot. Null if empty otherwise format {name: itemName, amount: amountOfItem}

PARAMETERS
chestPos
number[]
idx
number
RETURNS
PNull<InvenItem>
getUnitCoordinatesLifeformWithin#
Copy call
api.getUnitCoordinatesLifeformWithin(lifeformId)
→
number[][]

Get the up to 12 unit co-ordinates the entity is located within

(Samples the four horizontal corners at up to three vertical levels)

PARAMETERS
lifeformId
EntityId
RETURNS
number[][]

List of x, y, z positions e.g. [[-1, 0, 0], [-1, 1, 0], [-1, 2, 0]]

getVariation#
Copy call
api.getVariation()
→
string

Get the current sub-variation name.

Returns "default" when there is no named sub-variation.

RETURNS
string
USED IN
Variations
CHANGELOG
18th August 2026
getVehicleSeats#
Copy call
api.getVehicleSeats(vehicleEId)
→
VehicleSeat[]

The seat layout for a vehicle entity - at minimum one driver seat (index 0), optionally more

passenger seats after it. Resolved from the spawned vehicle's def (VehicleMeshEntityDef.seats,

falling back to a single driver seat at the physics type/tier's own riderOffset default) or a

rideable mob's override (getMobVehicleSeats, falling back to its rideHeight). Throws if

vehicleEId is not a vehicle.

PARAMETERS
vehicleEId
EntityId
RETURNS
VehicleSeat[]
getVehicleSetting#
Copy call
api.getVehicleSetting(vehicleEId, setting, returnDefaultIfNotOverridden)
→
SettableVehicleSettingValue<TSetting>

The current value of a physics setting for a specific vehicle entity: the value set via

setVehicleSetting if overridden, otherwise (when returnDefaultIfNotOverridden) the type/tier

default from the vehicle's physics state. Mirrors getMobSetting.

The one default not read from the type/tier is a mob's riderOffset, which comes from its ride height.

A per-block setting (e.g. "IceCanAutoStep") is undefined when that block is unlisted, which means

the block does not change the setting rather than that the setting is off.

PARAMETERS
vehicleEId
EntityId
setting
TSetting
returnDefaultIfNotOverridden
boolean
RETURNS
SettableVehicleSettingValue<TSetting>
getVelocity#
Copy call
api.getVelocity(eId)
→
[number, number, number]

Get the velocity of an entity

Will return [0, 0, 0] if the entity doesn't have a physics body

PARAMETERS
eId
EntityId
RETURNS
[number, number, number]
giveCurrencyAmount#
Copy call
api.giveCurrencyAmount(playerId, currencyId, amount)

Give a player an amount of currency. Can be negative to remove money.

The currency must exist for the player first, or this throws: make it with setCurrency (with an icon), e.g. in onPlayerJoin.

PARAMETERS
playerId
PlayerId
currencyId
string
amount
number
CHANGELOG
11th August 2026
giveItem#
Copy call
api.giveItem(playerId, itemName, itemAmount, attributes)
→
number

Inventory stuff

Give a player an item and a certain amount of that item.

Returns the amount of item added to the users inventory.

PARAMETERS
playerId
PlayerId
itemName
ItemName
itemAmount
number
attributes
ItemAttributes
An optional object for certain types of item. For guns this can contain the shotsLeft field which is the amount of ammo the gun currently has.
RETURNS
number
USED IN
Snippets
giveStandardChestItem#
Copy call
api.giveStandardChestItem(chestPos, itemName, itemAmount, playerId, attributes)
→
number

Give a standard chest an item and a certain amount of that item.

Returns the amount of item added to the chest.

PARAMETERS
chestPos
number[]
itemName
ItemName
itemAmount
number
playerId
PlayerId
The player who is interacting with the chest.
attributes
ItemAttributes
An optional object for certain types of item. For guns this can contain the shotsLeft field which is the amount of ammo the gun currently has.
RETURNS
number
hasActiveQTE#
Copy call
api.hasActiveQTE(playerId)
→
boolean

Check whether the player has any qteRequests

PARAMETERS
playerId
PlayerId
RETURNS
boolean
USED IN
QTEs
hasEffect#
Copy call
api.hasEffect(lifeformId, name, atOrAboveLevel)
→
boolean

Check if a lifeform has an effect.

PARAMETERS
lifeformId
LifeformId
name
string
atOrAboveLevel
number
Checks whether the effect is at or above the given level
RETURNS
boolean
CHANGELOG
11th May 2026
hasItem#
Copy call
api.hasItem(playerId, itemName)
→
boolean

Whether a player has an item

PARAMETERS
playerId
PlayerId
itemName
ItemName
RETURNS
boolean

bool

initiateMiddleScreenBar#
Copy call
api.initiateMiddleScreenBar(playerId, duration, chargeExpiresAutomatically, horizontalBarRemOffset)

This will initiate the MiddleScreenBar, starting at empty and filling up to full over the given duration.

Good to represent cooldowns (eg gun reload) or charged items (eg crossbow)

PARAMETERS
playerId
PlayerId
duration
number
ms over which the MiddleScreenBar fills up
chargeExpiresAutomatically
boolean
Defaults to true. If true, the bar will disappear upon reaching full. If false, the bar will remain at full until hidden with removeMiddleScreenBar
horizontalBarRemOffset
number
Offset the bar left or right (in css unit - rem)
inventoryIsFull#
Copy call
api.inventoryIsFull(playerId)
→
boolean

Whether the player has space in their inventory to get new blocks

PARAMETERS
playerId
PlayerId
RETURNS
boolean
isAlive#
Copy call
api.isAlive(lifeformId)
→
boolean

Whether a lifeform is alive or dead (or on the respawn screen, in a player's case).

PARAMETERS
lifeformId
LifeformId
RETURNS
boolean
isBlockInLoadedChunk#
Copy call
api.isBlockInLoadedChunk(x, y, z)
→
boolean

Check if the block at a specific position is in a loaded chunk.

PARAMETERS
x
number
y
number
z
number
RETURNS
boolean
isInsideRect#
Copy call
api.isInsideRect(coordsToCheck, pos1, pos2, addOneToMax)
→
boolean

Check if a position is within a cubic rectangle

PARAMETERS
coordsToCheck
number[]
pos1
number[]
position of one corner
pos2
number[]
position of opposite corner
addOneToMax
boolean
RETURNS
boolean
isMobile#
Copy call
api.isMobile(playerId)
→
boolean

Whether the player is on a mobile device or a computer.

PARAMETERS
playerId
PlayerId
RETURNS
boolean
isNearInterrupt#
Copy call
api.isNearInterrupt()
→
boolean

Returns true if your code is about to be interrupted for exceeding its time budget.

Use this to break up long-running code into smaller chunks.

Example:#
JavaScript
Copy
// Resume from where we stopped last time (or 0 on the first run)
let savedLoopCounter = 0

// ...

for (let i = savedLoopCounter; i < 1000; i++) {
	if (api.isNearInterrupt()) {
		// Out of time - remember our progress and stop before getting killed
		savedLoopCounter = i
		break
	}

	someExpensiveFunction()
}
RETURNS
boolean
CHANGELOG
15th May 2026
isPlayerCrouching#
Copy call
api.isPlayerCrouching(playerId)
→
boolean

Check whether a player is crouching

PARAMETERS
playerId
PlayerId
RETURNS
boolean
isPublicLobby#
Copy call
api.isPublicLobby()
→
boolean

Integer lobby names are public

RETURNS
boolean

boolean

isUsingCustomGameTexturePack#
Copy call
api.isUsingCustomGameTexturePack(playerId)
→
boolean

Whether the player joined with this custom game's texture pack applied. False if they skipped applying it

(kicking them shows the prompt again when they rejoin).

Only published custom games prompt for their pack, so anywhere else this says so and returns true.

PARAMETERS
playerId
PlayerId
RETURNS
boolean
kickPlayer#
Copy call
api.kickPlayer(playerId, reason)
PARAMETERS
playerId
PlayerId
reason
string
killLifeform#
Copy call
api.killLifeform(lifeformId, whoKilled)

Kill a lifeform, e.g. api.killLifeform(playerId).

PARAMETERS
lifeformId
LifeformId
whoKilled
LifeformId | { lifeformId: LifeformId; withItem: string }
Optional: who killed them, as a lifeform id or { lifeformId, withItem }. Leave it out (not null) when nothing killed them
matchmakePlayer#
Copy call
api.matchmakePlayer(playerId, game, lobbyName)

Tell a player to disconnect from the current lobby and join a new one.

To connect to a specific variation, format is gamename_variation.

For Custom Games, this will be classic_playerSchematic|XXXXXXXXXX or

classic_playerSchematic|XXXXXXXXXX|<varname> for a named sub-variation.

NOTE: Players won't disconnect immediately (they may play an ad before being redirected).

PARAMETERS
playerId
PlayerId
game
string
Defaults to the current game.
lobbyName
string
Defaults to "Quick Play"
CHANGELOG
23rd April 2026
matchmakeToVariation#
Copy call
api.matchmakeToVariation(playerId, varname)

Matchmake a player into a sub-variation of the current custom game.

Pass "default" for the default variation.

PARAMETERS
playerId
PlayerId
The player to matchmake
varname
string
Sub-variation name ([A-Za-z0-9_-], 1-32 chars), or "default"
USED IN
Variations
CHANGELOG
18th August 2026
now#
Copy call
api.now()
→
number

Obtain Date.now() value saved at start of current game tick

RETURNS
number
USED IN
Building a SessionBasedGame
Interactable NPCs
Dialogue
openChestForPlayer#
Copy call
api.openChestForPlayer(playerId, x, y, z)

Open a chest for a player.

If there is no chest, or the player cannot open it, do nothing.

WARNING: This may call "onPlayerAttemptOpenChest" to determine if the player has permission to open it. Using this function inside that callback risks infinite recursion.

PARAMETERS
playerId
PlayerId
x
number
y
number
z
number
CHANGELOG
23rd March 2026
openShop#
Copy call
api.openShop(playerId, toggle, forceCategoryKey, onlyIfNonEmpty)

Open the shop UI for a player

PARAMETERS
playerId
PlayerId
toggle
boolean
Whether to close the shop if it's already open. Leave this off when opening from an interaction: holding the interact button re-fires the alt action every ~50-150ms, so a toggle would flicker the shop open and closed until release.
forceCategoryKey
PNull<ShopCategoryKey>
If set, will change the shop to this category
onlyIfNonEmpty
boolean
If true, will only open the shop if the category (or shop, if no category is provided) is non-empty
USED IN
Interactable NPCs
passifyHostility#
Copy call
api.passifyHostility(mobId, targetLifeformId)

Clears any aggro the mob has towards the given lifeform.

If the mob is currently chasing or running away from it, this also transitions the mob back to idle.

PARAMETERS
mobId
MobId
targetLifeformId
LifeformId
playClientPredictedSound#
Copy call
api.playClientPredictedSound(soundName, volume, rate, posSettings, predictedBy)

See documentation for api.playSound

PARAMETERS
soundName
string
volume
number
rate
number
posSettings
{ playerIdOrPos: EntityId | number[] maxHearDist?: number refDistance?: number }
predictedBy
EntityId
playerIsInGame#
Copy call
api.playerIsInGame(playerId)
→
boolean

Whether a player is currently in the game

PARAMETERS
playerId
PlayerId
RETURNS
boolean
playerIsLoggedIn#
Copy call
api.playerIsLoggedIn(playerId)
→
boolean

Whether a player is signed in to a Bloxd account: false for guests, who are still in the game.

To check that a player is still in the game, use playerIsInGame.

PARAMETERS
playerId
PlayerId
RETURNS
boolean
playParticleEffect#
Copy call
api.playParticleEffect(opts, clientPredictedBy)

Play particle effect on all clients, or only on some clients if clientPredictedBy is specified

PARAMETERS
opts
TempParticleSystemOpts | ParticlePresetOpts
clientPredictedBy
EntityId
Play only on clients where the entity clientPredictedBy is visible and not the viewing player
USED IN
Particles
playSound#
Copy call
api.playSound(playerId, soundName, volume, rate, posSettings)
PARAMETERS
playerId
PlayerId
hears the sound
soundName
string
Can also be a prefix. If so, a random sound with that prefix will be played
volume
number
0-1. If it's too quiet and volume is 1, normalise your sound in audacity
rate
number
The speed of playback. Also affects pitch. 0.5-4. Lower playback = lower pitch Good for varying the sound. E.g. item pickup sound has a random rate between 1 and 1.5.
posSettings
{ playerIdOrPos: EntityId | number[] maxHearDist?: number refDistance?: number }
: EntityId | number[], maxHearDist: number, refDistance: number} playerIdOrPos: The entity the sound originates from, or the position of the sound maxHearDist: sound is not played if player is further than this. Default 15 refDistance: higher means the sound decreases less in volume with distance. Default 3. Hitting is 4. Guns are 10
USED IN
Snippets
Sounds & Music
preventFallDamageNextGrounding#
Copy call
api.preventFallDamageNextGrounding(playerId)

Prevents the player from taking fall damage next time they land on the ground

PARAMETERS
playerId
PlayerId
CHANGELOG
11th May 2026
progressBarUpdate#
Copy call
api.progressBarUpdate(playerId, toFraction, toDuration)

Update the progress bar in the bottom right corner.

Can be queued.

PARAMETERS
playerId
PlayerId
toFraction
number
The fraction of the progress bar you want to be filled up.
toDuration
number
The time it takes for the bar to reach the given toFraction in ms. If this is too low and you queue multiple updates, this toFraction could be skipped. Treat 200ms as a minimum.
queueCrosshairText#
Copy call
api.queueCrosshairText(playerId, text, duration)
→
QueuedCommandId

Schedule text to be displayed in the crosshair.

This text will be removed after the duration.

Stacking queued texts will schedule them to be displayed one after the other.

NOTE: Overriding the crosshairText client option may cause queued texts to be displayed incorrectly.

PARAMETERS
playerId
PlayerId
The ID of the player to display the text to.
text
string | CustomTextStyling
The text to display.
duration
number
The duration of the text in milliseconds.
RETURNS
QueuedCommandId

The ID of the queued command.

CHANGELOG
18th May 2026
queueMiddleTextLower#
Copy call
api.queueMiddleTextLower(playerId, text, duration)
→
QueuedCommandId

Schedule small text to be displayed in the middle of the screen (middleTextLower).

This text will be removed after the duration.

Stacking queued texts will schedule them to be displayed one after the other.

NOTE: Overriding the middleTextLower client option may cause queued texts to be displayed incorrectly.

PARAMETERS
playerId
PlayerId
The ID of the player to display the text to.
text
string | CustomTextStyling
The text to display.
duration
number
The duration of the text in milliseconds.
RETURNS
QueuedCommandId

The ID of the queued command.

CHANGELOG
18th May 2026
queueMiddleTextUpper#
Copy call
api.queueMiddleTextUpper(playerId, text, duration)
→
QueuedCommandId

Schedule large text to be displayed in the middle of the screen (middleTextUpper).

This text will be removed after the duration.

Stacking queued texts will schedule them to be displayed one after the other.

NOTE: Overriding the middleTextUpper client option may cause queued texts to be displayed incorrectly.

PARAMETERS
playerId
PlayerId
The ID of the player to display the text to.
text
string | CustomTextStyling
The text to display.
duration
number
The duration of the text in milliseconds.
RETURNS
QueuedCommandId

The ID of the queued command.

CHANGELOG
18th May 2026
raycastForBlock#
Copy call
api.raycastForBlock(fromPos, dirVec)
→
BlockRaycastResult

Raycast for a block in the world.

Given a position and a direction, find the first block that the "ray" hits.

PARAMETERS
fromPos
number[]
dirVec
number[]
RETURNS
BlockRaycastResult
registerAnalyticsEvent#
Copy call
api.registerAnalyticsEvent(playerId, eventType, eventValue, gameCategoryId, gameStartTimeMs, position, numericValue)

Register an event for analytics. Custom games only: anywhere else, World Code gets an error.

Special value is eventType "match" and eventValue "match_started" to mark the start of a match when calculating average quantities

Each player can send 20 events a minute. Each day a game can have 20 game categories, 20 event types in each and

50 event values for each type; once it goes past one, events at that level are dropped until midnight UTC

PARAMETERS
playerId
string
The player associated with the event
eventType
string
The type of event e.g. "shop" or "death", at most 64 characters
eventValue
string | null
The detail of the event e.g. the item bought or cause of death, at most 128 characters
gameCategoryId
string | null
The game category id e.g. the map you're playing on or the variant of the game to filter by or compare, at most 128 characters
gameStartTimeMs
number
The time the game or match started in milliseconds since 1970, within the last 30 days - use to get event times relative to the start of the game. Each event also records the player's lifetime playtime
position
PNull<[number, number, number]>
Where the event happened, e.g. where the player died or the block they broke, shown on Studio's heatmap. In the same frame of reference as the game's registerAnalyticsPlayerPosition positions for this category. Without one, no position is recorded
numericValue
PNull<number>
A number the event measures, e.g. the coins earned, the round's score or the seconds it took.
registerAnalyticsPlayerPosition#
Copy call
api.registerAnalyticsPlayerPosition(playerId, gameCategoryId, gameStartTimeMs, position)

Record where a player is for the analytics heatmap. Call it at a regular interval (e.g. once a second).

Custom games only: anywhere else, World Code gets an error.

Each player can send 120 positions a minute. Each day a game can send 100,000 different blocks (event positions

included); once it goes past that, positions are dropped until midnight UTC

PARAMETERS
playerId
string
The player whose position to record
gameCategoryId
string | null
The game category id e.g. the map you're playing on or the variant of the game to filter by, at most 128 characters
gameStartTimeMs
number
The time the game or match started in milliseconds since 1970, within the last 30 days - used to get a playback of positions
position
PNull<[number, number, number]>
The position of the player to record. Defaults to the player's global position.
removeAppliedSkin#
Copy call
api.removeAppliedSkin(playerId)

Remove gamemode-applied skin from a player

PARAMETERS
playerId
PlayerId
removeEffect#
Copy call
api.removeEffect(lifeformId, name)

Remove an effect from a lifeform.

PARAMETERS
lifeformId
LifeformId
name
string
removeFollowingEntityFromPlayer#
Copy call
api.removeFollowingEntityFromPlayer(playerId, entityEId)

Remove following entity from an entity

PARAMETERS
playerId
EntityId
entityEId
EntityId
removeFromQueue#
Copy call
api.removeFromQueue(id)

Remove a queued command from the queue.

PARAMETERS
id
QueuedCommandId
The ID of the queued command to remove.
CHANGELOG
18th May 2026
removeItemCraftingRecipes#
Copy call
api.removeItemCraftingRecipes(playerId, itemName)

Removes crafting recipes

PARAMETERS
playerId
PlayerId
itemName
PNull<string>
Removes all crafting recipes for the given player if null, otherwise removes the crafting recipes for the given item.
removeItemName#
Copy call
api.removeItemName(playerId, itemName, amount)

Remove an amount of item from a player's inventory

PARAMETERS
playerId
PlayerId
itemName
ItemName
amount
number
removeItemNameFromStandardChest#
Copy call
api.removeItemNameFromStandardChest(chestPos, itemName, amount, playerId)

Remove an amount of item from a standardChest inventory

PARAMETERS
chestPos
number[]
itemName
ItemName
amount
number
playerId
PlayerId
The player who is interacting with the chest.
CHANGELOG
11th May 2026
removeMiddleScreenBar#
Copy call
api.removeMiddleScreenBar(playerId)

If there is any current middle screen bar running, this will hide it

PARAMETERS
playerId
PlayerId
resetCanChangeBlock#
Copy call
api.resetCanChangeBlock(playerId, x, y, z)

Remove any previous can/cant change block settings for a player at a specific co-ordinate

PARAMETERS
playerId
PlayerId
x
number
y
number
z
number
CHANGELOG
11th May 2026
resetCanChangeBlockRect#
Copy call
api.resetCanChangeBlockRect(playerId, pos1, pos2)

Remove any previous can/cant change block rect settings for a player

PARAMETERS
playerId
PlayerId
pos1
number[]
pos2
number[]
resetCanChangeBlockType#
Copy call
api.resetCanChangeBlockType(playerId, blockName)

Remove any previous can/cant change block type settings for a player

PARAMETERS
playerId
PlayerId
blockName
BlockName
resetCanPickUpItem#
Copy call
api.resetCanPickUpItem(playerId, itemId)

Reset a player's ability to pick up an item. itemId returned by createItemDrop

PARAMETERS
playerId
PlayerId
itemId
EntityId
CHANGELOG
11th May 2026
resetItemCraftingRecipes#
Copy call
api.resetItemCraftingRecipes(playerId, itemName)

Reset the crafting recipes for a given back to its original bloxd state

PARAMETERS
playerId
PlayerId
itemName
PNull<string>
Resets all crafting recipes for the given player if null, otherwise resets the crafting recipes for the given item.
resetShopItemForPlayer#
Copy call
api.resetShopItemForPlayer(playerId, categoryKey, itemKey)

Delete a specific player's overrides for a shop item.

Like other methods, it doesn't matter whether the overrides were created

using createShopItemForPlayer or by using updateShopItemForPlayer instead.

This method does nothing if the overrides don't exist or are defined internally by the engine.

PARAMETERS
playerId
PlayerId
The player to reset the item for
categoryKey
ShopCategoryKey
The key of the category containing the item
itemKey
ShopItemKey
The unique key for the item
scalePlayerMeshNodes#
Copy call
api.scalePlayerMeshNodes(playerId, nodeScales)

Set an entity's meshScaling setting by 3d vector. Model node scaling is applied to lifeforms;

for mesh entities, this setting affects nametag placement and interaction reach, not the model's nodes.

State from prior calls to this api is lost so if you want to have multiple nodes scaled, pass in all the scales at once.

PARAMETERS
playerId
EntityId
nodeScales
EntityMeshScalingMap
sendFlyingMiddleMessage#
Copy call
api.sendFlyingMiddleMessage(playerId, message, distanceFromAction, lifetimeMs)

Send a flying middle message to a specific player

PARAMETERS
playerId
PlayerId
Id of the player
message
string | CustomTextStyling
The text contained within the message. Can be either a string or use Custom Text Styling.
distanceFromAction
number
The distance from the action that has caused this message to be displayed, this value will be used to determine how the message flies across the screen.
lifetimeMs
number
How long the message will be visible in milliseconds. Defaults to 1000ms.
USED IN
Snippets
sendHitmarker#
Copy call
api.sendHitmarker(playerId, isCrit, directionVector)

Show a hitmarker on the player's screen (the X-shaped crosshair flash indicating a successful hit).

Useful for custom weapons or things that need visual hit feedback.

PARAMETERS
playerId
PlayerId
The player to show the hitmarker to
isCrit
boolean
If true, shows an enhanced critical-hit hitmarker with a longer, more dramatic animation
directionVector
PNull<number[]>
Optional [x, y, z] direction vector. When provided, the hitmarker appears at the projected screen position of that direction rather than at the centre of the screen. Same flow as mobile melee attacks where the tap point differs from screen centre.
sendMessage#
Copy call
api.sendMessage(playerId, message, style)

Send a message to a specific player

PARAMETERS
playerId
PlayerId
Id of the player
message
string | CustomTextStyling
The text contained within the message. Can use Custom Text Styling.
style
{ fontWeight?: number | string; color?: string }
An optional style argument. Can contain values for fontWeight and color of the message. style is ignored if message uses custom text styling (i.e. is not a string).
USED IN
Snippets
Icons
sendOverShopInfo#
Copy call
api.sendOverShopInfo(playerId, info)

Show a message over the shop in the same place that a shop item's onBoughtMessage is shown.

Displays for a couple seconds before disappearing

Use case is to show a dynamic message when player buys an item

PARAMETERS
playerId
PlayerId
info
string | CustomTextStyling
sendTopRightHelper#
Copy call
api.sendTopRightHelper(playerId, icon, text, opts)
Deprecated: prefer using other UI elements (this UI element hasn't been properly thought through in combination with other elements like killfeed, uirequests, etc)

Send a player an icon in the top right corner

PARAMETERS
playerId
PlayerId
icon
string
Can be any icon from font-awesome.
text
string
The text to send.
opts
{ duration?: number width?: number height?: number color?: string iconSizeMult?: number textAndIconColor?: string fontSize?: string }
Can include keys duration, width, height, color, iconSizeMult. Default opts: { duration: 8, // seconds width: 400px, height: 100px, color: 'rgb(102, 102, 102)', // must be rgb in this format (hex not supported), iconSizeMult: 5, textAndIconColor: "white", // can be any colour supported by css (e.g. hex, rgb), fontSize: '17px', }
setAuraLevel#
Copy call
api.setAuraLevel(playerId, level)

Set the aura level for a player - shortcut for setTotalAura(level * auraPerLevel)

PARAMETERS
playerId
PlayerId
level
number
setBlock#
Copy call
api.setBlock(x, y, z, blockName)

Set a block. Valid names are any block name, including 'Air'

This function is optimised for setting broad swathes of blocks. For example, if you have a 50x50x50 area you need to turn to air, it will run performantly if you call this in double nested loops.

IF you're only changing a few blocks, you want this to be super snappy for players, AND you're calling this outside of your _tick function, you can use api.setOptimisations(false).

If you want the optimisations for large quantities of blocks later on, then call api.setOptimisations(true) when you're done.

PARAMETERS
x
number | number[]
Can be an array
y
number | BlockName
Should be blockname if first param is array
z
number
blockName
BlockName
USED IN
Snippets
setBlockData#
Copy call
api.setBlockData(x, y, z, data)

Store data about a block in a performant manner. Data is cleared when block changes.

E.g. chest

Works well with blocks marked tickable (e.g. wheat)

PARAMETERS
x
number
y
number
z
number
data
object
setBlockRect#
Copy call
api.setBlockRect(pos1, pos2, blockName)

Helper function that sets all blocks in a rectangle to a specific block.

PARAMETERS
pos1
number[]
array [x, y, z]
pos2
number[]
array [x, y, z]
blockName
BlockName
USED IN
Variations
setBlockWalls#
Copy call
api.setBlockWalls(pos1, pos2, blockName, hasFloor, hasCeiling)

Create walls by providing two opposite corners of the cuboid

PARAMETERS
pos1
number[]
array [x, y, z]
pos2
number[]
array [x, y, z]
blockName
BlockName
hasFloor
boolean
hasCeiling
boolean
setCallbackValueFallback#
Copy call
api.setCallbackValueFallback(cbName, value)

Set a default value to be returned by your callback code if it throws an error.

PARAMETERS
cbName
UserCallbacks
The name of the callback to set the default value for.
value
any
The default value to return.
setCameraDirection#
Copy call
api.setCameraDirection(playerId, direction)

Set the direction the player is looking.

PARAMETERS
playerId
PlayerId
direction
number[]
a vector of the direction to look, format [x, y, z]
USED IN
Variations
setCameraZoom#
Copy call
api.setCameraZoom(playerId, zoom)

Set camera zoom for a player

PARAMETERS
playerId
PlayerId
zoom
number
setCanChangeBlock#
Copy call
api.setCanChangeBlock(playerId, x, y, z)

Let a player change a block at a specific co-ordinate. Useful when client option canChange is false.

Overrides blockRect and blockType settings, so also useful when you have disallowed changing of a block type with setCantChangeBlockType.

Using this on 1000s of blocks will cause lag - if that is needed, find a way to use setCanChangeBlockType.

PARAMETERS
playerId
PlayerId
x
number
y
number
z
number
setCanChangeBlockRect#
Copy call
api.setCanChangeBlockRect(playerId, pos1, pos2)

Make it so a player can Change blocks within two points. Coordinates are inclusive. E.g. if [0, 0, 0] is pos1

and [1, 1, 1] is pos2 then the 8 blocks contained within low and high will be able to be broken.

Overrides setCantChangeBlockType

PARAMETERS
playerId
PlayerId
pos1
number[]
Arg as [x, y, z]
pos2
number[]
Arg as [x, y, z]
setCanChangeBlockType#
Copy call
api.setCanChangeBlockType(playerId, blockName)

Lets a player Change a block type. Valid names are any block name, including 'Air'

Less priority than cant change block pos/can change block rect

PARAMETERS
playerId
PlayerId
blockName
BlockName
setCantChangeBlock#
Copy call
api.setCantChangeBlock(playerId, x, y, z)

Prevents a player from changing a block at a specific co-ordinate. Useful when client option canChange is true.

Overrides blockRect and blockType settings, so also useful when you have allowed changing of a block type with setCantChangeBlockType.

Using this on 1000s of blocks will cause lag - if that is needed, find a way to use setCantChangeBlockType.

PARAMETERS
playerId
PlayerId
x
number
y
number
z
number
setCantChangeBlockRect#
Copy call
api.setCantChangeBlockRect(playerId, pos1, pos2)

Make it so a player cant Change blocks within two points. Coordinates are inclusive. E.g. if [0, 0, 0] is pos1

and [1, 1, 1] is pos2 then the 8 blocks contained within pos1 and pos2 won't be able to be broken.

Overrides setCanChangeBlockType

PARAMETERS
playerId
PlayerId
pos1
number[]
Arg as [x, y, z]
pos2
number[]
Arg as [x, y, z]
setCantChangeBlockType#
Copy call
api.setCantChangeBlockType(playerId, blockName)

Stops a player from changing a block type. Valid names are any block name, including 'Air'

Less priority than can change block pos/can change block rect

PARAMETERS
playerId
PlayerId
blockName
BlockName
setCantPickUpItem#
Copy call
api.setCantPickUpItem(playerId, itemId)

Prevent a player from picking up an item. itemId returned by createItemDrop

PARAMETERS
playerId
PlayerId
itemId
EntityId
setChunkAsSchematic#
Copy call
api.setChunkAsSchematic(schematicPath, srcCoords, destCoords)

Replace a world chunk with a chunk from a project schematic, including air and block data.

Both positions are block coordinates selecting their containing 32-block chunk.

Add schematics in the Code Editor. Missing paths or source chunks throw an error.

PARAMETERS
schematicPath
string
Project-relative path, including .bloxdschem.
srcCoords
[number, number, number]
Block coordinates in the schematic's chunk grid (including selection padding).
destCoords
[number, number, number]
Block coordinates in the world. Existing blocks are replaced without break drops.
USED IN
Project schematics
CHANGELOG
29th September 2026
setClientOption#
Copy call
api.setClientOption(playerId, option, value)

Modify a client option at runtime and send to the client if it changed

PARAMETERS
playerId
PlayerId
option
PassedOption
The name of the option
value
ClientOptions[PassedOption]
The new value of the option
USED IN
Snippets
Variations
Dialogue Voices
Sounds & Music
CHANGELOG
22nd October 2026
setClientOptions#
Copy call
api.setClientOptions(playerId, optionsObj)

Modify client options at runtime

PARAMETERS
playerId
PlayerId
optionsObj
Partial<ClientOptions>
An object which contains key value pairs of new settings. E.g {canChange: true, speedMultiplier: false}
USED IN
Building a SessionBasedGame
setClientOptionToDefault#
Copy call
api.setClientOptionToDefault(playerId, option)

Sets a client option to its default value. This will be the value stored in your game's defaultClientOptions, otherwise Bloxd's default.

PARAMETERS
playerId
PlayerId
option
ClientOption
setCurrency#
Copy call
api.setCurrency(playerId, currencyId, info)

Dynamically define a currency for a player and show it on the HUD.

Amounts will persist between sessions if persistent is set to true.

Persistent currencies count towards db length limits.

Example usage:

JavaScript
Copy
api.setCurrency(myId, "myCurrency", { amount: 100, icon: "coins", iconColour: "blue", persistent: true })
PARAMETERS
playerId
PlayerId
currencyId
string
info
UgcCurrencyInfo
{ amount, icon } are required (icon is an icon name such as "coins"); iconColour, persistent, hidden and subtext are optional
CHANGELOG
11th August 2026
setCurrencyAmount#
Copy call
api.setCurrencyAmount(playerId, currencyId, amount, subtext)

Set the amount of a currency a player has. For persistent currencies, amount/subtext count towards db length limits.

PARAMETERS
playerId
PlayerId
currencyId
string
amount
number
subtext
string | CustomTextStyling
CHANGELOG
11th August 2026
setDefaultMobSetting#
Copy call
api.setDefaultMobSetting(mobType, setting, value)

Set the default value for a mob setting.

PARAMETERS
mobType
TMobType
setting
TMobSetting
value
MobSettings<TMobType>[TMobSetting]
setDirectionArrow#
Copy call
api.setDirectionArrow(playerId, id, position, text, showDistance, style)

Show a directional arrow indicator on the player's screen pointing toward a world position.

When the position is off-screen the indicator is a rotating chevron at the screen edge.

When the position is on-screen it becomes a small marker dot.

The arrow persists until explicitly cleared via clearDirectionArrow.

Calling again with the same id updates the existing arrow in-place.

PARAMETERS
playerId
PlayerId
The player to show the arrow to
id
string
Unique identifier for this arrow (allows multiple concurrent arrows)
position
number[]
[x, y, z] world position the arrow should point toward
text
PNull<string | CustomTextStyling>
Optional label rendered below the indicator. Supports CustomTextStyling for rich text with icons/colours.
showDistance
boolean
If true, displays the distance (in blocks) from the player to the arrow position.
style
PNull<TextStyle>
Optional style object (same format as CustomTextStyling's StyledText style). Controls chevron/marker colour, label typography, and opacity.
setEntityHeading#
Copy call
api.setEntityHeading(entityId, newHeading)
Deprecated: use setEntityRotation

Set the heading for a server-auth entity.

PARAMETERS
entityId
EntityId
newHeading
number
setEntityRotation#
Copy call
api.setEntityRotation(entityId, xRotation, yRotation, zRotation)

Set the rotation for a server-auth entity.

A mob or player-shaped entity turns its head first; set the lockHeadToBody entity setting to turn its whole body.

PARAMETERS
entityId
EntityId
xRotation
number
yRotation
number
zRotation
number
CHANGELOG
26th October 2026
setEveryoneSettingForPlayer#
Copy call
api.setEveryoneSettingForPlayer(playerId, settingName, settingValue, includeNewJoiners)

Set a player's other-entity setting for every player, mob and Person mesh in the game.

includeNewJoiners=true means that the player will have the setting applied to new joiners.

PARAMETERS
playerId
PlayerId
settingName
Setting
settingValue
OtherEntitySettings[Setting]
includeNewJoiners
boolean
setHealth#
Copy call
api.setHealth(entityId, newHealth, whoDidDamage, increaseMaxHealthIfNeeded)
→
boolean

Set the current health of an entity.

If you want to set their health to more than their current max health, the optional increaseMaxHealthIfNeeded must be true.

PARAMETERS
entityId
EntityId
newHealth
PNull<number>
Can be null to make the player not have health
whoDidDamage
LifeformId | { lifeformId: LifeformId; withItem: string }
Optional
increaseMaxHealthIfNeeded
boolean
Optional
RETURNS
boolean
USED IN
Snippets
setItemAmount#
Copy call
api.setItemAmount(itemId, newAmount)

Set the amount of an item in an item entity

PARAMETERS
itemId
EntityId
newAmount
number
setItemSlot#
Copy call
api.setItemSlot(playerId, itemSlotIndex, itemName, itemAmount, attributes, tellClient)

Put an item in a specific index. Default hotbar is indexes 0-9

PARAMETERS
playerId
PlayerId
itemSlotIndex
number
0-indexed
itemName
ItemName
Can be 'Air', in which case itemAmount will be ignored and the slot will be cleared.
itemAmount
PNull<number>
-1 for infinity. Should not be set, or null, for items that are not stackable.
attributes
ItemAttributes
An optional object for certain types of item. For guns this can contain the shotsLeft field which is the amount of ammo the gun currently has. customAttributes.bar = { fraction, colour? } (0 to 1, hex colour) draws a charge bar on the item's slot. A stack shares one bar, so make barred items unstackable.
tellClient
boolean
whether to tell client about it - results in desync between client and server if client doesnt locally perform the same action
USED IN
Building a SessionBasedGame
setItemStat#
Copy call
api.setItemStat(playerId, itemName, stat, value)

Set a stat attribute for a block or item

NOTE: Only a subset of stats are customisable this way.

afterEatenItem requires an unstackable food.

minChargeStateToUse must be within the item's chargeStages and set on the base item, applying to all its charging variants.

fishingRodInfo adjusts existing rods; drops names the replacement mining drop.

Example: setItemStat(playerId, "Iron Dagger", "comboInfo", { comboWindowMs: 1000, comboMultipliers: [1, 1.5, 2] })

PARAMETERS
playerId
PlayerId
itemName
ItemName
stat
K
value
AnyMetadataItem[K]
CHANGELOG
16th April 2026
setLifeformScale#
Copy call
api.setLifeformScale(lifeformId, scale)

Set the visual + physical scale of a lifeform. A scale of 1 is the default size,

PARAMETERS
lifeformId
LifeformId
scale
number
Must be a finite positive number.
CHANGELOG
11th June 2026
setLobbyDbValue#
Copy call
api.setLobbyDbValue(key, value)

Sets a database value that is saved per lobby. This persists between sessions.

PARAMETERS
key
string
value
string | number
setMaxPlayers#
Copy call
api.setMaxPlayers(softMaxPlayers, maxPlayers)

Update the max players and soft max players matchmaking will use

softMaxPlayers is the number of players that matchmaking will route to using "Quick Play".

Once the softMaxPlayers limit is reached, this lobby can only be joined by requesting the lobby name or joining a friend.

maxPlayers is the absolute maximum: a lobby will not have more players than this.

Tip: softMaxPlayers should be around 90% of maxPlayers

WARNING: This change is not immediate, as it takes a while for matchmaking to find out.

Also, this will not kick players out of the lobby if set to a lower value than the current player count.

PARAMETERS
softMaxPlayers
number
maxPlayers
number
setMobAiState#
Copy call
api.setMobAiState(mobId, state, params, opts)

Sets the current AI state for the given mob.

Some AI states will require context such as the ID of the lifeform being chased.

The mob's AI normally moves on by itself after a few seconds, or when a player comes near.

Pass { hold: true } to keep it in this state until you set another one.

PARAMETERS
mobId
MobId
state
TState
params
MobAiStateParams<TState>
opts
MobAiStateOptions
hold: never time out, ignore nearby players and don't fight back when hit. The mob still leaves the state if its target leaves the game or turns invisible, or if it is tamed.
CHANGELOG
26th October 2026
setMobSetting#
Copy call
api.setMobSetting(mobId, setting, value)

Set the current value of a mob setting for a specific mob.

PARAMETERS
mobId
MobId
setting
TMobSetting
value
MobSettings<MobType>[TMobSetting]
setMoonstoneChestItemSlot#
Copy call
api.setMoonstoneChestItemSlot(playerId, idx, itemName, itemAmount, metadata)

Moonstone chests are a type of chest where a player accesses the same contents no matter the location of the moonstone chest

PARAMETERS
playerId
PlayerId
idx
number
0-indexed
itemName
ItemName
Can be 'Air', in which case itemAmount will be ignored and the slot will be cleared.
itemAmount
number
-1 for infinity. Should not be set, or null, for items that are not stackable.
metadata
ItemAttributes
An optional object for certain types of item. For guns this can contain the shotsLeft field which is the amount of ammo the gun currently has.
setOtherEntitySetting#
Copy call
api.setOtherEntitySetting(relevantPlayerId, targetedEntityId, settingName, settingValue)

Set a player's other-entity setting for a specific entity.

PARAMETERS
relevantPlayerId
PlayerId
targetedEntityId
EntityId
settingName
Setting
settingValue
OtherEntitySettings[Setting]
setOtherEntitySettings#
Copy call
api.setOtherEntitySettings(relevantPlayerId, targetedEntityId, settingsObject)

Set many of a player's other-entity settings for a specific entity.

PARAMETERS
relevantPlayerId
PlayerId
targetedEntityId
EntityId
settingsObject
Partial<OtherEntitySettings>
setOtherEntitySettingToDefault#
Copy call
api.setOtherEntitySettingToDefault(relevantPlayerId, targetedEntityId, settingName)

Reset a player's other-entity setting for a specific entity to the game's default value.

PARAMETERS
relevantPlayerId
PlayerId
targetedEntityId
EntityId
settingName
Setting
CHANGELOG
11th May 2026
setPlayerDbValue#
Copy call
api.setPlayerDbValue(playerId, key, value)

Sets a database value that is saved per player. For custom games this persists between sessions and

between lobbies, and is shared across all of the game's variations (e.g. a hub and its sub-modes).

PARAMETERS
playerId
PlayerId
key
string
value
string | number
setPlayerGamemode#
Copy call
api.setPlayerGamemode(playerId, gamemode)

Set the gamemode of a player. This is persistent across lobbies for custom games.

PARAMETERS
playerId
PlayerId
The ID of the player to set the gamemode of.
gamemode
WorldGamemode
The gamemode to set the player to.
CHANGELOG
18th May 2026
setPlayerOpacity#
Copy call
api.setPlayerOpacity(playerId, opacity)

Set an entity's opacity

A simple helper that calls setTargetedPlayerSettingForEveryone

PARAMETERS
playerId
EntityId
opacity
number
setPlayerOpacityForOnePlayer#
Copy call
api.setPlayerOpacityForOnePlayer(playerIdWhoViewsOpacityPlayer, playerIdOfOpacityPlayer, opacity)

Set the opacity of an entity for one player

A simple helper that calls setOtherEntitySetting

PARAMETERS
playerIdWhoViewsOpacityPlayer
PlayerId
The player who sees that with opacity
playerIdOfOpacityPlayer
EntityId
The entity whose opacity is changed
opacity
number
setPlayerPhysicsState#
Copy call
api.setPlayerPhysicsState(playerId, physicsState, positionOffset)

Set physics state of player (vehicle type and tier).

For types that have tiers (e.g. BOAT, GLIDER, CAR), a tier of null defaults to the first

tier (0). Types without tiers (e.g. DEFAULT) must be given a null tier.

PARAMETERS
playerId
PlayerId
physicsState
PlayerPhysicsState<PhysicsType>
positionOffset
[number, number, number]
Optional offset to adjust the player's collision box
setPlayerPose#
Copy call
api.setPlayerPose(playerId, pose, poseOffset)

Set the pose of the player

PARAMETERS
playerId
PlayerId
pose
PlayerPose
poseOffset
[number, number, number]
USED IN
Snippets
Skins & Poses
setPlayerVehicle#
Copy call
api.setPlayerVehicle(playerId, vehicleEId, seatIndex)

Seat a player in a vehicle. Seat 0 drives; other seats follow the vehicle without movement control.

The player leaves their current vehicle and replaces anyone occupying the requested seat.

PARAMETERS
playerId
PlayerId
vehicleEId
EntityId
A spawned vehicle or a rideable mob.
seatIndex
number
Seat index (default 0).
setPosition#
Copy call
api.setPosition(entityId, x, y, z)

Set position of a player / entity.

PARAMETERS
entityId
EntityId
x
number | number[]
Can also be an array, in which case y and z shouldn't be passed
y
number
z
number
USED IN
Snippets
Variations
Interactable NPCs
Mesh Entities
setSelectedInventorySlotI#
Copy call
api.setSelectedInventorySlotI(playerId, newI)

Force the player to have the ith inventory slot selected. E.g. newI 0 makes the player have the 0th inventory slot selected

PARAMETERS
playerId
PlayerId
newI
number
integer from 0-9
setShieldAmount#
Copy call
api.setShieldAmount(lifeformId, newShieldAmount)

Set the current shield of a lifeform.

PARAMETERS
lifeformId
LifeformId
newShieldAmount
number
setStandardChestItemSlot#
Copy call
api.setStandardChestItemSlot(chestPos, idx, itemName, itemAmount, playerId, attributes)
PARAMETERS
chestPos
number[]
idx
number
0-indexed
itemName
ItemName
Can be 'Air', in which case itemAmount will be ignored and the slot will be cleared.
itemAmount
number
-1 for infinity. Should not be set, or null, for items that are not stackable.
playerId
PlayerId
The player who is interacting with the chest.
attributes
ItemAttributes
An optional object for certain types of item. For guns this can contain the shotsLeft field which is the amount of ammo the gun currently has.
setTargetedPlayerSettingForEveryone#
Copy call
api.setTargetedPlayerSettingForEveryone(targetedPlayerId, settingName, settingValue, includeNewJoiners)

Set every player's other-entity setting to a specific value for a particular entity.

includeNewJoiners=true means that new players joining the game will also have this other player setting applied.

PARAMETERS
targetedPlayerId
EntityId
settingName
Setting
settingValue
OtherEntitySettings[Setting]
includeNewJoiners
boolean
USED IN
Interactable NPCs
CHANGELOG
26th October 2026
10th September 2026
setTotalAura#
Copy call
api.setTotalAura(playerId, totalAura)

Sets the total aura for a player. Will not go over max level or under 0

PARAMETERS
playerId
PlayerId
totalAura
number
setVehicleSetting#
Copy call
api.setVehicleSetting(vehicleEId, setting, value)

Override a physics setting for a specific vehicle entity, replacing the type/tier default for that

vehicle's rider. The override is stored on the shared Bloxd and, when the vehicle currently has a

rider, replicated to that rider's client. Mirrors setMobSetting.

A setting can also be overridden for one block by naming the block first, e.g.

setVehicleSetting(boatId, "IceCanAutoStep", true). That is stored as an entry of the matching

<setting>ByBlock record, which the physics tick reads as a precomputed block lookup.

PARAMETERS
vehicleEId
EntityId
setting
TSetting
value
SettableVehicleSettingValue<TSetting>
setVelocity#
Copy call
api.setVelocity(eId, x, y, z)

Set the velocity of an entity

PARAMETERS
eId
EntityId
x
number
y
number
z
number
USED IN
Snippets
setWalkThroughRect#
Copy call
api.setWalkThroughRect(playerId, pos1, pos2, updateType)

Allow a player to walk through (or not walk through) voxels that are located within a given rectangle.

For blocks that are normally solid and not seethrough, the player will experience slight visual glitches while inside the block.

You could set both pos1 and pos2 to [0, 0, 0] to make only 0, 0, 0 walkthrough, for example.

A player standing inside a voxel that turns solid for them is lifted onto it if there is room above, including onto a CANT_WALK_THROUGH rect.

To let them stay where they are, remove the block before removing its exemption.

PARAMETERS
playerId
PlayerId
pos1
number[]
The one corner of the cuboid. Format [x, y, z]
pos2
number[]
The top right corner of the cuboid. Format [x, y, z]
updateType
WalkThroughType
The type of update. Whether to make a rect solid, or able to be walked through. Pass DEFAULT_WALK_THROUGH with a previously passed rect to disable any walkthrough setting for that rect.
setWalkThroughType#
Copy call
api.setWalkThroughType(playerId, blockName, disable)

Allow a player to walk through a type of block. For blocks that are normally solid and not seethrough, the player will experience slight visual glitches while inside the block.

A player standing inside a block that turns solid for them is lifted onto it if there is room above. To let them stay where they are, remove the block before making its type solid again.

PARAMETERS
playerId
PlayerId
blockName
BlockName
disable
boolean
If you've enabled a player to walk through a block and want to make the block solid for them again, pass this with true. Otherwise you only need to pass playerId and blockName
shakePlayerCamera#
Copy call
api.shakePlayerCamera(playerId, intensity, durationMs)

Shake a player's camera.

PARAMETERS
playerId
PlayerId
intensity
number
Shake "power" (0..1); the client clamps the accumulated power to 1.
durationMs
number
How long the shake lasts, in milliseconds.
showShopTutorial#
Copy call
api.showShopTutorial(playerId)

Show the shop tutorial for a player. Will not be shown if they have ever seen the shop tutorial in your game before.

PARAMETERS
playerId
PlayerId
updateAudioEntity#
Copy call
api.updateAudioEntity(eId, opts)

Update an audio entity's config (sound, volume, falloff, rate). Only the provided fields

change.

PARAMETERS
eId
EntityId
opts
Partial<AudioEntityOpts>
Any subset of soundName, volume, refDistance, maxHearDist, rate.
updateEntityNodeMeshAttachment#
Copy call
api.updateEntityNodeMeshAttachment(eId, node, type, opts, offset, rotation)

Attach/detach mesh instances to/from an entity

PARAMETERS
eId
EntityId
node
EntityNamedNode
node to attach to
type
PNull<MeshType>
if null, detaches mesh from this node
opts
MeshEntityOpts[MeshType]
offset
[number, number, number]
rotation
[number, number, number]
USED IN
Mesh Entities
updateMeshEntity#
Copy call
api.updateMeshEntity(eId, type, opts)

Update a mesh entity. If used on a non-mesh entity, will do nothing.

PARAMETERS
eId
EntityId
type
MeshType
opts
MeshEntityOpts[MeshType]
USED IN
Mesh Entities
CHANGELOG
24th March 2026
updateMeshParticleSystems#
Copy call
api.updateMeshParticleSystems(updates)

Updates the particle systems of multiple mesh entities at specified nodes

PARAMETERS
updates
MeshParticleSystemUpdates
CHANGELOG
11th May 2026
updateShopItem#
Copy call
api.updateShopItem(categoryKey, itemKey, changes)

Update selected properties of an existing shop item.

For example, { canBuy: true } to allow players to purchase the item.

Throws an error if the item does not exist.

PARAMETERS
categoryKey
ShopCategoryKey
The key of the category containing the item
itemKey
ShopItemKey
The unique key for the item
changes
Partial<ShopItem>
Partial shop item properties to update
updateShopItemForPlayer#
Copy call
api.updateShopItemForPlayer(playerId, categoryKey, itemKey, changes)

Update selected properties of an existing shop item for a specific player.

For example, { canBuy: true } to allow this player to purchase the item.

Throws an error if the item does not exist.

PARAMETERS
playerId
PlayerId
The player to update the item for
categoryKey
ShopCategoryKey
The key of the category containing the item
itemKey
ShopItemKey
The unique key for the item
changes
Partial<ShopItem>
Partial shop item properties to update
Previous
Project schematics
Next
Callbacks

---

## Callbacks

URL: https://bloxd.io/docs/callbacks

Functions your world code defines to react to game events.

84 callbacks

Players can use World Code in custom worlds get functions they've written to run when game events happen. These special functions are called callbacks. The world code can be viewed by pressing F8 by default. Initially the world code will have this comment, which can be removed:

Text
Copy
tick onClose onPlayerJoin onPlayerLeave onPlayerJump onRespawnRequest
playerCommand onPlayerChat onPlayerAttemptChangeBlock onPlayerChangeBlock
onPlayerDropItem onPlayerPickedUpItem onPlayerSelectInventorySlot
onBlockStand onBlockStandStart onBlockStandStop onPlayerAttemptCraft
onPlayerCraft onPlayerAttemptOpenChest onPlayerOpenedChest
onPlayerMoveItemOutOfInventory onPlayerMoveInvenItem onPlayerMoveItemIntoIdxs
onPlayerSwapInvenSlots onPlayerMoveInvenItemWithAmt onPlayerAttemptAltAction
onPlayerAltAction onPlayerClick onPlayerClickUp onClientOptionUpdated
onMobSettingUpdated onInventoryUpdated onChestUpdated
onWorldAttemptChangeBlock onWorldChangeBlock onCreateBloxdMeshEntity
onEntityCollision onPlayerAttemptSpawnMob onWorldAttemptSpawnMob
onPlayerSpawnMob onWorldSpawnMob onWorldAttemptDespawnMob onMobDespawned
onPlayerAttemptSpawnVehicle onWorldAttemptSpawnVehicle onPlayerSpawnVehicle
onWorldSpawnVehicle onVehicleDespawned onEntityDeleted onPlayerAttack
onPlayerDamagingOtherPlayer onPlayerDamagingMob onMobDamagingPlayer
onMobDamagingOtherMob onAttemptKillPlayer onPlayerKilledOtherPlayer
onMobKilledPlayer onPlayerKilledMob onMobKilledOtherMob onPlayerPotionEffect
onPlayerDamagingMeshEntity onPlayerBreakMeshEntity onPlayerUsedThrowable
onPlayerThrowableHitTerrain onTouchscreenActionButton onTaskClaimed
onChunkLoaded onPlayerRequestChunk onItemDropCreated
onPlayerStartChargingItem onPlayerFinishChargingItem onPlayerAttemptFish
onPlayerSucceededFishCatch onPlayerFailedFishCatch onPlayerFinishQTE
onPlayerToggledShopMenu onPlayerPlayedEmote onPlayerEnteredVehicle
onPlayerExitedVehicle onPlayerBoughtShopItem onPlayerPressedButton
onPlayerReleasedButton onUiRequestResponded doPeriodicSave

To use a callback, just assign a function to it in the world code!
tick = () => {}			 or			 function tick() {}

You can use api.setCallbackValueFallback("callbackName", defaultValue) to set a default value to be returned by your callback code if it throws an error.

doPeriodicSave#
Copy handler
doPeriodicSave = () => void

Called every so often.

You should save custom db values/s3 objects here.

Persisted items ARE saved on graceful shutdown (e.g. uncaught error, update, etc),

but this helps prevent large data-loss on non-graceful shutdowns.

onAttemptKillPlayer#
Copy handler
onAttemptKillPlayer = (killedPlayer, attackingLifeform) =>
void | "preventDeath"

Called when a player is about to be killed

Return "preventDeath" to prevent the player from being killed

PARAMETERS
killedPlayer
PlayerId
The id of the player being killed
attackingLifeform
LifeformId
The optional id of the lifeform attacking the player
RETURNS
void | "preventDeath"
onBlockStand#
Copy handler
onBlockStand = (playerId, x, y, z, blockName) => void

Called when a player stands on a block

PARAMETERS
playerId
PlayerId
The id of the player that stood on the block
x
number
The x coordinate of the block that was stood on
y
number
The y coordinate of the block that was stood on
z
number
The z coordinate of the block that was stood on
blockName
BlockName
The name of the block that was stood on
CHANGELOG
11th June 2026
onBlockStandStart#
Copy handler
onBlockStandStart = (playerId, x, y, z, blockName) => void

Called when a player enters a block. Only called once per block until the player leaves the block.

PARAMETERS
playerId
PlayerId
The id of the player that entered the block
x
number
The x coordinate of the block that was entered
y
number
The y coordinate of the block that was entered
z
number
The z coordinate of the block that was entered
blockName
BlockName
The name of the block that was entered
USED IN
Variations
CHANGELOG
11th June 2026
onBlockStandStop#
Copy handler
onBlockStandStop = (playerId, x, y, z, blockName) => void

Called when a player leaves a block. Stepping from one block onto another calls onBlockStandStart for the new block first and onBlockStandStop for the old one after it, so check blockName (or x, y, z) before undoing what onBlockStandStart did, or stepping onto the block you care about cancels it at once.

PARAMETERS
playerId
PlayerId
The id of the player that left the block
x
number
The x coordinate of the block that was left
y
number
The y coordinate of the block that was left
z
number
The z coordinate of the block that was left
blockName
BlockName
The name of the block that was left
CHANGELOG
11th June 2026
onChestUpdated#
Copy handler
onChestUpdated = (initiatorEId, isMoonstoneChest, x, y, z) => void

Called when a chest is updated by a player

x, y, z, will be null if isMoonstoneChest is true

PARAMETERS
initiatorEId
PlayerId
The id of the player who updated the chest
isMoonstoneChest
boolean
Whether the chest is a moonstone chest
x
number | null
The x coordinate of the chest
y
number | null
The y coordinate of the chest
z
number | null
The z coordinate of the chest
onChunkLoaded#
Copy handler
onChunkLoaded = (chunkId, chunk, wasPersistedChunk) => void

Called when a chunk is first loaded

API Methods that modify the chunk like setBlock cannot be used here to make

persisted changes, and will introduce client-server desync most cases,

but might have some creative uses if you know what you're doing.

For most use cases, consider using another callback e.g. tick.

PARAMETERS
chunkId
string
The id of the chunk being loaded
chunk
LoadedChunk
The chunk being loaded, which can be modified by this callback * For world code callbacks this value will always be null.
wasPersistedChunk
boolean
Whether the chunk was persisted
onClientOptionUpdated#
Copy handler
onClientOptionUpdated = (playerId, option, value) => void

Called when a client option is updated

PARAMETERS
playerId
PlayerId
The id of the player whose option was updated
option
ClientOption
The option that was updated
value
any
The new value of the option, always null for custom code
onClose#
Copy handler
onClose = (serverIsShuttingDown) => void

Called when the lobby is shutting down

PARAMETERS
serverIsShuttingDown
boolean
Whether the server is shutting down
onCreateBloxdMeshEntity#
Copy handler
onCreateBloxdMeshEntity = (eId, type, initiatorId) => void

Called when a mesh entity is created

PARAMETERS
eId
EntityId
The id of the mesh entity
type
string
The type of mesh entity
initiatorId
EntityId | null
The id of the entity that created the mesh entity, if any
onEntityCollision#
Copy handler
onEntityCollision = (eId, otherEId) => void

Called when a entity collides with another entity

PARAMETERS
eId
EntityId
The id of the entity
otherEId
EntityId
The id of the other entity
onEntityDeleted#
Copy handler
onEntityDeleted = (eId, entityType) => void

Called when any non-player entity is deleted, after any type specific callback such as "onMobDespawned".

Not called when an item drop is picked up or expires, or when a throwable expires or hits something.

PARAMETERS
eId
EntityId
The id of the entity deleted
entityType
EntityType
What the entity was: for a mob, its mob type (e.g. "Draugr Zombie"), never "mob"; "Item" for an item drop
CHANGELOG
28th August 2026
onInventoryUpdated#
Copy handler
onInventoryUpdated = (playerId) => void

Called when a player's inventory is updated

PARAMETERS
playerId
PlayerId
The id of the player whose inventory was updated
onItemDropCreated#
Copy handler
onItemDropCreated = (itemEId, itemName, itemAmount, x, y, z) => void

Called when an item drop is created

PARAMETERS
itemEId
EntityId
The id of the item drop
itemName
string
The name of the item dropped
itemAmount
number
The amount dropped
x
number
The x coordinate of the item drop
y
number
The y coordinate of the item drop
z
number
The z coordinate of the item drop
onMobDamagingOtherMob#
Copy handler
onMobDamagingOtherMob = (attackingMob, damagedMob, damageDealt, withItem, damageInfo) =>
number | void | "preventDamage"

Called when a mob is damaging another mob

Return "preventDamage" to prevent damage

Return number to change damage dealt to that amount

PARAMETERS
attackingMob
MobId
the id of the mob attacking
damagedMob
MobId
the id of the mob being damaged
damageDealt
number
the amount of damage dealt
withItem
string
the item used to attack
damageInfo
DamageInfo
what dealt the hit: a melee swing, an explosion, a projectile, etc.
RETURNS
number | void | "preventDamage"
CHANGELOG
16th October 2026
onMobDamagingPlayer#
Copy handler
onMobDamagingPlayer = (attackingMob, damagedPlayer, damageDealt, withItem, damageInfo) =>
number | void | "preventDamage"

Called when a mob is damaging a player

Return "preventDamage" to prevent damage

Return number to change damage dealt to that amount

PARAMETERS
attackingMob
MobId
the id of the mob damaging the player
damagedPlayer
PlayerId
the id of the player being damaged
damageDealt
number
the amount of damage dealt
withItem
string
the item used to attack
damageInfo
DamageInfo
what dealt the hit: a melee swing, an explosion, a projectile, etc.
RETURNS
number | void | "preventDamage"
CHANGELOG
16th October 2026
onMobDespawned#
Copy handler
onMobDespawned = (mobId) => void

Called when a mob is gone for any reason: killed, despawned by the world, or removed by code. Use it to know when mobs you spawned are dead.

PARAMETERS
mobId
MobId
The id of the mob despawned
onMobKilledOtherMob#
Copy handler
onMobKilledOtherMob = (attackingMob, killedMob, damageDealt, withItem) =>
void | "preventDrop"

Called when a mob kills another mob

Return "preventDrop" to prevent the mob from dropping items

PARAMETERS
attackingMob
MobId
The id of the mob attacking
killedMob
MobId
The id of the mob killed
damageDealt
number
The amount of damage dealt
withItem
string
The item used to attack
RETURNS
void | "preventDrop"
onMobKilledPlayer#
Copy handler
onMobKilledPlayer = (attackingMob, killedPlayer, damageDealt, withItem) =>
void | "keepInventory"

Called when a mob kills a player

Return "keepInventory" to not drop the player's inventory

PARAMETERS
attackingMob
any
The id of the mob attacking
killedPlayer
any
The id of the player killed
damageDealt
any
The amount of damage dealt
withItem
any
The item used to attack
RETURNS
void | "keepInventory"
USED IN
Building a SessionBasedGame
onMobSettingUpdated#
Copy handler
onMobSettingUpdated = (mobId, setting, value) => void

Called when a mob setting is updated

PARAMETERS
mobId
MobId
The id of the mob whose setting was updated
setting
MobSetting
The setting that was updated
value
any
The new value of the setting
onPlayerAltAction#
Copy handler
onPlayerAltAction = (playerId, x, y, z, block, targetEId) => void

Called when player completes an alt action. Right click, the interact bind (E by default) and a mobile tap all arrive here; a left click does not, so this is the callback to use for anything a player should have to choose to do rather than trigger by swinging.

Keeps firing while the input is held, roughly every 50-150ms. That is harmless for anything idempotent, but an interaction that grants an item, charges a currency or advances a conversation has to swallow the repeats itself - open shops with toggle off, and debounce the rest per player.

The co-ordinates will be undefined if there is no targeted block (and block will be "Air")

PARAMETERS
playerId
PlayerId
The id of the player completing the alt action
x
number
The x coordinate of the targeted block
y
number
The y coordinate of the targeted block
z
number
The z coordinate of the targeted block
block
BlockName
The name of the targeted block
targetEId
EntityId | null
The id of the targeted entity
USED IN
Interactable NPCs
Dialogue
CHANGELOG
30th September 2026
10th September 2026
onPlayerAttack#
Copy handler
onPlayerAttack = (playerId) => void

Called when a player attacks another player

PARAMETERS
playerId
string
The id of the player attacking
onPlayerAttemptAltAction#
Copy handler
onPlayerAttemptAltAction = (playerId, x, y, z, block, targetEId) =>
void | "preventAction"

Called when player alt actions (right click on pc).

The co-ordinates will be undefined if there is no targeted block (and block will be "Air")

Some actions can be prevented by returning "preventAction",

but this may not work as well for certain actions which the game client predicts to succeed -

test it to see if it works for your use case, feel free to report any broken ones.

PARAMETERS
playerId
PlayerId
The id of the player attempting the alt action
x
number
The x coordinate of the targeted block
y
number
The y coordinate of the targeted block
z
number
The z coordinate of the targeted block
block
BlockName
The name of the targeted block
targetEId
EntityId | null
The id of the targeted entity
RETURNS
void | "preventAction"
onPlayerAttemptChangeBlock#
Copy handler
onPlayerAttemptChangeBlock = (playerId, x, y, z, fromBlock, toBlock, droppedItem, fromBlockInfo, toBlockInfo) =>
void | "preventChange"

Called before a player changes a block.

Return "preventChange" to stop it. Then onPlayerChangeBlock will not run.

Growing EZ placements validate at request time and again at completion; keep validation free of rewards or charges.

When placing, fromBlock is Air, or the slab a matching slab completes. When breaking, toBlock is Air.

PARAMETERS
playerId
PlayerId
The player trying to change the block
x
number
The block's x coordinate
y
number
The block's y coordinate
z
number
The block's z coordinate
fromBlock
BlockName
The current block
toBlock
BlockName
The proposed block
droppedItem
BlockName | null
The item that would drop
fromBlockInfo
MultiBlockInfo
The current multiblock info
toBlockInfo
MultiBlockInfo
The proposed multiblock info
RETURNS
void | "preventChange"
onPlayerAttemptCraft#
Copy handler
onPlayerAttemptCraft = (playerId, itemName, craftingIdx, craftTimes) =>
void | "preventCraft"

Called when a player attempts to craft an item

Return "preventCraft" to prevent a craft from happening

PARAMETERS
playerId
PlayerId
The id of the player that is attempting to craft the item
itemName
string
The name of the item that is being crafted
craftingIdx
number
The index of the used recipe in the item's recipe list
craftTimes
number
The number of times the craft recipe is used at once (e.g. shift held while crafting)
RETURNS
void | "preventCraft"
onPlayerAttemptFish#
Copy handler
onPlayerAttemptFish = (playerId, rodName, x, y, z) =>
void | FishingAttemptOptions | "preventFish"

Called once when a fishing hook first enters water. Coordinates are the bob's position at water entry.

Return "preventFish" to cancel, or { caughtItemName?, biteDelayMs?, qte? } to select the fish and override the rod's bite delay

and nine-second timed-click QTE. Default delays are Rusty 7–9 seconds, Sturdy 5–7, and Carbon/other rods 2–4.

The selected fish is fixed for the attempt; omitting caughtItemName uses the engine's default fish selection.

PARAMETERS
playerId
PlayerId
rodName
string
x
number
y
number
z
number
RETURNS
void | FishingAttemptOptions | "preventFish"
onPlayerAttemptOpenChest#
Copy handler
onPlayerAttemptOpenChest = (playerId, x, y, z, isMoonstoneChest, isIronChest) =>
void | "preventOpen"

Called when a player attempts to open a chest

Return "preventOpen" to prevent the player from opening the chest

PARAMETERS
playerId
PlayerId
The id of the player that is attempting to open the chest
x
number
The x coordinate of the chest that the player is attempting to open
y
number
The y coordinate of the chest that the player is attempting to open
z
number
The z coordinate of the chest that the player is attempting to open
isMoonstoneChest
boolean
Whether the chest is a moonstone chest
isIronChest
boolean
Whether the chest is an iron chest
RETURNS
void | "preventOpen"
onPlayerAttemptSpawnMob#
Copy handler
onPlayerAttemptSpawnMob = (playerId, mobType, x, y, z) =>
void | "preventSpawn"

Called when a player attempts to spawn a mob, e.g. using a spawn orb.

Return "preventSpawn" to prevent the mob from spawning.

PARAMETERS
playerId
PlayerId
The id of the player
mobType
MobType
The type of mob
x
number
The potential x coordinate of the mob
y
number
The potential y coordinate of the mob
z
number
The potential z coordinate of the mob
RETURNS
void | "preventSpawn"
onPlayerAttemptSpawnVehicle#
Copy handler
onPlayerAttemptSpawnVehicle = (playerId, vehicleType, x, y, z) =>
void | "preventSpawn"

Called when a vehicle is spawned on a player's behalf.

Return "preventSpawn" to prevent the vehicle from spawning.

PARAMETERS
playerId
PlayerId
The id of the player
vehicleType
MeshEntityVehicleType
The type of vehicle
x
number
The potential x coordinate of the vehicle
y
number
The potential y coordinate of the vehicle
z
number
The potential z coordinate of the vehicle
RETURNS
void | "preventSpawn"
CHANGELOG
28th August 2026
onPlayerBoughtShopItem#
Copy handler
onPlayerBoughtShopItem = (playerId, categoryKey, itemKey, item, userInput) => void

Called after a player successfully buys a shop item

PARAMETERS
playerId
PlayerId
The id of the player that bought the item
categoryKey
ShopCategoryKey
The shop category key
itemKey
ShopItemKey
The shop item key
item
BoughtShopItem
The resolved shop item (with per-player overrides applied, internal properties stripped)
userInput
string
The user input provided, if the item has a userInput config
onPlayerBreakMeshEntity#
Copy handler
onPlayerBreakMeshEntity = (playerId, entityId) => void

Called when a player breaks a mesh entity

PARAMETERS
playerId
PlayerId
The id of the player breaking the mesh entity
entityId
EntityId
The id of the mesh entity being broken
onPlayerChangeBlock#
Copy handler
onPlayerChangeBlock = (playerId, x, y, z, fromBlock, toBlock, droppedItem, fromBlockInfo, toBlockInfo, dropsPrevented) =>
void | "preventChange" | "preventDrop" | [number, number, number]

In World Code, called once after all attempt callbacks allow a player block change, before the block is set.

The current block and its data are still available. Return "preventChange" to cancel the request.

Return "preventDrop" to stop the engine item drop, or [x, y, z] to set its position.

Drop returns do not skip built-in validation or change notifications; any "preventDrop" takes precedence over a position.

A block written here with api.setBlock is preserved, with normal drops/inventory charges unless the request is cancelled.

Cancellation does not undo your own script effects. Built-in change effects run after this callback.

For growing EZ placements this runs at request time only; completion validates again without repeating this callback.

Writing the target yourself completes that EZ request immediately, without delayed growth or a growth refund.

Native games/plugins receive uninterrupted before-commit notifications and must veto in onPlayerAttemptChangeBlock.

When placing, fromBlock is Air, or the slab a matching slab completes. When breaking, toBlock is Air.

PARAMETERS
playerId
PlayerId
The id of the player that changed the block
x
number
The x coordinate of the block that was changed
y
number
The y coordinate of the block that was changed
z
number
The z coordinate of the block that was changed
fromBlock
BlockName
The old block that was replaced
toBlock
BlockName
The new block that was placed
droppedItem
BlockName | null
The item that was dropped
fromBlockInfo
MultiBlockInfo
The info of the old block that was replaced
toBlockInfo
MultiBlockInfo
The info of the new block that was placed
dropsPrevented
boolean
Whether earlier notifications prevented drops; false during World Code validation
RETURNS
void | "preventChange" | "preventDrop" | [number, number, number]
onPlayerChat#
Copy handler
onPlayerChat = (playerId, chatMessage, channelName) =>
boolean | void | ChatTags | OnPlayerChatObjectResponse

Called when a player sends a chat message

Return false or null to prevent the broadcast of the message.

Return a string or CustomTextStyling to add a prefix to message.

Return for most flexibility: an object where keys are playerIds -

the value for a playerId being false means that player won't receive the message. Every player needs a key: one left out doesn't receive it either, so give the players who should see it {} (or a prefixContent).

Otherwise playerId values should be an object with (optional) keys

prefixContent and chatContent to modify the prefix and the chat.

CustomTextStyling[] prefixContent is expected, e.g. [["prefix"]] or [[{ str: "prefix" }]]. A colour goes inside style: [[{ str: "[Red]", style: { color: "red" } }]]; any other key makes the whole return value invalid, and the message goes to everyone.

World code is not permitted to specify chatContent, it will be ignored.

A message world code sends while handling the chat that ends with the player's name and then their message, e.g. "Bob: hi", counts as their chat: players who ignore them don't get it, and others can report it.

PARAMETERS
playerId
PlayerId
The id of the player that sent the message
chatMessage
string
The message that the player sent
channelName
string
The name of the channel that the message was sent in
RETURNS
boolean | void | ChatTags | OnPlayerChatObjectResponse
onPlayerClick#
Copy handler
onPlayerClick = (playerId, wasAltClick, x, y, z, block, targetEId) => void

Called when a player clicks

Don't have important functionality depending on wasAltClick,

as it'll always be false for touchscreen players.

PARAMETERS
playerId
PlayerId
The id of the player clicking
wasAltClick
boolean
Whether the click was an alt click (e.g. right click
x
number
y
number
z
number
block
BlockName
targetEId
EntityId | null
onPlayerClickUp#
Copy handler
onPlayerClickUp = (playerId, wasAltClick, x, y, z, block, targetEId) => void

Called when a player releases a click (mouse-up on desktop, touch-end on mobile).

Fires for both primary and secondary click releases.

Keep in mind wasAltClick will always be false for touchscreen players.

PARAMETERS
playerId
PlayerId
The id of the player releasing click
wasAltClick
boolean
Whether the released click was an alt click (e.g. right click
x
number
y
number
z
number
block
BlockName
targetEId
EntityId | null
onPlayerCraft#
Copy handler
onPlayerCraft = (playerId, itemName, craftingIdx, recipe, craftTimes) => void

Called when a player crafts an item

PARAMETERS
playerId
PlayerId
The id of the player that crafted the item
itemName
string
The name of the item that was crafted
craftingIdx
number
The index of the used recipe in the item's recipe list
recipe
RecipesForItem[number]
The recipe that was used to craft the item
craftTimes
number
The number of times the craft recipe is used at once (e.g. shift held while crafting)
onPlayerDamagingMeshEntity#
Copy handler
onPlayerDamagingMeshEntity = (playerId, damagedId, damageDealt, withItem) => void

Called when a player is damaging a mesh entity

PARAMETERS
playerId
PlayerId
The id of the player damaging the mesh entity
damagedId
EntityId
The id of the mesh entity being damaged
damageDealt
number
The amount of damage dealt
withItem
string
The item used to attack
onPlayerDamagingMob#
Copy handler
onPlayerDamagingMob = (playerId, mobId, damageDealt, withItem, damagerDbId, damageInfo) =>
number | void | "preventDamage"

Called when a player is damaging a mob

Return "preventDamage" to prevent damage

Return number to change damage dealt to that amount

PARAMETERS
playerId
PlayerId
The id of the player damaging the mob
mobId
MobId
The id of the mob being damaged
damageDealt
number
The amount of damage dealt
withItem
string
The item used to attack
damagerDbId
PlayerDbId
The database id of the player attacking
damageInfo
DamageInfo
What dealt the hit: a melee swing, an explosion, a projectile, etc.
RETURNS
number | void | "preventDamage"
CHANGELOG
16th October 2026
onPlayerDamagingOtherPlayer#
Copy handler
onPlayerDamagingOtherPlayer = (attackingPlayer, damagedPlayer, damageDealt, withItem, bodyPartHit, damagerDbId, damageInfo) =>
number | void | "preventDamage"

Called when a player is damaging another player

Return "preventDamage" to prevent damage

Return number to change damage dealt to that amount

Sometimes the damager will have left the game (e.g. spikes placer);

in this case, attackingPlayer will be the damagedPlayer,

but we pass damagerDbId for use cases where it's important.

PARAMETERS
attackingPlayer
PlayerId
The id of the player attacking
damagedPlayer
PlayerId
The id of the player being damaged
damageDealt
number
The amount of damage dealt
withItem
string
The item used to attack
bodyPartHit
LifeformBodyPart
The body part hit
damagerDbId
PlayerDbId
The database id of the player attacking
damageInfo
DamageInfo
What dealt the hit: a melee swing, an explosion, a projectile, etc.
RETURNS
number | void | "preventDamage"
CHANGELOG
16th October 2026
onPlayerDropItem#
Copy handler
onPlayerDropItem = (playerId, x, y, z, itemName, itemAmount, fromIdx) =>
void | "preventDrop" | "allowButNoDroppedItemCreated"

Called when a player drops an item

Return "preventDrop" to prevent the player from dropping the item at all.

Return "allowButNoDroppedItemCreated" to allow discarding items without dropping them.

PARAMETERS
playerId
PlayerId
The id of the player that dropped the item
x
number
The x coordinate of the item that was dropped
y
number
The y coordinate of the item that was dropped
z
number
The z coordinate of the item that was dropped
itemName
ItemName
The name of the item that was dropped
itemAmount
number
The amount of the item that was dropped
fromIdx
number
The index of the item that was dropped from the player's inventory
RETURNS
void | "preventDrop" | "allowButNoDroppedItemCreated"
USED IN
Building a SessionBasedGame
onPlayerEnteredVehicle#
Copy handler
onPlayerEnteredVehicle = (playerId, vehicleType, vehicleEId) => void

Called when a player enters a vehicle

PARAMETERS
playerId
PlayerId
The id of the player that entered the vehicle
vehicleType
MeshEntityVehicleType
The type of the vehicle
vehicleEId
EntityId
The id of the vehicle
onPlayerExitedVehicle#
Copy handler
onPlayerExitedVehicle = (playerId, vehicleType, vehicleEId) => void

Called when a player exits a vehicle

PARAMETERS
playerId
PlayerId
The id of the player that exited the vehicle
vehicleType
MeshEntityVehicleType
The type of the vehicle
vehicleEId
EntityId
The id of the vehicle
onPlayerFailedFishCatch#
Copy handler
onPlayerFailedFishCatch = (playerId, rodName, x, y, z, caughtItemName) => void

Called after the fishing QTE fails or its time window expires, after removing the bob/session.

Coordinates are the fishing position captured at water entry. Retracting, switching rods, dying, and leaving cancel silently.

caughtItemName is the item selected for the failed attempt; no reward is given.

PARAMETERS
playerId
PlayerId
rodName
string
x
number
y
number
z
number
caughtItemName
ItemName
onPlayerFinishChargingItem#
Copy handler
onPlayerFinishChargingItem = (playerId, used, itemName, duration) => void

Called when a player finishes charging an item

PARAMETERS
playerId
PlayerId
The id of the player charging the item
used
boolean
Whether the item was used
itemName
string
The name of the charged item
duration
number
The duration of the charge
onPlayerFinishQTE#
Copy handler
onPlayerFinishQTE = (playerId, qteId, result) => void
PARAMETERS
playerId
PlayerId
qteId
QTERequestId
result
boolean
USED IN
QTEs
onPlayerJoin#
Copy handler
onPlayerJoin = (playerId, fromGameReset) => void

Called when a player joins the lobby

PARAMETERS
playerId
string
The id of the player that joined
fromGameReset
boolean
Whether this call is from a game reset (used by SessionBasedGame)
USED IN
Snippets
Variations
Dialogue
onPlayerJump#
Copy handler
onPlayerJump = (playerId) => void

Called when a player jumps

PARAMETERS
playerId
string
The id of the player that jumped
onPlayerKilledMob#
Copy handler
onPlayerKilledMob = (playerId, mobId, damageDealt, withItem) =>
void | "preventDrop"

Called when a player kills a mob

Return "preventDrop" to prevent the mob from dropping items

PARAMETERS
playerId
PlayerId
The id of the player killed
mobId
MobId
The id of the mob that killed the player
damageDealt
number
The amount of damage dealt
withItem
string
The item used to attack
RETURNS
void | "preventDrop"
onPlayerKilledOtherPlayer#
Copy handler
onPlayerKilledOtherPlayer = (attackingPlayer, killedPlayer, damageDealt, withItem) =>
void | "keepInventory"

Called when a player kills another player

Return "keepInventory" to not drop the player's inventory

PARAMETERS
attackingPlayer
string
The id of the player attacking
killedPlayer
string
The id of the player killed
damageDealt
number
The amount of damage dealt
withItem
string
The item used to attack
RETURNS
void | "keepInventory"
USED IN
Building a SessionBasedGame
onPlayerLeave#
Copy handler
onPlayerLeave = (playerId, serverIsShuttingDown) => void

Called when a player leaves the lobby

PARAMETERS
playerId
string
The id of the player that left
serverIsShuttingDown
boolean
Whether the server is shutting down
USED IN
Interactable NPCs
Dialogue
onPlayerMoveInvenItem#
Copy handler
onPlayerMoveInvenItem = (playerId, fromIdx, toStartIdx, toEndIdx, amt) =>
void | "preventChange"

Called for all types of inventory item movement.

Certain methods of moving item can result in splitting a stack

into multiple slots. (e.g. shift-click).

toStartIdx and toEndIdx provide the min and max idxs moved into.

Return "preventChange" to prevent item movement.

PARAMETERS
playerId
PlayerId
The id of the player moving the item
fromIdx
number
The index that the item is being moved from
toStartIdx
number
The start index that the item is being moved into
toEndIdx
number
The end index that the item is being moved into
amt
number
The amount of the item being moved
RETURNS
void | "preventChange"
onPlayerMoveInvenItemWithAmt#
Copy handler
onPlayerMoveInvenItemWithAmt = (playerId, i, j, amt) =>
void | "preventChange"

Return "preventChange" to prevent the movement

PARAMETERS
playerId
PlayerId
The id of the player moving the item
i
number
The index of the first slot
j
number
The index of the second slot
amt
number
The amount of the item being moved
RETURNS
void | "preventChange"
onPlayerMoveItemIntoIdxs#
Copy handler
onPlayerMoveItemIntoIdxs = (playerId, start, end, moveIdx, itemAmount) =>
void | "preventChange"

Called when a player moves an item into an index within a range of inventory slots

Return "preventChange" to prevent the movement

PARAMETERS
playerId
PlayerId
The id of the player moving the item
start
number
The start index of the range
end
number
The end index of the range
moveIdx
number
The index of the item being moved
itemAmount
number
The amount of the item being moved
RETURNS
void | "preventChange"
onPlayerMoveItemOutOfInventory#
Copy handler
onPlayerMoveItemOutOfInventory = (playerId, itemName, itemAmount, fromIdx, movementType) =>
void | "preventChange"

Called when a player moves an item out of their inventory

Return "preventChange" to prevent the movement

PARAMETERS
playerId
PlayerId
The id of the player moving the item
itemName
string
The name of the item being moved
itemAmount
number
The amount of the item being moved
fromIdx
number
The index which the item is being moved from
movementType
string
The type of movement that occurred
RETURNS
void | "preventChange"
onPlayerOpenedChest#
Copy handler
onPlayerOpenedChest = (playerId, x, y, z, isMoonstoneChest, isIronChest) => void

Called when a player opens a chest

PARAMETERS
playerId
PlayerId
The id of the player that opened the chest
x
number
The x coordinate of the chest that was opened
y
number
The y coordinate of the chest that was opened
z
number
The z coordinate of the chest that was opened
isMoonstoneChest
boolean
Whether the chest is a moonstone chest
isIronChest
boolean
Whether the chest is an iron chest
onPlayerPickedUpItem#
Copy handler
onPlayerPickedUpItem = (playerId, itemName, itemAmount, itemEntityId) => void

Called when a player picks up an item

PARAMETERS
playerId
PlayerId
The id of the player that picked up the item
itemName
string
The name of the item that was picked up
itemAmount
number
The amount of the item that was picked up
itemEntityId
EntityId
The entityId of the item that was picked up
onPlayerPlayedEmote#
Copy handler
onPlayerPlayedEmote = (playerId, emoteId) => void

/** Called after a player plays an emote from the emote wheel. */

PARAMETERS
playerId
PlayerId
emoteId
string
onPlayerPotionEffect#
Copy handler
onPlayerPotionEffect = (initiatorId, targetId, effectName) =>
void | "preventEffect"

Called when a player is affected by a new potion effect

PARAMETERS
initiatorId
string
The id of the player who initiated the potion effect
targetId
string
The id of the player who has started being affected
effectName
"Damage" | "Speed" | "Damage Reduction" | "Invisible" | "Jump Boost" | "Knockback" | "Poisoned" | "Slowness" | "Weakness" | "Cleansed" | "Instant Damage" | "Health Regen" | "Healing Pulse" | "Instant Health" | "Haste" | "Shield" | "Double Jump" | "Heat Resistance" | "Thief" | "X-Ray Vision" | "Mining Yield" | "Brain Rot" | "Aura" | "Wall Climbing" | "Air Walk" | "Pickpocketer" | "Lifesteal" | "Bounciness" | "Blindness" | "Poopy" | "Glowing" | "Night Vision"
The name of the potion effect
RETURNS
void | "preventEffect"
onPlayerPressedButton#
Copy handler
onPlayerPressedButton = (playerId, buttonId) => void

Called when a player presses a custom button

PARAMETERS
playerId
PlayerId
The id of the player pressing the button
buttonId
string
The id of the button pressed
onPlayerReleasedButton#
Copy handler
onPlayerReleasedButton = (playerId, buttonId) => void

Called when a player releases a custom button

PARAMETERS
playerId
PlayerId
The id of the player releasing the button
buttonId
string
The id of the button released
onPlayerRequestChunk#
Copy handler
onPlayerRequestChunk = (playerId, chunkX, chunkY, chunkZ, chunkId) => void

Called when a player requests a chunk

PARAMETERS
playerId
PlayerId
The id of the player requesting the chunk
chunkX
number
The x coordinate of the chunk being requested
chunkY
number
The y coordinate of the chunk being requested
chunkZ
number
The z coordinate of the chunk being requested
chunkId
string
The id of the chunk being requested
onPlayerSelectInventorySlot#
Copy handler
onPlayerSelectInventorySlot = (playerId, slotIndex) => void

Called when a player selects a different inventory slot.

This will be called eventually when you have already set the slot using

api.setSelectedInventorySlotI so be careful not to cause an infinite loop doing this.

PARAMETERS
playerId
PlayerId
The id of the player that selected the inventory slot
slotIndex
number
The index of the inventory slot that was selected
onPlayerSpawnMob#
Copy handler
onPlayerSpawnMob = (playerId, mobId, mobType, x, y, z, mobHerdId, playSoundOnSpawn) => void

Called when a mob is spawned by a player

PARAMETERS
playerId
PlayerId
The id of the player who spawned the mob
mobId
MobId
The id of the mob
mobType
MobType
The type of mob
x
number
The x coordinate of the mob
y
number
The y coordinate of the mob
z
number
The z coordinate of the mob
mobHerdId
MobHerdId
The herd id of the mob
playSoundOnSpawn
boolean
Whether to play a sound on spawn
onPlayerSpawnVehicle#
Copy handler
onPlayerSpawnVehicle = (playerId, vehicleEId, vehicleType, x, y, z) => void

Called when a vehicle is spawned by a player, e.g. by placing a boat

PARAMETERS
playerId
PlayerId
The id of the player who spawned the vehicle
vehicleEId
EntityId
The id of the vehicle
vehicleType
MeshEntityVehicleType
The type of vehicle
x
number
The x coordinate of the vehicle
y
number
The y coordinate of the vehicle
z
number
The z coordinate of the vehicle
CHANGELOG
28th August 2026
onPlayerStartChargingItem#
Copy handler
onPlayerStartChargingItem = (playerId, itemName) =>
void | "preventCharge"

Called when a player starts charging an item

PARAMETERS
playerId
PlayerId
The id of the player charging the item
itemName
string
The name of the item being charged
RETURNS
void | "preventCharge"
onPlayerSucceededFishCatch#
Copy handler
onPlayerSucceededFishCatch = (playerId, rodName, x, y, z, caughtItemName) =>
void | "preventDrop" | "preventItemGrant"

Called after the fishing QTE succeeds and the bob/session have been removed.

Coordinates are the fishing position captured at water entry. caughtItemName is the item selected for the attempt.

Returning nothing gives one of that item, or drops it if the inventory is full.

Return "preventDrop" to suppress the default reward and award custom catches here instead.

Return "preventItemGrant" to deliver the item yourself while keeping the default catch effects.

PARAMETERS
playerId
PlayerId
rodName
string
x
number
y
number
z
number
caughtItemName
ItemName
RETURNS
void | "preventDrop" | "preventItemGrant"
onPlayerSwapInvenSlots#
Copy handler
onPlayerSwapInvenSlots = (playerId, i, j) =>
void | "preventChange"

Return "preventChange" to prevent the swap

PARAMETERS
playerId
PlayerId
The id of the player swapping the inventory slots
i
number
The index of the first slot
j
number
The index of the second slot
RETURNS
void | "preventChange"
onPlayerThrowableHitTerrain#
Copy handler
onPlayerThrowableHitTerrain = (playerId, throwableName, thrownEntityId) => void

Called when a player's thrown projectile hits the terrain

PARAMETERS
playerId
PlayerId
The id of the player that threw the throwable item
throwableName
ThrowableItem
The name of the throwable item
thrownEntityId
EntityId
The id of the entity which hit the terrain
onPlayerToggledShopMenu#
Copy handler
onPlayerToggledShopMenu = (playerId, isOpen) => void

Called when a player opens or closes the shop menu

PARAMETERS
playerId
PlayerId
The id of the player whose shop menu changed
isOpen
boolean
Whether the shop menu is now open
CHANGELOG
7th May 2026
onPlayerUsedThrowable#
Copy handler
onPlayerUsedThrowable = (playerId, throwableName, thrownEntityId) => void

Called when a player uses a throwable item

PARAMETERS
playerId
PlayerId
The id of the player using the throwable item
throwableName
ThrowableItem
The name of the throwable item
thrownEntityId
EntityId
The id of the projectile created by the player
onRespawnRequest#
Copy handler
onRespawnRequest = (playerId) =>
true | void | number[]

Called when a player requests to respawn.

Optionally return the respawn location. Defaults to [0, 0, 0].

Return true to handle yourself (good for async,

but be careful that the player isn't at the place they died,

as they could pick up their old items or hit the player they were fighting).

PARAMETERS
playerId
string
The id of the player that requested to respawn
RETURNS
true | void | number[]
USED IN
Building a SessionBasedGame
onTaskClaimed#
Copy handler
onTaskClaimed = (playerId, taskId, isPromoTask, claimedRewards) =>
any

Called when a player claims a task

PARAMETERS
playerId
string
The id of the player claiming the task
taskId
any
The id of the task being claimed
isPromoTask
any
Whether the task is a promo task
claimedRewards
any
The rewards claimed by the player
RETURNS
any
onTouchscreenActionButton#
Copy handler
onTouchscreenActionButton = (playerId, touchDown) => void

Set client option touchscreenActionButton to take effect

Called when a player presses the touchscreen action button

Called for both touchDown and touchUp

PARAMETERS
playerId
PlayerId
The id of the player pressing the touchscreen action button
touchDown
boolean
Whether the touchscreen action button was pressed or released
onUiRequestResponded#
Copy handler
onUiRequestResponded = (playerId, id, response) => void

Called when a player responds to a UI request.

PARAMETERS
playerId
PlayerId
The id of the player responding to the UI request.
id
UiRequestId
The id of the UI request.
response
boolean
The response to the UI request.
CHANGELOG
7th August 2026
onVehicleDespawned#
Copy handler
onVehicleDespawned = (vehicleEId, vehicleType) => void

Called when a vehicle is despawned

PARAMETERS
vehicleEId
EntityId
The id of the vehicle despawned
vehicleType
MeshEntityVehicleType
The type of vehicle despawned
CHANGELOG
28th August 2026
onWorldAttemptChangeBlock#
Copy handler
onWorldAttemptChangeBlock = (x, y, z, fromBlock, toBlock, initiatorDbId, extraInfo) =>
void | "preventChange"

Called before the world changes a block.

Return "preventChange" to stop it. Then onWorldChangeBlock will not run.

PARAMETERS
x
number
The block's x coordinate
y
number
The block's y coordinate
z
number
The block's z coordinate
fromBlock
BlockName
The current block
toBlock
BlockName
The proposed block
initiatorDbId
string | null
The player who caused the change, or null for game code
extraInfo
WorldBlockChangedInfo
More information about the change
RETURNS
void | "preventChange"
onWorldAttemptDespawnMob#
Copy handler
onWorldAttemptDespawnMob = (mobId) =>
void | "preventDespawn"

Called when the world tries to despawn a mob, e.g. one far from every player. Not called when a mob is killed: use onMobDespawned for that.

Return "preventDespawn" to prevent the mob from despawning.

PARAMETERS
mobId
MobId
The id of the mob despawned
RETURNS
void | "preventDespawn"
onWorldAttemptSpawnMob#
Copy handler
onWorldAttemptSpawnMob = (mobType, x, y, z) =>
void | "preventSpawn"

Called when the world attempts to spawn a mob.

Return "preventSpawn" to prevent the mob from spawning.

PARAMETERS
mobType
MobType
The type of mob
x
number
The potential x coordinate of the mob
y
number
The potential y coordinate of the mob
z
number
The potential z coordinate of the mob
RETURNS
void | "preventSpawn"
onWorldAttemptSpawnVehicle#
Copy handler
onWorldAttemptSpawnVehicle = (vehicleType, x, y, z) =>
void | "preventSpawn"

Called when the world attempts to spawn a vehicle.

Return "preventSpawn" to prevent the vehicle from spawning.

PARAMETERS
vehicleType
MeshEntityVehicleType
The type of vehicle
x
number
The potential x coordinate of the vehicle
y
number
The potential y coordinate of the vehicle
z
number
The potential z coordinate of the vehicle
RETURNS
void | "preventSpawn"
CHANGELOG
28th August 2026
onWorldChangeBlock#
Copy handler
onWorldChangeBlock = (x, y, z, fromBlock, toBlock, initiatorDbId, extraInfo, dropsPrevented) =>
void | "preventChange" | "preventDrop"

In World Code, called after all attempt callbacks allow a world block change, before the block is set.

Read the old block/data here; return "preventChange" to cancel the request, or "preventDrop" to stop its engine item drop.

Drop prevention does not skip built-in validation or change notifications.

Blocks/data written here are preserved. Cancelling the original request does not undo your script effects.

Native games/plugins receive uninterrupted before-commit notifications and must veto in onWorldAttemptChangeBlock.

initiatorDbId is null for game code, such as a growing sapling.

PARAMETERS
x
number
The x coordinate of the block
y
number
The y coordinate of the block
z
number
The z coordinate of the block
fromBlock
BlockName
The old block that was replaced
toBlock
BlockName
The new block that was placed
initiatorDbId
string | null
The id of the player who updated the block
extraInfo
WorldBlockChangedInfo
Extra info about the block change
dropsPrevented
boolean
Whether earlier notifications prevented drops; false during World Code validation
RETURNS
void | "preventChange" | "preventDrop"
onWorldSpawnMob#
Copy handler
onWorldSpawnMob = (mobId, mobType, x, y, z, mobHerdId, playSoundOnSpawn) => void

Called when a mob is spawned by the world

PARAMETERS
mobId
MobId
The id of the mob
mobType
MobType
The type of mob
x
number
The x coordinate of the mob
y
number
The y coordinate of the mob
z
number
The z coordinate of the mob
mobHerdId
MobHerdId
The herd id of the mob
playSoundOnSpawn
boolean
Whether to play a sound on spawn
onWorldSpawnVehicle#
Copy handler
onWorldSpawnVehicle = (vehicleEId, vehicleType, x, y, z) => void

Called when a vehicle is spawned by the world

PARAMETERS
vehicleEId
EntityId
The id of the vehicle
vehicleType
MeshEntityVehicleType
The type of vehicle
x
number
The x coordinate of the vehicle
y
number
The y coordinate of the vehicle
z
number
The z coordinate of the vehicle
CHANGELOG
28th August 2026
playerCommand#
Copy handler
playerCommand = (playerId, command) =>
boolean

Called when a player sends a command

PARAMETERS
playerId
string
The id of the player that sent the command
command
string
The command that the player sent
RETURNS
boolean
tick#
Copy handler
tick = (ms) => void

Called every tick, 20 times per second

PARAMETERS
ms
number
The fixed timestep, can be used as "milliseconds since last tick"
USED IN
Snippets
Variations
Plugins
Building a SessionBasedGame
Interactable NPCs
Project schematics
Previous
API Reference
Next
Client Options

---

## Client Options

URL: https://bloxd.io/docs/client-options

Per-player options such as speed, health and camera.

132 settings

A player's "Client Options" impact what they are capable of doing in the world. For example you can give them a double jump by setting the player's airJumpCount to 1. Alternatively their health bar can be increased by setting their maxHealth to 200. These API methods allow you to modify the client options:

JavaScript
Copy
/**
 * Modify a client option at runtime and send to the client if it changed
 *
 * @param {PlayerId} playerId
 * @param {PassedOption} option - The name of the option
 * @param {ClientOptions[PassedOption]} value - The new value of the option
 * @returns {void}
 */
setClientOption(playerId, option, value)

/**
 * Returns the current value of a client option
 *
 * @param {PlayerId} playerId
 * @param {PassedOption} option
 * @returns {ClientOptions[PassedOption]}
 */
getClientOption(playerId, option)

/**
 * Modify client options at runtime
 *
 * @param {PlayerId} playerId
 * @param {Partial<ClientOptions>} optionsObj - An object which contains key value pairs of new settings. E.g {canChange: true, speedMultiplier: false}
 * @returns {void}
 */
setClientOptions(playerId, optionsObj)

/**
 * Sets a client option to its default value. This will be the value stored in your game's defaultClientOptions, otherwise Bloxd's default.
 *
 * @param {PlayerId} playerId
 * @param {ClientOption} option
 * @returns {void}
 */
setClientOptionToDefault(playerId, option)
Show all 36 lines

Here is the full list of available client options:

airAccScale#
Copy setter
TYPE
number
DEFAULT
1

Amount of acceleration to apply to airborne players.

Only change if absolutely necessary i.e. Rocket Obby uses 0.25.

Players are used to the default bloxd movement behaviour and speed,

and may be put off from your game if different muscle memory is required.

We suggest applying speed or slowness effects instead, using api.applyEffect.

airFrictionScale#
Copy setter
TYPE
number
DEFAULT
1

Amount of friction to apply to airborne players.

Only change if absolutely necessary i.e. Rocket Obby uses 0.

Players are used to the default bloxd movement behaviour and speed,

and may be put off from your game if different muscle memory is required.

We suggest applying speed or slowness effects instead, using api.applyEffect.

airJumpCount#
Copy setter
TYPE
number
DEFAULT
0

Amount of air jumps the player has

airMomentumConservation#
Copy setter
TYPE
boolean
DEFAULT
false

Whether to allow the player to strafe and conserve momentum while airborne.

Only change if absolutely necessary i.e. only Rocket Obby uses true.

Players are used to the default bloxd movement behaviour and speed,

and may be put off from your game if different muscle memory is required.

We suggest applying speed or slowness effects instead, using api.applyEffect.

ambientLightColourOverride#
Copy setter
TYPE
string
DEFAULT
null

Ambient (absence of sky light) colour override - hex string e.g. #ffffff.

arrowPotionEffectDuration#
Copy setter
TYPE
number
DEFAULT
6000

Duration of arrow potion effects

auraPerLevel#
Copy setter
TYPE
number
DEFAULT
100

How much Aura XP is required per level.

autoRespawn#
Copy setter
TYPE
boolean
DEFAULT
false

If true, player will respawn automatically after secsToRespawn seconds

blockReach#
Copy setter
TYPE
number
DEFAULT
6

How far, in blocks from the eye, the player can break, place and use blocks. 0 to 20.

bounciness#
Copy setter
TYPE
number
DEFAULT
0

How much the player bounces off of solid blocks.

A value of 1 is equivalent to every block acting as a mushroom.

bunnyhopMaxMultiplier#
Copy setter
TYPE
number
DEFAULT
1.3

Maximum multiplier for jump height when bunnyhopping

cameraPositionOffset#
Copy setter
TYPE
[number, number, number]
DEFAULT
[0, 0, 0]

Offsets the third-person camera from it's origin by [x, y, z] world units

CHANGELOG
15th June 2026
cameraRoll#
Copy setter
TYPE
number
DEFAULT
0

Roll angle of the camera in radians. Useful for disorientation effects, death effects, etc.

cameraRollTransitionMs#
Copy setter
TYPE
number
DEFAULT
0

Duration in ms to animate/transition to the camera roll angle (when you change cameraRoll). 0 = instant.

Useful for smooth camera roll transitions.

cameraRotationOffset#
Copy setter
TYPE
[number, number, number]
DEFAULT
[0, 0, 0]

Rotates the third-person camera around it's origin by [x, y, z] radians

CHANGELOG
15th June 2026
cameraTint#
Copy setter
TYPE
[number, number, number, number]
DEFAULT
null

RGBA array [r, g, b, a] for camera screen tint effect. Values fall between 0 and 1.

canAltAction#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the player can use the alt action key (right click on PC)

canChange#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the player can change blocks

canClimbWalls#
Copy setter
TYPE
boolean
DEFAULT
false

Whether the player can climb walls

canCraft#
Copy setter
TYPE
boolean
DEFAULT
true

Whether to allow the player to craft items

useFullInventory must be true for this to work

canCrouch#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the player can crouch

canCustomiseChar#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the player can customise their character

canFish#
Copy setter
TYPE
boolean
DEFAULT
true

Whether to allow players to fish with the default

fishing gameplay in Bloxd. Disable this if you want

to write custom (non-QTE) fishing mechanics

canPickBlocks#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the player can pick blocks (middle mouse click on PC), ignored if creative is false

canPickUpItems#
Copy setter
TYPE
boolean
DEFAULT
true

Whether to allow the player to pick up items

canRecordReplays#
Copy setter
TYPE
boolean
DEFAULT
true

When false, players can't record replays or save clips. Turning it off mid-game discards any recording in progress. Set it for the whole game, not per area: chunks load before players reach them, and turning it back on lets new clips include every loaded chunk.

canSeeNametagsThroughWalls#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the player can see name tags through walls

cantBreakError#
Copy setter
TYPE
string | CustomTextStyling
DEFAULT
null

Error message for when the player fails to break a block

cantBuildError#
Copy setter
TYPE
string | CustomTextStyling
DEFAULT
null

Error message for when the player fails to place a block

cantChangeError#
Copy setter
TYPE
string | CustomTextStyling
DEFAULT
"You cannot modify this block"

Error message for when the player fails to change a block

canUseZoomKey#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the player can use the zoom key

chatChannels#
Copy setter
TYPE
{ channelName: string; elementContent: string | CustomTextStyling; elementBgColor: string; }[]
DEFAULT
null

Allows player to select a channel that is passed as argument to onPlayerChat. See engineGameplayTypes.ts for expected format

compassTarget#
Copy setter
TYPE
string | number | number[]
DEFAULT
[0, 0, 0]

The target the compass will point towards

creative#
Copy setter
TYPE
boolean
DEFAULT
false

Whether the player is in creative mode

crosshairText#
Copy setter
TYPE
string | CustomTextStyling
DEFAULT
""

Text to display by the crosshair

crouchingSpeed#
Copy setter
TYPE
number
DEFAULT
2

Speed multiplier for the player when crouching.

Players are used to the default bloxd movement behaviour and speed,

and may be put off from your game if different muscle memory is required.

We suggest applying speed or slowness effects instead, using api.applyEffect.

crouchMobDetectionRadiusMultiplier#
Copy setter
TYPE
number
DEFAULT
2

Mult for the radius within which mobs can detect the player when crouching.

If a player's mult is 2, then mobs will think they are twice as far away.

customButtons#
Copy setter
TYPE
CustomButtonsType
DEFAULT
null

Custom buttons to show in game

CHANGELOG
5th November 2026
customVariationTitle#
Copy setter
TYPE
string
DEFAULT
""

Overridden subtitle after the game name in the top-left header.

dealingDamageDefaultMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Mult for when the player hits neither a leg or a head. Only applies to guns

dealingDamageHeadMultiplier#
Copy setter
TYPE
number
DEFAULT
1.75

Damage multiplier for when the player hits a head. Only applies to guns

dealingDamageLegMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Damage multiplier for when the player hits a leg. Only applies to guns

dealingDamageMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Damage multiplier for all types of damage

defaultBlock#
Copy setter
TYPE
string
DEFAULT
"Block of Gold"

The default block the player can change blocks to, used if canChange is true but useInventory is false

dialogue#
Copy setter
TYPE
{ line: DialogueText; speakerName?: string | CustomTextStyling; voice?: SpeechVoice; animateIn?: boolean; }
DEFAULT
null

A line of dialogue in the panel below the crosshair, revealed word by word with a blip in its voice per syllable.

Each new value is a new line, which replays its reveal; null hides the panel.

A line stays up until it is replaced or hidden, so World Code can use sayDialogue from @plugins/dialogue to hide it after a while.

The voice presets are "soft", "regular", "dark", "high-pitched", "gruff", "lively", "posh" and "mechanical".

TypeScript
Copy
 {
     line: string | TranslatedText                 // `[[Item Name]]` shows the item's icon inline
     speakerName?: string | CustomTextStyling      // Shown above the line, such as a portrait icon and a name
     voice?: SpeechVoicePreset | SpeechSynth       // A preset such as "regular" or "soft", or every synth parameter. Omit for a silent line
     animateIn?: boolean                           // False shows the line whole, without its reveal or voice
 }
CHANGELOG
22nd October 2026
droppedItemScale#
Copy setter
TYPE
number
DEFAULT
1

Scale factor to use for dropped item meshes

effectDamageDuration#
Copy setter
TYPE
number
DEFAULT
8000

Duration of the +damage effect from plum

effectDamageReductionDuration#
Copy setter
TYPE
number
DEFAULT
13000

Duration of +damage reduction effect from pear

effectHealthRegenDuration#
Copy setter
TYPE
number
DEFAULT
5000

Duration of +health regen effect from cherry

effectSpeedDuration#
Copy setter
TYPE
number
DEFAULT
8000

Duration of +speed effect from cracked coconut

ezBridging#
Copy setter
TYPE
boolean
DEFAULT
true

Assisted bridging. When on, the player can place a block off the edge of the block they are

standing on without aiming back at it, but that block grows in place and only becomes solid

when finished - nothing can be placed off it until then.

A block takes 900ms to finish, making assisted bridging 1.11 blocks/s: slower than crouch

bridging and far slower than speed bridging, so the skill ceiling is preserved. A growing

cell is never valid support, and the assist stops at one rather than looking past it, so

bridging out along a single aim is paced one block at a time. In creative the block is

placed instantly, as there is nothing to pace. ezBridgingGrowMs changes the growth time.

ezBridgingGrowMs#
Copy setter
TYPE
number
DEFAULT
null

How long, in whole milliseconds (0 to 60000), an ez bridging block takes to grow before it becomes

solid. 0 places it instantly. Applies in creative too when set. Null uses the default: 900ms, or

instant in creative.

ezTowering#
Copy setter
TYPE
boolean
DEFAULT
true

Assisted towering: a player standing still, or in the air with no movement or jump input, can

place a block on the one beneath them - into their own feet - where it grows for ezToweringGrowMs

and then lifts them onto it. Only blocks ez bridging can place can be towered with.

ezToweringGrowMs#
Copy setter
TYPE
number
DEFAULT
null

How long, in whole milliseconds (0 to 60000), an ez towering block takes to grow before it becomes

solid. 0 places it instantly. Applies in creative too when set. Null uses the default: 900ms, or

instant in creative.

fallDamage#
Copy setter
TYPE
boolean
DEFAULT
false

Whether to deal damage to the player when they fall

fillBrokenBlocksWithWater#
Copy setter
TYPE
boolean
DEFAULT
false

Whether a block the player breaks becomes Water when water touches it from the side or above, rather than Air.

flySpeedMultiplier#
Copy setter
TYPE
number
DEFAULT
1.5

Multiplier for the flying speed in creative mode

fogBlockDistanceOverride#
Copy setter
TYPE
number
DEFAULT
null

Blocks from the eye at which fog turns solid, thickening all the way out from the eye. Overrides

fogChunkDistanceOverride and graphic settings when set.

fogChunkDistanceOverride#
Copy setter
TYPE
number
DEFAULT
null

Fog distance which overrides graphic settings. Uses graphic settings if null.

fogColourOverride#
Copy setter
TYPE
string
DEFAULT
null

RGB string for fog colour override. e.g. #ffffff

fogOnSkybox#
Copy setter
TYPE
boolean
DEFAULT
false

Applies fog to the skybox, which is otherwise unaffected by fog.

forcedCameraDirection#
Copy setter
TYPE
[number, number, number]
DEFAULT
null

Force the camera to look in a specific direction [x, y, z]. Set to null to allow free camera movement.

forcedCameraDirectionTransitionMs#
Copy setter
TYPE
number
DEFAULT
0

Duration in ms to animate/transition to the forced camera direction (when you change forcedCameraDirection). 0 = instant.

Useful for smooth camera movements.

gameCamera#
Copy setter
TYPE
CameraSettings
DEFAULT
{ mode: "default" }

Takes over the player's camera. mode picks the kind of camera:

"default": the player's own first or third person camera.
"fixed": stands at position, looking at lookAt (a position or entity id, the player if left out) or along lookDirection.
"follow": moves with target (the player if left out), offset blocks away; offsetSpace: "target" turns the offset with the target, +z ahead of it. Good for top-down, side-on and chase cameras. Set avoidTerrain: true to move in rather than go through terrain between the camera and the target.
"path": flies through keyframes, each with a timeMs and a position, and optionally lookAt, lookDirection, fov and easing. It stays on the last keyframe at the end, or set loop: true to go round again.
"frame": keeps every one of targets (up to 64 positions or entity ids) in view, looking down viewElevation degrees (45 if left out) towards viewHeading (0, along +z), with padding blocks around them, between closestDistance and furthestDistance blocks away. Good for board game overviews, arenas and boss fights.

blendInMs glides from the current view to the new camera over that many ms, or cuts straight to it at 0.

Every mode, "default" included, also takes:

transition: { colour, outMs, holdMs, inMs }: fades through a colour instead of blending. The screen fades out to colour ("#rrggbb", black if left out) over outMs. The view cuts to the new camera once the colour covers the screen, and a path's clock starts there. The colour holds for holdMs (0 if left out), then fades back in over inMs. Each fade takes 200 to 5000 ms, and the hold up to 5000 ms. To spare players flashing, a fade turns between going out and coming in at most once every 333 ms; until then it goes on as it was. A fade already showing keeps its colour until the screen clears. The colour covers the world and the HUD, including chat history and the chat button on touch screens. It doesn't cover menus, the chat being typed in, dialogue, the respawn and sleeping screens, QTEs, UI requests, touch controls or the settings button on touch screens. The HUD under the colour can still be clicked unless hideHud hides it. Until the cut, the camera on screen stays. Setting that camera again cancels the transition, even with a different transition, letterbox or hideHud. A change to the camera on its way in must repeat transition, or it cuts in at once.
letterbox: true: black bars across the top and bottom of the screen, for cutscenes. They slide in and out as it changes, or switch under the colour of a transition. A "frame" camera fits its targets between them. Presses on the bars do nothing in the world, and dragging on them doesn't turn the camera.
hideHud: true: hides the HUD while the camera is set, from the cut of a transition. What the player still needs stays: nametags, dialogue, the chat while they type, the respawn and sleeping screens, QTEs, UI requests, touch controls, menus, and the settings button on touch screens.

The other modes also take fov in degrees, and playerLook: { maxYaw, maxPitch } to let the mouse look that many degrees either side of where the camera aims. Leave one out to lock that axis, as in { maxYaw: 180 }.

playerFacing: "movement" (the default) turns the player to face where they walk, "camera" to face where the camera looks, and "cursor" to face what is under the mouse cursor (or the last tap), which they mine, build, hit and shoot at, for top-down and isometric games. Walking is always relative to the camera.

Setting the camera the player already has does nothing, so to replay a path from the start, set another camera first (in the same tick is fine).

The player only sees the world and other entities near them, so keep cameras and their targets within their view distance.

JavaScript
Copy
 // Top-down camera following the player, who aims with the mouse cursor
 api.setClientOption(playerId, "gameCamera", { mode: "follow", offset: [0, 20, 5], playerFacing: "cursor" })
 // Fly over the map for 8 seconds, looking at its centre
 api.setClientOption(playerId, "gameCamera", {
     mode: "path",
     keyframes: [
         { timeMs: 0, position: [0, 80, 0], lookAt: [50, 60, 50] },
         { timeMs: 8000, position: [100, 80, 0], lookAt: [50, 60, 50] },
     ],
 })
 // Spectate another player from behind
 api.setClientOption(playerId, "gameCamera", { mode: "follow", target: otherPlayerId, offset: [0, 3, -6], offsetSpace: "target", avoidTerrain: true })
 // Keep every player in view from above, easing out as they spread apart (up to 64 targets)
 api.setClientOption(playerId, "gameCamera", { mode: "frame", targets: api.getPlayerIds().slice(0, 64), viewElevation: 60 })
 // Back to the player's own camera, gliding there over half a second
 api.setClientOption(playerId, "gameCamera", { mode: "default", blendInMs: 500 })
 // A cutscene: fade through black into a path, with letterbox bars and no HUD
 const transition = { outMs: 500, holdMs: 250, inMs: 600 }
 api.setClientOption(playerId, "gameCamera", { mode: "path", keyframes, transition, letterbox: true, hideHud: true })
 // ...and when it ends, fade back to the player's own camera
 api.setClientOption(playerId, "gameCamera", { mode: "default", transition })
CHANGELOG
5th November 2026
gravityMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Multiplier applied to gravity during normal movement.

Set to 1 for default gravity.

groundArrowPath#
Copy setter
TYPE
{ target: [number, number, number]; colour?: string; }
DEFAULT
null

Renders a terrain-following strip of animated chevron arrows on the ground from this player to the target position.

The arrow path is not visible to other players.

Configure a target position with target: [x, y, z] to show, or null to hide.

Optional colour is any CSS colour string (e.g. "red", "#ffaa00", "rgb(255,0,0)"), or null for default white.

CHANGELOG
12th May 2026
groundFrictionScale#
Copy setter
TYPE
number
DEFAULT
1

Amount of friction to apply to grounded players.

Only change if absolutely necessary i.e. Rocket Obby uses 3.

Players are used to the default bloxd movement behaviour and speed,

and may be put off from your game if different muscle memory is required.

We suggest applying speed or slowness effects instead, using api.applyEffect.

gunshotOrigin#
Copy setter
TYPE
GunshotOrigin
DEFAULT
"default"

Where gunshots originate from.

-"default" preserves classic bloxd behavior (casts originate from the camera in third person).

-"head" always spawns raycasts from the player's head. Useful for certain camera perspectives.

headerChips#
Copy setter
TYPE
HeaderChip[]
DEFAULT
[]

A row of compact chips shown in the top-left HUD strip, concatenated immediately after the FPS counter,

coordinates and room name. Each chip is bare text or a TextWithDisplayOptions wrapper to toggle its

background panel.

CHANGELOG
26th June 2026
healthRegenAmount#
Copy setter
TYPE
number
DEFAULT
0.05

Fraction of max health that regens each regen tick

healthRegenInterval#
Copy setter
TYPE
number
DEFAULT
4000

How often health regen is ticked

healthRegenStartAfter#
Copy setter
TYPE
number
DEFAULT
5000

How long after a player receives damage to start regen again

heldLightColourOverride#
Copy setter
TYPE
string
DEFAULT
null

Held item light colour override - hex colour string e.g. #ffffff. Applied regardless of any held item.

heldLightConeAngleOverride#
Copy setter
TYPE
number
DEFAULT
null

Held item light cone angle override. Angle is measured in degrees. Larger number = wider beam.

heldLightRangeOverride#
Copy setter
TYPE
number
DEFAULT
null

Held item light range override. Distance is measured in blocks.

hideCoordinates#
Copy setter
TYPE
boolean
DEFAULT
false

When true, hides world and chunk coordinates regardless of the player's setting.

horizontalKnockbackMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Multiplier for horizontal knockback when dealing damage

initialHealth#
Copy setter
TYPE
number
DEFAULT
100

Health upon joining or respawning. Can be null for the player to not have health

initialShield#
Copy setter
TYPE
number
DEFAULT
0

Shield upon joining or respawning

inventoryColourOverride#
Copy setter
TYPE
string
DEFAULT
null

Background colour of the hotbar, inventory and crafting panels, as a hex string e.g. "#682323".

Slot colours are derived from it. Chests and crafting stations keep their own colours.

null uses the default colours.

inventoryItemsMoveable#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the player can move items in their inventory, only applicable if useInventory is true

invincible#
Copy setter
TYPE
boolean
DEFAULT
false

Whether the player is invincible

isReceivingDamageCooldownGlobal#
Copy setter
TYPE
boolean
DEFAULT
true

When the player is attacked, a short cooldown prevents further damage from the same attack type. If true, all attackers share that cooldown. If false, each attacker has their own.

jumpAmount#
Copy setter
TYPE
number
DEFAULT
8

Amount of jump power the player has

jumpHoldThrust#
Copy setter
TYPE
{ maxUpSpeed: number; force: number; }
DEFAULT
null

Jetpack-style lift while the player holds jump in the air: { maxUpSpeed, force }, or null for off.

Pushes up with force (blocks/s per second, 0 to 45; gravity is 20 times gravityMultiplier) until the player's vertical speed nears maxUpSpeed (blocks/s, -20 to 20).

With force above gravity the player climbs at about maxUpSpeed - gravity / force, e.g. { maxUpSpeed: 8, force: 36 } climbs at about 7.4 blocks/s.

A negative maxUpSpeed slows a fall instead, e.g. { maxUpSpeed: -3, force: 36 } glides down at about 3.6 blocks/s.

With force at or below gravity it only weakens gravity by force: the player never reaches maxUpSpeed and a fall keeps speeding up.

No effect on the ground, in water, on ladders or climbable walls, in cobwebs, while flying, in vehicles, or with a glider or other held vehicle selected.

Separate from the jump itself: a jumpAmount or jump multiplier of 0 doesn't turn it off.

It still pushes while the player is knocked back, so a held jump can soften or extend a hit.

killstreakDuration#
Copy setter
TYPE
number
DEFAULT
200000000

Duration before a killstreak expires. (defaults to never expiring)

lightingOverride#
Copy setter
TYPE
boolean
DEFAULT
null

When null, just use the player's graphics setting. When set, forces lighting on (true) or off (false).

lobbyLeaderboardInfo#
Copy setter
TYPE
LobbyLeaderboardInfo
DEFAULT
TypeScript
Copy
{
name: {
	displayName: "Name",
	sortPriority: 0,
},
	}

Columns of the lobby leaderboard

maxAuraLevel#
Copy setter
TYPE
number
DEFAULT
0

The maximum Aura Level attainable - Set to 0 to disable Aura XP

maxHealth#
Copy setter
TYPE
number
DEFAULT
100

Maximum health the player can have

maxPlayerZoom#
Copy setter
TYPE
number
DEFAULT
15

Maximum camera zoom level for the player

maxShield#
Copy setter
TYPE
number
DEFAULT
100

Maximum shield the player can have

middleTextLower#
Copy setter
TYPE
string | CustomTextStyling | TextWithDisplayOptions
DEFAULT
""

Small text to display in the middle of the screen

middleTextTop#
Copy setter
TYPE
string | CustomTextStyling | TextWithDisplayOptions
DEFAULT
""

Text to display centred at the very top of the screen, in line with the FPS counter, coordinates and room name.

Drops to immediately below that strip when a centred placement would not fit without overlapping it.

CHANGELOG
26th June 2026
middleTextUpper#
Copy setter
TYPE
string | CustomTextStyling | TextWithDisplayOptions
DEFAULT
""

Large text to display in the middle of the screen

minChunkAddDist#
Copy setter
TYPE
[number, number]
DEFAULT
[2, 2]

Minimum size of region around player where chunks are loaded.

Format [horizontalMinChunkRadius, verticalMinChunkRadius].

Each value should be between 2 and 4.

We recommend leaving this at the default of [2, 2] unless you have a specific reason to change it.

(e.g. you need players to see the bottom of a dropper)

This is because higher values can be laggier on low-end devices.

movementBasedFovScale#
Copy setter
TYPE
number
DEFAULT
1

Amount that player camera is affected by movement based fov

music#
Copy setter
TYPE
Song
DEFAULT
null

The music track to play in the background

musicVolumeLevel#
Copy setter
TYPE
number
DEFAULT
0.6

Volume level for the music

numClosestPlayersVisible#
Copy setter
TYPE
number
DEFAULT
null

If set, clients will only be able to see the closest x players (good for client perf in games with many players)

playerZoom#
Copy setter
TYPE
number
DEFAULT
0

Default camera zoom level for the player

potionEffectDuration#
Copy setter
TYPE
number
DEFAULT
12000

Duration of potion effects

preserveProtectedFluidSources#
Copy setter
TYPE
boolean
DEFAULT
false

Whether empty buckets can collect protected water/lava without removing the source block.

proximityFadeDistance#
Copy setter
TYPE
number
DEFAULT
0.625

Distance in blocks over which we reduce the opacity of entities as they approach the camera.

proximityFadeMinOpacity#
Copy setter
TYPE
number
DEFAULT
0.5

Minimum opacity multiplier reachable when fading entities based on camera proximity.

The player's own model is always able to fade to 0, and entities being ridden stay fully opaque (as if this value was 1).

receivingDamageMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Damage multiplier for all types of incoming damage

respawnButtonText#
Copy setter
TYPE
string
DEFAULT
"general:respawn"

Text to show on respawn button. (E.g. "Spectate")

RightInfoText#
Copy setter
TYPE
string | CustomTextStyling | TextWithDisplayOptions
DEFAULT
""

Text to display in the right info box

runningSpeed#
Copy setter
TYPE
number
DEFAULT
7

Running speed for the player.

STRONGLY recommend using speedMultiplier unless you have a specific use case for this, runningSpeed doesn't make UX sense on mobile.

(Walking speed is ignored for mobile players, mobile player speed is determined by joystick input and the max of runningSpeed & walkingSpeed).

Players are used to the default bloxd movement behaviour and speed,

and may be put off from your game if different muscle memory is required.

We suggest applying speed or slowness effects instead, using api.applyEffect.

The only use case for walkingSpeed/runningSpeed over speedMultiplier or speed effects is to disable running or to inverse walking/running (so you run by default and e.g. hold shift to go slower).

secsToRespawn#
Copy setter
TYPE
number
DEFAULT
5

After dying the player can respawn after this many seconds

showBasicMovementControls#
Copy setter
TYPE
boolean
DEFAULT
true

Whether to show basic movement controls

showChatBubbles#
Copy setter
TYPE
boolean
DEFAULT
false

Whether the viewer renders speech bubbles above other players when they send chat messages. Off by default.

CHANGELOG
10th June 2026
showKillfeed#
Copy setter
TYPE
boolean
DEFAULT
true

Whether to show the killfeed

showPlayersInUnloadedChunks#
Copy setter
TYPE
boolean
DEFAULT
false

Whether to show the player in unloaded chunks

showProgressBar#
Copy setter
TYPE
boolean
DEFAULT
false

Whether to show the progress bar

skyBox#
Copy setter
TYPE
string | EarthSkyBox
DEFAULT
"default"

Not recommended to use anything other than "default" as client FPS can drop while loading the skybox

skyLightColourOverride#
Copy setter
TYPE
string
DEFAULT
null

Sky light colour override - hex string e.g. #ffffff.

speedMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Speed multiplier for the player.

Players are used to the default bloxd movement behaviour and speed,

and may be put off from your game if different muscle memory is required.

We suggest applying speed or slowness effects instead, using api.applyEffect.

splashPotionEffectDuration#
Copy setter
TYPE
number
DEFAULT
8000

Duration of splash potion effects

stompDamageMultiplier#
Copy setter
TYPE
number
DEFAULT
0

Mult for the damage done by "stomping" on a lifeform, i.e.: falling on them wearing Spiked Boots.

stompDamageRadius#
Copy setter
TYPE
number
DEFAULT
0

Radius around the player that will be affected by the stomp damage.

strictFluidBuckets#
Copy setter
TYPE
boolean
DEFAULT
true

Whether a player can place fluid when canChange is false

touchscreenActionButton#
Copy setter
TYPE
string | CustomTextStyling
DEFAULT
null

The contents of the action button. Supports custom text styling. onTouchscreenActionButton will be called when button pressed.

ttbMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Multiplier for the time to break any block

useFullInventory#
Copy setter
TYPE
boolean
DEFAULT
true

For now just enables the UI of the full inventory

useInventory#
Copy setter
TYPE
boolean
DEFAULT
true

Whether to allow the player to use the inventory

Disabling this will also disable the hotbar

usePlayAgainButton#
Copy setter
TYPE
boolean
DEFAULT
false

When player is dead, also show a play again button to matchmake player into a new lobby. Mostly useful for sessionBased games

useRespawnButton#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the player can use the respawn button. Otherwise forces either play again or exit

CHANGELOG
10th June 2026
verticalKnockbackMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Multiplier for vertical knockback when dealing damage

visionMinLightColour#
Copy setter
TYPE
string
DEFAULT
null

The dimmest light the player can see by - hex string e.g. #ffffff. Anywhere darker is lifted

to it, e.g. caves and night, after the sky/ambient colour overrides. Used by Night Vision.

walkingSpeed#
Copy setter
TYPE
number
DEFAULT
4

Walking speed for the player.

STRONGLY recommend using speedMultiplier unless you have a specific use case for this, walkingSpeed doesn't make UX sense on mobile.

(Walking speed ignored for mobile players, mobile player speed is determined by joystick input and the max of runningSpeed & walkingSpeed).

Players are used to the default bloxd movement behaviour and speed,

and may be put off from your game if different muscle memory is required.

We suggest applying speed or slowness effects instead, using api.applyEffect.

The only use case for walkingSpeed/runningSpeed over speedMultiplier or speed effects is to disable running or to inverse walking/running (so you run by default and e.g. hold shift to go slower).

zoomOutDistance#
Copy setter
TYPE
number
DEFAULT
3

Distance to zoom the camera out to

Previous
Callbacks
Next
Types

---

## Types

URL: https://bloxd.io/docs/types

The types the API Reference's parameters and return values refer to.


These 'types' can't be referenced by your code, but they help explain some of the parameters in the API.

CustomTextStyling#
TypeScript
Copy
type CustomTextStyling = (string | EntityName | TranslatedText | StyledIcon | StyledText | ProgressBar | StyledKeyBinding)[]
EntityMeshScalingMap#
TypeScript
Copy
type EntityMeshScalingMap = {
    [key in "TorsoNode" | "HeadMesh" | "ArmRightMesh" | "ArmLeftMesh" | "LegLeftMesh" | "LegRightMesh"]?: number[]
}
EntityName#
TypeScript
Copy
type EntityName = {
    entityName: string
    style?: {
        color?: string
        colour?: string
    }
}
IngameIconName#
TypeScript
Copy
type IngameIconName = "Damage" | "Damage Reduction" | "Speed" | "VoidJump" | "Fist" | "Frozen" | "Hydrated" | "Invisible" | "Jump Boost" | "Poisoned" | "Slowness" | "Weakness" | "Health Regen" | "Healing Pulse" | "Haste" | "Double Jump" | "Heat Resistance" | "Gliding" | "Boating" | "Obsidian Boating" | "Riding" | "Bunny Hop" | "FallDamage" | "Feather Falling" | "Thief" | "X-Ray Vision" | "Mining Yield" | "Brain Rot" | "Rested Damage" | "Rested Haste" | "Rested Speed" | "Rested Farming Yield" | "Rested Aura" | "Blindness" | "Pickpocketer" | "Lifesteal" | "Bounciness" | "Air Walk" | "Wall Climbing" | "Thorns" | "Poopy" | "Glowing" | "Night Vision" | "Irradiated" | "Draugr Knight Head" | "Draugr Warper Head" | "Magma Golem Head" | "Mystery Fish" | "Damage Enchantment" | "Critical Damage Enchantment" | "Attack Speed Enchantment" | "Protection Enchantment" | "Health Enchantment" | "Health Regen Enchantment" | "Stomp Damage Enchantment" | "Knockback Resist Enchantment" | "Arrow Speed Enchantment" | "Arrow Damage Enchantment" | "Quick Charge Enchantment" | "Break Speed Enchantment" | "Momentum Enchantment" | "Mining Yield Enchantment" | "Farming Yield Enchantment" | "Mining Aura Enchantment" | "Digging Aura Enchantment" | "Lumber Aura Enchantment" | "Farming Aura Enchantment" | "Vertical Knockback Enchantment" | "Horizontal Knockback Enchantment" | "Firecracker Cooldown Enchantment" | "Firecracker Boost Enchantment" | "Gliding Speed Enchantment" | "Self Yield" | "Friends" | "Riding Speed" | "Feed Aura" | "Double Poop" | "Mob Slayer" | "Rainbow Wool" | "Pack Leader" | "Max Health" | "Poison Claws" | "Mob Yield" | "Antlers Bonus" | "Health" | "HealthShield" | "Cross" | "Friendship" | "Dotted Friendship" | "Hunger" | "Empty Hunger" | "Pixelated Heart" | "Question Mark" | "Trader Black" | "Trader Blue" | "Trader Piggy"
ParticleSystemBlendMode#
TypeScript
Copy
enum ParticleSystemBlendMode {
    // Source color is added to the destination color without alpha affecting the result
    OneOne = 0,
    // Blend current color and particle color using particle's alpha
    Standard = 1,
    // Add current color and particle color multiplied by particle's alpha
    Add,
    // Multiply current color with particle color
    Multiply,
    // Multiply current color with particle color then add current color and particle color multiplied by particle's alpha
    MultiplyAdd,
}
RecipesForItem#
TypeScript
Copy
type RecipesForItem =
    {
        requires: { items: ItemName[]; amt: number }[]
        produces: number
        station?: string | string[]
        onCraftedAura?: number
        isStarterRecipe?: boolean
        attributes?: ItemAttributes
    }[]
StyledIcon#
TypeScript
Copy
type StyledIcon = {
    icon: string
    style?: {
        color?: string
        colour?: string
        fontSize?: string
        opacity?: number
    }
}
StyledText#
TypeScript
Copy
type StyledText = {
    str: string | EntityName | TranslatedText
    style?: TextStyle
}
TempParticleSystemOpts#
TypeScript
Copy
type TempParticleSystemOpts = {
    texture: string
    minLifeTime: number
    maxLifeTime: number
    minEmitPower: number
    maxEmitPower: number
    minSize: number
    maxSize: number
    gravity: number[]
    velocityGradients: {
        timeFraction: number
        factor: number
        factor2: number
    }[]
    colorGradients: {
        timeFraction: number
        minColor: [number, number, number, number]
        maxColor?: [number, number, number, number]
    }[] | {
        color: [number, number, number]
    }[]
    blendMode: ParticleSystemBlendMode
    dir1: number[]
    dir2: number[]
    pos1: number[]
    pos2: number[]
    manualEmitCount: number
    hideDist: number
}
TranslatedText#
TypeScript
Copy
type TranslatedText = {
    translationKey: string
    params?: Record<string, string | number | boolean | EntityName>
}
ItemAttributes#
TypeScript
Copy
type ItemAttributes = {
    customDisplayName?: string
    customDescription?: string
    /** Free-form data kept with the item. `bar: { fraction, colour? }` (0 to 1, hex colour) draws a bar under the item's slot. */
    customAttributes?: Record<string, any>
}
WalkThroughType#
TypeScript
Copy
enum WalkThroughType {
    CANT_WALK_THROUGH = 0,
    CAN_WALK_THROUGH = 1,
    DEFAULT_WALK_THROUGH = 2,
}
WorldBlockChangedInfo#
TypeScript
Copy
type WorldBlockChangedInfo = {
    cause: PNull<"Paintball" | "FloorCreator" | "Sapling" | "StemFruit" | "MeltingIce" | "Explosion" | "AutoShape">
}
DamageInfo#
TypeScript
Copy
type DamageInfo = {
    cause: PNull<"Melee" | "Projectile" | "Gun" | "Explosion" | "Spikes" | "Fall" | "Stomp" | "Thorns" | "Effect">
}
EarthSkyBox#
TypeScript
Copy
type EarthSkyBox = {
    type: "earth"
    inclination?: number
    turbidity?: number
    infiniteDistance?: boolean
    luminance?: number
    // Sky appearance (light intensity); higher = more saturated sky.
    rayleigh?: number
    // Mie scattering coefficient in [0, 0.1]; affects mieDirectionalG impact.
    mieCoefficient?: number
    // Amount of haze particles per Mie scattering theory.
    mieDirectionalG?: number
    // Distance of the sun from the active scene camera.
    distance?: number
    // When `useSunPosition` is true, this overrides `inclination` + `azimuth`.
    sunPosition?: Vec3
    useSunPosition?: boolean
    xCameraOffset?: number
    yCameraOffset?: number
    zCameraOffset?: number
    // Direction the sky considers "up"; defaults to [0, 1, 0].
    up?: Vec3
    // Dither the sky to reduce visible banding.
    dithering?: boolean
    azimuth?: number
    // Not part of sky model by default; heavily tint to a vertex color
    vertexTint?: Vec3
}
ShopItem#
TypeScript
Copy
type ShopItem = {
    image: string
    cost?: number
    currency?: string
    amount?: number // Display amount shown on the shop tile image (0 and 1 are not displayed)
    imageColour?: string
    canBuy?: boolean
    isSelected?: boolean
    buyButtonText?: string | CustomTextStyling
    customTitle?: string | CustomTextStyling
    description?: string | CustomTextStyling
    onBoughtMessage?: string | CustomTextStyling
    redDot?: boolean
    forceRemoveRedDot?: boolean
    badge?: { text: string | CustomTextStyling; type: ShopItemBadgeType }
    userInput?: ShopItemUserInput
    enchant?: {
        tier: EnchantmentTier
        enchantments: Partial<Record<EnchantmentPerk, number>>
        enchantmentData?: Record<string, { icon?: string; description?: string }>
    }
    sell?: boolean // Optional, defaults to false. If true, the sign of "cost" is flipped. So a "cost" of -25 would give the player 25 currency AND be displayed as "25" (instead of -25)
    sortPriority?: number // Descending, bigger number means closer to the top
    hidden?: boolean
}
ShopItemUserInput#
TypeScript
Copy
type ShopItemUserInput =
    | { type: "text"; placeholderText?: string; wordCharsOnly?: boolean; initialValue?: string } // wordCharsOnly defaults to false. If true, only allows \w character (alphanumeric and _). initialValue always takes precedence as the text input value when set.
    | { type: "number"; placeholderText?: string; initialValue?: string }
    | {
            type: "dropdown"
            dropdownOptions: (string | { option: string; cost: number })[]
            shouldResetSelectionOnOptionsChange?: boolean // Defaults to false. If true, the selection will reset to the first option when dropdownOptions changes.
            initialValue?: string
            autoSubmit?: boolean // Defaults to false. If true, the dropdown will automatically submit when the user selects an option.
      }
    | { type: "player"; excludedPlayers?: PlayerId[] } // Defaults to excluding the current player
    | { type: "color"; initialValue?: string }
ShopCategoryConfig#
TypeScript
Copy
type ShopCategoryConfig = Partial<{
    autoSelectCategory: boolean
    customTitle: string // Supports translation keys and ordinary text
    redDot: boolean
    forceRemoveRedDot: boolean
    sortPriority: number
    description: string | CustomTextStyling
}>
MobSpawnOpts#
TypeScript
Copy
type MobSpawnOpts<TMobType extends MobType> = Partial<{
    mobHerdId: MobHerdId
    spawnerId: PlayerId
    mobDbId: MobDbId
    name: string
    playSoundOnSpawn: boolean
    variation: MobVariation<TMobType>
    physicsOpts: Partial<{
        width: number
        height: number
        collidesEntities: boolean
    }>
}>
MeshEntityOpts#
TypeScript
Copy
type MeshEntityOpts = {
    Box: CommonMeshEntityOpts & {
        width: number
        height: number
        depth: number
        diffuseColor?: number[]
        emissiveColor?: number[]
        backFaceCulling?: boolean // Default true
        texture?: string // Can be a blockname. Wraps every one block
        faceUV?: number[][]
        animateTexture?: boolean // If true, `texture` must be an animated block name (e.g. "Lava", "Red Portal") and the Box cycles through its frames.
    }
    BloxdBlock: CommonMeshEntityOpts & {
        blockName: BlockNameOrId
        size: number | [number, number, number]
        /** Enchantment sheen, drawn only when attached to an entity node, as a worn glider is. */
        enchantmentTier?: EnchantmentTier
    }
    Person: CommonMeshEntityOpts & {
        size?: number
        textures?: Partial<Cosmetics>
        pose?: PlayerPose
    }
    Leaderboard: LeaderboardMeshOpts
    ParticleEmitter: MeshParticleSystemOpts
}
CommonMeshEntityOpts#
TypeScript
Copy
type CommonMeshEntityOpts = {
    hideDist?: number
    meshOffset?: number[]
    autoRotate?: boolean
    lineToEId?: EntityId // EntityId to connect to using a line
}
MeshEntityPhysicsOpts#
TypeScript
Copy
type MeshEntityPhysicsOpts = {
    doPhysics: boolean
    onCollideTerrain?: () => void // Unsupported for custom code
    collidesEntities?: boolean
    collideBits?: number // bitmask category of this entity
    collideMask?: number // bitmask category of entities this entity collides with
    heightExpandAmt?: number // expand hitbox height by this amount
    widthExpandAmt?: number // expand hitbox width by this amount
}
AnimationSchema#
TypeScript
Copy
/**
 * ANIMATION SCHEMA TYPES
 *
 * An animation schema describes how an entity should be positioned as time passes.
 * For each node in the entity's skeleton, we define an animation timeline.
 * A timeline is sequence of "key frames".
 * A keyframe represents an important position; if this is a jumping animation,
 * then an example of a keyframe would be the peak of the jump.
 *
 * When deciding how an entity should be positioned during an animation,
 * we will usually find ourselves between two keyframes.
 * For example, if our keyframes are at time fractions 0.0, 0.5 and 1.0,
 * and the current time fraction is 0.3, then we will need to find a middle ground
 * between the first and second keyframe.
 * This process is known as interpolating, or "lerping".
 * The default way of doing this is linear lerping; drawing a straight line between two points.
 * An alternative is splining; drawing a curve.
 */
export type AnimationSchema = {
    animationDurationMs: number
    loop?: LoopModeSchema
    nodeAnimations?: NodeSkeletonAnimationSchema
}
LoopModeSchema#
TypeScript
Copy
type LoopModeSchema = boolean | "hold-on-last-frame"
NodeSkeletonAnimationSchema#
TypeScript
Copy
type NodeSkeletonAnimationSchema = Record<NodeName, NodeAnimationSchema>
NodeAnimationSchema#
TypeScript
Copy
type NodeAnimationSchema = {
    timeline: AnimationTimelineSchema
}
AnimationTimelineSchema#
TypeScript
Copy
type AnimationTimelineSchema = KeyframeSchema[]
KeyframeSchema#
TypeScript
Copy
type KeyframeSchema = {
    timeFraction: number
    rotation?: LerpPointSchema // Rotations are assumed to be in radians.
    position?: LerpPointSchema // Position offsets in mesh-local units; (0, 0, 0) means the node's rest pose.
}
LerpPointSchema#
TypeScript
Copy
/**
 * "pre" and "post" points exist to allow for discontinuities.
 */
export type LerpPointSchema =
    | Point
    | {
            lerpMode?: LerpModeSchema
            point: Point
      }
    | {
            lerpMode?: LerpModeSchema
            pre: Point // When lerping towards a point, we lerp towards its pre.
            post: Point // When lerping away from a point, we lerp away from its post.
      }
LerpModeSchema#
TypeScript
Copy
/**
 * "catmull-rom-spline" is a form of splining; drawing a curve between two points.
 */
export type LerpModeSchema = "linear" | "catmull-rom-spline"
BlockbenchAnimationSchema#
TypeScript
Copy
/**
 * BLOCKBENCH ANIMATION SCHEMA TYPES
 *
 * We support native Blockbench animations. It should just be a case of copying and pasting
 * the specific animation from the exported JSON file.
 *
 * Notable differences:
 * - Blockbench animations do not use time fractions. Instead, they use absolute time.
 * - The unit of time is seconds, not milliseconds.
 * - The angular unit is degrees, not radians.
 * - The x-axis is mirrored.
 */
export type BlockbenchAnimationSchema = {
    animation_length: number // The duration of the animation in seconds.
    loop?: BlockbenchLoopModeSchema
    bones?: BlockbenchBonesAnimationSchema
}
BlockbenchLoopModeSchema#
TypeScript
Copy
type BlockbenchLoopModeSchema = boolean | "hold_on_last_frame"
BlockbenchBonesAnimationSchema#
TypeScript
Copy
type BlockbenchBonesAnimationSchema = Record<NodeName, BlockbenchBoneAnimationSchema>
BlockbenchBoneAnimationSchema#
TypeScript
Copy
type BlockbenchBoneAnimationSchema = {
    rotation?: BlockbenchAnimationTimelineSchema // Blockbench rotations are in degrees.
    position?: BlockbenchAnimationTimelineSchema // Blockbench position offsets in mesh-local units; rest pose is (0, 0, 0).
}
BlockbenchAnimationTimelineSchema#
TypeScript
Copy
type BlockbenchAnimationTimelineSchema = Point | Record<TimestampString, BlockbenchAnimationFrameSchema>
BlockbenchAnimationFrameSchema#
TypeScript
Copy
/**
 * "pre" and "post" points exist to allow for discontinuities.
 */
export type BlockbenchAnimationFrameSchema =
    | Point
    | {
            lerp_mode?: BlockbenchLerpModeSchema
            pre?: Point // When lerping towards a point, we lerp towards its pre.
            post: Point // When lerping away from a point, we lerp away from its post.
      }
BlockbenchLerpModeSchema#
TypeScript
Copy
/**
 * "catmullrom" is a form of splining; drawing a curve between two points.
 */
export type BlockbenchLerpModeSchema = "linear" | "catmullrom"
TimestampString#
TypeScript
Copy
/**
 * The timestamp of the keyframe in seconds.
 */
type TimestampString = string
Point#
TypeScript
Copy
type Point = Vec3
CustomButtonType#
TypeScript
Copy
type CustomButtonType = {
    id: string // Identifier for the button. Used in the callbacks onPlayerPressedButton and onPlayerReleasedButton.
    icon: string // Icon to display for the button. Can be a font awesome icon such as "house" or a bloxd icon such as "Dirt".
    keycode: string // Key to trigger the button. Use a keycode like "KeyR" for the letter R. Allowed keys are letters ("KeyA" to "KeyZ"), the number row ("Digit0" to "Digit9"), arrow keys ("ArrowUp", "ArrowDown", "ArrowLeft", "ArrowRight") and "Space", shown as "_" next to the button. A key keeps its usual action too, so Space also jumps for players who have not changed their jump key.
    description?: string // Optional description for the button explaining what it does.
}
CustomButtonsType#
TypeScript
Copy
type CustomButtonsType = CustomButtonType[]
Previous
Client Options
Next
Entity Settings

---

## Entity Settings

URL: https://bloxd.io/docs/entity-settings

How one player sees and interacts with another entity.

19 settings

An "Entity Setting" impacts how a player sees or interacts with another player or entity. E.g. Player 1 could have an otherEntitySetting for entity 2 as opacity set to 0.5. This means player 1 sees entity 2 as partly see-through. Player1 is the relevant player, player2 is the targeted player. These API methods allow you to modify entity settings:

JavaScript
Copy
/**
 * Set every player's other-entity setting to a specific value for a particular entity.
 * includeNewJoiners=true means that new players joining the game will also have this other player setting applied.
 *
 * @param {EntityId} targetedPlayerId
 * @param {Setting} settingName
 * @param {OtherEntitySettings[Setting]} settingValue
 * @param {boolean} [includeNewJoiners]
 * @returns {void}
 */
setTargetedPlayerSettingForEveryone(targetedPlayerId, settingName, settingValue, includeNewJoiners)

/**
 * Set a player's other-entity setting for every player, mob and Person mesh in the game.
 * includeNewJoiners=true means that the player will have the setting applied to new joiners.
 *
 * @param {PlayerId} playerId
 * @param {Setting} settingName
 * @param {OtherEntitySettings[Setting]} settingValue
 * @param {boolean} [includeNewJoiners]
 * @returns {void}
 */
setEveryoneSettingForPlayer(playerId, settingName, settingValue, includeNewJoiners)

/**
 * Set a player's other-entity setting for a specific entity.
 *
 * @param {PlayerId} relevantPlayerId
 * @param {EntityId} targetedEntityId
 * @param {Setting} settingName
 * @param {OtherEntitySettings[Setting]} settingValue
 * @returns {void}
 */
setOtherEntitySetting(relevantPlayerId, targetedEntityId, settingName, settingValue)

/**
 * Set many of a player's other-entity settings for a specific entity.
 *
 * @param {PlayerId} relevantPlayerId
 * @param {EntityId} targetedEntityId
 * @param {Partial<OtherEntitySettings>} settingsObject
 * @returns {void}
 */
setOtherEntitySettings(relevantPlayerId, targetedEntityId, settingsObject)

/**
 * Get the value of a player's other-entity setting for a specific entity.
 *
 * @param {PlayerId} relevantPlayerId
 * @param {EntityId} targetedEntityId
 * @param {Setting} settingName
 * @returns {OtherEntitySettings[Setting]}
 */
getOtherEntitySetting(relevantPlayerId, targetedEntityId, settingName)

/**
 * Reset a player's other-entity setting for a specific entity to the game's default value.
 *
 * @param {PlayerId} relevantPlayerId
 * @param {EntityId} targetedEntityId
 * @param {Setting} settingName
 * @returns {void}
 */
setOtherEntitySettingToDefault(relevantPlayerId, targetedEntityId, settingName)
Show all 64 lines

Here is the full list of available entity settings:

alwaysInInterest#
Copy setter
TYPE
boolean
DEFAULT
false

Keep sending this entity to the player at any distance, for markers or objectives they follow from afar, once players are sent only the entities near them

canAttack#
Copy setter
TYPE
boolean
DEFAULT
false

Whether the relevant player can attack this entity, ignored if the entity is invincible. Also makes the entity pickable, so the player's aim lands on it - as does interactable, which is the setting to use for an entity that should be aimed at without being a valid target.

CHANGELOG
10th September 2026
canSee#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the entity can be seen by the relevant player

colorInLobbyLeaderboard#
Copy setter
TYPE
string
DEFAULT
""

The colour of the player in the lobby leaderboard.

hasPriorityNametag#
Copy setter
TYPE
boolean
DEFAULT
false

Whether the player has a priority name tag

interactable#
Copy setter
TYPE
boolean
DEFAULT
false

Whether alt actioning this entity (right click / the interact bind / a mobile tap) counts as interacting with it. When true the alt action is consumed, so a held block isn't placed through the entity and a held throwable isn't used, and onPlayerAltAction fires with it as the target. Leave false on decorative entities, or they will swallow player input.

Also makes the entity pickable, so an entity can be interactable without canAttack: the player's aim lands on it, but swinging or shooting at it does nothing.

Works on mobs too, taking priority over held items and native harvesting, riding and pet actions. Native action packets are also rejected by the server for interactable entities.

CHANGELOG
30th September 2026
10th September 2026
interactionPrompt#
Copy setter
TYPE
string | CustomTextStyling
DEFAULT
null

Replaces the label in the interaction prompt shown by the crosshair while the relevant player is looking at this entity, e.g. "Open Shop". Left null, the prompt reads "Interact". The engine draws the player's interact key next to it, so write what interacting does rather than which button to press. Only used on entities that have interactable set, and not shown on touchscreens, where there is no key to show.

CHANGELOG
10th September 2026
killfeedColour#
Copy setter
TYPE
string
DEFAULT
""

The colour of kills in the killfeed. Defaults to blue for themselves and red for everyone else.

lobbyLeaderboardTags#
Copy setter
TYPE
ChatTags
DEFAULT
null

The tags to the left of a player's name in the lobby leaderboard.

CHANGELOG
10th June 2026
lobbyLeaderboardValues#
Copy setter
TYPE
LobbyLeaderboardValues
DEFAULT
{}

The values of the leaderboard.

lockHeadToBody#
Copy setter
TYPE
boolean
DEFAULT
false

Whether the entity turns as one piece, so api.setEntityRotation sets where its whole body faces. Otherwise a mob or player-shaped entity turns its head first, and its body only follows once the head is turned past a limit.

Turning stays smooth. Works on mobs, players and Person mesh entities.

CHANGELOG
26th October 2026
meshScaling#
Copy setter
TYPE
EntityMeshScalingMap
DEFAULT
{}

Scaling of mesh nodes, see api.scalePlayerMeshNodes

multilineTextBox#
Copy setter
TYPE
MultilineTextBox
DEFAULT
null

Multiline text info for displaying text next to entities:

TypeScript
Copy
 {
     content: (CustomTextStyling[number] | RankInfo)[]    // Array of text content
     backgroundColor?: string                             // Background color
     animateIn?: boolean                                  // Whether text should animate in character-by-character
     visibleThroughWalls?: boolean                        // Overrides canSeeNametagsThroughWalls for this text: true draws it over blocks and entities, false lets them hide it
 }

Hidden whenever the entity's own mesh is, so a mesh entity's hideDist applies to its text too.

CHANGELOG
10th June 2026
nameColour#
Copy setter
TYPE
"default" | "yellow" | "lime" | "green" | "aqua" | "cyan" | "blue" | "purple" | "pink" | "red" | "orange"
DEFAULT
"default"

The colour of the entity's name.

nameTagInfo#
Copy setter
TYPE
NameTagInfo
DEFAULT
null

The name tag info of the player:

TypeScript
Copy
 {
     backgroundColor?: string
     content?: StyledText[]
     subtitle?: StyledText[]
     subtitleBackgroundColor?: string
     minLighting?: number
     healthbar?: { display?: "always" | "never" | "onDamage"; height?: FontSize; backgroundColour?: string; foregroundColour?: string | { healthFraction: number; colour: string }[] }
     border?: { colour: string; style?: "solid" | "glow" | "double"; width?: FontSize; applyTo?: "both" | "nametag" | "healthbar" }
 }
opacity#
Copy setter
TYPE
number
DEFAULT
1

Opacity of the entity

Fractional values will use dithering

0 opacity will hide the entity but not its name tag

overlayColour#
Copy setter
TYPE
string
DEFAULT
null

Applies a colour tint to the entity when set, like the red tint when an entity gets hurt.

showDamageAmounts#
Copy setter
TYPE
boolean
DEFAULT
true

Whether you can see damage amounts when shooting the entity

zIndex#
Copy setter
TYPE
0 | 1
DEFAULT
0

Rendering order of the entity, higher zIndex renders on top of lower ones.

Previous
Types
Next
Mob Settings

---

## Mob Settings

URL: https://bloxd.io/docs/mob-settings

Health, movement, combat and AI settings for mobs.

68 settings

These impact the behaviour of mobs, what they look like, and how they sound. These can either be set on a per-mob basis or the default can be set for all mobs of a particular type. These API methods allow you to modify mob settings:

JavaScript
Copy
/**
 * Returns the current default value for a mob setting.
 *
 * @param {TMobType} mobType
 * @param {TMobSetting} setting
 * @returns {MobSettings<TMobType>[TMobSetting]}
 */
getDefaultMobSetting(mobType, setting)

/**
 * Set the default value for a mob setting.
 *
 * @param {TMobType} mobType
 * @param {TMobSetting} setting
 * @param {MobSettings<TMobType>[TMobSetting]} value
 * @returns {void}
 */
setDefaultMobSetting(mobType, setting, value)

/**
 * Get the current value of a mob setting for a specific mob.
 *
 * @param {MobId} mobId
 * @param {TMobSetting} setting
 * @param {boolean} [returnDefaultIfNotOverridden] - If true, return the default setting if not overridden.
 * @returns {MobSettings<MobType>[TMobSetting]}
 */
getMobSetting(mobId, setting, returnDefaultIfNotOverridden)

/**
 * Set the current value of a mob setting for a specific mob.
 *
 * @param {MobId} mobId
 * @param {TMobSetting} setting
 * @param {MobSettings<MobType>[TMobSetting]} value
 * @returns {void}
 */
setMobSetting(mobId, setting, value)
Show all 38 lines

Here is the full list of available mob settings:

armour#
Copy setter
TYPE
Partial<Record<ArmourPart, {itemName: string, enchantmentTier?: "Tier 1" | "Tier 2" | "Tier 3" | "Tier 4" | "Tier 5" }>>
TypeScript
Copy
{
	"Helmet": {
		itemName: "Diamond Helmet",
		enchantmentTier: "Tier 5",
	},
	"Boots": {
		itemName: "Iron Boots",
	},
}
attackDamage#
Copy setter
TYPE
number
EXAMPLE
0
attackEffectDuration#
Copy setter
TYPE
number
EXAMPLE
0
attackEffectName#
Copy setter
TYPE
string
EXAMPLE
null
attackImpulse#
Copy setter
TYPE
number
EXAMPLE
0
attackInterval#
Copy setter
TYPE
number
EXAMPLE
0
attackItemName#
Copy setter
TYPE
string
EXAMPLE
null
attackRadius#
Copy setter
TYPE
number
EXAMPLE
0
attackSound#
Copy setter
TYPE
string
EXAMPLE
null
baseJumpImpulseXZ#
Copy setter
TYPE
number
EXAMPLE
0
baseJumpImpulseY#
Copy setter
TYPE
number
EXAMPLE
0
baseRunningSpeed#
Copy setter
TYPE
number
EXAMPLE
4.55 * 0.85
baseWalkingSpeed#
Copy setter
TYPE
number
EXAMPLE
3.5
bridgeInfo#
Copy setter
TYPE
MobBridgeInfo
TypeScript
Copy
{
	blockToPlace: "Grass",
	mustBeGrounded: false,
	yOffset: -1,
}

Makes the mob lay blocks into the world as it moves. If msToDecay is set to a number, and a |Decaying variant exists for blockToPlace, the trail/bridge will turn into air after msToDecay milliseconds.

CHANGELOG
13th July 2026
burstAttackInfo#
Copy setter
TYPE
{ burstAttackIntervals: number[]; }
EXAMPLE
null
chargeSpecialAttackInfo#
Copy setter
TYPE
MobChargeSpecialAttackInfo
EXAMPLE
{ chargeSpeedMult: 1.5 }
chaseRadius#
Copy setter
TYPE
number
EXAMPLE
0
combatTetherInfo#
Copy setter
TYPE
MobCombatTetherCombatInfo
TypeScript
Copy
{
	range: 11,
	particleOpts: {
		texture: "soul_0",
		colorGradients: [
			{
				timeFraction: 0,
				minColor: [245, 35, 25, 1],
				maxColor: [255, 45, 35, 1],
			},
		],
	},
}
evadeInfo#
Copy setter
TYPE
MobEvadeInfo
TypeScript
Copy
{
	probability: 0.6,
	minAngle: Math.PI * 0.35,
	maxAngle: Math.PI * 0.6,
	impulse: 8,
}
healthRegen#
Copy setter
TYPE
{ amount: number; interval: number; startAfter: number; }
EXAMPLE
null
heldItemEnchantmentTier#
Copy setter
TYPE
"Tier 1" | "Tier 2" | "Tier 3" | "Tier 4" | "Tier 5"
EXAMPLE
null
heldItemName#
Copy setter
TYPE
string
EXAMPLE
null
hostilityRadius#
Copy setter
TYPE
number
EXAMPLE
0
hurtSound#
Copy setter
TYPE
string
EXAMPLE
"pigHurt"
idleSound#
Copy setter
TYPE
string
EXAMPLE
"pigOink"
initialHealth#
Copy setter
TYPE
number
EXAMPLE
75
isReceivingDamageCooldownGlobal#
Copy setter
TYPE
boolean
EXAMPLE
true
isRideable#
Copy setter
TYPE
boolean
EXAMPLE
false
jumpCount#
Copy setter
TYPE
number
EXAMPLE
0
jumpMultiplier#
Copy setter
TYPE
number
EXAMPLE
1
knockbackReceivedMultiplier#
Copy setter
TYPE
number
EXAMPLE
1
maxFollowingRadius#
Copy setter
TYPE
number
EXAMPLE
12
maxHealth#
Copy setter
TYPE
number
EXAMPLE
75
metaInfo#
Copy setter
TYPE
string
EXAMPLE
""
minFollowingRadius#
Copy setter
TYPE
number
EXAMPLE
5
name#
Copy setter
TYPE
string
EXAMPLE
""
onDeathAura#
Copy setter
TYPE
number
EXAMPLE
20
onDeathItemDrops#
Copy setter
TYPE
{ itemName: string; probabilityOfDrop?: number; dropMinAmount?: number; dropMaxAmount?: number; applyBurstImpulseToDrop?: boolean; }[]
TypeScript
Copy
[
	{
		itemName: "Raw Porkchop",
		probabilityOfDrop: 1,
		dropMinAmount: 1,
		dropMaxAmount: 3,
	},
]
onDeathParticleTexture#
Copy setter
TYPE
string
EXAMPLE
"critical_hit"
onTamedHealthMultiplier#
Copy setter
TYPE
number
EXAMPLE
4.0
ownerDbId#
Copy setter
TYPE
string
EXAMPLE
null
petInfo#
Copy setter
TYPE
MobPetInfo
TypeScript
Copy
{
friendshipPoints: 0,
lastFedAt: null,
highestFriendshipLevelReached: 0,
superlikedFood: null,
superlikedFoodKnown: false,
bonusesGained: [],
	}
rangedAttackInaccuracy#
Copy setter
TYPE
number
EXAMPLE
0
ridingSpeedMult#
Copy setter
TYPE
number
EXAMPLE
1
runAwayRadius#
Copy setter
TYPE
number
EXAMPLE
0
runningJumpInfo#
Copy setter
TYPE
MobJumpLocomotionInfo
TypeScript
Copy
{
	// Combat / following: hop toward the target on a rested cadence (no slides, base speed 0).
	intervalBounds: { min: 600, max: 1_000 },
}
CHANGELOG
20th July 2026
runningRandomFacingInfo#
Copy setter
TYPE
MobRandomFacingInfo
TypeScript
Copy
{
	// Cosmetic only (via baseRenderHeading): jitter +-30 degrees, each equally likely, so it's harder to tell which way it's heading.
	offsets: [
		{ offset: Math.PI / 6, weight: 0.5 },
		{ offset: -Math.PI / 6, weight: 0.5 },
	],
	intervalBounds: { min: 1_000, max: 2_500 },
}
CHANGELOG
20th July 2026
runningSlideInfo#
Copy setter
TYPE
MobSlideLocomotionInfo
TypeScript
Copy
{
	// A combat dash to close on a target: initial speed = impulse / mass.
	impulse: 8,
	friction: 0.1,
	durationBounds: { min: 500, max: 900 },
	intervalBounds: { min: 1_000, max: 2_000 },
}
CHANGELOG
20th July 2026
runningSpeedMultiplier#
Copy setter
TYPE
number
EXAMPLE
1
secondaryAttackDamage#
Copy setter
TYPE
number
EXAMPLE
0
secondaryAttackImpulse#
Copy setter
TYPE
number
EXAMPLE
0
secondaryAttackItemName#
Copy setter
TYPE
string
EXAMPLE
null
secondaryAttackRadius#
Copy setter
TYPE
number
EXAMPLE
0
secondaryAttackSound#
Copy setter
TYPE
string
EXAMPLE
null
secondaryBurstAttackInfo#
Copy setter
TYPE
{ burstAttackIntervals: number[]; }
EXAMPLE
null
stoppingRadius#
Copy setter
TYPE
number
EXAMPLE
0.5
swingArmOnAttack#
Copy setter
TYPE
boolean
EXAMPLE
true
swingArmOnSecondaryAttack#
Copy setter
TYPE
boolean
EXAMPLE
true
tameInfo#
Copy setter
TYPE
PNull<MobTameInfo>
TypeScript
Copy
{
  "tameItemName": [
    "Apple"
  ],
  "probabilityOfTame": 1,
  "isSaddleable": false,
  "supportsFriendship": true,
  "likedFoods": [
    "Plum",
    "Cracked Coconut",
    "Pumpkin Pie",
    "Bowl of Rice",
    "Melon Slice",
    "Gold Melon Slice",
    "Corn",
    "Bowl of Cranberries",
    "Mushroom Soup",
    "Chili Pepper",
    "Carrot",
    "Beetroot",
    "Raw Potato",
    "Baked Potato"
  ],
  "neutralFoods": [
    "Watermelon Slice",
    "Gold Watermelon Slice",
    "Apple",
    "Wheat",
    "Pear",
    "Cherry",
    "Bread"
  ],
  "dislikedFoods": [
    "Raw Porkchop",
    "Raw Beef",
    "Raw Mutton",
    "Raw Venison",
    "Cooked Porkchop",
    "Steak",
    "Cooked Mutton",
    "Cooked Venison",
    "Rotten Flesh",
    "Banana",
    "Rotten Brain"
  ],
  "guaranteedDrop": "Truffle",
  "commonDrops": [
    "Poop",
    "Wheat Seeds"
  ],
  "levelUpBonuses": {
    "1": "Renaming",
    "2": "Special Drops",
    "3": "Double Poop",
    "4": "Painting",
    "5": "Feed Aura"
  }
}
Show all 58 lines

Taming configuration for this mob type. Includes tame items, probability, saddle support, food preferences, drops, and level-up bonuses. See mobTameInfoDefaults for per-mob defaults. null for non-tameable mobs.

territoryRadius#
Copy setter
TYPE
number
EXAMPLE
0
variation#
Copy setter
TYPE
"default"
EXAMPLE
"default"
walkingJumpInfo#
Copy setter
TYPE
MobJumpLocomotionInfo
TypeScript
Copy
{
	// Wander hops; paired with walkingSlideInfo below for a lively mix of hops and slower slides.
	intervalBounds: { min: 600, max: 1_500 },
}
CHANGELOG
20th July 2026
walkingRandomFacingInfo#
Copy setter
TYPE
MobRandomFacingInfo
TypeScript
Copy
{
	// Cosmetic only (via baseRenderHeading): face mostly backwards, sometimes sideways, occasionally forwards.
	offsets: [
		{ offset: Math.PI, weight: 0.5 },
		{ offset: Math.PI / 2, weight: 0.15 },
		{ offset: (3 * Math.PI) / 2, weight: 0.15 },
		{ offset: 0, weight: 0.2 },
	],
	intervalBounds: { min: 2_000, max: 5_000 },
}
CHANGELOG
20th July 2026
walkingSlideInfo#
Copy setter
TYPE
MobSlideLocomotionInfo
TypeScript
Copy
{
	// Initial slide speed = impulse / mass; friction (far below the default mob 1.5) governs the coast.
	impulse: 6,
	friction: 0.1,
	durationBounds: { min: 850, max: 1_500 },
	// Longer interval bounds for sliding than hopping makes hopping the dominant behaviour.
	intervalBounds: { min: 1_500, max: 3_000 },
}
CHANGELOG
20th July 2026
walkingSpeedMultiplier#
Copy setter
TYPE
number
EXAMPLE
1
warpTargetSpecialAttackInfo#
Copy setter
TYPE
MobWarpTargetSpecialAttackInfo
TypeScript
Copy
{
	cooldown: 20_000,
	range: 32,
	sound: "warperPhase",
	delay: 1_000,
	minDestinationRadius: 5,
	maxDestinationRadius: 7,
	swingArm: false,
	particleOpts: {
		duration: 2_000,
		texture: "soul_0",
		colorGradients: [
			{
				timeFraction: 0,
				minColor: [70, 215, 230, 1],
				maxColor: [75, 225, 240, 1],
			},
		],
	},
}
Mob Variations#

Some mob types support variations other than just "default":

JavaScript
Copy
67: "default"
Pig: "default"
Cow: "default", "cream"
Sheep: "default", "black", "red", "orange", "pink", "purple", "yellow", "blue", "brown", "cyan", "gray", "green", "lightBlue", "lightGray", "lime", "magenta"
Horse: "default", "black", "brown", "cream"
Camel: "default", "brown"
Slime: "default"
Cave Golem: "default", "iron", "corrupted"
Draugr Zombie: "default", "longHairChestplate", "longHairClothed", "shortHairClothed", "flower", "flower2", "mushroom", "vine", "vine2", "corrupted", "corrupted2"
Draugr Skeleton: "default"
Frost Golem: "default"
Frost Zombie: "default", "longHairChestplate", "shortHairClothed"
Frost Skeleton: "default"
Draugr Knight: "default"
Wolf: "default", "white", "brown", "grey", "spectral"
Bear: "default"
Deer: "default"
Stag: "default"
Gold Watermelon Stag: "default"
Gorilla: "default"
Wildcat: "default", "tabby", "grey", "black", "calico", "siamese", "leopard"
Magma Golem: "default"
Draugr Huntress: "default", "chainmail"
Spirit Golem: "default"
Spirit Wolf: "default"
Spirit Bear: "default"
Spirit Stag: "default"
Spirit Gorilla: "default"
Draugr Warper: "default"
Frost Wraith: "default", "tattered", "frostKing", "accursed"
Draugr Reaver: "default"
Stalker: "default", "crimson", "frost", "void"
Crone: "default"
Iron Guardian: "default"
Gold Guardian: "default"
Diamond Guardian: "default"
Moonstone Guardian: "default"
Iron Goofy Golem: "default", "flaking", "patchy", "shedding", "bare", "stone"
Gold Goofy Golem: "default", "flaking", "patchy", "shedding", "bare", "stone"
Diamond Goofy Golem: "default", "flaking", "patchy", "shedding", "bare", "stone"
Moonstone Goofy Golem: "default", "flaking", "patchy", "shedding", "bare", "stone"
Tiki Terror: "default", "titan", "tormentor", "tyrant"
NPC: "default", "emma", "leo", "isabel", "sanjay", "imara", "enoch", "sara", "carmen", "chef"
Bobino Musculino: "default"
Capitano Explovissimo: "default"
Desert Fennec: "default"
Armour Collector: "default"
Furnace Knight: "default"
Lil Knight: "default"
Glass Gremlin: "default"
Glass Bro: "default"
Lord Vulcan: "default"
Zombie: "default"
Skeleton: "default"
Mummy: "default"
Scorpion: "default"
Vulcanite: "default"
Evil Tome: "default"
Magma Toad: "default"
Show all 59 lines
Mob AI#

A mob's AI state determines its behaviour, e.g.: whether it is stood still, walking in a straight line, chasing someone, running towards a coordinate, etc. These API methods allow you to modify a mob's AI state:

JavaScript
Copy
/**
 * Gets the current AI state for the given mob.
 *
 * @param {MobId} mobId
 * @returns { { state: MobAiState; params: MobAiStateParams<MobAiState> } }
 */
getMobAiState(mobId)

/**
 * Sets the current AI state for the given mob.
 * Some AI states will require context such as the ID of the lifeform being chased.
 * The mob's AI normally moves on by itself after a few seconds, or when a player comes near.
 * Pass `{ hold: true }` to keep it in this state until you set another one.
 *
 * @param {MobId} mobId
 * @param {TState} state
 * @param {MobAiStateParams<TState>} params
 * @param {MobAiStateOptions} [opts] - hold: never time out, ignore nearby players and don't fight back when hit. The mob still leaves the state if its target leaves the game or turns invisible, or if it is tamed.
 * @returns {void}
 */
setMobAiState(mobId, state, params, opts)

Here is the full list of available mob AI states and their parameters:

State	Description	Parameters
idle	The mob is stood still, but it still has awareness of its environment.<br>For example: if the mob is hostile, it will still chase and attack nearby players.	null
disabled	The mob is stood still, and it has no awareness of its environment.<br>It will not even react if provoked.	null
idleBeforeTurning	The mob is stood still (idle) and is about to turn.	null
turning	The mob has chosen a new direction at random and is turning to face it.	null
idleBeforeWalking	The mob is stood still (idle) and is about to walk.	null
walking	The mob is walking in the direction it is facing.	null
runningAway	The mob is running away from the target lifeform.	{ targetId: LifeformId }
chasing	The mob is chasing the target lifeform.	{ targetId: LifeformId }
turningBeforeCharging	A charge-attack mob is stood still, rotating at its turnRate until it faces the target,<br>at which point it captures the target's current position and transitions to charging.	{ targetId: LifeformId }
charging	A charge-attack mob is dashing straight at the position of the target captured when it<br>entered the state, ignoring the target's live position mid-dash (so the charge is dodgeable).	{ targetId: LifeformId }
following	The mob is following the target lifeform.<br>It will stop if it is within the minFollowingDistance (mob setting) of the target,<br>and teleport to the target if it is outside the maxFollowingDistance (mob setting) of the target.	{ targetId: LifeformId }
watching	The mob is stood still looking at the target.	{ targetId: LifeformId }
walkingToPosition	The mob is walking towards the position.<br>It will stop if it is within the stoppingRadius (mob setting) of the position.	{ pos: Pos }
runningToPosition	The mob is running towards the position.<br>It will stop if it is within the stoppingRadius (mob setting) of the position.	{ pos: Pos }
Previous
Entity Settings
Next
Vehicle Settings

---

## Vehicle Settings

URL: https://bloxd.io/docs/vehicle-settings

Movement, physics and camera settings for vehicles.

40 settings

A vehicle is something you get into and ride, like a boat or a kart. A physics type is a list of settings describing how something moves - its weight, speed, steering, and so on. The two are separate: riding a vehicle normally changes your physics type, but a player can be given one without riding anything.

Each setting's value is resolved in three steps:

The defaults, which are the same for everything.
The physics type (e.g. CAR) changes some of them.
The tier (e.g. OFF_ROADER) changes a few more.

One vehicle can also be given its own value for a setting, which beats all three - but only for whoever rides it.

A few settings (canAutoStep, speedMultiplier) can be given a value for one block at a time as well, by naming the block first - "IceCanAutoStep". That applies whenever the rider is stood on that block.

These API methods spawn vehicles and change how a player moves:

JavaScript
Copy
/**
 * Set physics state of player (vehicle type and tier).
 *
 * For types that have tiers (e.g. BOAT, GLIDER, CAR), a `tier` of `null` defaults to the first
 * tier (0). Types without tiers (e.g. DEFAULT) must be given a `null` tier.
 *
 * @param {PlayerId} playerId
 * @param {PlayerPhysicsState<PhysicsType>} physicsState
 * @param {[number, number, number]} [positionOffset] - Optional offset to adjust the player's collision box
 * @returns {void}
 */
setPlayerPhysicsState(playerId, physicsState, positionOffset)

/**
 * Get physics state for player
 *
 * @param {PlayerId} playerId
 * @returns {PlayerPhysicsState<PhysicsType>}
 */
getPlayerPhysicsState(playerId)

/**
 * Seat a player in a vehicle. Seat 0 drives; other seats follow the vehicle without movement control.
 * The player leaves their current vehicle and replaces anyone occupying the requested seat.
 *
 * @param {PlayerId} playerId
 * @param {EntityId} vehicleEId - A spawned vehicle or a rideable mob.
 * @param {number} [seatIndex] - Seat index (default 0).
 * @returns {void}
 */
setPlayerVehicle(playerId, vehicleEId, seatIndex)

/**
 * Take a player off whatever they are riding, dropping them where it is. Does nothing if they are
 * not riding anything.
 *
 * @param {PlayerId} playerId
 * @returns {void}
 */
exitPlayerVehicle(playerId)

/**
 * The seat layout for a vehicle entity - at minimum one driver seat (index 0), optionally more
 * passenger seats after it. Resolved from the spawned vehicle's def (`VehicleMeshEntityDef.seats`,
 * falling back to a single driver seat at the physics type/tier's own `riderOffset` default) or a
 * rideable mob's override (`getMobVehicleSeats`, falling back to its `rideHeight`). Throws if
 * `vehicleEId` is not a vehicle.
 *
 * @param {EntityId} vehicleEId
 * @returns {VehicleSeat[]}
 */
getVehicleSeats(vehicleEId)

/**
 * The current value of a physics setting for a specific vehicle entity: the value set via
 * `setVehicleSetting` if overridden, otherwise (when `returnDefaultIfNotOverridden`) the type/tier
 * default from the vehicle's physics state. Mirrors `getMobSetting`.
 *
 * The one default not read from the type/tier is a mob's `riderOffset`, which comes from its ride height.
 *
 * A per-block setting (e.g. `"IceCanAutoStep"`) is `undefined` when that block is unlisted, which means
 * the block does not change the setting rather than that the setting is off.
 *
 * @param {EntityId} vehicleEId
 * @param {TSetting} setting
 * @param {boolean} [returnDefaultIfNotOverridden]
 * @returns {SettableVehicleSettingValue<TSetting>}
 */
getVehicleSetting(vehicleEId, setting, returnDefaultIfNotOverridden)

/**
 * Override a physics setting for a specific vehicle entity, replacing the type/tier default for that
 * vehicle's rider. The override is stored on the shared Bloxd and, when the vehicle currently has a
 * rider, replicated to that rider's client. Mirrors `setMobSetting`.
 *
 * A setting can also be overridden for one block by naming the block first, e.g.
 * `setVehicleSetting(boatId, "IceCanAutoStep", true)`. That is stored as an entry of the matching
 * `<setting>ByBlock` record, which the physics tick reads as a precomputed block lookup.
 *
 * @param {EntityId} vehicleEId
 * @param {TSetting} setting
 * @param {SettableVehicleSettingValue<TSetting>} value
 * @returns {void}
 */
setVehicleSetting(vehicleEId, setting, value)

/**
 * Try to spawn a rideable vehicle, which players can mount with an alt action.
 * There is a limit to the number of mesh entities with physics that can be created.
 * WARNING: Either the "onPlayerAttemptSpawnVehicle" or the "onWorldAttemptSpawnVehicle" game callback will be called
 * depending on whether "spawnerId" is provided. Calling this function inside those callbacks risks infinite recursion.
 *
 * @param {MeshEntityVehicleType} vehicleType
 * @param {number} x
 * @param {number} y
 * @param {number} z
 * @param {VehicleSpawnOpts} [opts] - Includes:
 * - spawnerId The ID of the player who spawned the vehicle. The vehicle faces away from them.
 * @returns {PNull<EntityId>} - null if the vehicle could not be spawned, otherwise the entity ID of the vehicle.
 */
attemptSpawnVehicle(vehicleType, x, y, z, opts)

/**
 * Dispose of a vehicle's state and remove them from the world.
 * Always succeeds.
 *
 * @param {EntityId} vehicleId
 * @returns {void}
 */
despawnVehicle(vehicleId)
Show all 110 lines
Vehicle Catalogue#
Mesh-Entity Vehicles#

Objects placed in the world, which a player walks up to and climbs into. Use attemptSpawnVehicle to make one.

Vehicles	Physics	Placeable on	Mesh size	Place sound
Boat	BOAT / WOOD	Water, Lava	1.2	splash1
Obsidian Boat	BOAT / OBSIDIAN	Water, Lava	1.2	splash1
Speedboat	BOAT / SPEED	Water	1.2	splash1
Hovercraft	HOVERCRAFT	solidBlocksOrFluid	4	depends on the block it is put on
Yellow Kart, White Kart, Red Kart, Purple Kart, Pink Kart, Orange Kart, Magenta Kart, Lime Kart, Light Gray Kart, Light Blue Kart, Green Kart, Gray Kart, Cyan Kart, Brown Kart, Blue Kart, Black Kart	CAR / KART	solidBlocks	4	depends on the block it is put on
Off Roader	CAR / OFF_ROADER	solidBlocks	4	depends on the block it is put on
Gold Mining Drill	CAR / GOLD_MINING_DRILL	solidBlocks	4	depends on the block it is put on
Iron Mining Drill	CAR / IRON_MINING_DRILL	solidBlocks	4	depends on the block it is put on
Diamond Mining Drill	CAR / DIAMOND_MINING_DRILL	solidBlocks	4	depends on the block it is put on
Moonstone Mining Drill	CAR / MOONSTONE_MINING_DRILL	solidBlocks	4	depends on the block it is put on
Armored Car	CAR / ARMORED_CAR	solidBlocks	4	depends on the block it is put on
Light Blue Car	CAR / CAR	solidBlocks	4	depends on the block it is put on
Consumable Vehicles#

Nothing is placed in the world: the player's own movement changes and the vehicle appears attached to their body. Using the item consumes one, and the ride ends once the player stops floating.

Vehicles	Physics	Mesh attachment
Yellow Balloon	BALLOON / YELLOW	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
White Balloon	BALLOON / WHITE	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Red Balloon	BALLOON / RED	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Purple Balloon	BALLOON / PURPLE	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Pink Balloon	BALLOON / PINK	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Orange Balloon	BALLOON / ORANGE	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Magenta Balloon	BALLOON / MAGENTA	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Lime Balloon	BALLOON / LIME	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Light Gray Balloon	BALLOON / LIGHT_GRAY	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Light Blue Balloon	BALLOON / LIGHT_BLUE	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Green Balloon	BALLOON / GREEN	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Gray Balloon	BALLOON / GRAY	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Cyan Balloon	BALLOON / CYAN	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Brown Balloon	BALLOON / BROWN	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Blue Balloon	BALLOON / BLUE	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Black Balloon	BALLOON / BLACK	{ size: 0.12, offset: [0, 1.8, -0.24], rotation: [0, 0, 0] }
Held Vehicles#

Also attached to the player rather than placed in the world. Active for as long as the matching item is held - swap to something else and the ride ends.

Vehicles	Physics	Mesh attachment
Wood Hang Glider	GLIDER / WOOD	{ size: 3, offset: [0, 0.72, 0.3], rotation: [-1.5708, 3.14159, 3.14159] }
Iron Hang Glider	GLIDER / IRON	{ size: 3, offset: [0, 0.72, 0.3], rotation: [-1.5708, 3.14159, 3.14159] }
Gold Hang Glider	GLIDER / GOLD	{ size: 3, offset: [0, 0.72, 0.3], rotation: [-1.5708, 3.14159, 3.14159] }
Diamond Hang Glider	GLIDER / DIAMOND	{ size: 3, offset: [0, 0.72, 0.3], rotation: [-1.5708, 3.14159, 3.14159] }

Every vehicle setting and the default it starts from. Valid pose values are listed in SKINS_AND_POSES.md, and valid effect.icon values in ICONS.md.

Each example changes the setting on one vehicle, where the id came from attemptSpawnVehicle.

airborneFallSpeedLimit#
Copy setter
TYPE
PNull<FallSpeedLimitOpts>
DEFAULT
null

Caps how fast it falls while flying. Only used when airborneMovement is "heading". null = it falls at full speed. See FallSpeedLimitOpts.

JavaScript
Copy
// A flying hovercraft that drifts down at 4 blocks a second instead of dropping
api.setVehicleSetting(hovercraftId, "airborneMovement", { model: "heading" })
api.setVehicleSetting(hovercraftId, "airborneFallSpeedLimit", { maxFallSpeed: 4, slowDownSeconds: 0.15, compensateGravity: true })
airborneMode#
Copy setter
TYPE
PNull<AirborneModeOpts>
DEFAULT
null

Lets it fly once mid-air and descending. Supported movement types: GLIDING and FLOATING. null = it cannot fly. See AirborneModeOpts.

JavaScript
Copy
// Give a hovercraft a glider mode, so driving off a cliff becomes a flight
api.setVehicleSetting(hovercraftId, "airborneMode", { activeMovementType: MovementType.GLIDING, durationMs: null, exitsVehicleOnEnd: false })
airborneMovement#
Copy setter
TYPE
PNull<AirborneMovementOpts>
DEFAULT
null

How it moves while flying. null = it steers the same way it does on the ground. See AirborneMovementOpts.

JavaScript
Copy
// Make a flying hovercraft follow the camera, like a glider
api.setVehicleSetting(hovercraftId, "airborneMovement", {
    model: "cameraDirection",
    maxSpeed: 13,
    minSpeed: 0.5,
    pitchAcceleration: 0.0125,
    friction: 0,
    impulseDecayTicks: 100,
    biasMagnitude: 1.5,
    excessVelocityBleedPerTick: 0.5,
})
airSpeedMultiplier#
Copy setter
TYPE
number
DEFAULT
1

An extra speed multiplier used while in the air.

JavaScript
Copy
// A kart that barely steers while mid-jump
api.setVehicleSetting(kartId, "airSpeedMultiplier", 0.2)
canAutoStep#
Copy setter
TYPE
boolean
DEFAULT
true

Can also be set for a single block - see {BlockName}CanAutoStep.

Whether it climbs one-block steps by itself, rather than the rider jumping them.

JavaScript
Copy
// Make riders jump every kerb instead of rolling over it
api.setVehicleSetting(carId, "canAutoStep", false)
{BlockName}CanAutoStep#
Copy setter
TYPE
boolean
DEFAULT
unset - only the blocks a physics type lists in its `canAutoStepByBlock` below start with a value of their own.

Named as the block followed by the setting: "IceCanAutoStep", "Red ConcreteCanAutoStep".

Overrides canAutoStep for particular blocks, by block name. Unlisted blocks use canAutoStep.

JavaScript
Copy
// A boat that rides up onto ice, but nothing else
api.setVehicleSetting(boatId, "canAutoStep", false)
api.setVehicleSetting(boatId, "IceCanAutoStep", true)
canRun#
Copy setter
TYPE
boolean
DEFAULT
true

Whether the rider is allowed to sprint.

JavaScript
Copy
// Let riders sprint a kart, on top of its own speed
api.setVehicleSetting(kartId, "canRun", true)
disableBaseMovement#
Copy setter
TYPE
boolean
DEFAULT
false

Turns off the usual steering-driven movement, as for a sleeping player.

JavaScript
Copy
// A ghost train: riders cannot steer at all
api.setVehicleSetting(kartId, "disableBaseMovement", true)
disableFootstepSounds#
Copy setter
TYPE
boolean
DEFAULT
false

Whether footstep sounds are silenced.

JavaScript
Copy
// Turn footsteps back on for a kart
api.setVehicleSetting(kartId, "disableFootstepSounds", false)
effect#
Copy setter
TYPE
PNull<{ name: string; icon: string; duration?: number }>
DEFAULT
null

A badge shown to the rider for as long as they ride. null = none. icon is an ingame icon or an item name. name must be one that a physics type already uses, such as "Driving" or "Boating", because only those are cleared again when the rider gets off.

JavaScript
Copy
// Badge a kart with the off-roader icon instead of the usual kart one
api.setVehicleSetting(kartId, "effect", { name: "Driving", icon: "Off Roader" })
fixedHeading#
Copy setter
TYPE
PNull<number>
DEFAULT
null

Locks the direction it faces, in radians, ignoring the camera. null = it faces wherever the camera or steering points.

JavaScript
Copy
// Pin a boat to one direction, whichever way the rider looks
api.setVehicleSetting(boatId, "fixedHeading", Math.PI / 2)
fluidDrag#
Copy setter
TYPE
number
DEFAULT
-1

How much water and lava slow it down. -1 uses the world's normal drag.

JavaScript
Copy
// A boat that wallows through water
api.setVehicleSetting(boatId, "fluidDrag", 8)
fluidDragHorizontal#
Copy setter
TYPE
number
DEFAULT
-1

fluidDrag for sideways movement only. -1 falls back to fluidDrag.

JavaScript
Copy
// Let a car skate across water instead of bogging down in it
api.setVehicleSetting(carId, "fluidDragHorizontal", 0)
fluidDragVertical#
Copy setter
TYPE
number
DEFAULT
-1

fluidDrag for up-and-down movement only. -1 falls back to fluidDrag.

JavaScript
Copy
// A boat that sinks and surfaces slowly instead of bobbing
api.setVehicleSetting(boatId, "fluidDragVertical", 6)
fluidSkip#
Copy setter
TYPE
PNull<FluidSkipOpts>
DEFAULT
null

Makes it skip across water like a stone once it is fast enough. null = it floats normally. See FluidSkipOpts.

JavaScript
Copy
// Let any boat skim across water like a stone
api.setVehicleSetting(boatId, "fluidSkip", { minSpeed: 11, launchSpeedFraction: 0.4, launchApproachRate: 25 })
fluidSpeedMultiplier#
Copy setter
TYPE
number
DEFAULT
1

An extra speed multiplier used while in water or lava.

JavaScript
Copy
// An amphibious kart, as quick in water as on the road
api.setVehicleSetting(kartId, "fluidSpeedMultiplier", 1)
gravityMultiplier#
Copy setter
TYPE
number
DEFAULT
2

How hard gravity pulls it down, compared to a normal player. 0 = it never falls.

JavaScript
Copy
// A moon-buggy kart that hangs in the air after every jump
api.setVehicleSetting(kartId, "gravityMultiplier", 0.5)
height#
Copy setter
TYPE
number
DEFAULT
1.8

How tall it is, in blocks.

JavaScript
Copy
// A low-slung go-kart that fits under two-block tunnels
api.setVehicleSetting(kartId, "height", 0.9)
horizontalBounciness#
Copy setter
TYPE
number
DEFAULT
0

How bouncy walls are: 0 stops dead, 1 keeps all its speed. Stacks with the bounciness client option. Rebounds have a floor speed, so slow bumps come back faster than they arrived.

JavaScript
Copy
// A bumper car that pings off walls instead of stopping dead
api.setVehicleSetting(kartId, "horizontalBounciness", 0.8)
horizontalImpactCameraShake#
Copy setter
TYPE
PNull<ImpactCameraShakeOpts>
DEFAULT
null

Shakes the camera when it hits a wall hard enough; it need not bounce. null = no shake. See ImpactCameraShakeOpts.

JavaScript
Copy
// Rattle the screen when a car wraps itself round a wall
api.setVehicleSetting(carId, "horizontalImpactCameraShake", { minSpeed: 6, intensityPerSpeed: 0.03, maxIntensity: 0.6, durationMs: 300 })
jumpMultiplier#
Copy setter
TYPE
number
DEFAULT
1

How hard the rider pushes off the ground when jumping, compared to a normal jump. 0 = cannot jump. Multiplies the jumpAmount client option rather than replacing it, and heavier types need a bigger value to reach the same height.

JavaScript
Copy
// A stunt kart with a much springier jump
api.setVehicleSetting(kartId, "jumpMultiplier", 5)
landSpeedMultiplier#
Copy setter
TYPE
number
DEFAULT
1

An extra speed multiplier used while on solid ground.

JavaScript
Copy
// A boat that drags itself along dry land at a tenth speed
api.setVehicleSetting(boatId, "landSpeedMultiplier", 0.1)
mass#
Copy setter
TYPE
number
DEFAULT
1

How heavy it is. Heavier things resist being pushed around, and sink rather than float.

JavaScript
Copy
// A featherweight kart that every explosion sends flying
api.setVehicleSetting(kartId, "mass", 0.3)
maxPushDistance#
Copy setter
TYPE
number
DEFAULT
0

Caps how hard it is pushed while far below the speed it is aiming for, so it takes longer to get going. 0 = no cap.

JavaScript
Copy
// A heavy lorry takes its time getting up to speed; a nippy racecar has no cap at all
api.setVehicleSetting(lorryId, "maxPushDistance", 2)
api.setVehicleSetting(raceCarId, "maxPushDistance", 0)
minHorizontalSpeedToBounce#
Copy setter
TYPE
number
DEFAULT
0

How fast it must hit a wall, in blocks per second, before horizontalBounciness applies. 0 = any contact.

JavaScript
Copy
// Only bounce off walls hit at speed, not gentle scrapes
api.setVehicleSetting(kartId, "minHorizontalSpeedToBounce", 8)
minVerticalSpeedToBounce#
Copy setter
TYPE
number
DEFAULT
0

How fast it must be falling, in blocks per second, before verticalBounciness applies. 0 bounces off any contact, leaving a bouncy vehicle jiggling in place.

JavaScript
Copy
// Bounce off big drops only, so a parked kart sits still
api.setVehicleSetting(kartId, "minVerticalSpeedToBounce", 5)
movementForceMultiplier#
Copy setter
TYPE
number
DEFAULT
1

How hard steering pushes it. Bigger = it speeds up and changes direction more sharply.

JavaScript
Copy
// A twitchy kart that reaches top speed almost instantly
api.setVehicleSetting(kartId, "movementForceMultiplier", 2)
pose#
Copy setter
TYPE
PlayerPose
DEFAULT
"standing"

How the rider's body is posed while riding.

JavaScript
Copy
// Riders lie back in this boat instead of sitting up
api.setVehicleSetting(boatId, "pose", "sleeping")
riderOffset#
Copy setter
TYPE
[number, number, number]
DEFAULT
[0, 0, 0]

Where the rider sits, as [x, y, z] blocks from the middle of the vehicle. A rideable mob defaults to its own ride height rather than to this type's value.

JavaScript
Copy
// Sit the rider further back, as if in the boot
api.setVehicleSetting(carId, "riderOffset", [0, 0.25, -0.8])
speedMultiplier#
Copy setter
TYPE
number
DEFAULT
1

Can also be set for a single block - see {BlockName}SpeedMultiplier.

Its top speed, as a multiplier on normal walking speed. 0 = it cannot move.

JavaScript
Copy
// Double a kart's top speed for a boost pickup
api.setVehicleSetting(kartId, "speedMultiplier", 24)
{BlockName}SpeedMultiplier#
Copy setter
TYPE
number
DEFAULT
unset - only the blocks a physics type lists in its `speedMultiplierByBlock` below start with a value of their own.

Named as the block followed by the setting: "IceSpeedMultiplier", "Red ConcreteSpeedMultiplier".

Extra speed multipliers for the block underfoot, by block name. Solid ground only, and stacks with speedMultiplier and the land/fluid/air multiplier. When several listed blocks are underfoot, the value furthest from 1 wins.

JavaScript
Copy
// A car that crawls through snow and flies down stone roads
api.setVehicleSetting(carId, "SnowSpeedMultiplier", 0.4)
api.setVehicleSetting(carId, "StoneSpeedMultiplier", 1.5)
standingFriction#
Copy setter
TYPE
number
DEFAULT
5

How quickly it slows to a stop once the rider stops steering. Bigger = stops sooner.

JavaScript
Copy
// An icy kart that slides on after the rider stops steering
api.setVehicleSetting(kartId, "standingFriction", 0.2)
steering#
Copy setter
TYPE
PNull<SteeringOpts>
DEFAULT
null

Makes it steer like a car: left and right turn it rather than sliding it sideways. null moves freely in any direction, like a walking player. See SteeringOpts.

JavaScript
Copy
// A drift kart: quick to turn, but the back end steps out on every corner
api.setVehicleSetting(kartId, "steering", { turnRate: 3.5, corneringSpeedDamping: 0.1, gripStrength: 2, gripInFluid: false })
upwardImpulseOnUse#
Copy setter
TYPE
number
DEFAULT
0

Cannot be changed for a single vehicle - it is always read from the physics type's own values.

An upward shove the moment the rider uses the vehicle, like a balloon lifting off. 0 = none.

JavaScript
Copy
// In physics/settings/*.ts: a balloon that launches its rider higher
upwardImpulseOnUse: 30
verticalBounciness#
Copy setter
TYPE
number
DEFAULT
0

How bouncy the floor is: 0 lands flat, 1 bounces back as fast as it fell. Stacks with the bounciness client option, and has the same rebound floor as horizontalBounciness.

JavaScript
Copy
// A space hopper kart that bounces every time it lands
api.setVehicleSetting(kartId, "verticalBounciness", 0.7)
verticalImpactCameraShake#
Copy setter
TYPE
PNull<ImpactCameraShakeOpts>
DEFAULT
null

Shakes the camera when it hits a floor or ceiling hard enough; it need not bounce. null = no shake. See ImpactCameraShakeOpts.

JavaScript
Copy
// A bone-shaking thump when an off-roader lands a big jump
api.setVehicleSetting(offRoaderId, "verticalImpactCameraShake", { minSpeed: 3, intensityPerSpeed: 0.05, maxIntensity: 1, durationMs: 400 })
width#
Copy setter
TYPE
number
DEFAULT
0.5

How wide it is, in blocks.

JavaScript
Copy
// A monster truck too wide for one-block alleys
api.setVehicleSetting(offRoaderId, "width", 1.2)
Physics Type Defaults#

Only the changes are shown - anything not listed keeps the value from the step before.

DEFAULT#

A player walking around on foot. Every other type starts from these values.

Uses the default values, with nothing changed.

BOAT#

Floats on water and slides over ice. The fast tier can steer, and skips along the surface like a stone.

TypeScript
Copy
mass: 0.25
fluidDrag: 2
fluidDragHorizontal: 0
fluidDragVertical: 2
height: 1.2
canRun: false
jumpMultiplier: 0
canAutoStep: false
canAutoStepByBlock: {
    Ice: true,
    "Ice Bricks": true,
    "Ice Bricks Slab": true,
    "Melting Ice": true,
    "Melting Ice|Breaking": true,
}
pose: "sitting"
effect: { name: "Boating", icon: "Boating" }
standingFriction: 0.4
speedMultiplier: 0.25
fluidSpeedMultiplier: 40
airSpeedMultiplier: 32
speedMultiplierByBlock: { Ice: 40, "Ice Bricks": 40, "Ice Bricks Slab": 40, "Melting Ice": 40, "Melting Ice|Breaking": 40 }
maxPushDistance: 7.3
movementForceMultiplier: 0.03
disableFootstepSounds: true
Tier WOOD#

The same as BOAT above, with nothing changed.

Tier OBSIDIAN#
TypeScript
Copy
effect: { name: "Boating", icon: "Obsidian Boating" }
Tier SPEED#
TypeScript
Copy
fluidDragVertical: 1
fluidSpeedMultiplier: 60
airSpeedMultiplier: 56
movementForceMultiplier: 0.07
horizontalBounciness: 0.2
steering: { turnRate: 1.6, corneringSpeedDamping: 0.2, gripStrength: 4.5, gripInFluid: true }
fluidSkip: { minSpeed: 11, launchSpeedFraction: 0.4, launchApproachRate: 25 }
GLIDER#

Glides where you look while mid-air and falling, for as long as the glider is held.

TypeScript
Copy
gravityMultiplier: 0
height: 1.4
pose: "gliding"
effect: { name: "Gliding", icon: "Gliding" }
airborneMode: { activeMovementType: MovementType.GLIDING, durationMs: null, exitsVehicleOnEnd: false }
airborneMovement: {
    model: "cameraDirection",
    maxSpeed: 13,
    minSpeed: 0.5,
    pitchAcceleration: 0.0125,
    friction: 0,
    impulseDecayTicks: 100,
    biasMagnitude: 1.5,
    excessVelocityBleedPerTick: 0.5,
}
Tier WOOD#

The same as GLIDER above, with nothing changed.

Tier IRON#
TypeScript
Copy
airborneMovement: {
    model: "cameraDirection",
    maxSpeed: 17,
    minSpeed: 0.5,
    pitchAcceleration: 0.0125,
    friction: 0,
    impulseDecayTicks: 100,
    biasMagnitude: 1.5,
    excessVelocityBleedPerTick: 0.5,
}
Tier GOLD#
TypeScript
Copy
airborneMovement: {
    model: "cameraDirection",
    maxSpeed: 21,
    minSpeed: 0.5,
    pitchAcceleration: 0.0125,
    friction: 0,
    impulseDecayTicks: 100,
    biasMagnitude: 1.5,
    excessVelocityBleedPerTick: 0.5,
}
Tier DIAMOND#
TypeScript
Copy
airborneMovement: {
    model: "cameraDirection",
    maxSpeed: 25,
    minSpeed: 0.5,
    pitchAcceleration: 0.0125,
    friction: 0,
    impulseDecayTicks: 100,
    biasMagnitude: 1.5,
    excessVelocityBleedPerTick: 0.5,
}
BALLOON#

Shoves you upwards on use, then drifts back down until the time runs out.

TypeScript
Copy
gravityMultiplier: 0
upwardImpulseOnUse: 20
effect: { name: "Floating", icon: "Red Balloon", duration: 16000 }
airborneMode: { activeMovementType: MovementType.FLOATING, durationMs: 16000, exitsVehicleOnEnd: true }
airborneMovement: { model: "heading" }
airborneFallSpeedLimit: { maxFallSpeed: 3, slowDownSeconds: 0.15, compensateGravity: true }
Tier YELLOW#
TypeScript
Copy
effect: { name: "Floating", icon: "Yellow Balloon", duration: 16000 }
Tier WHITE#
TypeScript
Copy
effect: { name: "Floating", icon: "White Balloon", duration: 16000 }
Tier RED#

The same as BALLOON above, with nothing changed.

Tier PURPLE#
TypeScript
Copy
effect: { name: "Floating", icon: "Purple Balloon", duration: 16000 }
Tier PINK#
TypeScript
Copy
effect: { name: "Floating", icon: "Pink Balloon", duration: 16000 }
Tier ORANGE#
TypeScript
Copy
effect: { name: "Floating", icon: "Orange Balloon", duration: 16000 }
Tier MAGENTA#
TypeScript
Copy
effect: { name: "Floating", icon: "Magenta Balloon", duration: 16000 }
Tier LIME#
TypeScript
Copy
effect: { name: "Floating", icon: "Lime Balloon", duration: 16000 }
Tier LIGHT_GRAY#
TypeScript
Copy
effect: { name: "Floating", icon: "Light Gray Balloon", duration: 16000 }
Tier LIGHT_BLUE#
TypeScript
Copy
effect: { name: "Floating", icon: "Light Blue Balloon", duration: 16000 }
Tier GREEN#
TypeScript
Copy
effect: { name: "Floating", icon: "Green Balloon", duration: 16000 }
Tier GRAY#
TypeScript
Copy
effect: { name: "Floating", icon: "Gray Balloon", duration: 16000 }
Tier CYAN#
TypeScript
Copy
effect: { name: "Floating", icon: "Cyan Balloon", duration: 16000 }
Tier BROWN#
TypeScript
Copy
effect: { name: "Floating", icon: "Brown Balloon", duration: 16000 }
Tier BLUE#
TypeScript
Copy
effect: { name: "Floating", icon: "Blue Balloon", duration: 16000 }
Tier BLACK#
TypeScript
Copy
effect: { name: "Floating", icon: "Black Balloon", duration: 16000 }
SLEEPING#

A player lying in a bed. They face whichever way the bed points, so there is one tier per bed direction.

TypeScript
Copy
canRun: false
jumpMultiplier: 0
pose: "sleeping"
effect: { name: "Sleeping", icon: "Red Bed" }
speedMultiplier: 0
movementForceMultiplier: 0
disableBaseMovement: true
Tier ROTATION_1#
TypeScript
Copy
fixedHeading: 0
Tier ROTATION_2#
TypeScript
Copy
fixedHeading: 1.5708
Tier ROTATION_3#
TypeScript
Copy
fixedHeading: 3.14159
Tier ROTATION_4#
TypeScript
Copy
fixedHeading: -1.5708
RIDING_MOB#

A player riding an animal. The animal does the moving, so the player's own movement is switched off.

TypeScript
Copy
fluidDrag: 4
gravityMultiplier: 6
height: 1.5
pose: "riding"
effect: { name: "Riding", icon: "Riding" }
speedMultiplier: 2.25
movementForceMultiplier: 0.9
CAR#

Quick on solid ground and hopeless in water. It steers like a car instead of sliding sideways.

TypeScript
Copy
mass: 2.5
fluidDrag: 1
fluidDragHorizontal: 1
fluidDragVertical: 0
gravityMultiplier: 3
width: 0.25
height: 1.1
canRun: false
jumpMultiplier: 2.25
riderOffset: [0, 0.25, -0.5]
pose: "driving"
effect: { name: "Driving", icon: "Red Kart" }
standingFriction: 2
speedMultiplier: 12
fluidSpeedMultiplier: 0.0333333
maxPushDistance: 10
movementForceMultiplier: 0.5
disableFootstepSounds: true
horizontalBounciness: 0.6
steering: { turnRate: 3, corneringSpeedDamping: 0.25, gripStrength: 10, gripInFluid: false }
Tier KART#

The same as CAR above, with nothing changed.

Tier OFF_ROADER#
TypeScript
Copy
mass: 3
gravityMultiplier: 4
jumpMultiplier: 3
riderOffset: [0, 0.25, -0.2]
effect: { name: "Driving", icon: "Off Roader" }
speedMultiplier: 10
fluidSpeedMultiplier: 0.04
horizontalBounciness: 0.3
verticalBounciness: 0.4
minVerticalSpeedToBounce: 2
verticalImpactCameraShake: { minSpeed: 4, intensityPerSpeed: 0.025, maxIntensity: 0.5, durationMs: 250 }
steering: { turnRate: 2.2, corneringSpeedDamping: 0.25, gripStrength: 5, gripInFluid: false }
Tier CAR#
TypeScript
Copy
mass: 2.75
gravityMultiplier: 3.5
jumpMultiplier: 2.625
riderOffset: [0, 0, -0.25]
effect: { name: "Driving", icon: "Light Blue Car" }
speedMultiplier: 11
fluidSpeedMultiplier: 0.0367
speedMultiplierByBlock: {
    Dirt: 0.6,
    "Messy Dirt": 0.6,
    "Rocky Dirt": 0.6,
    "Grass Block": 0.6,
    "Pine Grass Block": 0.6,
    "Jungle Grass Block": 0.6,
    "Overgrown Grass Block": 0.6,
    "Overgrown Pine Grass Block": 0.6,
    "Overgrown Jungle Grass Block": 0.6,
    "Dry Grass Block": 0.6,
    "Overgrown Dry Grass Block": 0.6,
    Sand: 0.6,
    "Red Sand": 0.6,
    Gravel: 0.6,
    Clay: 0.6,
    Snow: 0.6,
    "Packed Snow": 0.6,
}
horizontalBounciness: 0.45
minVerticalSpeedToBounce: 2
verticalImpactCameraShake: { minSpeed: 4, intensityPerSpeed: 0.0125, maxIntensity: 0.25, durationMs: 250 }
steering: { turnRate: 2.6, corneringSpeedDamping: 0.25, gripStrength: 7.5, gripInFluid: false }
Tier GOLD_MINING_DRILL#
TypeScript
Copy
mass: 3
gravityMultiplier: 4
jumpMultiplier: 3
riderOffset: [0, 0.25, -0.2]
effect: { name: "Driving", icon: "Gold Mining Drill" }
speedMultiplier: 5
fluidSpeedMultiplier: 0.02
horizontalBounciness: 0
verticalBounciness: 0.4
minVerticalSpeedToBounce: 2
verticalImpactCameraShake: { minSpeed: 4, intensityPerSpeed: 0.025, maxIntensity: 0.5, durationMs: 250 }
steering: { turnRate: 1.65, corneringSpeedDamping: 0.25, gripStrength: 5, gripInFluid: false }
Tier ARMORED_CAR#
TypeScript
Copy
mass: 4.5
gravityMultiplier: 4
jumpMultiplier: 2.5
riderOffset: [0, 0.25, -0.2]
effect: { name: "Driving", icon: "Armored Car" }
standingFriction: 1.6
speedMultiplier: 9
fluidSpeedMultiplier: 0.0444444
horizontalBounciness: 0.15
verticalBounciness: 0.15
minVerticalSpeedToBounce: 2
verticalImpactCameraShake: { minSpeed: 4, intensityPerSpeed: 0.03, maxIntensity: 0.5, durationMs: 300 }
steering: { turnRate: 1.6, corneringSpeedDamping: 0.35, gripStrength: 6, gripInFluid: false }
Tier IRON_MINING_DRILL#
TypeScript
Copy
mass: 3
gravityMultiplier: 4
jumpMultiplier: 3
riderOffset: [0, 0.25, -0.2]
effect: { name: "Driving", icon: "Iron Mining Drill" }
speedMultiplier: 4
fluidSpeedMultiplier: 0.02
horizontalBounciness: 0
verticalBounciness: 0.4
minVerticalSpeedToBounce: 2
verticalImpactCameraShake: { minSpeed: 4, intensityPerSpeed: 0.025, maxIntensity: 0.5, durationMs: 250 }
steering: { turnRate: 1.65, corneringSpeedDamping: 0.25, gripStrength: 5, gripInFluid: false }
Tier DIAMOND_MINING_DRILL#
TypeScript
Copy
mass: 3
gravityMultiplier: 4
jumpMultiplier: 3
riderOffset: [0, 0.25, -0.2]
effect: { name: "Driving", icon: "Diamond Mining Drill" }
speedMultiplier: 6
fluidSpeedMultiplier: 0.02
horizontalBounciness: 0
verticalBounciness: 0.4
minVerticalSpeedToBounce: 2
verticalImpactCameraShake: { minSpeed: 4, intensityPerSpeed: 0.025, maxIntensity: 0.5, durationMs: 250 }
steering: { turnRate: 1.65, corneringSpeedDamping: 0.25, gripStrength: 5, gripInFluid: false }
Tier MOONSTONE_MINING_DRILL#
TypeScript
Copy
mass: 3
gravityMultiplier: 4
jumpMultiplier: 3
riderOffset: [0, 0.25, -0.2]
effect: { name: "Driving", icon: "Moonstone Mining Drill" }
speedMultiplier: 7
fluidSpeedMultiplier: 0.02
horizontalBounciness: 0
verticalBounciness: 0.4
minVerticalSpeedToBounce: 2
verticalImpactCameraShake: { minSpeed: 4, intensityPerSpeed: 0.025, maxIntensity: 0.5, durationMs: 250 }
steering: { turnRate: 1.65, corneringSpeedDamping: 0.25, gripStrength: 5, gripInFluid: false }
HOVERCRAFT#

Skims over both land and water, and slides sideways easily because it has no grip.

TypeScript
Copy
mass: 0.5
fluidDrag: 2
fluidDragHorizontal: 0
fluidDragVertical: 2
gravityMultiplier: 3
height: 1.2
canRun: false
jumpMultiplier: 0.7
riderOffset: [0, 0.25, -0.25]
pose: "driving"
effect: { name: "Hovering", icon: "Hovercraft" }
standingFriction: 0.4
speedMultiplier: 9
maxPushDistance: 6
movementForceMultiplier: 0.11
disableFootstepSounds: true
Types Glossary#

The object shapes taken by some of the settings above.

SteeringOpts#
TypeScript
Copy
type SteeringOpts = {
    /** How fast it turns, in radians per second. Bigger = snappier steering and tighter corners. */
    turnRate: number
    /** How much speed a hard corner costs, from `0` (none) to `1` (all of it). */
    corneringSpeedDamping: number
    /**
     * How much it grips the ground. `0` slides sideways like a hovercraft on ice; bigger values make it
     * follow its nose round corners. Solid ground only, unless `gripInFluid` is on.
     */
    gripStrength: number
    /** Whether it also grips while floating in water, so a boat can corner like a kart. */
    gripInFluid: boolean
}
FluidSkipOpts#
TypeScript
Copy
type FluidSkipOpts = {
    /** How fast it must be going, in blocks per second, to start skipping. */
    minSpeed: number
    /** How much of its speed above `minSpeed` becomes upward launch speed. Bigger = higher skips. */
    launchSpeedFraction: number
    /** How snappily it leaves the water. Bigger = a sharp pop; smaller = a slow heave. */
    launchApproachRate: number
}
ImpactCameraShakeOpts#
TypeScript
Copy
type ImpactCameraShakeOpts = {
    /** The crash speed, in blocks per second, needed to shake at all, so small bumps are ignored. */
    minSpeed: number
    /** How much shake each extra block per second adds. Shake runs from `0` (still) to `1` (violent). */
    intensityPerSpeed: number
    /** The most shake one crash can cause. */
    maxIntensity: number
    /** How long the shake lasts, in milliseconds. */
    durationMs: number
}
AirborneModeOpts#
TypeScript
Copy
type AirborneModeOpts = {
    /** Which movement type to switch to: `GLIDING` for gliders, `FLOATING` for balloons. */
    activeMovementType: MovementType
    /** How long the flying lasts, in milliseconds, before it drops the rider. `null` = no limit. */
    durationMs: PNull<number>
    /** Whether the flying ending also throws the rider off, as a popping balloon does. */
    exitsVehicleOnEnd: boolean
}
AirborneMovementOpts#
TypeScript
Copy
type AirborneMovementOpts = HeadingAirborneMovement | CameraDirectionAirborneMovement
HeadingAirborneMovement#
TypeScript
Copy
type HeadingAirborneMovement = { model: "heading" }
CameraDirectionAirborneMovement#
TypeScript
Copy
type CameraDirectionAirborneMovement = {
    model: "cameraDirection"
    /** The fastest it can fly. Better gliders get a bigger value, and dive and climb more sharply. */
    maxSpeed: number
    /** The slowest it can fly. It never stalls below this, however steeply it climbs. */
    minSpeed: number
    /** How much looking up or down changes its speed. Bigger = dives gain speed quickly. */
    pitchAcceleration: number
    /** How much drag slows it each tick. `0` = none. */
    friction: number
    /** How many ticks an outside shove - a fuel boost, or knockback - keeps its momentum before flight takes over again. */
    impulseDecayTicks: number
    /** How strongly it is nudged forwards, then gently downwards, so a level glider sinks slowly. */
    biasMagnitude: number
    /** How much leftover speed from a shove is shed each tick. */
    excessVelocityBleedPerTick: number
}
FallSpeedLimitOpts#
TypeScript
Copy
type FallSpeedLimitOpts = {
    /** The fastest it may fall, in blocks per second. */
    maxFallSpeed: number
    /** Roughly how long, in seconds, it takes to slow back to the limit. Smaller = a firmer catch. */
    slowDownSeconds: number
    /** Whether to also cancel gravity while holding it back, so the limit is not slowly overpowered. */
    compensateGravity: boolean
}
Previous
Mob Settings
Next
Mesh Entities

---

## Mesh Entities, Throwables & Node Mesh Attachment

URL: https://bloxd.io/docs/mesh-entities

Spawn mesh entities and throwables, and attach meshes to nodes.


Mesh entities are server-created 3D objects whose position is synced with all clients. Throwables are a specialised subset that use the engine's built-in projectile physics. Node mesh attachment lets you attach additional meshes to specific bones/nodes of an existing entity (e.g. a weapon on a player's hand).

Limits#
There is a limit to the number of mesh entities and throwables that can be created. attemptCreateMeshEntity returns null when the limit is reached instead of throwing.
There are two separate limits: one for mesh entities without physics and one for mesh entities with physics (which is a lot smaller).
Mesh Entities#
Mesh Types#

The following mesh types are available, each with different options:

Box
BloxdBlock
Person
Leaderboard
ParticleEmitter
Box#
TypeScript
Copy
type BoxOpts = {
    hideDist?: number
    meshOffset?: number[]
    autoRotate?: boolean
    lineToEId?: EntityId // EntityId to connect to using a line
    width: number
    height: number
    depth: number
    diffuseColor?: number[]
    emissiveColor?: number[]
    backFaceCulling?: boolean // Default true
    texture?: string // Can be a blockname. Wraps every one block
    faceUV?: number[][]
    animateTexture?: boolean // If true, `texture` must be an animated block name (e.g. "Lava", "Red Portal") and the Box cycles through its frames.
}
BloxdBlock#
TypeScript
Copy
type BloxdBlockOpts = {
    hideDist?: number
    meshOffset?: number[]
    autoRotate?: boolean
    lineToEId?: EntityId // EntityId to connect to using a line
    blockName: BlockNameOrId
    size: number | [number, number, number]
    enchantmentTier?: EnchantmentTier // Enchantment sheen, drawn only when attached to an entity node, as a worn glider is.
}
Person#
TypeScript
Copy
type PersonOpts = {
    hideDist?: number
    meshOffset?: number[]
    autoRotate?: boolean
    lineToEId?: EntityId // EntityId to connect to using a line
    size?: number
    textures?: Partial<Cosmetics>
    pose?: PlayerPose
}
Leaderboard#
TypeScript
Copy
type LeaderboardOpts = {
    hideDist?: number
    meshOffset?: number[]
    autoRotate?: boolean
    lineToEId?: EntityId // EntityId to connect to using a line
    leaderboard: string
    title?: string
    scoreLabel?: string
    size?: number // Uniform scale of the 2.5 by 3.75 block board. Defaults to 1.
    width?: number // Absolute width in blocks, overriding the width derived from size.
    height?: number // Absolute height in blocks, overriding the height derived from size.
}
ParticleEmitter#
TypeScript
Copy
type ParticleEmitterOpts = {
    texture: string
    minLifeTime: number
    maxLifeTime: number
    minEmitPower: number
    maxEmitPower: number
    minSize: number
    maxSize: number
    gravity: number[]
    velocityGradients: VelocityGradient[]
    colorGradients: TimeColorGradient[] | RandomColorGradient[]
    blendMode: ParticleSystemBlendMode
    hideDist?: number
    meshOffset?: number[]
    autoRotate?: boolean
    lineToEId?: EntityId // EntityId to connect to using a line
    height: number
    width: number
    depth: number
    emitRate: number
    followTargetMeshOffset?: boolean // Include the followed lifeform's visual offset, including its vehicle seat.
    emitterShape?: "box" | "ring" // Ring emits radially from the perimeter; width/depth set its diameters, height its thickness.
    dir1?: number[]
    dir2?: number[]
}
Creating a Mesh Entity#
TypeScript
Copy
/**
 * Try to create a mesh entity. This creates an entity whose mesh position is synced with clients.
 * Set entity position using setPosition
 * There is a limit to the number of mesh entities and throwables that can be created, with an even smaller limit for mesh entities with physics.
 *
 * @param {MeshType} type
 * @param {MeshEntityOpts[MeshType]} opts
 * @param {string} [name] - The default name for the nametag
 * @param {MeshEntityPhysicsOpts} [physicsOptions] - Physics Options
 * @param {EntityId} [initiatorId] - The entity that initiated the creation of the mesh entity.
 * @returns {PNull<EntityId>} - null if the entity creation failed, otherwise the entity ID.
 */
attemptCreateMeshEntity(type, opts, name, physicsOptions, initiatorId)

Use api.setPosition() to move the entity after creation.

Examples#

Create a red box:

TypeScript
Copy
const boxId = api.attemptCreateMeshEntity("Box", {
    width: 1,
    height: 1,
    depth: 1,
    diffuseColor: [255, 0, 0],
})
if (boxId) {
    api.setPosition(boxId, 10, 50, 10)
}

Create a Bloxd block mesh:

TypeScript
Copy
const blockId = api.attemptCreateMeshEntity("BloxdBlock", {
    blockName: "Block of Diamond",
    size: 1,
})

Create a person mesh:

TypeScript
Copy
const personId = api.attemptCreateMeshEntity("Person", {
    size: 1,
    pose: "standing",
    textures: { head: "trader_black" },
}, "Bedwars Merchant")

Create a mesh entity with physics:

TypeScript
Copy
const physicsBoxId = api.attemptCreateMeshEntity(
    "Box",
    { width: 0.5, height: 0.5, depth: 0.5, diffuseColor: [0, 255, 0] },
    "",
    {
        doPhysics: true,
        collidesEntities: true,
        collideBits: 1,
        collideMask: 1,
    },
)
Updating a Mesh Entity#
TypeScript
Copy
/**
 * Update a mesh entity. If used on a non-mesh entity, will do nothing.
 *
 * @param {EntityId} eId
 * @param {MeshType} type
 * @param {MeshEntityOpts[MeshType]} opts
 * @returns {void}
 */
updateMeshEntity(eId, type, opts)
TypeScript
Copy
api.updateMeshEntity(boxId, "Box", {
    width: 2,
    height: 2,
    depth: 2,
    diffuseColor: [0, 0, 255],
})
Deleting a Mesh Entity#
TypeScript
Copy
/**
 * Delete a mesh entity
 *
 * @param {EntityId} eId
 * @returns {boolean} - whether the api successfully deleted the meshEntity
 */
deleteMeshEntity(eId)
TypeScript
Copy
api.deleteMeshEntity(boxId)
Throwables#

Throwables use the engine's built-in projectile system. Each throwable item has predefined velocity, damage, and gravity. You can multiply these defaults with the velocityMult, damageMult, and gravityMult parameters.

Creating a Throwable#
TypeScript
Copy
/**
 * Try to create a throwable entity.
 * Similar to creating a mesh entity and uses the same rate limiting.
 * However, this uses the predefined throwables system and physics used by throwable items with the game
 * Each throwable item has its own behaviour already, including default velocity, damage and gravity multipliers.
 *
 * @param {EntityId} throwerEId
 * @param {ThrowableItem} itemName - Must be an Item that is usually throwable in-engine
 * @param {[number, number, number]} position - Starting position
 * @param {[number, number, number]} direction
 * @param {number} [velocityMult] - Multiplier for the default velocity of the throwable item
 * @param {number} [damageMult] - Multiplier for the default damage of the throwable item
 * @param {number} [gravityMult] - Multiplier for the default gravity of the throwable item
 * @param {ItemAttributes} [attributes] - item attributes (currently used only for the "Boomerag" item)
 * @returns {string} - null if throwable creation failed, otherwise the entity ID.
 */
attemptCreateThrowable(throwerEId, itemName, position, direction, velocityMult, damageMult, gravityMult, attributes)
Example#
TypeScript
Copy
const pos = api.getPosition(playerId)
const { dir } = api.getPlayerFacingInfo(playerId)
const throwableId = api.attemptCreateThrowable(
    playerId,
    "Fireball",
    [pos[0], pos[1] + 1.5, pos[2]],
    dir,
    2,    // double velocity
    1.5,  // 1.5x damage
)
Deleting a Throwable#

Some throwables are deleted automatically when they hit a block or entity, or despawn after a certain time. You can delete them manually with this method.

TypeScript
Copy
/**
 * Delete a throwable entity before it automatically removes itself.
 *
 * @param {EntityId} eId
 * @returns {boolean} - true if the entity was deleted, false if it was not a throwable entity
 */
deleteThrowable(eId)
TypeScript
Copy
api.deleteThrowable(throwableId)
Node Mesh Attachment#

Attach or detach a mesh to a specific node ("bone") of an entity. This is useful for attaching items, effects, or decorations to player body parts or other entity nodes.

TypeScript
Copy
/**
 * Attach/detach mesh instances to/from an entity
 *
 * @param {EntityId} eId
 * @param {EntityNamedNode} node - node to attach to
 * @param {PNull<MeshType>} type - if null, detaches mesh from this node
 * @param {MeshEntityOpts[MeshType]} [opts]
 * @param {[number, number, number]} [offset]
 * @param {[number, number, number]} [rotation]
 * @returns {void}
 */
updateEntityNodeMeshAttachment(eId, node, type, opts, offset, rotation)
Available Nodes#

EntityNamedNode is one of:

"TorsoNode"
"HeadMesh"
"ArmRightMesh"
"ArmLeftMesh"
"LegLeftMesh"
"LegRightMesh"
Examples#

Attach a block to a player's right arm:

TypeScript
Copy
api.updateEntityNodeMeshAttachment(
    playerId,
    "ArmRightMesh",
    "BloxdBlock",
    { blockName: "Block of Diamond", size: 0.3 },
    [0, -0.5, 0],  // offset
    [0, 0, 0],     // rotation
)

Attach a glowing box to a player's head:

TypeScript
Copy
api.updateEntityNodeMeshAttachment(
    playerId,
    "HeadMesh",
    "Box",
    { width: 0.3, height: 0.3, depth: 0.3, emissiveColor: [255, 215, 0] },
    [0, 0.5, 0],
)

Detach a mesh from a node:

TypeScript
Copy
api.updateEntityNodeMeshAttachment(playerId, "ArmRightMesh", null)
Types Glossary#

Reference types that you may find useful.

MeshEntityOpts#
TypeScript
Copy
type MeshEntityOpts = {
    Box: CommonMeshEntityOpts & {
        width: number
        height: number
        depth: number
        diffuseColor?: number[]
        emissiveColor?: number[]
        backFaceCulling?: boolean // Default true
        texture?: string // Can be a blockname. Wraps every one block
        faceUV?: number[][]
        animateTexture?: boolean // If true, `texture` must be an animated block name (e.g. "Lava", "Red Portal") and the Box cycles through its frames.
    }
    BloxdBlock: CommonMeshEntityOpts & {
        blockName: BlockNameOrId
        size: number | [number, number, number]
        /** Enchantment sheen, drawn only when attached to an entity node, as a worn glider is. */
        enchantmentTier?: EnchantmentTier
    }
    Person: CommonMeshEntityOpts & {
        size?: number
        textures?: Partial<Cosmetics>
        pose?: PlayerPose
    }
    Leaderboard: LeaderboardMeshOpts
    ParticleEmitter: MeshParticleSystemOpts
}
CommonMeshEntityOpts#
TypeScript
Copy
type CommonMeshEntityOpts = {
    hideDist?: number
    meshOffset?: number[]
    autoRotate?: boolean
    lineToEId?: EntityId // EntityId to connect to using a line
}
MeshEntityPhysicsOpts#
TypeScript
Copy
type MeshEntityPhysicsOpts = {
    doPhysics: boolean
    onCollideTerrain?: () => void // Unsupported for custom code
    collidesEntities?: boolean
    collideBits?: number // bitmask category of this entity
    collideMask?: number // bitmask category of entities this entity collides with
    heightExpandAmt?: number // expand hitbox height by this amount
    widthExpandAmt?: number // expand hitbox width by this amount
}
MeshParticleSystemOpts#
TypeScript
Copy
type MeshParticleSystemOpts = ParticleSystemOpts &
    CommonMeshEntityOpts & {
        height: number
        width: number
        depth: number
        emitRate: number
        /** Include the followed lifeform's visual offset, including its vehicle seat. */
        followTargetMeshOffset?: boolean
        /** Ring emits radially from the perimeter; width/depth set its diameters, height its thickness. */
        emitterShape?: "box" | "ring"
        dir1?: number[]
        dir2?: number[]
    }
ParticleSystemOpts#
TypeScript
Copy
type ParticleSystemOpts = {
    texture: string
    minLifeTime: number
    maxLifeTime: number
    minEmitPower: number
    maxEmitPower: number
    minSize: number
    maxSize: number
    gravity: number[]
    velocityGradients: VelocityGradient[]
    colorGradients: TimeColorGradient[] | RandomColorGradient[]
    blendMode: ParticleSystemBlendMode
}
TimeColorGradient#

Colours are [r, g, b, a]: RGB 0-255, alpha 0-1.

TypeScript
Copy
type TimeColorGradient = {
    timeFraction: number
    minColor: [number, number, number, number]
    maxColor?: [number, number, number, number]
}
RandomColorGradient#

Colour is [r, g, b]: RGB 0-255.

TypeScript
Copy
type RandomColorGradient = {
    color: [number, number, number]
}
VelocityGradient#
TypeScript
Copy
type VelocityGradient = {
    timeFraction: number
    factor: number
    factor2: number
}
ParticleSystemBlendMode#
TypeScript
Copy
enum ParticleSystemBlendMode {
    // Source color is added to the destination color without alpha affecting the result
    OneOne = 0,
    // Blend current color and particle color using particle's alpha
    Standard = 1,
    // Add current color and particle color multiplied by particle's alpha
    Add,
    // Multiply current color with particle color
    Multiply,
    // Multiply current color with particle color then add current color and particle color multiplied by particle's alpha
    MultiplyAdd,
}
EntityNamedNode#

Nodes on a player/entity skeleton that meshes can be attached to.

TypeScript
Copy
type EntityNamedNode = "TorsoNode" | "HeadMesh" | "ArmRightMesh" | "ArmLeftMesh" | "LegLeftMesh" | "LegRightMesh"
Previous
Vehicle Settings
Next
QTEs

---

## Quick Time Events (QTEs)

URL: https://bloxd.io/docs/qte

Quick time events: progress bars, timed clicks and rhythm games.


QTEs are interactive prompts shown to a player that require a response (clicking, holding, etc). They are triggered from server-side game code via api.addQTE() and the result is received via the onPlayerFinishQTE callback.

Overview#
progressBar: Click rapidly to fill a progress bar before it drains to zero.
timedClick: Click within a time window to succeed.
gravityBar: Hold click to keep a catch zone aligned with a moving target.
precisionBar: Click when the marker is within the success zone to succeed.
rhythmClick: Click when a shrinking outer circle aligns with a fixed inner circle.
progressBar#

The player clicks repeatedly to increase a progress bar. The bar drains continuously over time. Reaching 100% completes the QTE successfully. If canFail is true and progress reaches 0, the QTE fails; otherwise progress is clamped at 0 and the player can keep trying.

Parameters#
TypeScript
Copy
type ProgressBarQteParams = {
    progressStartValue?: number // Starting progress value (0-100). default: 30
    progressDecreasePerTick: number // How much progress drains each tick while the player isn't clicking. default: 0.075
    progressPerClick: number // How much progress is gained per click. default: 5
    canFail: boolean // If true, the QTE fails when progress reaches 0; otherwise progress clamps at 0. default: false
    description: CustomTextStyling // Rich text shown as the QTE prompt. default: [{ str: "Click repeatedly to complete!" }]
    clickIcon: string // Icon displayed on the click target. default: "fa-solid fa-computer-mouse"
    scale?: number // Scale multiplier for the click icon (must be > 0). default: 1
    rotation?: number // Rotation in degrees for the click icon (must be ≥ 0). default: 15
}
Sensible Defaults#
TypeScript
Copy
api.addQTE(playerId, {
    type: "progressBar",
    parameters: {
        progressStartValue: 30,
        progressDecreasePerTick: 0.075,
        progressPerClick: 5,
        canFail: false,
        description: [{ str: "Click repeatedly to complete!" }],
        clickIcon: "fa-solid fa-computer-mouse",
        scale: 3,
        rotation: 15,
    },
})
Try progressBar
timedClick#

A prompt appears and the player must click before the timer runs out. Clicking within the time window succeeds; letting it expire fails the QTE.

Parameters#
TypeScript
Copy
type TimedClickQteParams = {
    timeWindow: number // Duration in milliseconds the player has to click. default: 3000
    icon: string // Icon displayed on the click target. default: "fa-solid fa-computer-mouse"
    label: CustomTextStyling // Rich text shown as the QTE prompt. default: [{ str: "Click to complete the QTE!" }]
    showTimer: boolean // Whether to display a countdown timer. default: true
    scale?: number // Scale multiplier for the icon (must be > 0). default: 1
    rotation?: number // Rotation in degrees for the icon (must be ≥ 0). default: 15
    breatheCenter?: boolean // If true, the icon pulses with a breathing animation anchored to the centre. default: false
}
Sensible Defaults#
TypeScript
Copy
api.addQTE(playerId, {
    type: "timedClick",
    parameters: {
        timeWindow: 3000,
        icon: "fa-solid fa-computer-mouse",
        label: [{ str: "Click to complete the QTE!" }],
        showTimer: true,
        scale: 3,
        rotation: 15,
        breatheCenter: false,
    },
})
Try timedClick
gravityBar#

A mover travels along a bar, periodically changing direction. The player holds click to push their catch zone upward and releases to let gravity pull it down. Progress fills while the mover overlaps the catch zone and drains when it doesn't. Reaching 100% succeeds. If canFail is true, hitting 0% fails the QTE.

Parameters#
TypeScript
Copy
type GravityBarQteParams = {
    progressStartValue?: number // Starting progress value (0-100). default: 30
    catchZoneSize: number // Size of the player's catch zone as a fraction of the bar (must be > 0, 0-1). default: 0.25
    moverSpeed: number // Speed at which the mover travels along the bar (must be > 0). default: 3
    moverErraticness: number // How erratically the mover changes direction (higher = more unpredictable). default: 0.8
    gravity: number // Downward pull on the catch zone when the player isn't holding click. default: 1
    riseSpeed: number // Upward force on the catch zone while the player holds click. default: 1.5
    progressGainPerSecond: number // Progress gained per second while the mover is inside the catch zone. default: 8
    progressDrainPerSecond: number // Progress lost per second while the mover is outside the catch zone. default: 4
    canFail: boolean // If true, the QTE fails when progress reaches 0; otherwise progress clamps at 0. default: false
    description: CustomTextStyling // Rich text shown as the QTE prompt. default: [{ str: "Hold to catch!" }]
    icon?: string // Icon displayed on the mover. default: "Moonfish"
}
Sensible Defaults#
TypeScript
Copy
api.addQTE(playerId, {
    type: "gravityBar",
    parameters: {
        progressStartValue: 30,
        catchZoneSize: 0.25,
        moverSpeed: 3,
        moverErraticness: 0.8,
        gravity: 1,
        riseSpeed: 1.5,
        progressGainPerSecond: 8,
        progressDrainPerSecond: 4,
        canFail: false,
        description: [{ str: "Hold to catch!" }],
        icon: "Moonfish",
    },
})
Try gravityBar

The Moonfish icon is a Bloxd item, so it shows in game only.

precisionBar#

A marker oscillates back and forth along a bar. A highlighted success zone sits in the centre. The player has one click — if the marker is inside the success zone, the QTE succeeds; otherwise it fails. The marker keeps bouncing indefinitely until the player clicks.

Parameters#
TypeScript
Copy
type PrecisionBarQteParams = {
    speed: number // Speed of the marker in full bar-widths per second (must be > 0, e.g. 1.0 = one full sweep per second). default: 0.5
    successZoneSize: number // Fraction of the bar that counts as the success zone, centred in the middle (must be > 0, 0-1, e.g. 0.15 = 15%). default: 0.15
    label: CustomTextStyling // Rich text shown as the QTE prompt. default: [{ str: "Click when the marker is within the green zone." }]
    icon?: string // Icon displayed on the marker. default: ""
    scale?: number // Scale multiplier for the icon (must be > 0). default: 1
    rotation?: number // Rotation in degrees for the icon (must be ≥ 0). default: 0
}
Sensible Defaults#
TypeScript
Copy
api.addQTE(playerId, {
    type: "precisionBar",
    parameters: {
        speed: 0.5,
        successZoneSize: 0.15,
        label: [{ str: "Click when the marker is within the green zone." }],
        icon: "",
        scale: 1,
        rotation: 0,
    },
})
Try precisionBar
rhythmClick#

An outer circle shrinks toward a fixed inner circle. The player must click when the two overlap. Each successful click counts toward requiredSuccesses. Missing the window (clicking too early/late or letting the circle pass without clicking) counts as a miss. If maxMisses is set and exceeded, the QTE fails; otherwise missed attempts simply reset the circle for another try.

Parameters#
TypeScript
Copy
type RhythmClickQteParams = {
    requiredSuccesses: number // Number of successful clicks needed to complete the QTE (must be a positive integer). default: 5
    shrinkDurationMs: number // Duration in milliseconds for the outer circle to shrink from max size to centre (must be > 0). default: 1200
    toleranceFraction: number // Fraction of the inner circle radius that counts as a successful overlap (must be > 0, 0-1, e.g. 0.15 = ±15%). default: 0.15
    maxMisses?: number // Max misses allowed before failing. If omitted, unlimited misses are permitted (must be a non-negative integer). default: 3
    label: CustomTextStyling // Rich text shown as the QTE prompt. default: [{ str: "Click when the circles align!" }]
    icon?: string // Icon displayed in the centre of the circles. default: ""
}
Sensible Defaults#
TypeScript
Copy
api.addQTE(playerId, {
    type: "rhythmClick",
    parameters: {
        requiredSuccesses: 5,
        shrinkDurationMs: 1200,
        toleranceFraction: 0.15,
        maxMisses: 3,
        label: [{ str: "Click when the circles align!" }],
        icon: "",
    },
})
Try rhythmClick
Usage#
Starting a QTE#
TypeScript
Copy
const qteId = api.addQTE(playerId, {
    type: "progressBar",
    parameters: {
        progressDecreasePerTick: 0.075,
        progressPerClick: 7,
        canFail: false,
        description: [{ str: "Click repeatedly to complete!" }],
        clickIcon: "fa-solid fa-computer-mouse",
    },
})
Handling the Result#
TypeScript
Copy
onPlayerFinishQTE(playerId, qteId, result) {
    if (result) {
        // Player succeeded
    } else {
        // Player failed
    }
}
Cancelling a QTE#
TypeScript
Copy
api.deleteQTE(playerId, qteId)
Checking Active QTEs#
TypeScript
Copy
const hasQTE = api.hasActiveQTE(playerId)
Previous
Mesh Entities
Next
Dialogue Voices

---

## Dialogue Voices

URL: https://bloxd.io/docs/dialogue-voices

The voices dialogue is read out in, with a playground for making voices of your own.


Each line of dialogue blips once for each syllable in its speaker's voice, as its words appear. Give voice a preset's name, or every parameter of the synth for a voice of your own. The Dialogue how-to shows how to say lines with @plugins/dialogue.

TypeScript
Copy
api.setClientOption(playerId, "dialogue", { line: "Welcome to my shop!", speakerName: "Shopkeeper", voice: "regular" })

Leave out voice for a silent line.

Try it: voices
Start from a preset and change it to suit your character. The line replays as you go.
Copy code
soft
regular
dark
high-pitched
gruff
lively
posh
mechanical
Innkeeper

Welcome, traveller. The road ahead is long.

Speak
Welcome, traveller. The road ahead is long.
Have you seen my lost sheep anywhere?
Watch out, the bridge is about to collapse!
Speaker
VOICE
Tone
sine
triangle
square
sawtooth
Pitch
195 Hz
Time per syllable
52 ms
Volume
1
EACH BLIP
Length
70 ms
Fade in
2 ms
Fade out
12 ms
Glide
-0.6 st
Muffle with a filter
INTONATION
Word variation
1.5 st
Fall over a sentence
2 st
Question rise
4 st
Exclamation lift
2 st
TypeScript
Copy
const voice = "regular"

api.setClientOption(playerId, "dialogue", {
    line: "Welcome, traveller. The road ahead is long.",
    speakerName: "Innkeeper",
    voice,
})
Voice presets#

Give voice a preset's name for a voice that suits a kind of character:

soft: Gentle and unhurried: the elderly, the kindly, calm animals.
regular: An everyday adult.
dark: Low, slow and falling: the sinister and the imperious.
high-pitched: Small and quick: children and little creatures.
gruff: Deep and rough: dwarves, sailors and anyone built like a wall.
lively: Bright, bouncy and fast: the eager, the cheeky and the hurried.
posh: A rising drawl with grand swoops: nobility and showmen.
mechanical: Flat and even: constructs and guardians.
Custom voices#

Give voice every parameter of the synth instead, to make a voice of your own. Characters that share a preset sound apart with a different pitchHz or syllableMs. The voice playground on the docs site's Dialogue Voices page starts from any preset and writes the code for what you hear.

TypeScript
Copy
type SpeechSynth = {
    waveform: "sine" | "triangle" | "square" | "sawtooth" // The tone of each blip, from the purest (sine) to the buzziest (sawtooth).
    pitchHz: number // The voice's pitch, which intonation moves each word away from.
    glideSemitones: number // How far the pitch slides over each blip; negative falls.
    durationMs: number // How long each blip sounds.
    attackMs: number // The fade in at the start of the blip.
    releaseMs: number // The fade at the end of the blip, within `durationMs`.
    lowpassHz: number | null // Darkens a bright waveform; null leaves it unfiltered.
    volume: number // 1 is the engine's speech level.
    intonation: SpeechIntonation
    syllableMs: number // The speaking rate: each syllable takes this long, and sets when the next word appears.
}

type SpeechIntonation = {
    variationSemitones: number // How far each word sits from the voice's pitch, either way.
    declineSemitones: number // How far the pitch falls from the first word of a sentence to its last.
    questionRiseSemitones: number // How far the last word of a question rises.
    exclaimLiftSemitones: number // How far a whole exclamation is lifted.
}

The game keeps each number within what it can play: a blip's attack and release fit within its length, for instance.

Example#

A gruff voice, pitched down and slowed for a giant:

TypeScript
Copy
const giantVoice = {
    waveform: "sawtooth",
    pitchHz: 80,
    glideSemitones: -0.8,
    durationMs: 75,
    attackMs: 4,
    releaseMs: 14,
    lowpassHz: 900,
    volume: 0.85,
    intonation: {
        variationSemitones: 1.2,
        declineSemitones: 3,
        questionRiseSemitones: 3,
        exclaimLiftSemitones: 2,
    },
    syllableMs: 70,
}

api.setClientOption(playerId, "dialogue", { line: "Who goes there?", speakerName: "Giant", voice: giantVoice })
Previous
QTEs
Next
Particles

---

## Particles

URL: https://bloxd.io/docs/particles

Particle textures and presets, with a live effect playground.

Try it: particle effects
Pick a preset or change the settings, and the burst replays. Drag the preview to turn it.
Copy code
Example
aura
stomp
brainRot
mobTameSuccess
mango
redFirecrackerLarge
Example effect
brainRot
stomp
fertiliser
bonemeal
mobTameSuccess
mobTameFailure
mobCatch
spawnCaughtMob
mobFeedDefault
mobFeedSuperliked
mobFeedLike
mobFeedNeutral
mobFeedDisliked
mobDeath
mobDeathSoul
boardShopSuccess
mobSpawnerBlockFail
mobSpawnerBlockPassive
mobSpawnerBlockNeutral
mobSpawnerBlockHostile
mobSpawnOrb
aura
yellowFirecrackerSmall
yellowFirecrackerLarge
whiteFirecrackerSmall
whiteFirecrackerLarge
redFirecrackerSmall
redFirecrackerLarge
purpleFirecrackerSmall
purpleFirecrackerLarge
pinkFirecrackerSmall
pinkFirecrackerLarge
orangeFirecrackerSmall
orangeFirecrackerLarge
magentaFirecrackerSmall
magentaFirecrackerLarge
limeFirecrackerSmall
limeFirecrackerLarge
lightGrayFirecrackerSmall
lightGrayFirecrackerLarge
lightBlueFirecrackerSmall
lightBlueFirecrackerLarge
greenFirecrackerSmall
greenFirecrackerLarge
grayFirecrackerSmall
grayFirecrackerLarge
cyanFirecrackerSmall
cyanFirecrackerLarge
brownFirecrackerSmall
brownFirecrackerLarge
blueFirecrackerSmall
blueFirecrackerLarge
blackFirecrackerSmall
blackFirecrackerLarge
defaultFirecrackerSmall
defaultFirecrackerLarge
mango
speedInner
speedOuter
damageReductionInner
damageReductionOuter
damageInner
damageOuter
invisibleInner
invisibleOuter
jumpBoostInner
jumpBoostOuter
knockbackInner
knockbackOuter
poisonedInner
poisonedOuter
slownessInner
slownessOuter
weaknessInner
weaknessOuter
cleansedInner
cleansedOuter
instantDamageInner
instantDamageOuter
healthRegenInner
healthRegenOuter
healingPulseInner
healingPulseOuter
instantHealthInner
instantHealthOuter
hasteInner
hasteOuter
shieldInner
shieldOuter
doubleJumpInner
doubleJumpOuter
heatResistanceInner
heatResistanceOuter
thiefInner
thiefOuter
xRayVisionInner
xRayVisionOuter
miningYieldInner
miningYieldOuter
brainRotInner
brainRotOuter
auraInner
auraOuter
wallClimbingInner
wallClimbingOuter
airWalkInner
airWalkOuter
pickpocketerInner
pickpocketerOuter
lifestealInner
lifestealOuter
bouncinessInner
bouncinessOuter
blindnessInner
blindnessOuter
poopyInner
poopyOuter
glowingInner
glowingOuter
nightVisionInner
nightVisionOuter
Replay
Stop looping
Texture
bubble
Particles
20
Lifetime
0.2–0.6
Emit power
2
Size
0.25–0.35
Gravity (up)
-10
Blend mode
0 · OneOne (glow)
1 · Standard
2 · Add
3 · Multiply
4 · MultiplyAdd
Colour over lifetime
min · max
0%
TypeScript
Copy
let [x, y, z] = thisPos
y += 1
api.playParticleEffect({
    dir1: [-1, -1, -1],
    dir2: [1, 1, 1],
    pos1: [x, y, z],
    pos2: [x + 1, y + 1, z + 1],
    texture: "bubble",
    minLifeTime: 0.2,
    maxLifeTime: 0.6,
    minEmitPower: 2,
    maxEmitPower: 2,
    minSize: 0.25,
    maxSize: 0.35,
    manualEmitCount: 20,
    gravity: [0, -10, 0],
    colorGradients: [
        {
            timeFraction: 0,
            minColor: [60, 60, 150, 1],
            maxColor: [200, 200, 255, 1],
        },
    ],
    velocityGradients: [
        {
            timeFraction: 0,
            factor: 1,
            factor2: 1,
        },
    ],
    blendMode: 1,
})
Show all 32 lines

These are the strings you can give to functions that take a particle effect texture as input:

arrow
bubble
critical_hit
drift
effect_5
fishingFishSilhouette
generic_2
glint
heart
scary_face
soul_0
square_particle
z-particle

Here's the code for an example particle effect:

TypeScript
Copy
let [x, y, z] = thisPos
y += 1
api.playParticleEffect({
    dir1: [-1, -1, -1],
    dir2: [1, 1, 1],
    pos1: [x, y, z],
    pos2: [x + 1, y + 1, z + 1],
    texture: "bubble",
    minLifeTime: 0.2,
    maxLifeTime: 0.6,
    minEmitPower: 2,
    maxEmitPower: 2,
    minSize: 0.25,
    maxSize: 0.35,
    manualEmitCount: 20,
    gravity: [0, -10, 0],
    colorGradients: [
        {
            timeFraction: 0,
            minColor: [60, 60, 150, 1],
            maxColor: [200, 200, 255, 1],
        },
    ],
    velocityGradients: [
        {
            timeFraction: 0,
            factor: 1,
            factor2: 1,
        },
    ],
    blendMode: 1,
})
Show all 32 lines

You can also use a presetId instead to use a pre-defined particle effect, to replicate effects we use in-engine. Here is the code for an example of using a presetId:

TypeScript
Copy
let [x, y, z] = thisPos
y += 1
api.playParticleEffect({
    presetId: "aura",
    pos1: [x, y, z],
    pos2: [x + 1, y + 1, z + 1],
})

Here is a list of the presetIds you can use:

brainRot
stomp
fertiliser
bonemeal
mobTameSuccess
mobTameFailure
mobCatch
spawnCaughtMob
mobFeedDefault
mobFeedSuperliked
mobFeedLike
mobFeedNeutral
mobFeedDisliked
mobDeath
mobDeathSoul
boardShopSuccess
mobSpawnerBlockFail
mobSpawnerBlockPassive
mobSpawnerBlockNeutral
mobSpawnerBlockHostile
mobSpawnOrb
aura
yellowFirecrackerSmall
yellowFirecrackerLarge
whiteFirecrackerSmall
whiteFirecrackerLarge
redFirecrackerSmall
redFirecrackerLarge
purpleFirecrackerSmall
purpleFirecrackerLarge
pinkFirecrackerSmall
pinkFirecrackerLarge
orangeFirecrackerSmall
orangeFirecrackerLarge
magentaFirecrackerSmall
magentaFirecrackerLarge
limeFirecrackerSmall
limeFirecrackerLarge
lightGrayFirecrackerSmall
lightGrayFirecrackerLarge
lightBlueFirecrackerSmall
lightBlueFirecrackerLarge
greenFirecrackerSmall
greenFirecrackerLarge
grayFirecrackerSmall
grayFirecrackerLarge
cyanFirecrackerSmall
cyanFirecrackerLarge
brownFirecrackerSmall
brownFirecrackerLarge
blueFirecrackerSmall
blueFirecrackerLarge
blackFirecrackerSmall
blackFirecrackerLarge
defaultFirecrackerSmall
defaultFirecrackerLarge
mango
speedInner
speedOuter
damageReductionInner
damageReductionOuter
damageInner
damageOuter
invisibleInner
invisibleOuter
jumpBoostInner
jumpBoostOuter
knockbackInner
knockbackOuter
poisonedInner
poisonedOuter
slownessInner
slownessOuter
weaknessInner
weaknessOuter
cleansedInner
cleansedOuter
instantDamageInner
instantDamageOuter
healthRegenInner
healthRegenOuter
healingPulseInner
healingPulseOuter
instantHealthInner
instantHealthOuter
hasteInner
hasteOuter
shieldInner
shieldOuter
doubleJumpInner
doubleJumpOuter
heatResistanceInner
heatResistanceOuter
thiefInner
thiefOuter
xRayVisionInner
xRayVisionOuter
miningYieldInner
miningYieldOuter
brainRotInner
brainRotOuter
auraInner
auraOuter
wallClimbingInner
wallClimbingOuter
airWalkInner
airWalkOuter
pickpocketerInner
pickpocketerOuter
lifestealInner
lifestealOuter
bouncinessInner
bouncinessOuter
blindnessInner
blindnessOuter
poopyInner
poopyOuter
glowingInner
glowingOuter
nightVisionInner
nightVisionOuter

No sections match “”.

Previous
Dialogue Voices
Next
Sounds & Music

---

## Sounds and Songs

URL: https://bloxd.io/docs/sounds

Every sound effect and song you can play.


This document lists all available sound effects and songs that can be used in game modes.

Sound Effects#

Sound effects are short audio clips (e.g., footsteps, hits, ambient sounds). Use the playSound, or broadcastSound API methods.

API Usage#
TypeScript
Copy
// Play a sound for a specific player
api.playSound(playerId, soundName, volume, rate, posSettings?)

// Broadcast a sound to all players (or all except one)
api.broadcastSound(soundName, volume, rate, posSettings?, exceptPlayerId?)

Parameters:

soundName: One of the sound names listed below
volume: 0.0 to 1.0
rate: Playback rate (1.0 = normal speed, 0.5 = half speed, 2.0 = double speed)
posSettings (optional): { playerIdOrPos: EntityId | number[], maxHearDist?: number, refDistance?: number }

Tip: If you want a random similar sound, remove the number suffix from the sound name (e.g., use "grass" instead of "grass1").

Available Sounds (402 total)#
ambient#
lavaFlow
crowd#
crowdAmbience
crowdCheer
refereeWhistle
customGame_horror#
cryptWhoosh
doorKnock
futureStrangePulse
hauntedHorrorImpact
horrorAccent1
horrorFright
horrorMaleDrone
intensiveRainLoop
metalDoorKnock
ominousBellHit
pulseFromTheDark
suspenseRiser
thunderRain
zapAccent1
zapAccent2
dig#
cloth1
cloth2
cloth3
cloth4
glass1
glass2
glass3
grass1
grass2
grass3
grass4
gravel1
gravel2
gravel3
gravel4
pickUp
sand1
sand2
sand3
sand4
snow1
snow2
snow3
snow4
stone1
stone2
stone3
stone4
wood1
wood2
wood3
wood4
fishing#
caughtFish
reel
gameStart#
game_start_countdown_01
game_start_countdown_02
game_start_countdown_03
game_start_countdown_final
gunMisc#
bullet_shell_bounce_general_07
bullet_shell_bounce_general_08
headshot_04
headshot_06
headshot_08
headshot_11
gunPistol#
pistol_cock_01
pistol_cock_02
pistol_cock_03
pistol_cock_06
pistol_magazine_load_01
pistol_magazine_load_02
pistol_magazine_load_03
pistol_magazine_unload_01
pistol_magazine_unload_02
pistol_magazine_unload_03
pistol_shot_01
pistol_shot_02
pistol_shot_03
pistol_shot_04
pistol_shot_05
gunRifle#
rifle_cock_01
rifle_cock_02
rifle_magazine_load_01
rifle_magazine_load_02
rifle_magazine_load_03
rifle_magazine_unload_01
rifle_magazine_unload_02
rifle_magazine_unload_04
rifle_shot_01
rifle_shot_02
rifle_shot_03
rifle_shot_04
gunSemiAutomatic#
semiAuto_cock_01
semiAuto_cock_02
semiAuto_cock_03
semiAuto_cock_04
semiAuto_cock_05
semiAuto_first_shot_01
semiAuto_magazine_load_01
semiAuto_magazine_load_02
semiAuto_magazine_load_03
semiAuto_magazine_load_04
semiAuto_magazine_load_05
semiAuto_magazine_unload_01
semiAuto_magazine_unload_02
semiAuto_magazine_unload_03
semiAuto_magazine_unload_04
semiAuto_shot_01
semiAuto_shot_02
semiAuto_shot_03
semiAuto_shot_04
semiAuto_shot_05
semiAuto_shot_06
semiAuto_shot_07
semiAuto_shot_08
semiAuto_tail_only_shot_01
gunShotgun#
shotgun_cock_01
shotgun_cock_02
shotgun_cock_03
shotgun_cock_04
shotgun_cock_05
shotgun_load_bullet_01
shotgun_load_bullet_02
shotgun_load_bullet_03
shotgun_load_bullet_04
shotgun_load_bullet_05
shotgun_load_bullet_06
shotgun_load_bullet_07
shotgun_load_bullet_08
shotgun_shot_01
shotgun_shot_02
shotgun_shot_03
shotgun_shot_04
gunSubmachineGun#
submachine_cock_01
submachine_cock_02
submachine_cock_03
submachine_cock_04
submachine_first_shot_01
submachine_magazine_load_01
submachine_magazine_load_02
submachine_magazine_load_03
submachine_magazine_load_04
submachine_magazine_unload_01
submachine_magazine_unload_02
submachine_magazine_unload_03
submachine_shot_01
submachine_shot_02
submachine_shot_03
submachine_shot_04
submachine_shot_05
submachine_shot_06
submachine_shot_07
submachine_shot_08
submachine_shot_09
submachine_tail_only_shot_01
mob#
bearRoar1
bearRoar2
bearRoar3
bearRoar4
bearRoar5
catHiss1
catHiss2
catHiss3
catHiss4
catHurt1
catHurt2
catHurt3
catMeow1
catMeow2
catMeow3
catMeow4
catMeow5
cowHurt1
cowMoo1
cowMoo2
cowMoo3
croneAttack1
croneHurt1
croneIdle1
deerGrunt1
deerHurt1
dogBark1
dogBark2
dogBark3
dogGrowl1
dogGrowl2
dogGrowl3
dogHurt1
dogHurt2
fennecYip1
fennecYip2
fennecYip3
golemGrunt1
golemGrunt2
gorillaIdle1
gorillaIdle2
gorillaIdle3
gorillaIdle4
gorillaRoar1
horseHurt1
horseHurt2
horseIdle1
horseIdle2
horseIdle3
knightGrunt1
knightGrunt2
knightGrunt3
pigHurt1
pigHurt2
pigHurt3
pigOink1
pigOink2
pigOink3
pigOink4
pigOink5
reaverAttack1
reaverAttack2
reaverAttack3
reaverGrunt1
reaverGrunt2
reaverGrunt3
sheepBaa1
sheepBaa2
sheepBaa3
sheepBaa4
sheepHurt1
skeletonRattle1
skeletonRattle2
skeletonRattle3
skeletonRattle4
stagGrunt1
stagHurt1
stalkerAttack1
stalkerIdle1
warperGrunt1
warperGrunt2
warperGrunt3
warperGrunt4
warperGrunt5
warperPhase1
warperPhase2
wraithGrunt1
wraithGrunt2
wraithHurt
ZombieGrunt1
ZombieGrunt2
ZombieGrunt3
ZombieHurt1
ZombieHurt2
ZombieHurt3
ZombieHurt4
note#
bass
bassattack
bd
bigDrumSwish1
bigDrumSwish2
bigDrumSwish3
drumSwish1
drumSwish2
harp_pling
hat
levelup
lowDrum1
lowDrum2
lowDrum3
snare
sonarBeep
trumpetFlare
trumpetNote1
trumpetNote2
trumpetNote3
random#
beep
bow
bucketEmpty1
bucketEmpty2
bucketEmpty3
bucketFill1
bucketFill2
bucketFill3
burp
cannonFire1
cannonFire2
cannonFire3
cashRegister
chestClose
chestOpen
doorClose
doorClose2
doorOpen-bloxd1
doorOpen-bloxd2
drink
eat1
equip_leather1
exp_collect
exp_levelup
fallsmall
fireBurn
firecracker1
firecracker2
firecracker3
firecracker4
hoeTill1
hoeTill2
hoeTill3
hoeTill4
laugh1
laugh2
laugh3
magicAccent1
magicAccent2
magicAccent3
magicAccent4
splash1
successfulBowHit
trapdoorOpen
rpg#
rpgBeltCloth1
rpgBeltCloth2
rpgBeltHandle1
rpgBeltHandle2
rpgBookClose
rpgBookFlip1
rpgBookFlip2
rpgBookFlip3
rpgBookOpen
rpgBookPlace1
rpgBookPlace2
rpgBookPlace3
rpgChop
rpgCloth1
rpgCloth2
rpgCloth3
rpgCloth4
rpgCreak1
rpgCreak2
rpgCreak3
rpgDoorClose1
rpgDoorClose2
rpgDoorClose3
rpgDoorClose4
rpgDoorOpen1
rpgDoorOpen2
rpgDrawKnife1
rpgDrawKnife2
rpgDrawKnife3
rpgDropLeather
rpgFootstep00
rpgFootstep01
rpgFootstep02
rpgFootstep03
rpgFootstep04
rpgFootstep05
rpgFootstep06
rpgFootstep07
rpgFootstep08
rpgFootstep09
rpgHandleCoins1
rpgHandleCoins2
rpgHandleSmallLeather1
rpgHandleSmallLeather2
rpgKnifeSlice1
rpgKnifeSlice2
rpgMetalClick
rpgMetalLatch
rpgMetalPot1
rpgMetalPot2
rpgMetalPot3
step#
hit1
hit2
hit3
step_cloth1
step_cloth2
step_cloth3
step_cloth4
step_grass1
step_grass2
step_grass3
step_grass4
step_grass5
step_gravel1
step_gravel2
step_gravel3
step_gravel4
step_sand2
step_sand3
step_sand4
step_sand5
step_snow1
step_snow2
step_snow3
step_snow4
step_stone1
step_stone2
step_stone3
step_stone4
step_stone5
step_stone6
step_wood1
step_wood2
step_wood3
step_wood4
step_wood5
step_wood6
sweep6
survivalFactory#
rocketEngineLoop
Music#

Music tracks are longer audio for background ambiance. Use the setClientOption API method with the "music" option.

API Usage#
TypeScript
Copy
// Play a song for a specific player
api.setClientOption(playerId, "music", "Adigold - Dreamless Sleep")

// Stop the current song
api.setClientOption(playerId, "music", null)

Note: Unlike sound effects, songs are played via client options, not the playSound API. Only one song plays at a time per player; setting a new song replaces the current one.

Available Songs (49 total)#
Adigold - A Place To Be Free
2:11
Adigold - Butterfly Effect
1:24
Adigold - Dreamless Sleep
1:58
Adigold - Frozen Pulse
1:39
Adigold - Frozen Skies
2:45
Adigold - Healing Thoughts
1:59
Adigold - Here Forever
2:43
Adigold - Just a Little Hope
1:48
Adigold - Just Like Heaven
1:22
Adigold - Memories Remain
2:06
Adigold - Place To Be
2:36
Adigold - The Riverside
2:28
Adigold - The Wonder
2:09
Adigold - Vetrar (Cut B)
1:30
Awkward Comedy Quirky
0:29
battle-ship-111902
1:26
cdk-Silence-Await
3:18
corsairs-studiokolomna-main-version-23542-02-33
2:34
ghost-Reverie-small-theme
0:41
happy
3:01
Heroic-Demise-New
5:02
I-am-the-Sea-The-Room-4
3:21
Juhani Junkala [Retro Game Music Pack] Ending
0:44
Juhani Junkala [Retro Game Music Pack] Level 1
1:14
Juhani Junkala [Retro Game Music Pack] Level 2
1:12
Juhani Junkala [Retro Game Music Pack] Level 3
1:21
Juhani Junkala [Retro Game Music Pack] Title Screen
0:11
LonePeakMusic-Highway-1
2:27
Mojo Productions - Pirates
1:54
Mojo Productions - Sneaky Jazz
1:43
Mojo Productions - The Sneaky
1:50
Mojo Productions - The Sneaky Jazz
2:20
progress
2:34
raise-the-sails-152124
1:44
ramblinglibrarian-I-Have-Often-T
3:42
Slow-Motion-Bensound
3:27
snowflake-Ethereal-Space
1:16
the-epic-adventure-131399
2:01
TownTheme
1:37
The Suspense Ambient
1:59
Epic1
2:16
Epic2
2:23
Emotional Epic
1:52
Enemy Marked
1:29
spooky
2:07
Shuffling Crypt
3:44
Tower of Doom
2:33
Wild Infernos
5:09
Molten Rift
3:06
Previous
Particles
Next
Icons

---

## Icons

URL: https://bloxd.io/docs/icons

Icons for styled text, from Bloxd icons to Font Awesome.


Icons can be used in CustomTextStyling arrays with the StyledIcon type:

JavaScript
Copy
api.sendMessage(playerId, [{ icon: "fa-solid fa-heart" }, " You gained a life!"])
api.sendMessage(playerId, [{ icon: "fa-solid fa-star", style: { color: "gold" } }, " Achievement!"])

Prefer Bloxd-native icons: For the best visual consistency with Bloxd's theme, use item names (see ITEM_NAMES.txt), block names (see BLOCK_NAMES.txt), or ingame icons (below) wherever possible. These are designed specifically for Bloxd and will look more cohesive. Only fall back to Font Awesome icons when no Bloxd-native option fits your use case.

Styled text editor
Add parts, click one to style it, and copy the code. The preview draws it as the game does.
Icon and text
Coloured words
Achievement
Loading bar
 You gained a life!
PARTS
ICON
Pixelated Heart
TEXT
You gained a life!
Add a part
CODE
Edit
JavaScript
Copy
api.sendMessage(playerId, [{ icon: "Pixelated Heart" }, " You gained a life!"])
Ingame Icons (96 icons)#

These are the values of the IngameIconName type.

Damage
Damage Reduction
Speed
VoidJump
Fist
Frozen
Hydrated
Invisible
Jump Boost
Poisoned
Slowness
Weakness
Health Regen
Healing Pulse
Haste
Double Jump
Heat Resistance
Gliding
Boating
Obsidian Boating
Riding
Bunny Hop
FallDamage
Feather Falling
Thief
X-Ray Vision
Mining Yield
Brain Rot
Rested Damage
Rested Haste
Rested Speed
Rested Farming Yield
Rested Aura
Blindness
Pickpocketer
Lifesteal
Bounciness
Air Walk
Wall Climbing
Thorns
Poopy
Glowing
Night Vision
Irradiated
Draugr Knight Head
Draugr Warper Head
Magma Golem Head
Mystery Fish
Damage Enchantment
Critical Damage Enchantment
Attack Speed Enchantment
Protection Enchantment
Health Enchantment
Health Regen Enchantment
Stomp Damage Enchantment
Knockback Resist Enchantment
Arrow Speed Enchantment
Arrow Damage Enchantment
Quick Charge Enchantment
Break Speed Enchantment
Momentum Enchantment
Mining Yield Enchantment
Farming Yield Enchantment
Mining Aura Enchantment
Digging Aura Enchantment
Lumber Aura Enchantment
Farming Aura Enchantment
Vertical Knockback Enchantment
Horizontal Knockback Enchantment
Firecracker Cooldown Enchantment
Firecracker Boost Enchantment
Gliding Speed Enchantment
Self Yield
Friends
Riding Speed
Feed Aura
Double Poop
Mob Slayer
Rainbow Wool
Pack Leader
Max Health
Poison Claws
Mob Yield
Antlers Bonus
Health
HealthShield
Cross
Friendship
Dotted Friendship
Hunger
Empty Hunger
Pixelated Heart
Question Mark
Trader Black
Trader Blue
Trader Piggy
Font Awesome Icons (214 icons)#

Use with fa-solid, fa-regular, or fa-duotone prefix. Only use these when no Bloxd-native icon fits.

fa-solid fa-add
fa-solid fa-angle-double-up
fa-solid fa-angle-down
fa-solid fa-angle-up
fa-solid fa-angles-up
fa-solid fa-arrow-left
fa-solid fa-arrow-up
fa-solid fa-arrow-up-right-from-square
fa-solid fa-arrows
fa-solid fa-arrows-h
fa-solid fa-arrows-left-right
fa-solid fa-arrows-rotate
fa-solid fa-arrows-up-down-left-right
fa-solid fa-award
fa-solid fa-backpack
fa-solid fa-bars
fa-solid fa-bee
fa-solid fa-bell
fa-solid fa-block-question
fa-solid fa-bolt
fa-solid fa-boot
fa-solid fa-calendar
fa-solid fa-caret-down
fa-solid fa-caret-right
fa-solid fa-caret-up
fa-solid fa-cart-shopping
fa-solid fa-check
fa-solid fa-chess-knight
fa-solid fa-chess-rook
fa-solid fa-child-reaching
fa-solid fa-circle-check
fa-solid fa-circle-info
fa-solid fa-circle-plus
fa-solid fa-circle-question
fa-solid fa-circle-xmark
fa-solid fa-clock-rotate-left
fa-solid fa-cog
fa-solid fa-coins
fa-solid fa-comment-dots
fa-solid fa-commenting
fa-solid fa-compress
fa-solid fa-computer-mouse
fa-solid fa-cookie
fa-solid fa-copy
fa-solid fa-crosshairs
fa-solid fa-crown
fa-solid fa-cube
fa-solid fa-cubes
fa-solid fa-cut
fa-solid fa-dice
fa-solid fa-dizzy
fa-solid fa-door-closed
fa-solid fa-door-open
fa-solid fa-download
fa-solid fa-edit
fa-solid fa-ellipsis
fa-solid fa-ellipsis-h
fa-solid fa-exclamation
fa-solid fa-exclamation-triangle
fa-solid fa-expand
fa-solid fa-external-link
fa-solid fa-eye
fa-solid fa-eye-slash
fa-solid fa-face-diagonal-mouth
fa-solid fa-face-dizzy
fa-solid fa-face-raised-eyebrow
fa-solid fa-face-smile
fa-solid fa-face-worried
fa-solid fa-feather-alt
fa-solid fa-feather-pointed
fa-solid fa-file-alt
fa-solid fa-file-clipboard
fa-solid fa-file-lines
fa-solid fa-file-text
fa-solid fa-film
fa-solid fa-fire
fa-solid fa-fist-raised
fa-solid fa-flag
fa-solid fa-folder
fa-solid fa-folder-image
fa-solid fa-folder-open
fa-solid fa-gauge-high
fa-solid fa-gear
fa-solid fa-gem
fa-solid fa-globe
fa-solid fa-hammer
fa-solid fa-hand-back-point-up
fa-solid fa-hand-fist
fa-solid fa-hand-holding-medical
fa-solid fa-hand-point-left
fa-solid fa-hand-wave
fa-solid fa-hands-clapping
fa-solid fa-hat-santa
fa-solid fa-hat-witch
fa-solid fa-heart
fa-solid fa-heart-music-camera-bolt
fa-solid fa-history
fa-solid fa-hourglass
fa-solid fa-hourglass-clock
fa-solid fa-hourglass-empty
fa-solid fa-house
fa-solid fa-icons
fa-solid fa-image
fa-solid fa-image-slash
fa-solid fa-info-circle
fa-solid fa-joystick
fa-solid fa-layer-group
fa-solid fa-left-from-bracket
fa-solid fa-lightbulb
fa-solid fa-list
fa-solid fa-list-squares
fa-solid fa-location-check
fa-solid fa-location-xmark
fa-solid fa-lock
fa-solid fa-lock-open
fa-solid fa-magnifying-glass
fa-solid fa-male
fa-solid fa-map-marker-check
fa-solid fa-map-marker-times
fa-solid fa-map-marker-xmark
fa-solid fa-minus
fa-solid fa-minus-square
fa-solid fa-moon
fa-solid fa-mouse
fa-solid fa-music
fa-solid fa-music-slash
fa-solid fa-navicon
fa-solid fa-palette
fa-solid fa-pants
fa-solid fa-party-horn
fa-solid fa-paste
fa-solid fa-pause
fa-solid fa-pen
fa-solid fa-pen-field
fa-solid fa-pen-to-square
fa-solid fa-person
fa-solid fa-person-arrow-down-to-line
fa-solid fa-person-arrow-up-from-line
fa-solid fa-person-falling-burst
fa-solid fa-person-military-pointing
fa-solid fa-planet-ringed
fa-solid fa-play
fa-solid fa-plus
fa-solid fa-plus-circle
fa-solid fa-power-off
fa-solid fa-ranking-star
fa-solid fa-recycle
fa-solid fa-redo-alt
fa-solid fa-refresh
fa-solid fa-right-from-bracket
fa-solid fa-rocket-launch
fa-solid fa-rotate-forward
fa-solid fa-rotate-right
fa-solid fa-scissors
fa-solid fa-search
fa-solid fa-shield
fa-solid fa-shield-alt
fa-solid fa-shield-blank
fa-solid fa-shield-halved
fa-solid fa-shirt
fa-solid fa-shoe
fa-solid fa-shopping-cart
fa-solid fa-sign-out-alt
fa-solid fa-skull
fa-solid fa-smile
fa-solid fa-snowflake
fa-solid fa-sparkle
fa-solid fa-square-dashed
fa-solid fa-square-minus
fa-solid fa-star
fa-solid fa-star-christmas
fa-solid fa-store
fa-solid fa-subtract
fa-solid fa-sun-bright
fa-solid fa-swords
fa-solid fa-sync
fa-solid fa-t-shirt
fa-solid fa-tachometer-alt
fa-solid fa-tachometer-alt-fast
fa-solid fa-terminal
fa-solid fa-trash-alt
fa-solid fa-trash-can
fa-solid fa-triangle-exclamation
fa-solid fa-trophy
fa-solid fa-tshirt
fa-solid fa-up-from-bracket
fa-solid fa-upload
fa-solid fa-user
fa-solid fa-user-astronaut
fa-solid fa-user-check
fa-solid fa-user-clock
fa-solid fa-user-friends
fa-solid fa-user-group
fa-solid fa-user-group-crown
fa-solid fa-user-minus
fa-solid fa-user-plus
fa-solid fa-user-slash
fa-solid fa-user-unlock
fa-solid fa-users-crown
fa-solid fa-video
fa-solid fa-video-camera
fa-solid fa-volume
fa-solid fa-volume-down
fa-solid fa-volume-low
fa-solid fa-volume-medium
fa-solid fa-volume-slash
fa-solid fa-warning
fa-solid fa-wifi
fa-solid fa-wifi-3
fa-solid fa-wifi-strong
fa-solid fa-wrench
fa-solid fa-x
fa-solid fa-xmark
fa-solid fa-zap
Brand Icons (11 icons)#
fa-solid fa-brands fa-apple
fa-solid fa-brands fa-chrome
fa-solid fa-brands fa-discord
fa-solid fa-brands fa-google-play
fa-solid fa-brands fa-instagram
fa-solid fa-brands fa-reddit-alien
fa-solid fa-brands fa-tiktok
fa-solid fa-brands fa-twitch
fa-solid fa-brands fa-windows
fa-solid fa-brands fa-x-twitter
fa-solid fa-brands fa-youtube
Previous
Sounds & Music
Next
Skins & Poses

---

## Skins and Poses

URL: https://bloxd.io/docs/skins

Skin parts, NPC skins and poses for players.


This document lists all API-selectable skins and poses that can be used with the game API.

Usage#
Changing Player Skin#

Use api.changePlayerIntoSkin(playerId, part, skinName) to change a player's skin:

JavaScript
Copy
api.changePlayerIntoSkin(playerId, "body", "body_0_0")
api.changePlayerIntoSkin(playerId, "head", "wizard") // NPC skin
Setting Player Pose#

Use api.setPlayerPose(playerId, pose) to change a player's pose:

JavaScript
Copy
api.setPlayerPose(playerId, "standing")
api.setPlayerPose(playerId, "sitting")
Poses (7 poses)#
standing
sitting
zombie
gliding
driving
sleeping
riding
Skin Parts#

The following skin parts can be customised: skin, hat, head, eyebrows, eyes, back, body, legs, shoes

NPC Skins (15 skins)#

These are special full-body skins typically used for NPCs. Apply them via the head part:

JavaScript
Copy
api.changePlayerIntoSkin(playerId, "head", "wizard")
chef
farmer
farmer_gill
general
monster_hunter_lorenzo
painter_spencer
piggy_banker
portal_mage
tentacle_girl
tentacle_guy
trader
trader_black
trader_blue
wizard
zombie
Skin (24 skins)#
skin_0_0
skin_0_1
skin_0_2
skin_0_3
skin_0_4
skin_0_5
skin_0_6
skin_0_7
skin_0_8
skin_0_9
skin_0_10
skin_0_11
skin_0_12
skin_0_13
skin_0_14
skin_0_15
skin_0_16
skin_0_17
skin_0_18
skin_0_19
skin_0_20
skin_0_21
skin_0_22
skin_0_23
Hat (1 skins)#
hat_none
Head (46 skins)#
head_0
head_1_0
head_1_1
head_1_2
head_1_3
head_1_4
head_2_0
head_2_1
head_2_2
head_2_3
head_2_4
head_3_0
head_3_1
head_3_2
head_3_3
head_3_4
head_4_0
head_4_1
head_4_2
head_4_3
head_4_4
head_5_0
head_5_1
head_5_2
head_5_3
head_5_4
head_6_0
head_6_1
head_6_2
head_6_3
head_6_4
head_7_0
head_7_1
head_7_2
head_7_3
head_7_4
head_8_0
head_8_1
head_8_2
head_8_3
head_8_4
head_9_0
head_9_1
head_9_2
head_9_3
head_9_4
Eyebrows (16 skins)#
eyebrows_0
eyebrows_1_0
eyebrows_1_1
eyebrows_1_2
eyebrows_1_3
eyebrows_1_4
eyebrows_2_0
eyebrows_2_1
eyebrows_2_2
eyebrows_2_3
eyebrows_2_4
eyebrows_3_0
eyebrows_3_1
eyebrows_3_2
eyebrows_3_3
eyebrows_3_4
Eyes (50 skins)#
eyes_0_0
eyes_0_1
eyes_0_2
eyes_0_3
eyes_0_4
eyes_1_0
eyes_1_1
eyes_1_2
eyes_1_3
eyes_1_4
eyes_2_0
eyes_2_1
eyes_2_2
eyes_2_3
eyes_2_4
eyes_3_0
eyes_3_1
eyes_3_2
eyes_3_3
eyes_3_4
eyes_4_0
eyes_4_1
eyes_4_2
eyes_4_3
eyes_4_4
eyes_5_0
eyes_5_1
eyes_5_2
eyes_5_3
eyes_5_4
eyes_6_0
eyes_6_1
eyes_6_2
eyes_6_3
eyes_6_4
eyes_7_0
eyes_7_1
eyes_7_2
eyes_7_3
eyes_7_4
eyes_8_0
eyes_8_1
eyes_8_2
eyes_8_3
eyes_8_4
eyes_9_0
eyes_9_1
eyes_9_2
eyes_9_3
eyes_9_4
Back (1 skins)#
back_none
Body (56 skins)#
body_0_0
body_0_1
body_0_2
body_0_3
body_0_4
body_0_5
body_0_6
body_0_7
body_1_0
body_1_1
body_1_2
body_1_3
body_1_4
body_1_5
body_1_6
body_1_7
body_2_0
body_2_1
body_2_2
body_2_3
body_2_4
body_2_5
body_2_6
body_2_7
body_3_0
body_3_1
body_3_2
body_3_3
body_3_4
body_3_5
body_3_6
body_3_7
body_4_0
body_4_1
body_4_2
body_4_3
body_4_4
body_4_5
body_4_6
body_4_7
body_5_0
body_5_1
body_5_2
body_5_3
body_5_4
body_5_5
body_5_6
body_5_7
body_6_0
body_6_1
body_6_2
body_6_3
body_6_4
body_6_5
body_6_6
body_6_7
Legs (15 skins)#
legs_0_0
legs_0_1
legs_0_2
legs_0_3
legs_0_4
legs_1_0
legs_1_1
legs_1_2
legs_1_3
legs_1_4
legs_2_0
legs_2_1
legs_2_2
legs_2_3
legs_2_4
Shoes (10 skins)#
shoes_none
shoes_0_0
shoes_0_1
shoes_0_2
shoes_1_0
shoes_1_1
shoes_1_2
shoes_2_0
shoes_2_1
shoes_2_2
Notes#
Skin names ending with _none are internal variants and cannot be used via the API.
Skin variants follow the pattern {part}_{style}_{colour} (e.g., body_0_0, head_1_2).
NPC skins apply a complete character appearance through the head part. Person mesh entities also apply the skin's configured default layers; explicit textures slots override those defaults.
Previous
Icons
Next
Block Names

---

## Block Names (1466 blocks)

URL: https://bloxd.io/docs/block-names

Every block name, with its texture and variants.


Each block name listed below is the ROOT block - use it exactly as shown (no suffix).

Some blocks also have meta variants, indicated by codes in brackets.

ROOT BLOCK: Use the block name exactly as listed (e.g. "Maple Door", "Wheat", "Stone")

META VARIANTS: If a block has codes in brackets, you can append suffixes to get variants:

Code	Variant	Name to use
R	rotation	BlockName|meta|rot1 through |meta|rot4
H	halfblockPlacement	BlockName|meta|rot1|top or |bot or |side (combine with R; stairs have no |side)
G	growing	BlockName|Growing
TB	treeBase	BlockName|TreeBase|<WoodType> (e.g. Maple Log|TreeBase|Maple)
TC	treeCanopy	BlockName|TreeCanopy
B	books	BlockName|meta|rot1|books1 through |books6 (combine with R)
FG	freshlyGrown	BlockName|FreshlyGrown (harvestable crop state)
RT	roots	BlockName|Roots (flower with roots for world gen)
LV	lava	BlockName|Lava (lava-growing variant)
TP	top	BlockName|Top (top half of tall plants)
GR	grassRoots	BlockName|GrassRoots (dirt with grass roots)
BK	breaking	BlockName|Breaking (breaking animation state)
FL	flashing	BlockName|Flashing (flashing animation state)
SC	stairsCorner	BlockName|meta|rot1|bot|innerLeft, innerRight, outerLeft or outerRight (combine with R and H)
Text
Copy
Stone           -> Just use "Stone" (no brackets = no variants, root block only)
Maple Door [O,R] -> Root: "Maple Door", Variants: "Maple Door|meta|rot2|open", etc.
Wheat [FG]       -> Root: "Wheat", Variant: "Wheat|FreshlyGrown"
Dirt
GR
Messy Dirt
Grass Block
Sand
Clay
Gravel
Snow
Maple Log
TB
Pine Log
TB
Plum Log
TB
Cedar Log
TB
Aspen Log
TB
Jungle Log
TB
Maple Wood Planks
Aspen Wood Planks
Plum Wood Planks
Jungle Wood Planks
Pine Wood Planks
Cedar Wood Planks
Barkless Maple Log
TB
Barkless Aspen Log
TB
Barkless Plum Log
TB
Barkless Jungle Log
TB
Barkless Pine Log
TB
Barkless Cedar Log
TB
free_placeholder2
Stone
Messy Stone
free_placeholder
Smooth Stone
Diorite
Smooth Diorite
Andesite
Smooth Andesite
Granite
Smooth Granite
Sandstone
Yellowstone
Coal Ore
Iron Ore
Gold Ore
Lapis Lazuli Ore
Emerald Ore
Diamond Ore
Block of Coal
Block of Iron
Block of Gold
Block of Lapis Lazuli
Block of Emerald
White Wool
Orange Wool
Magenta Wool
Light Blue Wool
Yellow Wool
Lime Wool
Pink Wool
Gray Wool
Light Gray Wool
Cyan Wool
Purple Wool
Blue Wool
Brown Wool
Green Wool
Red Wool
Black Wool
Baked Clay
White Baked Clay
Orange Baked Clay
Magenta Baked Clay
Light Blue Baked Clay
Yellow Baked Clay
Lime Baked Clay
Pink Baked Clay
Gray Baked Clay
Light Gray Baked Clay
Cyan Baked Clay
Purple Baked Clay
Blue Baked Clay
Brown Baked Clay
Green Baked Clay
Red Baked Clay
Black Baked Clay
Gray Concrete
Light Gray Concrete
Black Concrete
Blue Concrete
Brown Concrete
Cyan Concrete
Light Blue Concrete
Lime Concrete
Magenta Concrete
Orange Concrete
Pink Concrete
Purple Concrete
Red Concrete
White Concrete
Green Concrete
Yellow Concrete
Pine Leaves
TC
Aspen Leaves
TC
Maple Leaves
TC
Jungle Leaves
TC
Pumpkin_placeholder
Watermelon
Glass
Black Glass
Blue Glass
Brown Glass
Cyan Glass
Gray Glass
Light Gray Glass
Green Glass
Light Blue Glass
Lime Glass
Magenta Glass
Orange Glass
Pink Glass
Purple Glass
Red Glass
White Glass
Yellow Glass
UNUSED BLOCK TYPE
Dim Lamp On
Dim Lamp Off
Water
Invisible Solid
Bricks
Stone Bricks
Dark Red Brick
Dark Red Stone
Block of Quartz
Chiseled Block of Quartz
Engraved Stone
Mossy Stone Bricks
Cracked Stone Bricks
Smooth Sandstone
Engraved Sandstone
Ice
Obsidian
Hay Bale
Sponge
Beacon
temp
Golden Decoration
Moonstone Explosive
Bedrock
Smooth Double Stone Slab
Cactus
G
Grass
Dandelion
RT
Poppy
RT
Red Tulip
RT
Pink Tulip
RT
White Tulip
RT
Orange Tulip
RT
Daisy
RT
Bluebell
RT
Forget-me-not
RT
Allium
RT
Azure Bluet
RT
Lily of the Valley
RT
Shadow Rose
RT
Furnace
R
Workbench
R
Block of Diamond
Maple Door
O
R
_Maple Door Top
O
R
Maple Trapdoor
O
R
Aspen Sapling
Maple Sapling
Jungle Sapling
Plum Sapling
Pine Sapling
Cedar Sapling
Chest
R
Protector
Fat Cactus
G
Dry Fat Cactus
Maple Ladder
R
Vines
G
R
Iron Ladder
R
White Planks
Orange Planks
Magenta Planks
Light Blue Planks
Yellow Planks
Lime Planks
Pink Planks
Gray Planks
Light Gray Planks
Cyan Planks
Purple Planks
Blue Planks
Brown Planks
Green Planks
Red Planks
Black Planks
Artisan Bench
White Ceramic
R
Orange Ceramic
R
Magenta Ceramic
R
Light Blue Ceramic
R
Yellow Ceramic
R
Lime Ceramic
R
Pink Ceramic
R
Gray Ceramic
R
Light Gray Ceramic
R
Cyan Ceramic
R
Purple Ceramic
R
Blue Ceramic
R
Brown Ceramic
R
Green Ceramic
R
Red Ceramic
R
Black Ceramic
R
Wheat Seeds
Wheat_stage1
Wheat_stage2
Wheat_stage3
Wheat_stage4
Wheat_stage5
Wheat
FG
Tilled Soil
Bread Block
ReservedBread BlockRotation1
ReservedBread BlockRotation2
ReservedBread BlockRotation3
Mossy Messy Stone
White Bed
R
_White Bed Head
R
Orange Bed
R
_Orange Bed Head
R
Magenta Bed
R
_Magenta Bed Head
R
Light Blue Bed
R
_Light Blue Bed Head
R
Yellow Bed
R
_Yellow Bed Head
R
Lime Bed
R
_Lime Bed Head
R
Pink Bed
R
Show all 1466
Previous
Skins & Poses
Next
Item Names

---

## Item Names (1492 items)

URL: https://bloxd.io/docs/item-names

Every item name, with its texture.

Wood Pickaxe
Stone Pickaxe
Iron Pickaxe
Gold Pickaxe
Diamond Pickaxe
Moonstone Pickaxe
Golem Pickaxe
Wood Axe
Stone Axe
Iron Axe
Gold Axe
Diamond Axe
Moonstone Axe
Artisan Axe
Wood Spade
Stone Spade
Iron Spade
Gold Spade
Diamond Spade
Wood Sword
Stone Sword
Iron Sword
Gold Sword
Diamond Sword
Knight Sword
Wood Hoe
Stone Hoe
Iron Hoe
Gold Hoe
Diamond Hoe
Flashlight
Mining Helmet
Wood Helmet
Iron Helmet
Gold Helmet
Diamond Helmet
Wood Chestplate
Iron Chestplate
Gold Chestplate
Diamond Chestplate
Fur Chestplate
Wood Leggings
Iron Leggings
Gold Leggings
Diamond Leggings
Wood Boots
Iron Boots
Gold Boots
Diamond Boots
Spiked Boots
Wood Gauntlets
Iron Gauntlets
Gold Gauntlets
Diamond Gauntlets
Military Helmet
Military Chestplate
Military Gauntlets
Military Leggings
Military Boots
White Wood Helmet
White Wood Chestplate
White Wood Leggings
White Wood Boots
White Wood Gauntlets
Orange Wood Helmet
Orange Wood Chestplate
Orange Wood Leggings
Orange Wood Boots
Orange Wood Gauntlets
Magenta Wood Helmet
Magenta Wood Chestplate
Magenta Wood Leggings
Magenta Wood Boots
Magenta Wood Gauntlets
Light Blue Wood Helmet
Light Blue Wood Chestplate
Light Blue Wood Leggings
Light Blue Wood Boots
Light Blue Wood Gauntlets
Yellow Wood Helmet
Yellow Wood Chestplate
Yellow Wood Leggings
Yellow Wood Boots
Yellow Wood Gauntlets
Lime Wood Helmet
Lime Wood Chestplate
Lime Wood Leggings
Lime Wood Boots
Lime Wood Gauntlets
Pink Wood Helmet
Pink Wood Chestplate
Pink Wood Leggings
Pink Wood Boots
Pink Wood Gauntlets
Gray Wood Helmet
Gray Wood Chestplate
Gray Wood Leggings
Gray Wood Boots
Gray Wood Gauntlets
Light Gray Wood Helmet
Light Gray Wood Chestplate
Light Gray Wood Leggings
Light Gray Wood Boots
Light Gray Wood Gauntlets
Cyan Wood Helmet
Cyan Wood Chestplate
Cyan Wood Leggings
Cyan Wood Boots
Cyan Wood Gauntlets
Purple Wood Helmet
Purple Wood Chestplate
Purple Wood Leggings
Purple Wood Boots
Purple Wood Gauntlets
Blue Wood Helmet
Blue Wood Chestplate
Blue Wood Leggings
Blue Wood Boots
Blue Wood Gauntlets
Brown Wood Helmet
Brown Wood Chestplate
Brown Wood Leggings
Brown Wood Boots
Brown Wood Gauntlets
Green Wood Helmet
Green Wood Chestplate
Green Wood Leggings
Green Wood Boots
Green Wood Gauntlets
Red Wood Helmet
Red Wood Chestplate
Red Wood Leggings
Red Wood Boots
Red Wood Gauntlets
Black Wood Helmet
Black Wood Chestplate
Black Wood Leggings
Black Wood Boots
Black Wood Gauntlets
Shears
Artisan Shears
Stick
Coal
Raw Iron
Iron Bar
Iron Fragment
Raw Gold
Gold Bar
Gold Fragment
Diamond
Diamond Fragment
Moonstone
Lunite
Moonstone Fragment
Bowl
Partially Full Bowl of Cranberries
Half Full Bowl of Cranberries
Nearly Full Bowl of Cranberries
Bowl of Cranberries
Mushroom Soup
Glowing Soup
Night Vision Soup
Cotton
Gold Crop
Bucket
Water Bucket
Lava Bucket
Boat
INTERNAL_MESH_Boat
Obsidian Boat
INTERNAL_MESH_Obsidian Boat
Speedboat
INTERNAL_MESH_Speedboat
Wood Hang Glider
INTERNAL_MESH_Wood Hang Glider
Iron Hang Glider
INTERNAL_MESH_Iron Hang Glider
Gold Hang Glider
INTERNAL_MESH_Gold Hang Glider
Diamond Hang Glider
INTERNAL_MESH_Diamond Hang Glider
Hovercraft
INTERNAL_MESH_Hovercraft
Yellow Kart
White Kart
Red Kart
Purple Kart
Pink Kart
Orange Kart
Magenta Kart
Lime Kart
Light Gray Kart
Light Blue Kart
Green Kart
Gray Kart
Cyan Kart
Brown Kart
Blue Kart
Black Kart
INTERNAL_MESH_Yellow Kart
INTERNAL_MESH_White Kart
INTERNAL_MESH_Red Kart
INTERNAL_MESH_Purple Kart
INTERNAL_MESH_Pink Kart
INTERNAL_MESH_Orange Kart
INTERNAL_MESH_Magenta Kart
INTERNAL_MESH_Lime Kart
INTERNAL_MESH_Light Gray Kart
INTERNAL_MESH_Light Blue Kart
INTERNAL_MESH_Green Kart
INTERNAL_MESH_Gray Kart
INTERNAL_MESH_Cyan Kart
INTERNAL_MESH_Brown Kart
INTERNAL_MESH_Blue Kart
INTERNAL_MESH_Black Kart
Off Roader
INTERNAL_MESH_Off Roader
Gold Mining Drill
Iron Mining Drill
Diamond Mining Drill
Moonstone Mining Drill
Armored Car
INTERNAL_MESH_Gold Mining Drill
INTERNAL_MESH_Iron Mining Drill
INTERNAL_MESH_Diamond Mining Drill
INTERNAL_MESH_Moonstone Mining Drill
INTERNAL_MESH_Armored Car
Light Blue Car
INTERNAL_MESH_Car
Snowball
Snowball Launcher
Pebble
Reinforced Pebble
Bullet
Ball
Reinforced Ball
Frag Grenade
Mining Grenade
Smoke Grenade
Moonstone Orb
Show all 1492
Previous
Block Names
