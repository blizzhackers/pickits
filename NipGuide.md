[pickit table of content](https://github.com/blizzhackers-d2/pickits/#pickits)

---

# Nip Guide

* [pickit walk-through](#pickit-walk-through)

* [format of the nip lines](#format-of-the-nip-lines)

	* [things that go before the #](#things-that-go-before-)

	* [things that go after #](#things-that-go-after-)

	* [comparison symbols](#comparison-symbols)

* [item-parser syntax information](#item-parser-syntax-information)

* [other examples](#other-examples)

	* [ring](#ring)

	* [max quantity](#max-quantity)

	* [druid pelt](#druid-pelt)

* [how to keep items unid](#how-to-keep-items-unid)

* [charged skill items](#charged-skill-items)

* [additional skill effect](#additional-skill-effect)

* [pickit FAQ](#pickit-faq)

* [d2nt pickit errors](#d2nt-pickit-errors)

* [pickit philosophy](#pickit-philosophy)

	* [fast cash](#fast-cash)

	* [big profit](#big-profit)

	* [editing](#editing)

* [the specific of poison charms](#the-specific-of-poison-charms)

---

### pickit walk-through

All pickit files are stored in d2bs/kolbot/pickit/ There are several default files to choose, you can also create and add your own or just edit these files.

* [classic.nip](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/pickit/classic.nip)
* [follower.nip](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/pickit/follower.nip)
* [gold.nip](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/pickit/gold.nip)
* [keyorg.nip](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/pickit/keyorg.nip)
* [kolton.nip](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/pickit/kolton.nip)
* [LLD.nip](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/pickit/LLD.nip)
* [pots.nip](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/pickit/pots.nip)
* [shopbot.nip](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/pickit/shopbot.nip)
* [test.nip](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/pickit/test.nip)

It is strongly recommended to use [notepad++](https://notepad-plus-plus.org/download/) to edit files. A useful plugin for notepad++ that works as a [NipCheck](nipcheck/readme.md).
It's important to check if your *.nip file is without errors. If you like you can use [Nipper](nipper/readme.md) which works both for kolbot and d2nt.

First off familiarize yourself with some important and useful information.

[NTItemAlias.dbl](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/libs/NTItemAlias.dbl) (or [NTItemAlias.ntl](d2nt/NTItemAlias.ntl) in d2nt case) will answer 99% of item names/stats questions.

**Remember**:

* Magic items can only get 2 affix, 1 prefix and 1 suffix. 

* Rares Get 6 affix, 3 prefix and 3 suffix

* Crafts Get 4 affix + craft mods, still limited to 3 prefix or suffix max

That's pretty much all there is to writing a pickit. Remember that everyone makes simple mistakes, but you can use [NipCheck](nipcheck/readme.md) to find easier the issued lines and to correct them.

### format of the nip lines

NIP lines are of the format:

***{properties} # {stats} # {maxquantity}***

##### things that go before \#

[type], [name], [class], [quality], [flag], [level], [prefix], [suffix]

```
 NTIPAliasType		-> [type] 
 NTIPAliasClassID	-> [name]
 NTIPAliasClass		-> [class]
 NTIPAliasQuality	-> [quality]
 NTIPAliasFlag		-> [flag]

 [level]  = item level
 [prefix] = number of a prefix that should be on the item, this and suffix number can be a bit hard to find
 [suffix] = number of a suffix that should be on the item
```

##### things that go after \#

[stat keywords] : [Number or Alias]

```
 NTIPAliasStat		-> (skills,stats, etc)

 The odd-man out seems to be [level] as its used as [property], but in NTItemAlias.dbl it's listed as a **[stat]**
 [level] != [itemlevelreq]
```

##### [comparison symbols](https://www.w3schools.com/JSREF/jsref_operators.asp):

```javascript
 ==	equals
 >	greater than
 >=	greater or equal to
 <	less than
 <=	less than or equal to
 !=	not equal to
 &&	and
 ||	or
 ()	group things up
```

### item-parser syntax information

[keyword] separates into two groups:

* **[property keywords]** = [type], [name], [class], [quality], [flag], [level], [prefix], [suffix]
* **[stat keywords]** = [{Number or NTItemAlias keyword}] or [Description] (description allow access to any text found in the item hover)


* **[maxquantity keywords]** = [maxquantity] (used to limit the quantity kept)
* **[keyword]** must be surrounded by **[** and **]**
* **[property keywords]** must be placed first
* insert **# symbol** between **[property keywords]** and **[stat keywords]**
* use **+   -   \*   /   (   )   &&   ||   >   >=   <   <=   ==   !=  symbols** for comparison
* use **// symbol** for comment

There is no getting around learning the NIP syntax. You simply have to bite the bullet and do it. No one here can learn it for you. While it is not the most user-friendly language, it is fairly easy to understand once you start working with it.

The NIP files you are using are configured in your character configuration file. You can include/exclude NIP files on a per character basis within that file. Anything that appears on a NIP line past the **//** symbol is ignored (we call this a comment).

Each NIP has 3 sections separated by **#** signs where the keywords associated with that section are found: 

**{property} # {stats} # {maxquantity}**

Each section is comprised of what are commonly called attribute-value pairs. An attribute-value pair is a keyword name that is assigned a value using an operator like this: 
```
[type] == circlet
```
These attribute-value pairs are then grouped using logical conjunctions like **&&** (for AND) and **||** (for OR) to create a NIP.

Now this was pretty straight forward to me, but to some it seems to be a little confusing.

Think of **[property]** keywords as "constants" that will remain the same no matter what.

These all go before the # (was pretty easy for me as I already tend to use item #'s).

This doesn't mean that they can't vary, just means that no matter what end item is still gonna be "boots".

If you were writing a line for all rare boots, the constants would be **[type] && [quality]**, those aren't gonna change no matter what you do.

Now think of **[stat]** keywords as "variables" things that you may want to be flexible with. Like above, it doesn't mean that it can't have a set value.

For example we can use **boots**, so if we want a **rare** ones we will write:
```javascript
[type] == boots && [quality] == rare
```
, but we also want them to have some **fasterrunwalk** and a little **fireresist**, so **# [stat] && [stat]** should be added.

Finally, it would look like this:
```javascript
[type] == boots && [quality] == rare # [frw] >= 10 && [fireresist] >= 10
```

Now, if you can't determine what goes before the **#** and what goes after the **#** simply open up [NTItemAlias.dbl](https://github.com/blizzhackers-d2/d2bot-with-kolbot/blob/master/d2bs/kolbot/libs/NTItemAlias.dbl) and search with CTRL+F what you're trying to find.

You can tell whether its a **[property]** or a **[stat]** simply by locating its alias, everything has an alias, just a matter of finding it.
	
Now, we can use the same example for boots, but this time we want rare boots with **fastrunwalk** and **fireresist** stats, and either **coldresist** or **lightresist** or **dex**
```javascript
[type] == boots && [quality] == rare # [frw] >= 10 && [fireresist] >= 10 && ([lightresist] >= 10 || [coldresist] >= 10 || [dexterity] >= 1)
```
or we can write the same line, changing the condition for **coldresist + lightresist** to be >= 10
```javascript
[type] == boots && [quality] == rare # [frw] >= 10 && [fireresist] >= 10 && ([lightresist]+[coldresist] >= 10 || [dexterity] >= 1)
```
It's the same premise for any item, so once you have it figured out its pretty easy. Using the same example lets say I wanted only boots of exceptional quality.

[class] can be **normal**, **exceptional**, **elite** , and you can find it on NTItemAlias.dbl lines 765-768.

**class** = **property** so it goes before the **#**

So the same boots, but only exceptional versions becomes:
```javascript
[type] == boots && [class] == exceptional && [quality] == rare # [frw] >= 10 && [fireresist] >= 10 && ([lightresist] >= 10 || [coldresist] >= 10 || [dexterity] >= 1)
```
Adding too many qualifiers to any one line will make it harder for a novice to find any mistakes they have made. Remember the simpler it is for you to read, the better.

Don't be afraid of using simple qualifiers. I hate writing rings/ammys/circlets and usually just use a couple of your standard catch-all lines.
```javascript
[type] == circlet && [quality] == rare # ([itemaddclassskills] >= 2 || [itemaddskilltab] >= 2) && [fcr] == 20 && ([strength] >= 10 || [dexterity] >= 10 || [frw] >= 30 || [sockets] == 2 || [maxhp]+[maxmana] >= 35)
```

Now is that gonna grab junk? yea probably but look at this line
```javascript
[type] == circlet && [quality] == rare # ([itemaddclassskills] >= 2 || [itemaddskilltab] >= 2) && [fcr] == 20 && ([strength] >= 15 || [dexterity] >= 15) && ([frw] >= 30 || [sockets] == 2 || [maxhp]+[maxmana] >= 35)
```
Guess what happens if your bot finds a rare Circlet with 2skills/20fcr/12str OR 12dex and 2soc?

A good basic catch all should simply have 2 stats you want and a selection of other stats.

For instance, this pickit line for rare Amazon helms:
```javascript
[type] == circlet && [quality] == rare && [flag] != ethereal # [amazonskills] == 2 && [frw] == 30 && [sockets] == 2
```

### other examples

##### ring
taking this line as an example:
```javascript
[type] == ring && [quality] == rare # [lifeleech] >= 4 && [tohit] >= 80 && [dexterity] >= 10 && [maxhp] >= 20
```
item must be of type ring, must be of quality rare
stats on the ring we are looking for with the line are:
lifeleech 4 or higher
attack rating 80 or higher
dexterity 10 or higher
life 20 or higher

The line would not keep a ring that has three of the four stats specified, the line specifies the minimum stats the ring MUST have to be kept.
So a ring with LifeLeech, Dexterity and Life wont be kept by this line as it is missing Attack rating (ToHit)

##### max quantity
this line:
```javascript
[name] == helrune # # [maxquantity] == 3
```
is for hel runes to be kept, to be precise 3 of them in stash and then don't bother with hel runes until less than 3 in stash.

the two # # seperate properties, stats and maxquantity. If no stats are on the item (like with a rune or a gem) then the two still needs to be there for the syntax to be correct.

##### druid pelt
One last example on how the () works in a line:
```javascript
[type] == pelt && [quality] == rare && [flag] != ethereal # ([druidskills] >= 2 || [elementalskilltab] >= 2) && [skilltornado] >= 3 && [fhr] >= 10 && [sockets] >= 2
```
This line looks for:
a druid helm (called pelt), [type] == pelt that is rare, [quality] == rare and that is NOT ethereal, [flag] != ethereal, then comes the first # so next comes the stats that should be on the item: either DruidSkills 2 or more (2 + to druid skills) OR elementalskilltab 2 or more (2 + to elemental skill tab) skilltornado 3 or higher (can't be higher than 3 but better safe than sorry if a bugged item happens to come along) faster hit recovery 3 or higher, [fhr] >= 3, sockets 2 or more, [sockets] >= 2


### how to keep items unid
Any pickit line without requirements for **[stat]** will keep that item unidentified. If it doesn't, check other lines from active pickit files to see if you not doubled that item. use notepad++ < Find in Files > tool. Example: 
```javascript
[name] == corona && [quality] == unique
[name] == ring && [quality] == unique
[name] == amulet && [quality] == unique
```

### charged skill items

the default lines 1301 - 1302 from NTItemAlias.dbl
```javascript
NTIPAliasStat["itemchargedskill"] = 204;
NTIPAliasStat["teleportcharges"] = [204,3461];
```
but in default LLD.nip and shopbot.nip you can find some examples for **itemchargedskill**:
```javascript
[name] == warscepter && [quality] <= rare && [flag] != ethereal # ([enhanceddamage] >= 40 || [tohit] >= 80 || [enhanceddamage] >= 30 && [tohit] >= 40) && [itemchargedskill] == 96 && [itemlevelreq] <= 9 // sacrifice

[type] == staff && [class] <= exceptional && [quality] == rare # [itemchargedskill] == 54 && [fcr] == 20 && [itemlevelreq] <= 30

[name] == warscepter # ([enhanceddamage] >= 40 || [tohit] >= 80 || [enhanceddamage] >= 30 && [tohit] >= 40) && [itemchargedskill] == 96 && [itemlevelreq] <= 9 // [H]Akara, [H]Drognan, [H]Ormus, [H]Jamella, [H]Malah; level 95+ char for level 11 charges
```

so, you should use ... skillID from ...\kolbot\sdk\skills.txt
```javascript
... [itemchargedskill] == xx ...
```

### additional skill effect

the default lines 1288 - 1297 from NTItemAlias.dbl
```javascript
NTIPAliasStat["itemskillonattack"] = 195;
NTIPAliasStat["itemskillonkill"] = 196;
NTIPAliasStat["itemskillondeath"] = 197;
...
NTIPAliasStat["itemskillonhit"] = 198;
...
NTIPAliasStat["itemskillonlevelup"] = 199;
...
NTIPAliasStat["itemskillongethit"] = 201;
```
according to the [previous chapter](#charged-skill-items) you should use in the pickit line stat field (after #) the desired effect ==  skillID (...\kolbot\sdk\skills.txt):
```javascript

... # [itemskillonattack] == xx
... # [itemskillonkill] == xx
... # [itemskillondeath] == xx
... # [itemskillonhit] == xx
... # [itemskillonlevelup] == xx
... # [itemskillongethit] == xx

```


### pickit FAQ

* **Q:** Why does my bot pick up and stash junk?

  **A:** Because it's on your pickit. Check the Item Log on manager to check what lines are responsible for that.

* **Q:** How do I add trap claws?

  **A:** Same way you add anything else, only they are like orbs and have 2x different types. I use names just like I do with orbs.
```javascript
[name] == greaterclaws
[name] == greatertalons
[name] == scissorsquhab
([name] >= handscythe && [name] <= scissorssuwayyah)
```

* **Q:** I noticed you use **[name] >= && [name] <=** just wondering why?

  **A:** Simply easier than writing out each individual item name, but it has its drawbacks, for instance in the case of orbs I also wind up picking up all normal/exceptional amazon weapons(because they are between orbs) not a biggie on orbs but imagine if you put >= crystalsword(#29) and <= phaseblade(#225)

* **Q:** Why does my bot keep picking up magic items when I have none on my pickit?

  **A:** If you're certain you don't have any magics on your pickt it is usually caused by >= or <= on normal or rares

* **Q:** How can I pick and sell items for gold

  **A:** By adding only an impossible affix after the #
```javascript
[class] == elite # [strength] >= 1000
```

* **Q:** How come for viperskin you only have FireRes?

  **A:** Unique items with all res only need one res to look for. If i have [fireresist] == 35, there is no need for it to look at any other qualifiers, Not like maras/vipers/metalgrids can spawn with 35FR,30LR,21PR,30CR. Same goes for charms, you only need 2 of the 4 Res to pickup an all res SC.

* **Q:** What is the difference between [itemlevelreq] and [level]?

  **A:** Well [level] is kinda odd as although its listed as a [stat] in NTItemAlias its actually used as a [property], so if you want items under a certain level you would use **[name] && [quality] # [itemlevelreq] <=**, and if you want to keep items of a certain Ilvl you would use **[name] && [quality] && [level]**

##### d2nt pickit errors

* Syntax error 64 ~ Usually means problem is after #
* Syntax Error 64 (missing ; ) ~ Missing or extra "][" or ")("
* Syntax Error 64 (invalid left hand assignment) ~ having "=" instead of "=="">=""<="
* Syntax Error 64 (xxx isn't defined) ~ having keyword missing "[]" or typo
* Syntax Error 60 ~ Usually means Problem is before #
* Syntax Error 60 (xxx isn't defined) ~ having keyword missing "[]" or typo
* Syntax Error 60 (missing ; ) ~ Misplaced or missing "#"(usually see a bunch of white writing)
* Syntax Error 60 (Syntax error) ~ Missing or extra "][" or ")("
* Syntax Error 111 ~ This is not an error in your pickit, but has to do with potions, usually grabbing + drinking.

And keep in mind just because you're not getting any errors from bot, that doesn't mean that your pickit isn't without mistakes.


### pickit philosophy

Everyone asks how to improve your pickit. The point usually being to rake in huge amounts of fg at a time. The secret is, most people customize their own. You can learn about customizing your pickit on the wiki.

I never share my pickit. Reason being, mine isn't designed to pick up awesomeness for reselling. Mine is designed to pick up stuff for my other characters. If I'm not looking to gear up any of my chars, I turn off my pickits.

I've decided to share some lines and philosophy in this wiki.

Note: If your goal is to pick up godly goodness, be prepared to not pick up ANYTHING for a few weeks. There's a reason those items sell for so much. It's because they're so rare.

You could also see the max stats of items on http://classic.battle.net/diablo2exp/items/

### fast cash

Now, let's talk about fast cash. Not a lot of cash, but fast cash.

```
[name] == twistedessenceofsuffering # # [maxquantity] == 2
[name] == chargedessenceofhatred # # [maxquantity] == 2
[name] == burningessenceofterror # # [maxquantity] == 2
[name] == festeringessenceofdestruction # # [maxquantity] == 2
[name] == tokenofabsolution
```

By now, everyone should know what a token is. It's always a good idea to have this in your pickit. Now we go over to the char config.

```javascript
Config.Cubing = true; // Set to true to enable cubing.
Config.Recipes.push([Recipe.Token]); // Make Token of Absolution
```

Why? I let my bot run for one day. I came back to a stash full of tokens. While they can be a pain to move around, they sell for 1 fg each. 20 tokens = 20 fg. It may not seem like much, but 20 fg/day = 120/week.

```javascript
[type] == amulet && [quality] == magic # [itemaddskilltab] >= 3
```

While your bot is looking for them, you sell a lot of amulets, filling up your gold really quick.

```javascript
[name] == coronet || [name] == circlet || [name] == tiara || [name] == diadem) && [quality] >= magic # [itemaddclassskills] >= 2
```

Same thing here. Magic versions of these can have +3 all class skills, rares can have +2 with some pretty sweet effects. They generally attract some attention.

```javascript
[name] == cm3 && [quality] == 4 # [palicombatskilltab] == 1 && [maxhp] >=30
```

This line is abbreviated. It's Paladin combat skills grand charm with >= 30 life. While these are hard to come by, it's no secret that they catch a high price.

### big profit

Of course, if you are looking for that godly gear, you'll need to beef up your lines.

```javascript
[type] == gloves && [quality] == rare # [IAS] == 20 && [itemaddskilltab] >= 2 && ([strength]+[dexterity] >= 18 ||[lifeleech] >= 3 || [manaleech] >= 3 || [fireresist]+[lightresist]+[coldresist]+[poisonresist] >= 40)
```

Rare gloves, 20% increased attack speed, +2 to a skill tab (usually zon jav/spear or bow/xbow or sin MA or SD), Combined str/dex of at least 18 OR 3% life leech OR 3% mana leech OR 40 all resist.

While I haven't found one of these yet, I imagine it will sell fast.

For these beefed up lines, I recommend Perfection by Sexuation.

### editing

Remember, what works for one person may not work for you. Even if you use a pre-made pickit, read through and make adjustments.

Example:

```javascript
[name] == slayerguard && [quality] == unique # [enhanceddefense] >= 200
```

This line is for Arreat's Face with perfect defense. While this is ideal, it's rare. You can drop it to

```javascript
[name] == slayerguard && [quality] == unique # [enhanceddefense] >= 180
```

If that one with perfect defense drops, you will still keep it.


### the specific of poison charms

When an item has both a poison damage prefix and suffix, it's not the total damage but the damage rates (i.e. damage per second) that are summed (as are the lengths).

The **pestilent** prefix applies 175 poison damage over 6 seconds; that's approximately 175/6 poison damage per second. The **anthrax** suffix applies 50 poison damage over 6 seconds; that's approximately 50/6 poison damage per second. So, a **pestilent small charm of anthrax** applies approximately 37.5 ((175 + 50)/6) poison damage per second for 12 (6 + 6) seconds, resulting in approximately 450 (37.5 x 12) poison damage over 12 seconds. You need to know the values and calculations used by the game for exact figures:
```
Affix      Rate  Frames  Poison Damage      Over seconds
________________________________________________________
pestilent  299    150    299*150/256 = 175  150/25 =  6
anthrax     86    150     86*150/256 =  50  150/25 =  6

Total      385    300    385*300/256 = 451  300/25 = 12
```

```javascript
//prefix
//septic    +  15 poison damage over 3 seconds
//foul      +  50 poison damage over 4 seconds
//toxic     + 100 poison damage over 5 seconds
//pestilent + 175 poison damage over 6 seconds
 
//suffix
//blight     +  6 poison damage over 3 seconds
//venom      + 15 poison damage over 4 seconds
//pestilence + 25 poison damage over 5 seconds
//anthrax    + 50 poison damage over 6 seconds
 
// prefix small charms
[poisonmaxdam] >= 52 && [poisonlength] == 3 // septic small charm
[poisonmaxdam] >= 128 && [poisonlength] == 4 // foul small charm
[poisonmaxdam] >= 205 && [poisonlength] == 5 // toxic small charm
[poisonmaxdam] >= 299 && [poisonlength] == 6 // pestilent small charm
 
// suffix small charms
[poisonmaxdam] >= 21 && [poisonlength] == 3 // small charm of blight
[poisonmaxdam] >= 39 && [poisonlength] == 4 // small charm of venom
[poisonmaxdam] >= 52 && [poisonlength] == 5 // small charm of pestilence
[poisonmaxdam] >= 86 && [poisonlength] == 6 // small charm of anthrax
 
// Combinations of Pre+Suf small Chamrs
[poisonmaxdam] >= 73 && [poisonlength] == 6 // septic small charm of blight             -  43 damage over 6 seconds
[poisonmaxdam] >= 91 && [poisonlength] == 7 // septic small charm of venom              -  62 damage over 7 seconds
[poisonmaxdam] >= 104 && [poisonlength] == 8 // septic small charm of pestilence        -  81 damage over 8 seconds
[poisonmaxdam] >= 138 && [poisonlength] == 9 // septic small charm of anthrax           - 121 damage over 9 seconds
 
[poisonmaxdam] >= 149 && [poisonlength] == 7 // foul small charm of blight              - 102 damage over 7 seconds
[poisonmaxdam] >= 167 && [poisonlength] == 8 // foul small charm of venom               - 130 damage over 8 seconds
[poisonmaxdam] >= 180 && [poisonlength] == 9 // foul small charm of pestilence          - 158 damage over 9 seconds
[poisonmaxdam] >= 214 && [poisonlength] == 10 // foul small charm of anthrax            - 209 damage over 10 seconds
 
[poisonmaxdam] >= 226 && [poisonlength] == 8 // toxic small charm of blight             - 177 damage over 8 seconds
[poisonmaxdam] >= 244 && [poisonlength] == 9 // toxic small charm of venom              - 214 damage over 9 seconds
[poisonmaxdam] >= 257 && [poisonlength] == 10 // toxic small charm of pestilence        - 251 damage over 10 seconds
[poisonmaxdam] >= 291 && [poisonlength] == 11 // toxic small charm of anthrax           - 313 damage over 11 seconds
 
[poisonmaxdam] >= 320 && [poisonlength] == 9 // pestilent small charm of blight         - 281 damage over 9 seconds
[poisonmaxdam] >= 338 && [poisonlength] == 10 // pestilent small charm of venom         - 330 damage over 10 seconds
[poisonmaxdam] >= 351 && [poisonlength] == 11 // pestilent small charm of pestilence    - 377 damage over 11 seconds
[poisonmaxdam] >= 385 && [poisonlength] == 12 // pestilent small charm of anthrax       - 451 damage over 12 seconds
 
//Affix      Rate  Frames  poison damage      over seconds
  ________________________________________________________
//pestilent  299    150    299*150/256 = 175  150/25 =  6
//anthrax     86    150     86*150/256 =  50  150/25 =  6

//Total      385    300    385*300/256 = 451  300/25 = 12

(damage*256) / (secound*25)
so in the case of the above mentioned 175/6
(175*256) / (6*25) = 44800 / 150 = 298,666666667
175 poison damage over 6 = [poisonmaxdam] >= 299 && [poisonlength] >= 6

(damage*256) / (secound*25)
so in the case of the above mentioned 100/5
(100*205) / (5*25) = 20500 / 125 = 164
100 poison damage over 5 = [poisonmaxdam] >= 164 && [poisonlength] >= 5
```

additional https://diablo2.diablowiki.net/Guide:Calculating_Poison_Damage_v1.10,_by_onderduiker
