# Premade Applicants Filter

Premade Applicants Filter helps you limit the visible applicants of the LFG
Premade Groups tool. When creating a premade group for a popular activity such
as the latest raid or a high mythic plus dungeon, group leaders find themselves
with a lot of applicants. Those applicants have to be checked manually for
role, class, item level and other external metrics such as a Raider.IO rating.
Premade Applicants Filter aims to help group leaders by filtering out
applicants that do not match the required criteria.

### Keywords

All applicants are technically an applicant group that consists of a list of
members. Most of the time, there is only one member in this group. This means
that all statements about the members of an applicant group have to be 
quantified using either the *some* or *all* quantifiers. The only unbound
keyword is the `members` variable which is a direct property of the applicant
group. This means instead of just boolean expression, you may now write
some sort of first-order logic expression!

**Examples:**

| Expression     | Explanation |
|----------------|-------------|
| `members == 1` | only applicant groups with one member |
| `some("heal")` | there is at least one heal in the applicant group |
| `all("ilvl >= 400")` | all members of the applicant group must have item level 400 or better |
| `all("ilvl >= 400 and (rio > 800 or rioprev > 800 or riomain > 800)")` | all members of the applicant group must have item level 400 or better and a Raider.IO rating of 800 this season, last season or on their main character |
| `some("heal or deathknight") and none("hunter")` | there is at least one heal or deathknight in the group, but no hunter |

#### Quantifiers

| Quantifier     | Synonyms | Description |
|----------------|----------|-------------|
| `all("...")`   | `every`  | all members of the applicant group must fulfill the given predicate |
| `some("...")`  | `exists` | at least one member of the applicant group must fulfill the given predicate |
| `none("...")`  |          | synonym to `not all()` |

#### Global keywords

This keyword must not be quantified (all other keywords require a quantifier).

| Keyword        | Type    | Description |
|----------------|---------|-------------|
| `members`      | integer | number of members in the applicant group |

#### Standard keywords

| Keyword        | Type    | Description |
|----------------|---------|-------------|
| `level`        | integer | applicant level |
| `ilvl`         | integer | maximum item level |
| `myilvl`       | integer | your own item level (for comparison) |
| `hlvl`         | integer | honor level |
| `relationship` | string  | your relationship to the applicant (friend, guild or empty) |
| `friend`       | boolean | if applicant is in your friend list |
| `guild`        | boolean | if applicant is in your guild |
| `tank`         | boolean | if applicant would like to play tank |
| `healer`       | boolean | if applicant would like to play heal |
| `heal`         | boolean | synonym for `healer` |
| `damage`       | boolean | if applicant would like to play damage dealer |
| `dps`          | boolean | synonym for `damage` |
| `range`        | boolean | if applicant's class can be a ranged class |
| `melee`        | boolean | if applicant's class can be a melee class |

#### Class keywords

| Keyword        | Type    | Description |
|----------------|---------|-------------|
| `deathknight`  | boolean | if applicant is a deathknight |
| `demonhunter`  | boolean | if applicant is a demonhunter |
| `druid`        | boolean | if applicant is a druid |
| `hunter`       | boolean | if applicant is a hunter |
| `paladin`      | boolean | if applicant is a paladin |
| `priest`       | boolean | if applicant is a priest |
| `mage`         | boolean | if applicant is a mage |
| `monk`         | boolean | if applicant is a monk |
| `rogue`        | boolean | if applicant is a rogue |
| `shaman`       | boolean | if applicant is a shaman |
| `warlock`      | boolean | if applicant is a warlock |
| `warrior`      | boolean | if applicant is a warrior |

#### Rating keywords
| Keyword        | Type    | Description |
|----------------|---------|-------------|
| mprating       | integer | overall mythic+ dungeon rating (0 if no rating) |
| mpmaprating    | integer | mythic+ rating in current dungeon (0 if no rating) |
| mpmapmaxkey    | integer | max key done in current mythic+ dungeon (0 if no rating) |
| mpmapintime    | boolean | current mythic+ dungeon completed successfully (false if no rating) |
| mpmapname      | string  | current mythic+ dungeon name (can be empty if no rating) |

#### Provided by [Premade Regions](https://github.com/0xbs/premade-regions)

| Keyword        | Type    | Description |
|----------------|---------|-------------|
| `region`       | string  | region name of the applicant |
| `oce`          | boolean | if the data center region of the applicant is Sydney |
| `chi`          | boolean | if the data center region of the applicant is Chicago |
| `la`           | boolean | if the data center region of the applicant is Los Angeles |
| `mex`          | boolean | if the data center region of the applicant is Mexico |
| `bzl`          | boolean | if the data center region of the applicant is Brazil |

#### Provided by Raider.IO

| Keyword             | Type    | Description | Example |
|---------------------|---------|-------------|---------|
| `hasrio`            | boolean | if the group leader has a raider.io profile|`hasrio`|
| `norio`             | boolean | if the the group leader does not have a raider.io profile|`( norio or rio > 500 )`|
| `rio`               | integer | Raider.io ranking of the group leader|`rio > 500`|
| `rioprev`           | integer | Raider.io ranking in previous season|`rioprev > 500`|
| `riomain`           | integer | Raider.io ranking of main character|`riomain > 500`|
| `rioprevmain`       | integer | Raider.io ranking of main character in previous season|`rioprevmain > 500`|
| `riokey5plus`       | integer | number of dungeons the group leader completed with keystone of level 5 or higher|`riokey5plus >= 5`|
| `riokey10plus`      | integer | number of dungeons the group leader completed with keystone of level 10 or higher|`riokey10plus >= 5`|
| `riokey15plus`      | integer | number of dungeons the group leader completed with keystone of level 15 or higher|`riokey15plus >= 5`|
| `riokey20plus`      | integer | number of dungeons the group leader completed with keystone of level 20 or higher|`riokey20plus >= 5`|
| `riokeymax`         | integer | the maximum keystone level the group leader completed|`riokeymax >= 10`|
| `rionormalprogress` | integer | the number of bosses killed in the current raid on normal difficulty (e.g. 2 means any two bosses killed)|`rionormalprogress > 0`|
| `rioheroicprogress` | integer | the number of bosses killed in the current raid on heroic difficulty (e.g. 2 means any two bosses killed)|`rioheroicprogress > 0`|
| `riomythicprogress` | integer | the number of bosses killed in the current raid on mythic difficulty (e.g. 2 means any two bosses killed)|`riomythicprogress > 0`|
| `riomainprogress`   | integer | the maximum number of bosses killed in the current raid on any difficulty with the main character (i.e. you are looking at a twink)|`riomainprogress > 0`|
| `rionormalkills`    | table   | a table that contains the number of kills for each boss on normal difficulty|`rionormalkills[1] > 0` means first boss killed at least once|
| `rioheroickills`    | table   | a table that contains the number of kills for each boss on heroic difficulty|`rioheroickills[8] > 0` means 8th boss killed at least once|
| `riomythickills`    | table   | a table that contains the number of kills for each boss on mythic difficulty|`riomythickills[3] > 0` means third boss killed at least once|
| `rioraidbosscount`  | integer | number of bosses in the current raid|`rionormalkills[rioraidbosscount] > 0` means last boss in the raid killed at least once on normal|

### License

The software is provided under the GNU General Public License, Version 3. See the `LICENSE` file for details.
