## What is instancing?

Instancing is the process of duplicating a previously existing map, replicating it into one unique *instance* and
copying the NPCs from the original map, onto the new one. And instanced map applies for only a single party and it's
members. Using this system, a party can have exclusive access to one map, where no-one else can access it unless in the
party.

## How to...

Before you start, you have to choose the map, that you want to have instanced. Various restrictions are put on the map
names on client-side. If you ignore them, the client usually crashes upon entering the instanced map.

- Only maps, that begin with a number and @ (e. g. 1@tower) are recognized as instance map by the client. If you want to
  use a map, that does not match this naming scheme, just must attach it with emulation (parameter <use basename> in
  command instance_attachmap), which makes the client think, that it is on the actual map, instead of an instance.
- Map name length limitations:
  - For emulated instance maps you cannot use maps, whose names are longer than 7 characters, because the instance map
    name is composed of 3 digits, followed by \# and the original map name.
  - For client-recognized instance maps, the map name limit is 8 characters, because the instance map name is composed
    of 3 digits and the original map name.
- Client-recognized instance maps require a self-reference inside the data\resnametable.txt file. Example:

<!-- -->

    1@tower.gnd#1@tower.gnd#
    1@tower.gat#1@tower.gat#
    1@tower.rsw#1@tower.rsw#
    유저인터페이스\map\1@tower.bmp#유저인터페이스\map\1@tower.bmp#

### Use the instance functions

There are several functions you need to familiarize yourself with:

**instance_create "<name>", <party id>;**  
Creates an instance with the name "<name>", for the party <party id>.  
*Returns:* Unique ID of the instance, negative number on failure.

**instance_attachmap "<map name>", <instance id>\[, <use basename>\];**  
Attaches the specified map onto the instance. Optional parameter <use basename> specifies whether a map requires
emulation for instancing or not (default).  
*Returns:* Name of the map if successful, otherwise an empty string.

**instance_attach <instance id>;**  
Attaches this instance onto the current script.

**instance_set_timeout <limit>, <limit2>\[, <instance id>\];**  
<limit> is the total time the instance will stay alive, <limit2> is how long players have when they are outside of the
instance until it is destroyed. If <instance id> is ommited, current instance attached to the current script is taken.
If no instance attached, instance of the attached player's party is taken.

**instance_init <instance id>;**  
Creates the instance, copying all NPCs and initializing the timer.

**instance_destroy \[<instance id>\];**  
Removes the instance, destroys all NPCs on the instanced map and ends the timer. If <instance id> is ommited, current
instance attached to the current script is taken. If no instance attached, instance of the attached player's party is
taken.

**instance_npcname "<npc name>"\[, <instance id>\];**  
Retrieves the unique address of an NPC on an instanced map. If <instance id> is ommited, current instance attached to
the current script is taken. If no instance attached, instance of the attached player's party is taken.

**instance_announce <instance id>, "<message>", <flag>, <color>\[, <type>\[, <size>\[, <alignment>\[,
<position>\]\]\]\]\];**  
Displays an announce inside the specified instance. If <instance id> is 0, current instance attached to the current
script is taken. If no instance attached, instance of the attached player's party is taken.

**has_instance "<map name>"\[, <instance id>\];**  
Checks, whether the given map is attached to the specified instance or not. If <instance id> is ommited, current
instance attached to the current script is taken. If no instance attached, instance of the attached player's party is
taken.  
*Returns:* Name of the instance map if successful, otherwise an empty string.

**instance_warpall "<map name>", <x>, <y>\[, <instance id>\];**  
Warps entire party, that is attached to given instance to a map at specified coordinates. If <instance id> is ommited,
current instance attached to the current script is taken. If no instance attached, instance of the attached player's
party is taken.

### Create an instanced map

Let's say we want to instance **payon**, allow players 1 hour on the map, and they have 5 minutes to return before the
instance is destroyed. We would do so like this:

    set .@instance, instance_create("Payon instanced", getcharid(1));
    if( .@instance < 0 )
    {
    	mes "Failed to create the instance!";
    	close;
    }
    if( instance_attachmap("payon", .@instance) == "" )
    {
     	instance_destroy(.@instance);
    	mes "Failed to attach payon as a map!";
    	close;
    }
    instance_attach(.@instance);
    instance_set_timeout(3600, 300, .@instance);
    instance_init(.@instance);

    warp "payon", 150, 150;

From the code mentioned above, allow me to iterate what each one does.

`set .@instance, instance_create("Payon instanced", getcharid(1));`

This piece of code creates an actual instance, returning the instances' unique ID into .@instance. `getcharid(1)` is
obviously the character's party ID. Please remember, it's up to you to perform the necessary party checks before this
function.

`if( .@instance < 0 )`  
`{`  
` mes "Failed to create the instance!";`  
` close;`  
`}`

This checks whether an instance was actually created. Generically, this will only happen if no instance name was
specified, or if there was no party ID.

`if( instance_attachmap("payon", .@instance) == "" )`  
`{`  
` instance_destroy(.@instance);`  
` mes "Failed to attach payon as a map!";`  
` close;`  
`}`

If the instance fails to attach payon as an instanced map, we need to destroy the instance altogether
(instance_destroy), and then we simply output that it failed.

`instance_attach(.@instance);`

Using this command, we attach the instance as a part of the current script. This means, instance commands which run from
this point will apply to the instance we created.

`instance_set_timeout(3600, 300, .@instance);`

This command tells the instance that the players who use this instance will have 1 hour (3600 seconds) to use the
instance, and 5 minutes (300 seconds) until the instance is destroyed, if they leave the instanced map(s).

`instance_init(.@instance);`

This command will now initiate the instance. This means it will duplicate all of the NPCs from the original map to the
instanced one, and will load the 'timer' display window with the name of the instance. From this point, the players will
have 1 hour to use the instance.

`warp "payon", 150, 150;`

By default, when an instance is created and a player is asked to warp to the map, if the source picks up that an
instance was created for this map, *for this party*, it will automatically warp the player to the **instanced version of
the map** and not the original.

### Manipulate NPCs on an instanced map

There's a very specific function which will determine how to retrieve and use NPCs. *instance_npcname* will change the
specified NPC name from the one you want, to the one that exists on the map, dependant on the instance.

    (Insert instance commands here)
    instance_init(.@instance);

    donpcevent instance_npcname("My duplicated NPC", instance_id()) + "::OnSomeEvent";

After *instance_init* has been called, we can alternately use the command *instance_id* which will return exactly the
same thing as we stored in .@instance. The function *instance_npcname* effectively translated the NPC name into the
specific one for the instance. "My duplicated NPC" will become the name of the NPC stored on the instance (not the one
on the original map).

### Broadcast on an instance map

To broadcast a message on an instanced map, there's a specific function designed for this purpose.

`instance_announce(instance_id(), "Hello to the players in the instanced map!", bc_npc|bc_yellow);`

Much functioning like the original *announce* command, this command broadcasts a message, with the flag and color
settings. In order to broadcast on the map, you'll need to provide the instance ID as the first argument.

## Conclusion

See \[\`doc/script_commands.txt\`\](https://github.com/HerculesWS/Hercules/blob/stable/doc/script_commands.txt) for a
couple more commands on how to instance a map, otherwise, hopefully this article should be enough to understand the
concept of instancing.

[Category:Client Configuration](Category:Client_Configuration "wikilink")
