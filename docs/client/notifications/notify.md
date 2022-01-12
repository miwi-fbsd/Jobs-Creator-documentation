Triggered after notifying player client side

## Event
``` lua
RegisterNetEvent("esx_job_creator:notify", function(message)

end)
```

### Parameters

| Name              | Data Type | Description                 |
| -                 | -         | -                             |
| `message`         | string    | Message of the notification  |

## Example
``` lua
RegisterNetEvent("esx_job_creator:esx:ready", function() 
    -- Disables the default script notification (otherwise there would be 2 notifications)
    exports["esx_job_creator"]:disableScriptEvent("esx_job_creator:notify")
end)

RegisterNetEvent("esx_job_creator:notify", function(message)
    TriggerEvent("external_script:notify", message)
end)
```