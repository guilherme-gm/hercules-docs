# RID

Most scripting commands and functions will want to request data about a character, store variables referenced to that
character, send stuff to the client connected to that specific character, etc. Whenever a script is invoked by a character,
it is passed a so-called RID - this is the account ID number of a character that caused the code to execute by clicking
on it, walking into it's [OnTouch](../scripting/events/ontouch.md) zone, or otherwise.

## Usage

When writing simple [NPCs](./npc.md) only, this topic will not require much attention. However, when using
[functions](../scripting/functions.md), [timers](../scripting/timers.md), or clock-based script activation, one
requires to be aware of all cases when a script execution can be triggered without a RID attached. This will make a lot
of commands and functions unusable, since they request data from a specific character, send data to a specific client,
or store variables specific to a character, which are unavailable, if there's no RID, which refers to the character to
work with, unless [attachrid](../scripting/commands/attachrid.md) is used to explicitly attach a character to the script first.

Whenever is stated **invoking character** or **currently attached character**, it actually means *the character whose RID is
currently attached to the running script*. The script function [playerattached](../scripting/commands/playerattached.md) can be used
to check which is the currently attached player to the script (it will return 0 if the there is no player attached or
the attached player no longer is logged on to the map-server). The function [detachrid](../scripting/commands//detachrid.md) will
explicitly set the RID to 0, so care must be taken, that follow-up commands do not depend on a character being attached,
especially access to [temporary character variables](../scripting/variables.md).
