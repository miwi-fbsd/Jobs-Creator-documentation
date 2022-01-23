Returns if the client/player is handcuffed

## Export
``` lua
exports["esx_job_creator"]:isPlayerHandcuffed()
```

### Return value
| Name                | Data Type | Description                                   |
| -                   | -         | -                                             |
| `isHandcuffed`   | boolean | true if the player is handcuffed. false if the player is **not** handcuffed   |

## Example
``` lua
if(not exports["esx_job_creator"]:isPlayerHandcuffed())then
    print("You are not handcuffed")
else
    print("You are handcuffed")
end
```