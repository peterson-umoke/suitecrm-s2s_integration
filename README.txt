Components for integration between the two SugarCRM

Creates tables to record changes and track changes in other builds.
To record changes to the table, you need to add hooks for the right modules
array(
'module' q '<module>', (indicate module
'hook' => 'after_save',
'order' => 50,
'description' => 'Insert into s2s_modifications_log create/update action',
'file' => 'custom/include/S2S_Integration/S2S_Hooks.php',
'class' => 'S2S_Hooks',
'function' => 'afterSave',
),
array(
'module' q '<module>', (indicate module
'hook' => 'after_delete',
'order' => 50,
'description' => 'Insert into s2s_modifications_log delete action',
'file' => 'custom/include/S2S_Integration/S2S_Hooks.php',
'class' => 'S2S_Hooks',
'function' => 'afterDelete',
),

To download changes from other builds, set up a job in the planner
"Start synchronization with other SugarCRM builds."
Add to config.php the customization of the connection to the external base, for example:
'integration_instances' => array(
'personal_cabinet' => array(
'type' => 'sugar2sugar',
'dbconfig' => array (
'db_host_name' => ...
...
),
'dbconfigoption' ... .../not necessarily
'portion_limit' => 1000,
'modules' => array(
'Cases',
...
),
),
),
Set up $sugar'config'min_cron_interval'min_cron_interval' and $sugar'config'min_retry_interval'.
For these modules, create a "custom/'modules/<module>/s2s_integration.php file
Custom_.<module>_S2S_Integration.
