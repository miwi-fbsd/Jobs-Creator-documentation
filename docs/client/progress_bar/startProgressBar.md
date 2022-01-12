Triggered when using progress bar

## Event
``` lua
RegisterNetEvent("esx_job_creator:startProgressBar", function(time, text)

end)
```

### Parameters

| Name              | Data Type | Description                       |
| -                 | -         | -                                 |
| `time`            | int       | Progress bar duration in seconds  |
| `text`            | string    | Description text                  |

## Example
``` lua
RegisterNetEvent("esx_job_creator:esx:ready", function() 
    -- Disables the default script progress bar (otherwise there would be 2 progress bars)
    exports["esx_job_creator"]:disableScriptEvent("esx_job_creator:startProgressBar")
end)

-- Example to replace the script progress bar with an external one
RegisterNetEvent("esx_job_creator:startProgressBar", function(time, text)
    -- The event to activate your external progress bar
    TriggerEvent("external_progressbar:start", time, text)
end)
```