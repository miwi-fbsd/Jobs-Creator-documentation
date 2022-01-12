Triggered after notifying player client side

## Event
``` lua
RegisterNetEvent("esx_job_creator:notify", function(message, uncoloredMessage)

end)
```

### Parameters

| Name              | Data Type | Description                 |
| -                 | -         | -                             |
| `message`         | string    | Message of the notification  |
| `uncoloredMessage`         | string    | Message of the notification but without ~r~, ~g~, etc.  |

## Example
``` lua
RegisterNetEvent("esx_job_creator:esx:ready", function() 
    -- Disables the default script notification (otherwise there would be 2 notifications)
    exports["esx_job_creator"]:disableScriptEvent("esx_job_creator:notify")
end)

RegisterNetEvent("esx_job_creator:notify", function(message, uncoloredMessage)
    TriggerEvent("external_script:notify", message)
end)
```