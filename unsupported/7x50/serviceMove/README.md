![NOKIA](https://raw.githubusercontent.com/nokia/nsp-workflow/master/logo.png)
# Nokia NSP Workflow Manager Sample Workflow
## L2 service move to LAG

### Description
This workflow will identify existing L2 services on phyiscal port and move them to LAG.
The workflow will create a LAG interface, with declared ID if it doesn't already exist.
The workflow will add declared ports to the new, or existing LAG.
After service move the workflow will initiate an ETH-CFM test on one of the moved services to confirm connectivity.

### Version
serviceMoveToLag - version 1.0

### Support level
Unsupported, use at your own risk!

### History
|Version|Author|Date      |Comments     |
|-------|------|----------|-------------|
|   1.0 |  MP  |2019-01-29|first version|

### Prerequisites
Nokia NSP with Workflow Manager and NFM-P

### Tested with
* Nokia NSP 18.12
* Nokia 7750SR SR OS 16.0.R5 (CLASSIC)

### Installation
Download the workflow and then use the Workflow Manager workflow Import functionality to import the workflow into your WFM instance.

### Usage
The workflow can be initiated either via the WFM GUI or via the workflow management REST API
The following parameters must be supplied

```
    "token_auth": The REST API Bearer as string. This is base64 encoding of 'username:password',
    "rest_gateway_host": The IP address of the NSP REST gateway in format  "a.b.c.d",
	"nmfp_host": The IP address of the NFM-P server in format  "d.e.f.g",
    "lagId": Required LAD-ID as integer,
	"lagDescr" : Required LAD description string,
	"servicePort" : The existing port where services reside, in format network:a.b.c.d:shelf-x:cardSlot-x:card:daughterCardSlot-x:daughterCard:port-x
	"targetNode" : System IP of node where lag and ports reside,
	"newPorts" : List of port to be added to LAG in format:
		[
        {
            "member": "x/y/z",
            "port": "network:a.b.c.d:shelf-1:cardSlot-x:card:daughterCardSlot-y:daughterCard:port-z"
        },
        {
            "member": "o/p/q",
            "port": "network:a.b.c.d:shelf-1:cardSlot-o:card:daughterCardSlot-p:daughterCard:port-q"
        },
        {
            "member": "e/f/g",
            "port": "network:a.b.c.d:shelf-1:cardSlot-e:card:daughterCardSlot-f:daughterCard:port-g"
        }
        
    ]


```

Additionally, the workflow may be initiated via the workflow management REST API

```
POST /wfm/api/v1/execution HTTP/1.1

{
 "input": {
     "token_auth": "base64encode",
     "rest_gateway_host": "x.x.x.x,
     "lagId": "integer",
     "lagDescr": "move_service_lag",
     "nfmp_host": "y.y.y.y",
     "servicePort": "network:a.b.c.d:shelf-x:cardSlot-x:card:daughterCardSlot-x:daughterCard:port-x",
     "targetNode": "a.b.c.d",
     "newPorts": [
        {
            "member": "x/y/z",
            "port": "network:a.b.c.d:shelf-1:cardSlot-x:card:daughterCardSlot-y:daughterCard:port-z"
        },
        {
            "member": "o/p/q",
            "port": "network:a.b.c.d:shelf-1:cardSlot-o:card:daughterCardSlot-p:daughterCard:port-q"
        },
        {
            "member": "e/f/g",
            "port": "network:a.b.c.d:shelf-1:cardSlot-e:card:daughterCardSlot-f:daughterCard:port-g"
        }
        
    ]

                },

                "workflow_id": "xxx-xxx-xxx"
}
```

### License
This project is licensed under the BSD-3 Clause License. See
[LICENSE.md](https://raw.githubusercontent.com/nokia/nsp-workflow/master/LICENSE.md) file for details.
