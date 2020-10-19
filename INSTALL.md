# How to install and setup the workflows in SecureX Orchestration (SXO)

1. Logon to SecureX via: https://sign-on.security.cisco.com/. 
> **NOTE:** If you don't have a SecureX Account, please follow the [Quick Start Guide](https://www.cisco.com/c/en/us/td/docs/security/secure-sign-on/sso-quick-start-guide/sso-qsg-welcome.html).
2. Go to Menu "Orchestration" 
  ![SecureX_Menu](/IMAGES/SecureX_Menu.jpg)


## Create New GitHub Repo
Add GitHub Repo to your SXO instance to import the SXO Workflows.

1. Go to Admin in the left-hand menu
  ![git_1_Menu](/IMAGES/git_1_Menu.jpg)
2. Go to Git Repositories and a **New Git Repository** 
  ![git_2_NewRep](/IMAGES/git_2_NewRep.jpg)
3. Use the following **DISPLAY NAME**: **CiscoSecureX-TheHive** and the following details:
  * **DEFAULT ACCOUNT KEYS**: **Git_Credentials**
  * **PROTOCOL** set to **HTTPS**
  * **REST API REPOSITORY**: **api.github.com/repos/P0nt05/CiscoSecureX-TheHive**
  * **BRANCH**: **main**
  * Leave all other fields on default/empty and click **SUBMIT**.
  * ![git_2_RepData](/IMAGES/git_2_RepData.jpg)
  
## Import SXO Workflow from Github
1. Go to Workflows and **IMPORT** the Workflow
    ![wrk_1_NewWorkflow](/IMAGES/wrk_1_NewWorkflow.jpg)
2. Select the created Git Repo from the previous step
  * FILENAME: **CreateCasebookAnySyncItWithTheHive**
  * GIT VERSION: **latest**
  * ![wrk_2_CreateCasebook](/IMAGES/wrk_2_CreateCasebook.jpg)
3. Import a 2nd workflow by repeating the process:
  * Select the created Git Repo from the previous step
  * FILENAME: **ParseCasebookObservablesAndAddMissingToTheHive**
  * GIT VERSION: **latest**
  * ![wrk_3_ParseCasebook](/IMAGES/wrk_3_ParseCasebook.jpg)

## Setting up the Global Variables
In order to store the mapping between SecuerX Casebook and TheHive Case via the unique ID, we have to create/check a table definition and then a table, which is referenced inside the workflows. 

### Variable Type
First we need to check the created variables (and type) to store the case ID's to keep them in sync.

1. In the left-hand menu, go to **Variables > Variables Types** and find **SecureX-TheHive__CaseID__syncTable** like below:
  *  ![var_1_NewType](/IMAGES/var_1_NewType.jpg)
2. Check the **DISPLAY NAME**, **FIELD NAME** and **FIELD TITLE**
> Variable type provide a way to define a new user defined variable type that is not represented by any default variable type
  *  ![var_2_Columns](/IMAGES/var_2_Columns.jpg)

### Global Variable
Next step is to check the global instance from our custom table variable type. Also, we will check the global variable for our TheHive token.

1. Find the global variable for the ID mapping - **SecureX-TheHive__CaseID__syncTable**
    * ![var_3_GlobalVar](/IMAGES/var_3_GlobalVar.jpg)
2. Check the Data Type: **SecureX-TheHive__CaseID__syncTable**
    * Displayname: **SecureX-TheHive__CaseID__syncTable**
    * ![var_5_NewVar](/IMAGES/var_5_NewVar.jpg)
    * There is a bogus line to instantiate the table, they could be removed later (*the issue is already addressed to integrate this into the workflow*)
3. Now add the API key into the global variable for the Bearer Token in order to authenticate to your TheHive instance. 
    * Click on **TheHive___BearerToken** and add your TheHive Bearer Token in the **VALUE** field and click **SUBMIT**:
    * ![var_4_TheHiveBearer](/IMAGES/var_4_TheHiveBearer.jpg)

## Setting up the Target for TheHive
TheHive API needs to be reachable from the internet. For this we will set up a so-called HTTP target.

> **NOTE:** A SecureX on-prem connector is in development and will be released in the next phase
1. In the left-hand menu, go to **Targets** and find **TheHive** target:
  * ![target_1_NewTarget](/IMAGES/target_1_NewTarget.jpg)
2. Check the details for your target:
  * **Do not change the values for**:
    * DISPLAY NAME: TheHive
    * Account Keys - NO ACCOUNT KEYS set to True
  * Please **change and modify** the settings to reach your **TheHive** instance
  * HTTP
    * **PROTOCOL** set to **HTTPS**
    * **HOST/IPADDRESS**: enter your FQDN to TheHive API (**make sure it is reachable**)
  * Leave all other fields on default/empty and click **SUBMIT**. 
  * ![target_2_TargetValues](/IMAGES/target_2_TargetValues.jpg)

## Optional: If you want to run the sync periodically
There is an option to schedule the sync between the Observables periodically.
For this we have to create a particular Generic Schedule and add it as a trigger action to the workflow.
1. Go to Schedules in the left-hand menu and create a **New Schedule**
    ![schdl_1_New](/IMAGES/schdl_1_New.jpg)
2. Add the details to the schedule (when to start, how often executed, ...)
    ![schdl_2_New_Values](/IMAGES/schdl_2_New_Values.jpg)
3. Next we need to assign the schedule to the workflow and add the trigger
  * Go to Workflows in the left-hand menu and click on **PARSE CASEBOOKS OBSERVABLES AND ADD MISSING TO THEHIVE 🧩**
    ![schdl_3_Wrkflw](/IMAGES/schdl_3_Wrkflw.jpg)
  * Scroll down in the Properties to the Section **Triggers** and add a new
      ![schdl_4_AddTrigger](/IMAGES/schdl_4_AddTrigger.jpg)
  * Add New Trigger
    * Name: *can be defined by your own*
    * Type: **Schedule**
    * Schedule: **The one you created in the previous step**
      ![schdl_5_Trigger](/IMAGES/schdl_5_Trigger.jpg)

# Have fun
You can see in the README.md how to use the workflows in Cisco SecureX threat response. Please find more details on this [link](https://www.cisco.com/c/en/us/products/security/threat-response/demos.html).
