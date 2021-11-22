Triggered after notifying player server side

## Event
``` lua
AddEventHandler("esx_job_creator:notify", function(playerId, message)

end)
```

### Parameters

| Name              | Data Type | Description                 |
| -                 | -         | -                 |
| `playerId`        | integer    | Target player server ID  |
| `message`         | string    | Message of the notification  |

## Example
``` lua
AddEventHandler("esx_job_creator:esx:ready", function() 
    -- Disables the default script notification (otherwise there would be 2 notifications)
    exports["esx_job_creator"]:disableScriptEvent("esx_job_creator:notify")
end)

AddEventHandler("esx_job_creator:notify", function(playerId, message)
    TriggerClientEvent("external_script:notify", playerId, message)
end)
```