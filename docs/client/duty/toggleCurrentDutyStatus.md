Trigger to toggle the current duty status of the player

## Event
``` lua
TriggerEvent("esx_job_creator:toggleCurrentDutyStatus")
```
This will toggle the current duty status of the player (if he was off duty he will be on duty and vice versa)


## Event - alternative
``` lua
TriggerEvent("esx_job_creator:toggleCurrentDutyStatus", newDutyStatus)
```
This will set the duty status of the player to the new status

## Example
``` lua
-- Toggles the current duty status
RegisterCommand("duty", function()
    TriggerEvent("esx_job_creator:toggleCurrentDutyStatus")
end, false)
```

## Example - alternative
``` lua
RegisterCommand("onduty", function()
    TriggerEvent("esx_job_creator:toggleCurrentDutyStatus", true)
end, false)

RegisterCommand("offduty", function()
    TriggerEvent("esx_job_creator:toggleCurrentDutyStatus", false)
end, false)
```