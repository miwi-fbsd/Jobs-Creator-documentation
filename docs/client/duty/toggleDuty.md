Triggered after player goes on/off duty client side

## Event
``` lua
AddEventHandler("esx_job_creator:toggleDuty", function(isOnDuty)

end)
```

### Parameters

| Name              | Data Type | Description                 |
| -                 | -         | -                 |
| `isOnDuty`         | boolean    | Player new duty status  |

## Example
``` lua
AddEventHandler("esx_job_creator:toggleDuty", function(isOnDuty)
    if(isOnDuty) then
        ESX.ShowNotification("You are now on duty")
    else
        ESX.ShowNotification("You are now off duty")
    end
end)
```