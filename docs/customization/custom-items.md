# Custom Items

## Structure

First, let's take a look at the item\\db.conf in the db folder, and its structure:

\`\`\`txt item_db: ( {

` // =================== Mandatory fields ===============================`  
` Id: ID                        (int)`  
` AegisName: "Aegis_Name"       (string, optional if Inherit: true)`  
` Name: "Item Name"             (string, optional if Inherit: true)`  
` // =================== Optional fields ================================`  
` Type: Item Type               (int, defaults to 3 = etc item)`  
` Buy: Buy Price                (int, defaults to Sell * 2)`  
` Sell: Sell Price              (int, defaults to Buy / 2)`  
` Weight: Item Weight           (int, defaults to 0)`  
` Atk: Attack                   (int, defaults to 0)`  
` Matk: Magical Attack          (int, defaults to 0, ignored in pre-re)`  
` Def: Defense                  (int, defaults to 0)`  
` Range: Attack Range           (int, defaults to 0)`  
` Slots: Slots                  (int, defaults to 0)`  
` Job: {                        (defaults to all job)`  
`   All: true/false               (boolean, defaults to false)`  
`   Novice: true/false            (boolean, defaults to false)`  
`   Swordsman: true/false         (boolean, defaults to false)`  
`   Magician: true/false          (boolean, defaults to false)`  
`   Archer: true/false            (boolean, defaults to false)`  
`   Acolyte: true/false           (boolean, defaults to false)`  
`   Merchant: true/false          (boolean, defaults to false)`  
`   Thief: true/false             (boolean, defaults to false)`  
`   Knight: true/false            (boolean, defaults to false)`  
`   Priest: true/false            (boolean, defaults to false)`  
`   Wizard: true/false            (boolean, defaults to false)`  
`   Blacksmith: true/false        (boolean, defaults to false)`  
`   Hunter: true/false            (boolean, defaults to false)`  
`   Assassin: true/false          (boolean, defaults to false)`  
`   Crusader: true/false          (boolean, defaults to false)`  
`   Monk: true/false              (boolean, defaults to false)`  
`   Sage: true/false              (boolean, defaults to false)`  
`   Rogue: true/false             (boolean, defaults to false)`  
`   Alchemist: true/false         (boolean, defaults to false)`  
`   Bard: true/false              (boolean, defaults to false)`  
`   Taekwon: true/false           (boolean, defaults to false)`  
`   Star_Gladiator: true/false    (boolean, defaults to false)`  
`   Soul_Linker: true/false       (boolean, defaults to false)`  
`   Gunslinger: true/false        (boolean, defaults to false)`  
`   Ninja: true/false             (boolean, defaults to false)`  
`   Gangsi: true/false            (boolean, defaults to false)`  
`   Death_Knight: true/false      (boolean, defaults to false)`  
`   Dark_Collector: true/false    (boolean, defaults to false)`  
`   Kagerou: true/false           (boolean, defaults to false)`  
`   Rebellion: true/false         (boolean, defaults to false)`  
` }`  
` Job: Job mask                 (int, defaults to all jobs = 0xFFFFFFFF)`  
` Upper: Upper mask             (int, defaults to any = 0x3f)`  
` Gender: Gender                (int, defaults to both = 2)`  
` Loc: Equip location           (int, required value for equipment)`  
` WeaponLv: Weapon Level        (int, defaults to 0)`  
` EquipLv: Equip required level (int, defaults to 0)`  
` EquipLv: [min, max]           (alternative syntax with min / max level)`  
` Refine: Refineable            (boolean, defaults to true)`  
` View: View ID                 (int, defaults to 0)`  
` BindOnEquip: true/false       (boolean, defaults to false)`  
` ForceSerial: true/false       (boolean, defaults to false)`  
` BuyingStore: true/false       (boolean, defaults to false)`  
` Delay: Delay to use item      (int, defaults to 0)`  
` KeepAfterUse: true/false      (boolean, defaults to false)`  
` Trade: {                      (defaults to no restrictions)`  
`   override: GroupID             (int, defaults to 100)`  
`   nodrop: true/false            (boolean, defaults to false)`  
`   notrade: true/false           (boolean, defaults to false)`  
`   nostorage: true/false         (boolean, defaults to false)`  
`   nocart: true/false            (boolean, defaults to false)`  
`   noselltonpc: true/false       (boolean, defaults to false)`  
`   nomail: true/false            (boolean, defaults to false)`  
`   noauction: true/false         (boolean, defaults to false)`  
`   nogstorage: true/false        (boolean, defaults to false)`  
`   partneroverride: true/false   (boolean, defaults to false)`  
` }`  
` Nouse: {                      (defaults to no restrictions)`  
` override: GroupID             (int, defaults to 100)`  
`   sitting: true/false           (boolean, defaults to false)`  
` }`  
` Stack: [amount, type]         (int, defaults to 0)`  
` Sprite: SpriteID              (int, defaults to 0)`  
` Script: <"`  
`   Script`  
`   (it can be multi-line)`  
` ">`  
` OnEquipScript: <" OnEquip Script (can also be multi-line) ">`  
` OnUnequipScript: <" OnUnequip Script (can also be multi-line) ">`  
` // =================== Optional fields (item_db2 only) ================`  
` Inherit: true/false           (boolean, if true, inherit the values`  
`                               that weren't specified, from item_db.conf,`  
`                               else override it and use default values)`

}, ) \`\`\`

` - **ID**: ID of the item.`  
` - **AegisName**: Server name to reference the item in scripts and`  
`   lookups, should use no spaces.`  
` - **Name**: Name in English for displaying as output for @ and script`  
`   commands.`  
` - **Type**: Purpose of the`

item.

\`\`\`txt 0 = Usable : healing 2 = Usable : other 3 = Misc 4 = Weapon 5 = Armor 6 = Card 7 = Pet Egg 8 = Pet Equipment
10 = Arrow/Ammunition 11 = Usable : delayed consumption (items with script "pet" or "itemskill") 18 = Another delayed
consume that requires user confirmation before using item. \`\`\`

` - **Buy**: Default [NPC](NPC "wikilink") buying price in Zeny. When`  
`   not specified, becomes double the sell price.`  
` - **Sell**: Default [NPC](NPC "wikilink") selling price in Zeny. When`  
`   not specified, becomes half the buy price.`  
` - **Weight**: Item's weight. Each 10 is 1 weight. When not specified,`  
`   becomes 0.`  
` - **ATK**: Base weapon attack, in case of a weapon. When not`  
`   specified, becomes 0.`  
`     - In **RE** enabled servers this field have a optional delimiter`  
`       **:** to define this item's weaponMATK bonus, for example,`  
`       **30:50** would mean the item gives 30 atk and 50 weaponMATK`  
` - **Matk**: Weapon's magical attack (only used in renewal mode,`  
`   ignored in pre-renewal). When not specified, becomes 0.`  
` - **DEF**: Base defense for armor-type items. When not specified,`  
`   becomes 0.`  
` - **Range**: Maximum range in map cells a weapon allows to be the`  
`   player apart from it's target. When not specified, becomes 0.`  
` - **Slots**: Amount of card slots in weapon/armor-type items. When not`  
`   specified, becomes 0.`  
` - **Job**: Which jobs this item is available for. Values below can be`  
`   combined to achieve availability for multiple job classes, i. e.`  
``    `0x2|0x4 -> 0x6` (Swordman+Mage) ``

\`\`\`txt (S.) Novice (2^00): 0x00000001 Swordman (2^01): 0x00000002 Mage (2^02): 0x00000004 Archer (2^03): 0x00000008
Acolyte (2^04): 0x00000010 Merchant (2^05): 0x00000020 Thief (2^06): 0x00000040 Knight (2^07): 0x00000080 Priest (2^08):
0x00000100 Wizard (2^09): 0x00000200 Blacksmith (2^10): 0x00000400 Hunter (2^11): 0x00000800 Assassin (2^12): 0x00001000

- Unused\* (2^13): 0x00002000

Crusader (2^14): 0x00004000 Monk (2^15): 0x00008000 Sage (2^16): 0x00010000 Rogue (2^17): 0x00020000 Alchemist (2^18):
0x00040000 Bard/Dancer (2^19): 0x00080000

- Unused\* (2^20): 0x00100000

Taekwon (2^21): 0x00200000 StarGladiator (2^22): 0x00400000 Soul Linker (2^23): 0x00800000 Gunslinger (2^24): 0x01000000
Ninja (2^25): 0x02000000 Gangsi (2^26): 0x04000000 Death Knight (2^27): 0x08000000 Dark Collector (2^28): 0x10000000
Kagerou/Oboro (2^29): 0x20000000 Rebellion (2^30): 0x40000000

Some commonly used values: All Classes : 0xFFFFFFFF Every Job Except Novice : 0xFFFFFFFE \`\`\`

` - **Upper**: Specifies whether the item can be used by normal, baby or`  
``    reborn classes. Values below can be combined, i. e. `1|4 -> 5` ``  
`   (Normal+Baby Classes)`  
``      - Note: Setting `2` enables the item for Transcendant and 3rd ``  
``        classes. Use `8` to enable the item for 3rd classes ``

only.

\`\`\`txt Normal jobs: 0x01 (1) Upper jobs: 0x02 (2) Baby jobs: 0x04 (4) Third jobs: 0x08 (8) Upper Third jobs: 0x10
(16) Baby Third jobs: 0x20 (32)

Under pre-re mode third classes are considered upper, making use of the 8 and above masks is therefore not necessary
unless in renewal mode. When no value is specified, all classes (mask 0x3f) are able to equip the item. \`\`\`

` - **Gender**: Gender restriction for the item.`

\`\`\`txt 0 = Female 1 = Male 2 = No restriction (both) \`\`\`

` - **Loc**: Equipment location of armor and arrow-type items. Values`  
`   below can be combined, i. e. 136 would indicate both accessory slots`  
`   (typical value for accessories).`

\`\`\`txt (2^0) 1 = Lower headgear (2^1) 2 = Right hand (2^2) 4 = Mantle (2^3) 8 = Accessory 1 (2^4) 16 = Armor (2^5) 32
= Left hand (2^6) 64 = Shoes (2^7) 128 = Accessory 2 (2^8) 256 = Upper headgear (2^9) 512 = Middle headgear (2^10) 1024
= Costume Top Headgear (2^11) 2048 = Costume Mid Headgear (2^12) 4096 = Costume Low Headgear (2^13) 8192 = Costume
Garment/Robe (2^15) 32768 = Arrow (arrow-type items only) (2^16) 65536 = Shadow Armor (2^17) 131072 = Shadow Weapon
(2^18) 262144 = Shadow Shield (2^19) 524288 = Shadow Shoes (2^20) 1048576 = Shadow Accessory 2 (2^21) 2097152 = Shadow
Accessory 1 \`\`\`

` - **WeaponLv**: Weapon level of an item (1-4), Becomes 0 when not`  
`   specified.`  
` - **EquipLv**: Base level required to be able to equip. It is possible`  
`   to specify two values, if an item has a maximum level, by using the`  
`   following`

syntax:

\`\`\`txt EquipLv: \[minLv, maxLv\]

`  If only one value is specified, maxLv becomes the current server's`  
`  MAX_LEVEL. If no values are specified, minLv becomes 0.`

\`\`\`

` - **Refineable**: Whether the item is available for refining (1) or`  
`   not (0). If no value is specified, it defaults to true.`  
` - **View**: For normal items, defines a replacement view-sprite for`  
`   the item`

` -   `  
`   (eg: Making apples look like apple juice). The special case are`  
`   weapons and ammo where this value indicates the weapon-class of the`  
`   item.`

` -   - Weapon-type items:`  
`       1.  Daggers`  
`       2.  One-Handed Swords`  
`       3.  Two-Handed Swords`  
`       4.  One-Handed Spears`  
`       5.  Two-Handed Spears`  
`       6.  One-Handed Axes`  
`       7.  Two-Handed Axes`  
`       8.  Maces`  
`       9.  *(not used)*`  
`       10. Wand/Staff`  
`       11. Bows/Crossbows`  
`       12. Knuckle Weapons`  
`       13. Musical Instruments`  
`       14. Whips`  
`       15. Books`  
`       16. Katars`  
`       17. Revolvers`  
`       18. Rifles`  
`       19. Shotguns`  
`       20. Gatling guns`  
`       21. Grenade launchers`  
`       22. Fuuma shuriken`  
`     - Shield-type items:`  
`       1.  Guard, Novice Guard`  
`       2.  Buckler`  
`       3.  Shield, Holy Guard, Evangelist`  
`       4.  Mirror Shield`  
`     - Ammunition-type items:`  
`       1.  Arrows`  
`       2.  Throw-able daggers`  
`       3.  Bullets`  
`       4.  Shells`  
`       5.  Grenades`  
`       6.  Shuriken`  
`       7.  Kunai`  
`       8.  Cannonballs`  
`       9.  Throwable Items (Sling Item)`  
`     - Headgear-type items: Please see the View IDs section of this`  
`       guide.`

` - **BindOnEquip**: Whether the item will automatically bind to the`  
`   character when it is equipped for the first time.`

` -   `  
`   An item that has this field set, will display a confirmation dialog`  
`   the first time it is equipped, and, if accepted, the item will`  
`   become character-bound.`

` - **Script**: This is where you put your item bonus. Whether it's an`  
`   usable item or an equip item, it will take effect according to the`  
`   item type.`  
` - **OnEquip\_Script**: Script to execute when the item is equipped.`  
`   Warning, not all item bonuses will work here as expected.`  
` - **OnUnequip\_Script**: Script to execute when the item is`  
`   unequipped. Warning, not all item bonuses will work here as`  
`   expected.`  
` - **Inherit**: This can be used only in item\_db2.conf, and if set to`  
`   true, and the item already exists in item\_db.conf,`

` -   `  
`   all the missing fields will be inherited from there rather than`  
`   using their default values.`

In the doc folder look for a text file called "item\\bonus", it shows all the scripts items can have and how they work.

For more information about this structure read \[Item DB file structure
overhaul\](https://herc.ws/board/topic/2954-item-db-file-structure-overhaul/)

1.  Defining Items clientside - all clients

For old and new clients alike, the following two files need to be updated

1.  1.  accname.lub

accname.lub can be found with the other lua files under RO folder/data/luafiles514/luafiles/datainfo. If you do not have
these folders or this file, \[see this topic\](https://herc.ws/board/topic/398-client-translation-project/) and download
the latest translated data folder. It points to the item's sprite file. It is as follows:

\` \[ACCESSORY_IDs.ACCESSORY_ITEM_NAME\] = "Item_Name",\`

1.  1.  accessoryid.lub

This is where the view ID for your item can be found. It can be located in the same folder as accname.lub. It is as
follows:

\` ACCESSORY_ITEM_NAME = ViewID#,\`

1.  Defining Items clientside - old clients

Renewal Clients \\ 2012-04-10a & Main Clients \\= 2012-07-10a

After you make your item, put it in your item\\db2.txt, so that you will not run into conflicts when updating your
repository later. Then go to your data folder and modify the following files, one after another.

1.  1.  idnum2itemdisplaynametable.txt

This file holds the item names, as displayed inside the client. Each item added as:

\`ItemID#ItemName#\`

ItemID is the number from your ID column inside the item db. If your item name contains spaces, replace those with \\
(underscore).

1.  1.  idnum2itemdesctable.txt

This file contains the description of your item, when it is right-clicked. The syntax for an item is:

\`\`\`txt ItemID# Item Description Line 1 Item Description Line 2 (And so on)

1.  

\`\`\`

You can use any amount of lines for the description. If your description contains a \\, make sure it is followed by a
space character. You can look at existing items for an idea of how to format a description.

1.  1.  idnum2itemresnametable.txt

This file sets the inventory and drop-sprite for the item. Item is defined as follows:

\`ItemID#SpriteName#\`

The SpriteName is the name of the files in collection and item folders inside texture and the ones inside sprite folder.
If you want to use the look of an another item, search for it's id and copy the sprite name from there.

1.  1.  itemslotcounttable.txt

In this file you set the amount of visible slots for the item. You do not need to add 0 slot items or items, which do
not have slots at all (i. e. usable items). Syntax:

\`ItemID#NumberOfSlots#\`

NumberOfSlots should be a number from 1-4, larger values might have undesired effects.

1.  1.  Files for non-identified items

The following files specify the name, description and look for items, which have not yet been identified. Their syntax
follows the same rules as for the files with \*idnum\* prefix. Normally the same text is entered for non-equipment and
generic description (which can be copied from official items) is used for equipment of all sorts (weapons, armor,
headgears).

` - num2itemdesctable.txt`  
` - num2itemdisplaynametable.txt`  
` - num2itemresnametable.txt`

1.  Defining Items clientside - new clients

If your client date is newer than specified above then you need to specify all the above item information in 1 file.

1.  1.  System/ItemInfo.lub

Syntax:

\`\`\`txt \[<item id>\] = {

` unidentifiedDisplayName = `<item name to show when not magnified>`,`  
` unidentifiedResourceName = `<file name prefix used for all the images and drop sprite when not magnified>`,`  
` unidentifiedDescriptionName = { `<comma separated list of strings>`,`<to get multiple lines>`,`<in item description>` },`  
` identifiedDisplayName = `<item name to show when magnified>`,`  
` identifiedResourceName = `<file name prefix used for all the images and drop sprite when magnified>`,`  
` identifiedDescriptionName = { `<same format as unidentifiedDescriptionName but for magnified items>` },`  
` slotCount = `<number of slots>`,`  
` ClassNum = <View ID - yes the same one that was there item_db>`

}, \`\`\`

<b>For Weapons, ClassNum = View ID specified in Weapon\\IDs table (inside weapontable.lub file). Look
\[below\](Custom_Items#Weapon_Sprite_Solution\_.28For_New_Clients.29 "wikilink") for details.</b>

You can also put the different values in DescriptionName in separate lines.

Example: Lets say I want to add a weapon to item id 25000 - a One-handed sword named Devastator with 3 slots and the
image/drop sprite files are all named Black\\Sword.\\ . Also I want to display a Sword when not identified.

\`\`\`txt \[25000\] = {

` unidentifiedDisplayName = "Sword",`  
` unidentifiedResourceName = "¼Òµå",`  
` unidentifiedDescriptionName = { "Unidentified item, can be identified with [Magnifier]." },`  
` identifiedDisplayName = "Devastator",`  
` identifiedResourceName = "Black_Sword",`  
` identifiedDescriptionName = {`  
`   "An Unholy Sword that was created with the sole purpose of destruction",`  
`   "Class :^777777 Sword^000000",`  
`   "Attack :^777777 325^000000",`  
`   "Weight :^777777 80^000000",`  
`   "Weapon Level :^777777 4^000000",`  
`   "Required Level :^777777 100^000000",`  
`   "Applicable Job :^777777 Novice, Swordsman Class, Merchant Class, Thief Class^000000"`  
` },`  
` slotCount = 3,`  
` ClassNum = 2`

}, \`\`\`

The unidentifiedResourceName is the Sword item's sprite name, so the client will show it as a sword when not identified.
The ClassNum is also 2, for a one-handed sword. If you want to use another sprite for your unidentifiedResourceName,
simply search (ctrl+f) for the item's name in iteminfo.lub and copy the identifiedResourceName value for that item and
apply it to your custom item's unidentifiedResourceName value.

1.  Allocating Items on Client Side

Most custom items will have 6 files (if yours does not, see \[Less Than 6 Files\](Custom_Items#Less_Than_6_Files
"wikilink")):

\`\`\`txt 1) Drop sprite -\> Helmet_drop.spr 2) Drop act file -\> Helmet_drop.act 3) Item Inventory image -\>
Helmet_item.bmp 4) Item Collection image -\> Helmet_collection.bmp (the one you see on its description window) 5)
Headgear View sprite -\> Helmet.spr 6) Headgear View act file -\> Helmet.act \`\`\`

Lets say I downloaded a custom item called Helmet which serves as a headgear and the above six files were in them.

1.  1.  Sprite Locations

We place the six files in the following folders

` - Copy Helmet\_drop.spr to `$$RO
    Folder$$`\\data\\sprite\\¾ÆÀÌÅÛ\\Helmet.spr`  
` - Copy Helmet\_drop.act to `$$RO
    Folder$$`\\data\\sprite\\¾ÆÀÌÅÛ\\Helmet.act`  
` - Copy Helmet\_item.bmp to `$$RO
    Folder$$`\\data\\texture\\À¯ÀúÀÎÅÍÆäÀÌ½º\\item\\Helmet.bmp`  
` - Copy Helmet\_collection.bmp to `$$RO
    Folder$$`\\data\\texture\\À¯ÀúÀÎÅÍÆäÀÌ½º\\collection\\Helmet.bmp`  
` - Copy Helmet.spr to `$$RO
    Folder$$`\\data\\sprite\\¾Ç¼¼»ç¸®\\¿©\\¿©\_Helmet.spr`  
`   (Female) **AND** ¿©\_Helmet.act`  
` - Copy Helmet.spr to `$$RO
    Folder$$`\\data\\sprite\\¾Ç¼¼»ç¸®\\³²\\³²\_Helmet.spr`  
`   (Male) **AND** ³²\_Helmet.act`

If the process confused you, \[here is an example folder\](http://www.mediafire.com/?8lzt4cbot100w44), the sprite is
done by drkangel. The folder is virus free.

1.  1.  Specifications of the files

1\\ Drop sprites - ideally have 1 frame & its act file will be just an empty act (only header will be there inside)

2\\ Equip sprites - typically have 3+ frames to show images for various orientations & its act file will have the info
on where to place each frame and movement animations.

3\\ Item bmp - 24x24 size 256 bit bmp file. Magenta (FF00FF hexadecimal value) background.

4\\ Collection bmp - 75x100 size bmp file (usually 256 bit but there is no restriction)

1.  1.  How to differentiate between sprite files?

Open both sprite files in \[Spr Conview\](http://ratemyserver.net/download_agent.php?type=1&file_num=10). The number of
frames in the files can be seen at bottom (Sprite: <currentframe>/<total>). If it says Sprite: 1/1 then its a drop
sprite and the other is equip sprite.

Sometimes what sprite authors do is they simply copy the original sprite itself to make a drop sprite. In this case you
will see both of them as identical when opened in Spr Conview & we don't need to worry about which one is which (since
they are the same).

1.  1.  Less Than 6 Files

In rare cases or for garment and accessory items, you may have less than 6 files to place. For a garment or accessory,
you do not need a .spr and .act because these items are not visible on a character, therefore they do not require a .spr
or .act file. For weapons, headgears, and shields, you should have 6 files. If you do not, you will have to create the
missing files yourself. Especially for old sprites, the spriter may have just made the sprites and made no collection
image, item image, or drop sprite. See \[Spriting\](Spriting "wikilink") on how to create these yourself.

1.  Modifications

<!-- -->

1.  1.  Sprite Replacement

To replace a headgear with your customized headgear, just delete one of the items you want, and replace your customised
item ID with that id.

Lets say you have something like this:

\`15000,Angel_Wing,Angel Wing,4,,10,10,0,,1,0,0,3,0,0,0,0,0,{},{},{}\`

And there's an item you wont need, such as:

\`2220,Hat,Hat,5,1000,,200,,2,,0,10477567,2,256,,0,1,16,{},{},{}\`

Well, to replace it, just delete everything in the hat line but its ID, and paste there your custom item, all the line
but the ID. Should be like this:

\`\`\`txt 2220,Hat,Hat,5,1000,,200,,2,,0,10477567,2,256,,0,1,16,{},{},{} 15000,Angel_Wing,Angel
Wing,4,,10,10,0,,1,0,0,3,0,0,0,0,0,{},{},{} 2220,Angel_Wing,Angel Wing,4,,10,10,0,,1,0,0,3,0,0,0,0,0,{},{},{} \`\`\`

All you need to do now is changing the View ID to the Hat, and change your file names to its name. You can find them on
the idnum2resnametable.txt Search for 2220 and the gibberish besides it, w/o the \\ \\ is the file name, then rename it
to your custom item name.

Remember to add the files to data\\sprite\\¾ÆÀÌÅÛ (Icon sprite) and both data\\sprite\\¾Ç¼¼»ç¸®\\³² (Male Item Sprite)
and data\\sprite\\¾Ç¼¼»ç¸®\\¿© (Female Item Sprite). Remember, these 2 last item names, must have either a ³²\\ for male
or ¿©\\ for female, at the beginning of the name, both .spr and .act. Also, don't forget to change the other files:

idnum2itemdisplaynametable.txt , idnum2itemdesctable.txt , idnum2itemdesctable.txt , num2itemdesctable.txt ,
num2itemdisplaynametable.txt , num2itemresnametable.txt and itemslotcounttable.txt

Use these files if you want to replace sprites, they will be useful.

` - **actOR:** with the actor you modify the act file, which is the one`  
`   who tells the client where does the weapon go and what does it have`  
`   to do and at a certain moment.`  
` - **SPR Conview:** you can use these to view which sprite is which,`  
`   and also see sequence per sequence.`

1.  1.  Item Restrictions

Look on your db folder for a file called item\\trade.txt and open it

Now, the pattern for a flag is:

\`Item ID, TradeMask, GM-Level Override\`

` - **Item ID**: the ID of your item.`  
` - **TradeMask**: Testrictions the item will have, such as being`  
`   dropped, stored or traded. These values can be combined to achieve`  
`   multiple effects.`

\`\`\`txt 1:Item can't be dropped 2:Item can't be traded (nor vended) 4:Item can only be traded with wedded partner
8:Item can't be sold to NPCs 16:Item can't be placed in the cart 32:Item can't be placed in the storage 64:Item can't be
placed in the guild storage \`\`\`

` - **GM-Level Override**: This is the minimum GM level a player must`  
`   have to avoid these restrictions.`

1.  1.  Item Script

Okay, I'll update this as I go; otherwise, I wont have anything new to show. First with usable items.

Well, there are 3 types of usables:

1.- Healing items, they have in the type field a 0.

2.- Other uses items, such as fly wings and so, which doesn't heal, but does have an instant effect, they have in the
type field a 2.

3.- Usable items, which are skills that requires a target selection, therefore they have a delayed use, and in newer
versions the item wont be gone until the target is chosen and the cast has finished. Means, you wont lose the item if
the skill hasn't been done. They have in the type field an 11.

Now, for an item skill, the pattern for a skill is:

\`itemskill \`<skill id>\`,\`<skill level>\`;\`

Without \\\\ of course.

Now, we go to our db\\skill\\db.txt and search for the blessing ID, searching for AL\\ or blessing, but first, the
structure of a skill:

\`id,range,hit,inf,element,nk,splash,max,list_num,castcancel,cast_defence_rate,inf2,maxcount,skill_type,blow_count,name,description\`

Now, the AL\\BLESSING or Blessing Skill:

\`34,9,6,16,0,0x1,0,10,1,yes,0,0,0,magic,0,  AL_BLESSING,Blessing\`

We grab the ID and put it on our code:

\`itemskill 34,\`<skill lvl>\`;\`

Don't mind the actual level of the skill\\db.txt for the skill level part. You can actually put the level you want here
below 99, so lets pick 4:

\`itemskill 34,4;\`

And finally, insert it on the code.

`   ,{ itemskill 34,4; },{},{}`

There, we have a Lvl 4 Blessing item skill.

Remember, one space before and one after the script, NOT TAB\\

And so on with other skills. Just remember these steps and they should be fine. And remember, itemskill is NOT the same
as skill. itemskill will make you CAST that skill, while skill will GIVE you the skill. If you give an item, whether
delayed use or normal usable two itemskill commands, only the latter will come into effect, as you cannot cast two
skills at the same time.

Now, for Potions.

Instead of using itemskill, we will use itemheal:

\`,{ itemheal 100,0; },{},{}\`

The green is the HP, the blue is the SP. To add that random heal amount effect, just pick a set amount, let's say 120,
then pick 1 or 2 numbers, up to you. Then, add the rand() command, like this:

\`,{ itemheal rand(120,9,49),0; },{},{}\`

Explanation: This item will heal about 49\\120 hp and 0 SP. To heal SP you change the 0 to a number. Like this:

\`,{ itemheal rand(120,9,49),50; },{},{}\`

It will now heal 50 SP. Now, for skilleffect and sc\\start.

Okay, let's see. Here's a example of an item casting a skill and simulating a skill.

\`,{ itemskill 34,10; skilleffect 29,0; sc_start 12,140000,5; },{},{}\`

skilleffect will display on your client a skill visual effect. The pattern is:

\`skilleffect \`<skill ID>\`,\`<number>\`;\`

` - skill ID  `  
`   Self-explanatory.`  
` - number  `  
`   Have you seen those skills that shows up numbers upon casting? Such`  
`   as heal? Well, putting a number there will display it. But only`  
`   works on skills with numbers floating.`

sc\\start has the following pattern:

\`sc_start \`<status id>\`,\`<duration>\`,\`<val1>\`\[,\`<unit id>\`\];\`

` - status id  `  
`   Refer to const.txt in your db folder for all effects. Open it with a`  
`   text editor then search by either clicking edit, then find, or press`  
`   and hold the ctrl key, and while still holding it press the f key,`  
`   then release, and search for "SC\_ALL -1". Everything below this is`  
`   an effect. The effects stop at "e\_gasp 0" which are emoticons.`  
` - duration  `  
`   Is the amount time in milliseconds (1000 msec = 1 sec) that the`  
`   status will be active.`  
` - val1  `  
`   Typically it's the level of the skill, associated with this status.`  
` - unit id  `  
`   Allows to start the status on an other unit, than the attached`  
`   player. For players this is account id. This parameter is optional,`  
`   and can be omitted.`

Now, for the item I said, it will show you the visual effect of Blessing and cast on you a lvl 5 Agi-Up\\ skill for 140
seconds.

For more item scripts see script\\commands.txt in your doc folder, as well as item\\bonus.txt in your doc folder.

\\=Weapon Sprite Solution (Renewal Clients \\= 2012-04-10a & Main Clients \\= 2012-07-10a)== For these clients, Weapons
are limited to use a range of Item IDs hardcoded in the clientn for each type. For e.g.

\`\`\`txt 1265,Bloody_Roar,Bloody Roar,4,,10,1000,120,,1,0,4096,7,2,34,4,75,1,16,{ bonus bIgnoreDefRace,RC_DemiHuman;
bonus bFlee,-160; bonus bFlee2,-160; bonus bNoRegen,1; bonus bNoRegen,2; },{},{}
1266,Test,Test,4,4000,2000,10,165,,1,0,4096,7,2,34,3,33,1,16,{}

// 1-Handed Axes 1301,Axe,Axe,4,500,,800,38,,1,3,8803555,7,2,2,1,3,1,6,{} \`\`\`

Here the item 1266 is a custom katar and it does show up as a katar (if you have the proper sprite files ofcourse). but
if i use some id like say 22000, client wont display it. So what is the range of item ids you can use? Look below:

` - One handed Swords = 1100-1149, 13400-13499`  
` - Two handed Swords = 1150-1199, 21000-21999`

` - Knives, Daggers etc = 1200-1249, 13000-13099`  
` - Katars = 1250-1299 ; Has 35 free IDs`

` - One handed Axes = 1300-1349; Has 43 free IDs`  
` - Two handed Axes = 1350-1399; Has 32 free IDs`

` - One handed Spears = 1400-1449; Has 34 free IDs`  
` - Two Handed Spears = 1450-1471, 1474-1499`

` - Maces = 1500-1549, 16000-16999`  
` - Books = 1550-1599 ; Has only 2 IDs.`  
` - Knuckles = 1800-1899 ; Has 95 free IDs`

` - One Handed Staves/Rods = 1600-1699; Has 79 free IDs`  
` - Two Handed Staves/Rods = 1472,1473,2000-2099`

` - Bows = 1700-1749, 18100-18499`  
` - Guitars = 1900-1949 ; Has 32 free IDs`  
` - Whips = 1950-1999 ; Has 130 free IDs`

` - Handguns = 13100-13149`  
` - Other guns = 13150-13199`

` - Ninja weapons = 13300-13399`

The number of unused Item IDs left known for a range has also been mentioned above. Best practice to follow check in
your range in official db before adding custom weapon.

1.  1.  Weapon Sprite Solution (For New Clients)

For new clients the view id system is also applicable to client. To add a custom weapon you need to first edit a file
called weapontable.lub in your data folder

\`data/luafiles514/lua files/datainfo/weapontable.lub\`

I will be adding <b>Oriental\\Sword</b> which will be a 1-Handed sword. Open weapontable.lub. First you will see a table
called <b>Weapon\\IDs</b>. Take note of the first 30 values in this table - these are the only available Weapon types in
the client right now.

Anyways go to the last entry which should be for Wizardy Staff = 97. You can use a view id after that like shown below

\` WEAPONTYPE_Oriental_Sword = 98,\`

Come down and you see the next table called <b>WeaponNameTable</b>. Here is where you add your sprite name suffix. What
do i mean by that? Its the last part in your weapon sprite & act file. Before it used to be \\<Item ID>.

\`data/sprite/\`<job dependent folder>\`/\`<job dependent prefix>\`\_\`<gender><weapon suffix>\`.spr\`

OK Back to topic. so I add my entry like shown below.

\`\[Weapon_IDs.WEAPONTYPE_Oriental_Sword\] = "Oriental"\`

Lastly come down further in weapontable.lub and you see the last table called <b>Expansion\\Weapon\\IDs</b>. Remember
the 30 types i told you to take note of ? here we assign one of those to our custom (like a mapping or connection).
Since mine is a 1-Handed Sword I specify it like below.

\`\[Weapon_IDs.WEAPONTYPE_Oriental_Sword\] = Weapon_IDs.WPCLASS_WEAPONTYPE_SWORD \`

<b>Now for the most important part. For our client to actually pick up all these details we need to provide the view id
which we used in Weapon\\IDs table as the ClassNum value in ItemInfo.lua. Check the \[ItemInfo.lub
format\](Custom_Items#System.2FItemInfo.lub "wikilink") shown above for details.</b>

With this your weapon sprite will become visible while attacking.

1.  Troubleshooting

<!-- -->

1.  1.  File Not Found "Cannot find File : path\\to\\file\\filename.extension"

As the error states, the client cannot find the file required to display the sprite, act, collection, or item image for
the item. Make sure you put your file in the right place and that it is named correctly.

1.  1.  Unknown Item

If your item's name is unknown item and it has an apple icon, refer to \[Defining Items
Clientside\](Custom_Items#Defining_Item_clientside\_.28Renewal_Clients\_.3C.3D_2012-04-10a\_.26_Main_Clients\_.3C.3D_2012-07-10a.29
"wikilink") and make sure you added the item to each and every file, or just iteminfo.lua for a newer client.

1.  1.  Files Configured Correctly, Sprite Still Does Not Show up In-game

If you do not have your sprites and files compressed into a GRF, you will need to make sure your client is diffed to
read your data folder first.

\[Category:Database\](Category:Database "wikilink") \[Category:Data\](Category:Data "wikilink")
\[Category:Customization\](Category:Customization "wikilink")
