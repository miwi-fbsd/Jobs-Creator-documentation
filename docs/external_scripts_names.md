In case your server uses different script names than the default ones, you can edit those names in `esx_job_creator/integrations/sh_integrations.lua`

Example of default ones
``` lua
EXTERNAL_SCRIPTS_NAMES = {
    ["es_extended"] = "es_extended",
    ["esx_addonaccount"] = "esx_addonaccount"
}
```
<br>
Example of edited ones

``` lua
EXTERNAL_SCRIPTS_NAMES = {
    ["es_extended"] = "mygamemode_extended",
    ["esx_addonaccount"] = "mygamemode_addonaccount"
}
```