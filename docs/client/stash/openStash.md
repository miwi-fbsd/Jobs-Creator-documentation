Triggered when opening a stash

## Event
``` lua
RegisterNetEvent("esx_job_creator:stash:openStash", function(markerId)

end)
```

### Parameters

| Name              | Data Type | Description                       |
| -                 | -         | -                                 |
| `markerId`        | int       | Marker ID  |

## Example
``` lua
RegisterNetEvent("esx_job_creator:esx:ready", function() 
    -- Disables the default script stash
    exports["esx_job_creator"]:disableScriptEvent("esx_job_creator:stash:openStash")
end)

-- Example to replace the script stash with an external one
RegisterNetEvent("esx_job_creator:stash:openStash", function(markerId)
    -- Example with Chezza's inventory
    TriggerEvent('inventory:open', {
        id = "marker_" .. markerId,
        type = "esx_job_creator_stash",
        title = 'Stash - ' .. markerId,
        weight = 1000,
        save = true,
        timeout = 1000
    })
end)
```