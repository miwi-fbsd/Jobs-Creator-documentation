Triggered when using billing option in F6 actions menu

## Event
``` lua
AddEventHandler("esx_job_creator:actions:createBilling", function()

end)
```

## Example
``` lua
AddEventHandler("esx_job_creator:esx:ready", function() 
    -- Disables the default script billing (otherwise there would be 2 billings)
    exports["esx_job_creator"]:disableScriptEvent("esx_job_creator:actions:createBilling")
end)

AddEventHandler("esx_job_creator:actions:createBilling", function()
    -- Uses Billing UI event
    TriggerEvent("billing_ui:activateBillingMode")
end)
```