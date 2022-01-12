Triggered when opening an armory

## Event
``` lua
AddEventHandler("esx_job_creator:armory:openArmory", function(markerId)

end)
```

### Parameters

| Name              | Data Type | Description                       |
| -                 | -         | -                                 |
| `markerId`            | int       | Marker ID  |

## Example
``` lua
RegisterNetEvent("esx_job_creator:esx:ready", function() 
    -- Disables the default script armory
    exports["esx_job_creator"]:disableScriptEvent("esx_job_creator:armory:openArmory")
end)

-- Example to replace the script armory with an external one
RegisterNetEvent("esx_job_creator:armory:openArmory", function(markerId)
    -- Example with Chezza's inventory
    TriggerEvent('inventory:open', {
        id = "marker_" .. markerId,
        type = "esx_job_creator_armory",
        title = 'Armory - ' .. markerId,
        weight = 1000,
        save = true,
        timeout = 1000
    })
end)
```