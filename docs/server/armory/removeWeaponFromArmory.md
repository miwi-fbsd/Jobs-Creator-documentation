

To add a weapon in a marker ID for a specific player

## Export
``` lua
exports["esx_job_creator"]:removeWeaponFromArmory(markerId, weaponId)
```

### Parameters

| Name    | Data Type | Description                 |
| -                 | -         | -                 |
| `markerId`        | integer   | The marker ID     |
| `weaponId`| integer    | Weapon ID in the database, can be seen in ``` exports["esx_job_creator"]:getAllArmoryWeapons(markerId) ``` |

### Return value
| Name              | Data Type | Description                                   |
| -                 | -         | -                                             |
| `isSuccessful`   | boolean     | If the weapon is removed or not   |

## Example
``` lua
local markerId = 15
local weaponId = 356

local success = exports["esx_job_creator"]:removeWeaponFromArmory(markerId, weaponId)

print(success)
```