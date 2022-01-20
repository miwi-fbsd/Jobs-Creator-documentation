Triggered when a vehicle is impounded

## Event
``` lua
AddEventHandler("esx_job_creator:actions:vehicleImpounded", function(vehiclePlate, vehicleModel)

end)
```

### Parameters

| Name              | Data Type | Description                       |
| -                 | -         | -                                 |
| `vehiclePlate`            | string       | The vehicle plate  |
| `vehicleModel`            | string       | The vehicle model  |

## Example
``` lua
RegisterNetEvent("esx_job_creator:actions:vehicleImpounded", function(vehiclePlate, vehicleModel)
    -- You can add your impound script exports here
    TriggerServerEvent("impound_script:impoundVehicle", vehiclePlate, vehicleModel)
end)
```