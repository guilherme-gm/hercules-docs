!!! warning
	This page may contain outdated information, incompatible with the current version of Hercules and its coding standards.

# Menus

## Menu Command

The menu command is hardly used anymore, but can be helpful for a few quick setups.

- menu "
  <menu option>

  ",<label>{,"

  <menu option>

  ",<label>,...}; // Thanks to Dj-Yhn

This command has two parts to it, the menu option (which is what the users see to select) and the label (where the menu
option takes them if they select it)

### Example 1.1 - Standard Menu Command Setup

`menu "Option 1",L_GoToOption1,"Option 2",L_GoToOption2;`  
  
`L_GoToOption1:`  
`mes "You chose option 1";`  
`close;`  
  
`L_GoToOption2:`  
`mes "You chose option 2";`  
`close;`

While this is nice, there is also a nifty little trick to this command. Notice that L_GoToOption1 is directly under the
menu command itself? We don't need to use a label for this option, because we can tell the menu command to simply
continue to the line down by replacing the label name in the menu line with a -.

### Example 1.2 - Optimizing the Menu Command

`menu "Option 1",-,"Option 2",L_GoToOption2;`  
  
`mes "You chose option 1";`  
`close;`  
  
`L_GoToOption2:`  
`mes "You chose option 2";`  
`close;`

Now we have a simplified menu command that only uses one label, rather than two.

------------------------------------------------------------------------------------------------------------------------

## Select Command

The Select command followed by the Prompt command are now usually the top two contenders for menu selection.

- select "Option"{,"Option",...,"Option"}; // Thanks to Dj-Yhn
- select "Option 1:Option 2";

Rather than selecting an option and then moving to a label, you get a returned value for the option selected. @menu is a
character variable that is set after selecting an option.

### Example 2.1 - Standard Select Command Setup

`select "Option 1","Option 2";`  
  
`if (@menu == 1) { mes "You chose option 1"; }`  
`else { mes "You chose option 2"; }`  
`close;`

This can be further broken down into an even more efficient method.

### Example 2.2.1 - Optimizing the Select Command

`if (select("Option 1","Option 2") == 1) { mes "You chose option 1"; }`  
`else { mes "You chose option 2"; )`  
`close;`

Select also has a different setup than the Menu Command. Notice that there are no labels anymore? That's because we use
values returned rather than going to different places.

In the second example, you will notice that the select command can run with a single string separated by a colon for
each option. This can be quite handy with arrays and dynamic menu setups, however that will come in a more later
discussion.

For a simple method, I will demonstrate how to include a GM Option to your menu that only GM Players can see.

### Example 2.2.2 - Optimizing the Select Command

`switch(select("Option 1:Option 2")) {`  
`  case 1:`  
`    mes "You chose option 1";`  
`    break;`

`  case 2:`  
`    mes "You chose option 2";`  
`}`  
`close;`

You can also jump right into the switch statement with the Select() command. Rather than using the predefined @menu
variable, you can simply switch the command itself.

### Example 2.3 - Using a Unique Variable for Returning an Option Choice

`set .@playerChoice, select("Option 1:Option 2");`  
`set .@myOtherChoice, select("Option 1:Option 2");`

By looking at these, if we were to only use the standard @menu, they would overwrite each other, simply for the fact
that each one of them would attempt to store @menu as the index chosen. By placing a set and a variable before to the
select returned value, we can now distinguish between the two menu options selected.

### Example 2.4 - Simple Dynamic Menu using Select

`set .@menu$, "Player Option 1:Player Option 2";`  
  
`if (getgmlevel() >= 99) { set .@menu$, .@menu$ + ":GM Menu"; }`  
  
`switch(select(.@menu$)) {`  
`  case 1:`  
`    mes "Player Option 1";`  
`    close;`  
  
`  case 2:`  
`    mes "Player Option 2";`  
`    close;`  
`  `  
`  case 3:`  
`    mes "GM Menu";`  
`    close;`  
`}`

Normal players will not be allowed to choose the case 3 option of GM Menu, because it is not added to the menu list
unless they meet the criteria of being a level 99 GM.

This can be tricky when trying to add more than a single added option based on criteria due to the fact that the case
might not be in order, if you don't add the options. This will be discussed in the "Advanced Scripting" area later.

------------------------------------------------------------------------------------------------------------------------

## Prompt Command

The Prompt command followed by the Select command are now usually the top two contenders for menu selection.

- prompt "Option"{,"Option",...,"Option"}; // Thanks to Dj-Yhn
- prompt "Option 1:Option 2";

The prompt command works exactly like the select command however a value of 255 is passed back to the script if the user
decides to choose the CANCEL button that is automatically generated by menus.

### Example 3.1 - Quick Example of the Prompt Command

`prompt "Click Me:No Click Me";`

`if (@menu == 255) { mes "You should not have closed the menu... BAD BOY!"; close; }`
