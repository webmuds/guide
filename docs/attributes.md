# Attributes

The platform provides a large number of attributes that directly affect how characters can perform in battles.

Skills and items with attributes (wearables except weapons, consumables, etc) will add up with character attributes.

Weapons with attributes will only apply on attacks with them.

## Damage-Type Attributes

Damage-type attributes are prefixed according to the damage type along with a base attribute.
* E.g, `Dmg` (`FireDmg`, `ColdDmg`), `Res` (`FireRes`, `ColdRes`), etc.
* For a list of prefixes, see [damage types](./damage-types.md).

Example for a character with `Dmg = 20` and `FireDmg = -50` (negative):
* This character will deal 20% additional damage with all types of damage other than Fire.
* This character will deal 30% less fire damage (`20 - 50 = -30`).

### `Dmg` (Damage)

Increases damage output. Values are percentages, so having `Dmg = -20` will cause a 20% reduction of all damage output, having `Dmg = 50` will increase all damage output by 50%, etc.

### `Res` (Resistance Points)

Reduces incoming damage. This attribute has diminishing returns, so having `Res = 100` will reduce incoming damage by 50%, `Res = 200` by 75%, etc.

### `ResCapMin` and `ResCapMax` (Resistance Caps)

Percentage values that represent the minimum and maximum amount of resistance percentages the character can earn.

The maximum defaults to 100, and is used in the diminishing formula of the `Res` attribute.

The minimum defaults to -100, meaning characters can be debuffed enough to take double incoming damage at most.

Specific damage type values will take precedence. E.g., a character with `ResCapMax = 100` and `FireResCapMax = 80` means that they can reach 100% resistance values against all damage types but fire (80%).

### `ResPct` (Resistance Percentage)

Reduces incoming damage by a percentage. This attribute has no diminishing returns, so having `DmgResPct = 100` means total invinciblity, so use with caution.

While calculating damage resistance, this attribute is calculated first, then whatever damage is left is then subjected to reduction from the `Res` attribute.

### `ResDR` (Resistance Debuff-Resistance Points)

Reduces the magnitude of incoming resistance debuffs. This attribute has diminishing returns, so `ResDR = 100` will reduce the magnitude of resistance debuffs by 50%.

### `ResDC` (Resistance Debuff Cleanse Points)

Reduces the duration of resistance debuffs on the character. This attribute has diminishing returns, so `ResDP = 100` will reduce the duration of resistance debuffs by 50%.

### `Def` (Defense Points)

Increases chance to evade incoming damage. A value of zero means the character will have 100% chance to be hit by that damage type. A value above zero is then checked against the enemy's accuracy to determine if it's a hit or a miss.

### `DefPct` (Defense Percentage)

Increases chance to evade by a percentage. A value of `DefPct = 100` means the character will evade 100% of incoming damage, so use with caution.

### `DefDR` (Defense Debuff-Resistance)

Reduces the magnitude of incoming defense debuffs. This attribute has diminishing returns, so `DefDR = 100` will reduce the magnitude of defense debuffs by 50%.

### `Acc` (Accuracy Points)

Increases accuracy. A value of zero means the character will always miss.

The final chance to hit is computed against the enemy's `Def`. If the `Acc` of the user and the `Def` of the enemy are above zero and equal, the chance to hit will be 50%.

### `AccPct` (Accuracy Percentage)

Increases accuracy by a percentage. A value of `AccPct = 100` means the user will always hit the target, regardless of the target's `Def`, so use with caution.

Note: the final chance-to-hit percentage can be reduced if the enemy has any points in `DefPct`. In such cases, the basic chance-to-hit formula will apply between the final percentages (e.g., equal values yield 50% chance to hit).
