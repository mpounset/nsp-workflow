 
Nokia NSP Workflow Manager Blueprints
Workflow Manager - nodeIntoMaint
Description
Version
WFM nodeIntoMaint- version 1.1.1
Support level
Unsupported, use at your own risk!
History
Version	Author	Date	Comments
1.1.1	MP	2019-04-15	first version
			
			
Prerequisites
Nokia NSP with Workflow Manager
Tested with
•	Nokia NSP 19.3
Installation
Download the workflow and then use the Workflow Manager workflow Import functionality to import the workflow into your WFM instance.
Usage
The workflow has been developed to automate placing the all links sourced on or leaving a designated node into MAINTENANCE mode and then, depending on input, will either re-signal all LSPs affected or tag them as affected by MAINT mode for manual re-signalling.
The same workflow can be used to restore the links back into ‘UP’ state and restore the LSPs affected when links were placed into MAINTENANCE mode

Inputs:
token_auth: Is the base64 encoded string for the NSP username:password
rest_gateway_host: NSP Rest Gateway IP
targetNode: System IP of the target device
status: One of either ‘MAINTENANCE’ or ‘UP’. 
mode: One of either ‘auto’ or ‘manual’

Option: Status = ‘MAINTENANCE’ and mode = ‘auto’
When ‘auto’ is selected the workflow will identify all IP links that are either a source or destination point for the targetNode. Once discovered the flow will set the admin state of the links to be in MAINT mode.
The flow will ten determine all LSPs that ride on the discovered links and re-signal them so that, where possible, they will be diverted off the maintenance mode links (where no alternative is possible i.e. LSP sourced on the targetNode, no movement of the LSP will be observed

Option: Status = ‘MAINTENANCE’ and mode = ‘manual’
When ‘manual is selected the workflow will identify all IP links that are either a source or destination point for the targetNode. Once discovered the flow will set the admin state of the links to be in MAINT mode.
LSPs will be tagged as affected by maintenance mode but no automatic re-signalling will take place 

Option: Status = ‘UP and mode = ‘auto’
When status is set to ‘UP’ the workflow will identify all IP links that are either a source or destination point for the targetNode. Once discovered the flow will set the admin state of the links to be in UP mode.
LSPs that were affected by the links being placed into MAINT mode will revert back to optimum path
License
This project is licensed under the BSD-3 Clause License. See LICENSE.md file for details.
