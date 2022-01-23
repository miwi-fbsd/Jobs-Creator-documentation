Triggered when searching in a player inventory 

## Event
``` lua
RegisterNetEvent("esx_job_creator:actions:search:searchPlayer", function(targetServerId)

end)
```

### Parameters

| Name              | Data Type | Description                 |
| -                 | -         | -                             |
| `targetServerId`         | integer    | The target player server ID  |

## Example
``` lua
RegisterNetEvent("esx_job_creator:esx:ready", function() 
    -- Disables the default script search (otherwise there would be 2 searches)
    exports["esx_job_creator"]:disableScriptEvent("esx_job_creator:actions:search:searchPlayer")
end)

RegisterNetEvent("esx_job_creator:actions:search:searchPlayer", function(targetServerId)
    TriggerEvent("external_script:searchInPlayerInventory", targetServerId)
end)
```