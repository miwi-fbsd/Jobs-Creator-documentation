Trigger to toggle the current duty status of the player

## Event
``` lua
TriggerEvent("esx_job_creator:toggleCurrentDutyStatus")
```

## Example
``` lua
-- Toggles the current duty status
RegisterCommand("duty", function()
    TriggerEvent("esx_job_creator:toggleCurrentDutyStatus")
end, false)
```