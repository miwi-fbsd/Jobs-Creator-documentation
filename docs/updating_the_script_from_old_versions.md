This section will explain how to update the script from old versions
<br>
<br>
You'll have to follow **all steps** from your _current version_ to the _newer one_

A **backup** is always suggested before doing these steps

## 3.5 Update - to do if your version is older than 3.5
Add the following code in `esx_job_creator/integrations/sv_integrations.lua` and use the command in the server console or in game (there will be an output when you use the command)
``` lua
RegisterCommand('updateRecipes', function(playerId)
    if(playerId == 0 or isAllowed(playerId)) then
        MySQL.Async.fetchAll('SELECT id, data FROM jobs_data WHERE type="crafting_table"', {}, function(results)
            for k, result in pairs(results) do
                local markerId = result.id

                if(result.data) then
                    local data = json.decode(result.data)

                    local newData = {}

                    local anythingChanged = false

                    if(data.craftablesItems) then
                        for itemName, craftingData in pairs(data.craftablesItems) do
                            if(not craftingData.recipes) then
                                anythingChanged = true
                            end

                            newData[itemName] = {
                                recipes = craftingData,
                                animations = {}
                            }
                        end
                    end

                    local markerData = {
                        craftablesItems = newData
                    }

                    if(anythingChanged) then
                        print("Updating marker ID: " .. markerId)
                        MySQL.Async.execute("UPDATE jobs_data SET data=@newData WHERE id=@markerId", {
                            ['@newData'] = json.encode(markerData),
                            ['@markerId'] = markerId
                        })
                    else
                        print("Marker ID " .. markerId .. " doesn't need to update")
                    end
                end
            end
        end)
    end
end)
```

## 3.8 Update - to do if your version is older than 3.8
Run this query in the database to convert old job shop items

```mysql
ALTER TABLE job_shop ADD COLUMN IF NOT EXISTS `item_type` VARCHAR(50) NOT NULL AFTER item_name;
UPDATE job_shop SET item_type = "item_standard";
```

## 3.11 Update - to do if your version is older than 3.11
Add the following code in `esx_job_creator/integrations/sv_integrations.lua` and use the command in the server console or in game (there will be an output when you use the command)
```lua
RegisterCommand('updateHarvest', function(playerId)
    if(playerId == 0 or isAllowed(playerId)) then
        MySQL.Async.fetchAll('SELECT id, data FROM jobs_data WHERE type="harvest"', {}, function(results)
            for k, result in pairs(results) do
                local markerId = result.id
                local data = json.decode(result.data)

                local anythingChanged = false

                if(data) then
                    if(data.itemQuantity) then
                        data.itemMinQuantity = data.itemQuantity
                        data.itemMaxQuantity = data.itemQuantity
                        data.itemQuantity = nil

                        anythingChanged = true
                    end
                end

                if(anythingChanged) then
                    print("Updating marker ID: " .. markerId)
                    MySQL.Async.execute("UPDATE jobs_data SET data=@newData WHERE id=@markerId", {
                        ['@newData'] = json.encode(data),
                        ['@markerId'] = markerId
                    })
                else
                    print("Marker ID " .. markerId .. " doesn't need to update")
                end
            end
        end)
    end
end)
```

## 3.14 Update - to do if your version is older than 3.14
Run this query in the database to convert old database tables and to create the new one

```mysql
CREATE TABLE IF NOT EXISTS `jobs_wardrobes` (
    `id` INT(11) NOT NULL AUTO_INCREMENT,
    `identifier` VARCHAR(100) NOT NULL COLLATE 'utf8mb4_general_ci',
    `label` VARCHAR(50) NOT NULL COLLATE 'utf8mb4_general_ci',
    `outfit` LONGTEXT NOT NULL DEFAULT '' COLLATE 'utf8mb4_bin',
    PRIMARY KEY (`id`) USING BTREE,
    INDEX `identifier` (`identifier`) USING BTREE
);

RENAME TABLE 
    job_armory TO jobs_armories,
    job_garage TO jobs_garages,
    job_shop TO jobs_shops;
```

## 3.16 Update - to do if your version is older than 3.16
Add the following code in `esx_job_creator/integrations/sv_integrations.lua` and use the command in the server console or in game (there will be an output when you use the command)

```lua
RegisterCommand('updateShops', function(playerId)
    if(playerId == 0 or isAllowed(playerId)) then
        MySQL.Async.fetchAll('SELECT id, data FROM jobs_data WHERE type="shop"', {}, function(results)
            for k, result in pairs(results) do
                local markerId = result.id
                local data = json.decode(result.data)

                local anythingChanged = false

                if(data and data.itemsOnSale) then
                    for itemName, itemData in pairs(data.itemsOnSale) do
                        if(type(itemData) == "number") then
                            data.itemsOnSale[itemName] = {
                                price = itemData
                            }
                            
                            anythingChanged = true
                        end
                    end
                end

                if(anythingChanged) then
                    print("Updating marker ID: " .. markerId)
                    MySQL.Async.execute("UPDATE jobs_data SET data=@newData WHERE id=@markerId", {
                        ['@newData'] = json.encode(data),
                        ['@markerId'] = markerId
                    })
                else
                    print("Marker ID " .. markerId .. " doesn't need to update")
                end
            end
        end)
    end
end)
```

## 3.18 Update - to do if your version is older than 3.18
Add the following code in `esx_job_creator/integrations/sv_integrations.lua` and use the command in the server console or in game (there will be an output when you use the command)

```lua
RegisterCommand('updateHarvest2', function(playerId)
    if(playerId == 0 or isAllowed(playerId)) then
        MySQL.Async.fetchAll('SELECT id, data FROM jobs_data WHERE type="harvest"', {}, function(results)
            for k, result in pairs(results) do
                local markerId = result.id
                local data = json.decode(result.data)

                local anythingChanged = false

                if(data) then
                    if(data.itemName or data.itemMinQuantity or data.itemMaxQuantity) then

                        data.harvestableItems = {
                            {
                                name = data.itemName,
                                minQuantity = data.itemMinQuantity,
                                maxQuantity = data.itemMaxQuantity,
                                time = data.itemTime,
                                chances = 100
                            }
                        }

                        data.itemMinQuantity = nil
                        data.itemMaxQuantity = nil
                        data.itemTime = nil
                        data.itemName = nil

                        anythingChanged = true
                    end
                end

                if(anythingChanged) then
                    print("Updating marker ID: " .. markerId)
                    MySQL.Async.execute("UPDATE jobs_data SET data=@newData WHERE id=@markerId", {
                        ['@newData'] = json.encode(data),
                        ['@markerId'] = markerId
                    })
                else
                    print("Marker ID " .. markerId .. " doesn't need to update")
                end
            end
        end)
    end
end)
```

## 4.0 Update - to do if your version is older than 4.0
**After running the server and the script is started**, run this query in the database
```mysql
UPDATE jobs_data SET grades_type="minimumGrade" WHERE grades_type IS NULL;
```

<br>

Add the following code in `esx_job_creator/integrations/sv_integrations.lua` and use **both commands** in the server console or in game (there will be an output when you use the command)

```lua
RegisterCommand('updateHarvest3', function(playerId)
    if(playerId == 0 or isAllowed(playerId)) then
        MySQL.Async.fetchAll('SELECT id, data FROM jobs_data WHERE type="harvest"', {}, function(results)
            for k, result in pairs(results) do
                local markerId = result.id
                local data = json.decode(result.data)

                local anythingChanged = false

                if(data) then
                    if(data.itemTool and not data.itemToolLoseProbability) then
                        data.itemToolLoseProbability = 100
                        anythingChanged = true
                    end
                end

                if(anythingChanged) then
                    print("Updating marker ID: " .. markerId)
                    MySQL.Async.execute("UPDATE jobs_data SET data=@newData WHERE id=@markerId", {
                        ['@newData'] = json.encode(data),
                        ['@markerId'] = markerId
                    })
                else
                    print("Marker ID " .. markerId .. " doesn't need to update")
                end
            end
        end)
    end
end)

RegisterCommand('updateMarkets', function(playerId)
    if(playerId == 0 or isAllowed(playerId)) then
        MySQL.Async.fetchAll('SELECT id, data FROM jobs_data WHERE type="market"', {}, function(results)
            for k, result in pairs(results) do
                local markerId = result.id
                local data = json.decode(result.data)

                local anythingChanged = false

                if(data and data.items) then
                    for itemName, itemData in pairs(data.items) do
                        if(itemData.price) then
                            itemData.maxPrice = itemData.price
                            itemData.minPrice = itemData.price
                            itemData.price = nil

                            anythingChanged = true
                        end
                    end
                end

                if(anythingChanged) then
                    print("Updating marker ID: " .. markerId)
                    MySQL.Async.execute("UPDATE jobs_data SET data=@newData WHERE id=@markerId", {
                        ['@newData'] = json.encode(data),
                        ['@markerId'] = markerId
                    })
                else
                    print("Marker ID " .. markerId .. " doesn't need to update")
                end
            end
        end)
    end
end)
```

