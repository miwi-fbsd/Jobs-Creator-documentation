Triggered after notifying player client side

## Event
``` lua
AddEventHandler("esx_job_creator:notify", function(message)

end)
```

### Parameters

| Name              | Data Type | Description                 |
| -                 | -         | -                             |
| `message`         | string    | Message of the notification  |

## Example
``` lua
-- To place in esx_job_creator/integrations/cl_integrations.lua

AddEventHandler("esx_job_creator:esx:ready", function() 
    -- Disables the default script notification (otherwise there would be 2 notifications)
    exports["esx_job_creator"]:disableScriptEvent("esx_job_creator:notify")
end)

AddEventHandler("esx_job_creator:notify", function(message)
    TriggerEvent("external_script:notify", message)
end)
```