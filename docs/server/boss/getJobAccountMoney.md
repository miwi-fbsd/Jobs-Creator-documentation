To get a list of weapons of a player stored in a specific armory ID.

## Export
``` lua
exports["esx_job_creator"]:getJobAccountMoney(jobName)
```

### Parameters

| Name              | Data Type | Description                 |
| -                 | -         | -                 |
| `jobName`         | string    | Job ID (example police)  |

### Return value
| Name              | Data Type | Description                                       |
| -                 | -         | -                                                 |
| `accountMoney`    | integer   | Money stored in society account |

## Example
``` lua
local jobMoney = exports["esx_job_creator"]:getJobAccountMoney("gang_job")

print(jobMoney)
```