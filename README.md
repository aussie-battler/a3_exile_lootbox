# LOOT BOX for Arma3 EXILE MOD and Community " a3_exile_lootbox"
A small happiness to fishing for items・・

Development and copyright: nabek (blog. ahh. jp) 2018/4
*Update history is at the end of the sentence

# Operating manual (Japanese）

# Index / table of contents
- Add-on Overview
- Check the operation.
- Operation description
- How to install
- Setting method
- Resources
- Log content
- About Log errors
- About mods
- About license support
- Known issues-bugs
- Maybe from the developer-like nabek
- Change log / update history

## Add-on Overview
It is an add-on for Arma3 EXILE MOD server.
We will provide mainly functions that place importance on the"town".
Many functions are obtained from the map data, so basically it works with no settings.

For item fishing in the town, place the item box somewhere on the surface of the town or in the building, apart from the usual item spring.
The item box contains items, pop-tabs, and trash that will be used for the initial player.
(Wire traps and landmines are installed around the item box）

The vehicle springing up also, it is equipped with its own(add a function）
There are many other features built-in that will keep players from getting bored and out of the ordinary.

Since I intend to have written the code as carefully as possible, please do not worry.Please remodel if necessary.
There is no necessary MOD (depends on the setting）
"Arma3 DMS(a3_dms)" is required as a server add-on.

### Functions related to the location engine
	o place the item box in the town
		Randomly placed indoors / outdoors
		You can set item elements finely
		Also, a wire trap can be installed at the same time
	o place vehicles and aircraft springing up in the town
		The difference with the Server side is the detailed setting of the fault condition and other items spring up
		There are also GRP traps and grenade traps
		(It sprang up near the building and does not springing on the road）
	o place Bandit AI in town
		It is located in a building, wandering the town, or holed up
		By location (altitude) will be a sniper
	o place mines around town
		Will be installed on the road
	o place strange objects and flaming objects in the town
		Give the player a different landscape of the city
	o random installation of a campfire
	o place the traveler AI
		AI who are moving between town and town
		Think of it as a moving item box
	o Iron Man AI (invincible?Place )
		Invincibility with healing ability?Bandit AI
	o GPS trap
		If found by bandit, it will be marked on the map.
		On the vehicle engine also operates in the established
	o grenade trap
		It is established at the vehicle engine ON and the trap is activated
		(Smoked or mini-grenades）

### Other
	o position setting is basically unnecessary(automatic recognition）
		It is automatically acquired from the map data and operates automatically
		Even if you change the map, it works as it is (basically
	o Water drawing object can be fixed and installed
	o you can create original place names in the map
	o you can display text in the map
	o you can create custom signage
		You can paste any image you want
	o server message delivery
		Deliver messages to all players on a regular basis

The start-up of this LOOTBOX add-on runs in parallel with other add-ons(waiting for delay or load）
Depending on the map data and server specifications, it may take a few minutes for the process to complete.
If the player is still available, the process may continue.
(It is according to the specifications of Arma3 server, other add-ons are also the same）
* Reference: for CUP Takistan, about 3 minutes(Windows / Core i5）

## Check the operation
Arma3 1.82.144710 64bit/32bit
Exile MOD Server 1.0.3 a/1.0.4 a (Pineapple)
Windows 10
Linux(Ubuntu 17.10/18.04 LTS)

## Operation description
[Map location]
The location information registered in the map (towns and landmarks, etc.) to the target, placing the item boxes and the like at random.
By default, it works for the ３ categories of"Village, Town, Big Town".
It is possible to specify not only the location type but also the location name (depending on the map）
If the type matches, it is unconditional for all towns, so if you want to disable it, set it separately.

If you also want to target other landmarks, see below or explore the map data.
https://community.bistudio.com/wiki/Location
	Location type name
	NameVillage village
	NameCity town
	NameCityCapital Big Town
	NameLocal some kind of landmark
	Mount mountain
	Airport
	etc..

	Technical：
	In the map data, it is registered in the set of"type name"and"place name"for each point.
	Therefore, if you specify a place name, not a type, only one part of the target.
	If you want to target any landmarks (NameLocal) that are not registered as towns, please set them manually by referring to the log file.
	(For CUP Takistan,"mountain and forest","village","oil pipeline","minefield", etc.)）
	It becomes the only setting item which depends on the map (NameLocal)in this add-on.

	Move the reference point slightly when finding a location to increase the random element.
	
[Create new location]
You can create your own location on the map.
It is also possible to make this location a target of operation.

	Technical：
	The location type takes over the settings registered on the Arma3 side.
	(Map display color, font, size, icon type, etc）

[Item Box location]
The location of the item box is randomly determined by the following conditions.
	o location in the MAP data within the range based on the registration point
	o pick a building in the range at random and either indoors or out
	* Indoor: any indoor location(mainly by window or doorway, etc）
		The place farthest from the entrance is chosen
	* Outdoor:around and near the building
	(If there is no building within the range, it will be invalid）
	
	Technical：
	o indoor springing, utilize the buildingPosition data

[Item list generation]
Applies to item boxes, springing vehicles, and possession of bandit AI.
The item list is determined by multiple elements, not by simple random generation.
For each individual item box, the sum of the following elements is consolidated and determined.

Item element → rare added?　→ Garbage → shuffle → decision

	o fixed (all types common）
	o fixed (if the magnification is specified, multiple random)
	５０％randomly selected in the o list
	o one of the "rare" list is selected at random
	o from within "special rare", select one in the establishment
	o pop tab added in range random
	Technical：
	We have taken care of the calculation so that it is distributed as fairly as possible.
	In the end, the order of the list will also fall apart.
	(Truncate due to container capacity limit）

[Garbage filter]
Replaces the percentage of garbage with the finished list of items.
(In other words, if you set the garbage reduction rate in one, all will be changed to garbage）
In the same setting, the item box in the village can be in the form of a lot of garbage.

[Pop tab]
The item box contains a random pop tab.
The value set as the maximum, it will be random at 30% lower limit.
The vehicle will be the same.

	Example: for a specified value of 1000, 1000 x 0.3 = 300 (lower limit value）
	Random in the range of 300-1000

[Item box strap]
A trap Wire is placed near the item box(outdoor & established）
It is installed around 2m in the circumference at random.
You can change it to another trap.

	Technical：
	Depending on the terrain, it may be hidden in the ground.
	(I have fine-tuned it, but there is a limit）

[Item box fixed springing]
You can have the item box springing to the designated place regardless of the location.
It is assumed a prized use, such as a maze, a mountaintop and a hard place to go.

	Technical：
	It is not limited to this item, but the coordinates can be only X/Y.
	"0" on the Z-value axis means the ground at that point.
	Example: [1800,2130,0]
	It can not be installed in the safe zone or near the stronghold.

[Traps-land mines]
１ once you have placed all the item boxes in the location, you will randomly place the mines on the surrounding roads.
Very, because it becomes brutal set, please note.
On the EAST side, because it is in the form that the location of the land mine is known, I think that there is no AI hanging.
You can change it to another trap.

	Technical：
	It is installed in the center of the road.
	All locations recognized as roads in the map data will be applied(e.g. airport runway）

GPS trap .]
When found in a vehicle trap or bandit, it will be marked as a black point on the map.
If found in bandit (shot), it will be always marked.
Bandit is limited to the ones you spawn with this add-on.
(Town AI, traveler AI, Iron Man AI）
It is also marked when shooting at a friend or a zombie because it is a trigger.
(Even if it is a zombie, it will know that the player is in the vicinity）
Even in the case of a vehicle, the trap is activated at the establishment.
The places to be marked will be approximate.

	Technical：
	In the case of the vehicle, in the establishment of the second%, the trap is determined, it will be the grenade trap or GPS trap. ５０ 車両の ５０ ５０、５０センターでトラップが 確定定し、ｇｐｇトラップとなります。
	The map marks are updated in AI Group increments and in one minute increments.

[Grenade trap]
Two seconds after the engine has been applied, a smoke grenade or a mini grenade is triggered by a vehicle-specific trap.
In the establishment of approximately ２０％, it will be a mini-grenade.

	Technical：
	The event Hook will be deleted at first one time only.

[Strange objects]
You can place a random number of the specified objects anywhere within the range.
By default, dead trees, statues, drums, damaged vehicles, etc. are set.
It is possible to provide a different atmosphere than usual by scattering broken vehicles, garbage, old tires, carcasses, etc.
In addition, it is also possible to put the building, it has become possible to change the city in a pseudo manner.

	Technical：
	Randomly located in the free space, but you choose as close to the building as possible.
	However, the flat type is placed preferentially on the road(oil leakage, blood pool, garbage band, etc）
	It can be avoided by setting the size of the object so that it does not overlap with other objects.
	On a load basis, it is recommended to disable the simulation.
	(It is generated by CreateSimpleObject.About 10-20% load drop）

[Campfire]]
A small campfire will be set up for crafting, cooking, night lighting, and more.
At random, it will be placed near the building.
Please use it as a measure for the initial player(such as spawning place and village）

[Fire object]
In the town random, fire and black smoke, multiple installation.
Together with it, you can install objects at random.
You can set up objects such as vehicles and helicopters, as well as buildings and building materials.
As a dummy of heli-crash, you can see the location of the town even from a distance.
	
	Technical：
	It is not limited to this item, but it will be installed avoiding the road.
	It is also in order to prevent the AI patrol vehicle collision.
	
[Bandit town AI]
Bandit AI can be randomly placed indoors (mainly near windows and inlets).
If the height of the location in the building is more than the specified height, you can place the sniper.
In addition, it is also possible to set the propriety of patrolling.
When patrolling, loitering nearby vehicles, roads, and gas stations.
You can set the class as a custom, the equipment can be set to another.
(DMS settings are used for AI skill settings）
If there is no building, it will be placed randomly within the range.
If the player is found (fired), the map marks the approximate location.
(Name: GPS trap）

	Technical：
	The difficulty level is set as DMS setting(random).
	If the player is not nearby, it has stopped working (DMS Freeze）
	The map position is selected as high as possible (ASL standard), but it is ignored in the following cases.
	o if the location type is airfield/Airport / military base
	o when the height difference in the region is less than or equal to 10m

	Indoor location utilizes the buildingposition data of the map.
	Among them, select the closest location to the road within the vicinity 100m.
	This is a consideration to increase the encounter rate with the player.

	We are processing one AI as a group.
	(Arma3 allows you to manage more than 200 groups, but bear that in mind）
	
	The AI that the patrol is allowed, the way point is set in the nearby vehicles and roads, refueling place.Up to ５ places
	(Both search in the location setting range from the spawn location）
	If there are few waypoints, the location reference points are used.
	Finally, return to the spawn location to patrol.

	If you make it a custom class, you can change the equipment.
	For the possession of the item, we will use this item box engine.
	(LB_LootAllFixedItems (all fixed settings) are not used）
	
[Vehicle]
Players will be freely available as well as vehicles springing up in the Exile server.
A vehicle is located on a vacant lot near a building, and similar to an item box, you can store items and pop tabs in your inventory.
It's more like someone parked the car than it is.
In addition, it is possible to specify the damage to each site.
The amount of gasoline specified is random, and the lower and upper limits can be specified, respectively.
If you do not use the random gasoline, the upper limit will be used.
If there is no building, it will be placed randomly within the range.
When the engine is turned on, a smoke or mini-grenade trap will be activated at the establishment (smoke or mini-grenade）
(Or, the GPS trap will activate）

	Technical：
	If the class name contains”_bike”, no damage is done.
	Please refer to the reference for damage.
	The range is examined according to the vehicle type(collision prevention with the building）
	Fixed-wing aircraft springing is not recommended(physics）

----------------------------------------------------------------
The following will work independently from the location engine.
----------------------------------------------------------------

[Traveler ]]
Place the AI moving between towns.
Occurs in all capital cities (large towns) on the map and moves nearby towns.
(Depending on the map, around 1-1. 5 Km）
Think of it as a moving item box.
１ you can set the number of AI in the group.
Equipment, location equipment settings of bandit town AI will be used.
You can set the possession item and pop tab.
If the player is found (fired), the map marks the approximate location.
(Name: GPS trap）

	Technical：
	In CUP Takistan map, the Big Town (NameCityCapital) will be four places.
	This is the best game I have ever played.
	Waypoints will be subject to any of the town's NameCity.
	In most cases, the roadway is supposed to be paved, so the encounter on the road is assumed.
	Within the location engine, we are collecting the location of the target.
	
[Iron Man]
It is a special bandit that is resistant to the zombie bacterium, it has a tremendous healing power.
Even if you knock it down, you will get up again(regeneration Springs）
If it falls, smoke is burned from the place.
I have a cap, a machine gun, and a grenade in my prison suit(I can't capture myself).）
It is equipped with a bi-pot and a scope.
As a fixed springing, specify the location.１ you can set as group multiple AI.
Please use such as difficulty adjustment.
If the player is found (fired), the map marks the approximate location.
If you die, all equipment and items will be removed.
There are no umami marks for the player.

	Technical：
	During the damage event, it is fully open the physical strength.
	We will patrol about 300m.
	Do not hide, as soon as you find the player, Fire.
	It is equipped with:
	MMG_01_hex_F/acc_flashlight/optic_AMS_snd/bipod_02_F_hex
	Within the location engine, we are collecting the location of the target.

[Water drawing object]
Fixed installation of objects that can craft fresh water.
exile_3den.it can be installed without relying on the export by the pbo tool.

	Technical：
	The default object is"Land_WaterCooler_01_new_F".
	If you have made a separate change, you will need to rewrite the code.

[Custom signs]
Custom signs can be placed anywhere on the map.
You can put your own server color, such as server rules and logos.
You can paste the images stored in the mission file and change the texture.
In the Eden editor, make a note of only the number of the position and direction, please set.
(The direction is the value of " z " in the rotation item）
It works with all objects, even if it is not a signboard object(only configurable objects）

	Technical：
	The image file must be stored in a mission file.
	Jpeg or Paa (Arma3 proprietary) format images are available.
	(The size must be 2^x size）
	※64/128/256 / 512, 512 * 256, 512 * 512
	*If possible, set the file size to less than 20KB
	enableSimulationGlobal/enableRopeAttach/allowDamage etc are generated with false
	Some objects cannot change the texture.
	(Here we recommend a sign）
	Only one object can handle multiple textures.

[Map characters]
Put characters anywhere on the map.
It is possible to specify the size and color specification.

	Technical：
	Because it is realized by the function of the existing map marker, it hangs a load when placed in large quantities.
	Size will be the magnification specified for each aspect.
	It depends on the main unit or mission settings, so you can not choose the Font from here.

[Server message delivery]
Periodically, we deliver messages to all players.
Multiple messages can be defined, and each row can be switched to deliver.

	Technical：
	The delivery interval can be specified in seconds, but the actual delivery will include lags.
	On the Arma3 specification, it becomes difficult to read because the font is special and the Japanese collapses.
	because it is distributed in systemChat, there are times when it disappears immediately by scrolling.

## How to install
a3_exile_lootbox.unpack the pbo and make the necessary settings.
* PBOManager (free) is required to manage PBO files
※This document(readme_jp.txt)is unnecessary for operation, so please delete it
Again, the a3_exile_lootbox.re-pack the PBO to pbo.

Please place it as a PBO file in the Exile server at@ExileServer/addons/.
The Exile server will call it automatically.
In addition, if necessary, the mission file (mission.sqm) (see below）
Check if there is an error in the log file when the server is running(see below）

## Setting method
There are several files in the distribution file, and you need to unpack PBO to edit the settings.
Basically, the " config.only " sqf " is eligible for configuration Editing.

	Main settings
	o target location
	o item type
	o traps related
	o Bandit AI-related
	o strange object related
	o fire-related objects
	o vehicle spring related
	o location creation

	(Non-location related）
	o traveler AI
	o Iron Man
	o custom signs

The default configuration is a fairly simple item configuration.
Set the position of this item box according to the environment of the server and change the setting.
Basically, it will auto-fit on all maps as they are.

[How to set]]
Please edit it carefully according to the notation of Arma3 scripting.
Many parts are commonly used in programming languages and have the same notation.
If you write it incorrectly, it will be reported in the log as a script error.

	o [], {},"", etc. must be paired
	the end of line of the o Code must always end with a"; " semicolon
	o separate elements by", " in the configuration of[]array
	(However, after the last element, there is no need to write）
	double-byte characters (Japanese, etc.) cannot be used in o code
	(However, you can freely write in the comments）
	o the character code is "UTF-8" and the line feed code should match the OS of the server
	(Windows: CR/LF,Linux: LF）
	when you specify the o object, you must specify the formal class name
	the portion to set the number of o is not necessarily applied only a few minutes
	(Due to errors, etc., the process may be skipped.This is the maximum value you would like）
	o items in the establishment setting are written from 0.00 through 1.00.1 is 100%.

	[Main files]
	config.sqf configuration file
	putBoxes.sqf implementation
	./functions/ generic script file
	readme_jp.txt this file, please delete at the time of Operation start
