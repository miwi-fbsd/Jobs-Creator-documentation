To add money to a society

## Export
``` lua
exports["esx_job_creator"]:addSocietyMoney(jobName, amount)
```

### Parameters

| Name              | Data Type | Description                 |
| -                 | -         | -                 |
| `jobName`         | string    | Job ID (example police)  |
| `amount`         | integer    | Amount of money to add |

### Return value
| Name              | Data Type | Description                                       |
| -                 | -         | -                                                 |
| `isSuccessful`    | boolean   | If money are added or not |

## Example
``` lua
local isSuccessful = exports["esx_job_creator"]:addSocietyMoney("police", 5000)

print(isSuccessful)
```