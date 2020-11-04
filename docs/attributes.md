# Attributes

WebMUDs provides a vast number of attributes that can directly affect how characters perform in battles.

All attributes work on a hierarchy, as follows:

* **MUD-wide Attributes**: defaults for all races, classes, and NPCs.
* **Race/Class Attributes**: modified defaults for specific races and classes.
* **Character/NPC Attributes**: upon leveling up, characters can improve their own attributes if creators decide so.
* **Effect Attributes**: skills that cause effects can increment or decrement attributes on targets.
* **Gear Attributes**: upon wearing a piece of gear, the user will benefit from any attributes embedded in it.
* **Weapon Attributes**: certain attributes, when present on weapons, will only modify attacks performed by that weapon.

Most attributes follow the hierarchy above, allowing creators to have different attributes per race/class combination, being added up down the chain. For instance, a character with the following race/class combination:

* MUD-wide `HpBase = +100`
* Race `HpBase = +20`
* Class `HpBase = -10`

Will have an initial 110 health points.

## Meter-related Attributes

### `HpBase` (Health Points Base)

The amount of health points that a character starts with.

### `HpPts` (Health Points Bonus)

Increases HP by an absolute amount of points.

### `HpPct` (Health Percentage)

Increases HP by a percentage, applied on `HpBase`.

### `HpPct2` (Health Percentage Tier 2)

Increases HP by a percentage, applied on the sum of `HpBase` and `HpPts`. This is a more powerful health bonus.

### `HpCap` (Health Points Cap)

The maximum amount of HP a character can earn.

### `RgBase` (Regeneration Points Base)

The amount of points health naturally regenerate per second.

### `RgPts` (Regeneration Points Bonus)

This attribute increases/decreases `RegenBase` by an absolute amount.

### `RgHpPct` (Health-percentage Regeneration Percentage)

This attribute represents the percentage of the character's maximum HP regenerated per second.

### `RgPct` (Regeneration Bonus Percentage)

This attribute increases the sum of `RegenBase` and the points-result of `RegenHealthPct` by a percentage.

### `RgPct2` (Regeneration Bonus Percentage Tier 2)

This attribute increases the sum of `RegenBase`, `RegenPts`, and the points-result of `RegenHealthPct` by a percentage. It's a more powerful regeneration bonus.

### `RgDR` and `RgDRPct` (Regeneration Debuff Resistance Points/Percentage)

This attribute reduces incoming regeneration debuffs by diminishing-return points, and/or a percentage.

### `RgMod` (Regeneration Modifier)

This attribute modifies the overall regeneration (after all calculations done). A character with `RegenMod = -0.1` will regenerate 10% less points than normal.

### `SpBase` (Special Points Base)

The amount of special points characters begin with.

### `MvBase` (Movement Points Base)

The amount of movement points characters begin with.

### `MvDscPts` (Movement Discount Points)

This attribute applies a discount upon usage of movement points. The resulting percentage has diminishing returns.

### `MvDscPct` (Movement Discount Percentage)

This attribute applies a discount on movement point usage by a percentage. `MvDscPct = 100` will make all movement skills cost zero movement points, so use with caution.

## Damage-Type Attributes

Damage-type attributes are prefixed according to the damage type along with a base attribute.
* E.g, `Dmg` (`FireDmg`, `ColdDmg`), `Res` (`FireRes`, `ColdRes`), etc.
* For a list of prefixes, see [damage types](./damage-types.md).

Example for a character with `Dmg = 20` and `FireDmg = -50` (negative):
* This character will deal 20% additional damage with all types of damage other than Fire.
* This character will deal 30% less fire damage (`20 - 50 = -30`).

### `Dmg` (Damage)

Increases damage output. Values are percentages, so having `Dmg = -20` will cause a 20% reduction of all damage output, having `Dmg = 50` will increase all damage output by 50%, etc.

### `DmgPen` (Damage Penetration)

A percentage value that indicates how much damage will ignore resistances. Having `DmgPen = 100` will cause **all** resistances to be ignored, so use with caution.

### `CritC` (Critical Chance)

The chance that the attack will be a critical hit. Having `CritC = 100` will cause all damage to always crit, so use with caution.

### `CritD` (Critical Damage)

The amount of extra damage dealt on a critical, as a percentage. Having `CritD = 50` will cause damage to increase by 50% on a critical hit.

### `Res` (Resistance Points)

Reduces incoming damage. This attribute has diminishing returns, so having `Res = 100` will reduce incoming damage by 50%, `Res = 200` by 75%, etc.

### `ResPct` (Resistance Percentage)

Reduces incoming damage by a percentage. This attribute has no diminishing returns, so having `ResPct = 100` means total invinciblity, so use with caution.

While calculating damage resistance, this attribute is calculated first, then whatever damage is left is then subjected to reduction from the `Res` attribute.

### `ResDR` and `ResDRPct` (Resistance Debuff-Resistance Points)

Reduces the magnitude of incoming resistance debuffs. This attribute has diminishing returns, so `ResDR = 100` will reduce the magnitude of resistance debuffs by 50%.

Use `ResDRPct` to apply a percentage directly. Having `ResDRPct = 100` means the user will be immune to resistance debuffs.

### `ResDC` (Resistance Debuff Cleanse Points)

Reduces the duration of resistance debuffs on the character. This attribute has diminishing returns, so `ResDC = 100` will reduce the duration of resistance debuffs by 50%.

### `ResCapMin` and `ResCapMax` (Resistance Caps)

Percentage values that represent the minimum and maximum amount of resistance percentages the character can earn. The default values can be adjusted by creators.

The maximum defaults to 100, and is used in the diminishing formula of the `Res` attribute. Any value above 100 means the target will be **healed** when hit by an attack of that type, so use with caution.

The minimum defaults to -100, meaning characters can be debuffed enough to take double incoming damage at most.

Specific damage type values will take precedence. E.g., a character with `ResCapMax = 100` and `FireResCapMax = 80` means that they can reach 100% resistance values against all damage types but fire (80%).

### `Def` (Defense Points)

Increases chance to evade incoming damage. A value of zero means the character will always be hit. A value above zero is then checked against the enemy's accuracy to determine if it's a hit or a miss.

### `DefPct` (Defense Percentage)

Increases chance to evade by a percentage. A value of `DefPct = 100` means the character will evade 100% of incoming damage regardless of the attacker's accuracy, so use with caution.

### `DefDR` and `DefDRPct` (Defense Debuff-Resistance)

Reduces the magnitude of incoming defense debuffs. This attribute has diminishing returns, so `DefDR = 100` will reduce the magnitude of defense debuffs by 50%.

Use `DefDRPct` to apply a percentage directly. Having `DefDRPct = 100` means the user will be immune to defense debuffs.

### `DefDC` (Defense Debuff Cleanse Points)

Reduces the duration of defense debuffs on the character. This attribute has diminishing returns, so `DefDC = 100` will reduce the duration of defense debuffs by 50%.

### `Acc` (Accuracy Points)

Increases accuracy. A value of zero means the character will always miss.

The final chance to hit is computed against the enemy's `Def`. If the `Acc` of the user and the `Def` of the enemy are above zero and equal, the chance to hit will be 50%.

### `AccMod` (Accuracy Modifier)

This attribute multiplies `Acc` points. Having `AccMod = 1.5` will cause every point in `Acc` to be worth 50% more points.

### `AccPct` (Accuracy Percentage)

Increases accuracy by a fixed percentage. A value of `AccPct = 100` means the user will always hit the target, regardless of the target's `Def`, so use with caution.

Note: the final chance-to-hit percentage can be reduced if the enemy has any points in `DefPct`. In such cases, the basic chance-to-hit formula will apply between the final percentages (e.g., equal values yield 50% chance to hit).
