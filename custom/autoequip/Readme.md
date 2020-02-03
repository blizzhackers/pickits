[pickit table of content](https://github.com/blizzhackers/pickits/#pickits)

[NipGuide](https://github.com/blizzhackers/pickits/blob/master/NipGuide.md)

---

## Autoequip

---

To use it, ADD these lines to your character config.

```javascript
Config.AutoEquip = true;
Config.PickitFiles.push("autoequip/sorceress.xpac.nip");
```

This is an example autoequip pickit.

```javascript
// weapon
[type] == wand && [quality] <= rare # [maxmana] > 0 # [tier] == 1
[type] == wand && [quality] <= rare # [fcr] > 0 && [maxmana] > 0 # [tier] == 2
//[type] == staff && [quality] <= rare # [skillfirebolt] >= 1 # [tier] == 2

// armor
[type] == armor && [quality] <= rare # # [tier] == 1
[type] == armor && [quality] <= rare # [maxhp] > 0 # [tier] == 2

// boots
[type] == boots && [quality] <= rare # # [tier] == 1
[type] == boots && [quality] <= rare # [lightresist] > 0 # [tier] == 2

// gloves
[type] == gloves && [quality] <= rare # # [tier] == 1
[type] == gloves && [quality] <= rare # [maxhp] > 0 # [tier] == 2

// amulet
[type] == amulet && [quality] <= rare # [maxhp] > 0 && [maxmana] > 0 # [tier] == 1

// ring
[type] == ring && [quality] <= rare # [maxhp] > 0 # [tier] == 1

// belt
[type] == belt && [quality] <= rare # # [tier] == 1
[type] == belt && [quality] <= rare # [maxhp] > 0 # [tier] == 2

// helm
[type] == helm && [quality] == rare # # [tier] == 1
[type] == helm && [quality] == rare # [maxhp] > 0 # [tier] == 2

// shield
[type] == shield && [quality] <= rare #  # [tier] == 1
[type] == shield && [quality] <= rare # [fireresist]+[lightresist]+[coldresist] >= 30 # [tier] == 3
[type] == shield && [quality] <= rare # [fireresist]+[lightresist]+[coldresist] >= 50 # [tier] == 4
```