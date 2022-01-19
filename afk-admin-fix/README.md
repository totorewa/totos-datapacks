# AFK Admin Fix


Restores the Admin team on worlds running an AFK datapack.

An AFK datapack adds the player to an AFK team when they haven't moved for a while. 
Upon movement, the AFK datapack then removes them from the team, but whatever team 
they were in before is not restored. This datapack will add a player with an `IsAdmin`
score of `1` to the `Admins` team if they are not in a team.

## Setting player as admin
No wrapper functions are provided for this functionality as to execute the function
for another player would be more effort and verbose than just setting the scoreboard
directly.

To add a player to the admin team, execute:
```
/scoreboard players set <player> IsAdmin 1
```

To remove a player from the admin team, execute:
```
/scoreboard players remove <player> IsAdmin
```

## Adding more teams
The datapack doesn't support teams other than `Admins`, but the datapack can easily
be altered to accomodate this by creating new scoreboards in 
`afk_admin_fix/functions/setup.mcfunction` with a command like:  
```
scoreboard objectives add IsSupporter dummy
```
and then appending `afk_admin_fix/functions/loop.mcfunction` with:
```
execute as @a[scores={IsSupporter=1},team=] run team join Supporters
```
