# CiscoSecureX-TheHive
## Short Description:
### Cisco SecureX Action Orchestrator Workflows - Casebook - TheHive sync
This Workflow creates a Case in [Cisco SecureX Casebook](https://securex.eu.security.cisco.com/help/casebook-app) and an associated [TheHive Case](https://github.com/TheHive-Project/TheHiveDocs), where all Observables are synced!

> **NOTE:**
> Please be aware of, that there are different regions available for SecureX:
> * [Cisco SecureX **US** region](https://securex.us.security.cisco.com/help/casebook-app)
> * [Cisco SecureX **EU** region](https://securex.eu.security.cisco.com/help/casebook-app)
> * [Cisco SecureX **Asian** region](https://securex.apjc.security.cisco.com/help/casebook-app)


![Automated_IR_with_SecureX___TheHive](/IMAGES/Automated_IR_with_SecureX___TheHive.jpg)

The goal is to handover Observables from SecureX to TheHive via the built-in orchestrator (SecureX Orchestration (SXO)) Workflows.

**Features:**
* faster Incident Respond and handover to the SOC Team
* easy exchange Observables from Cisco Secure platform into TheHive SIRP
* automatic Observable enrichment into TheHive via Casebook Browser PlugIn
  * no more manually Copy & Paste action
  * no more typos by adding Observables by typing 
  * automated start of Cortex Anaylzer by just adding the observables
  * completely independent, only a website is needed to extract the observables

## Create both Cases and map it via a Global Variable Table inside SXO
![SecureX orchestration](/IMAGES/SecureX_AO___Case_creation.jpg)
  
> AO Workflow: ". . . create Casebook and sync it with TheHive 🐝"
![Case Creation GIF](/IMAGES/Case_Creation.gif)


### Sync Obseravables from SecureX Casebook to TheHive (manual task via SXO Response Action in Threat Response)
*add slide about the sync*

> SXO Workflow: "Parse Casebooks Observables and add missing to TheHive 🧩"
![Casebook_TheHive_manually_sync](/IMAGES/Casebook_TheHive_manually_sync.gif)


## Integration of Casebook Browser PlugIn to add Observables into TheHive Case (via a Cisco Casebook Case)
*add slide about Casebook Integration*

> SXO Workflow: not needed - scheduled Workflow 

#### Find observable(s) in page via Casebook  browser plugin (for [Chrome](https://chrome.google.com/webstore/detail/cisco-threat-response-cas/himjbijchjdfcpnihaajckmjlignpkmh) and [Firefox](https://addons.mozilla.org/en-US/firefox/addon/cisco-threat-response-casebook/))
![Casebook_Find_observable_in_page GIF](/IMAGES/Casebook_Find_observable_in_page.gif)

#### TheHive gets the observable(s) and start the appropriate Analyzers
![TheHive_Added_observables_in_case_analyzer_starts GIF](/IMAGES/TheHive_Added_observables_in_case_analyzer_starts.gif)

# Installation
## Detailed installation instructions can be found [HERE](https://github.com/P0nt05/dragonfly/blob/main/INSTALL.md)
