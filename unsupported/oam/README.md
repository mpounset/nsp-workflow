![NOKIA](https://raw.githubusercontent.com/nokia/nsp-workflow/master/logo.png)
# Nokia NSP Workflow Manager Sample Workflow
## Y1731_TEST

### Description
This workflow will initiate a Y_1731 test against required service, where service is identified by service name only.

### Version
oam_1731_Test - version 1.0

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
    "serviceName": The displayed name of the required L2 Epipe service,
    "nmfp_host": The IP address of the NFM-P server in format  "d.e.f.g"

```

Additionally, the workflow may be initiated via the workflow management REST API

```
POST /wfm/api/v1/execution HTTP/1.1

{
 "input": {
     "token_auth": "xxxx",
     "rest_gateway_host": "a.b.c.d",
     "nfmp_host": "d.e.f.g",
     "serviceName": "$serviceName"

                },
                ##optional "notifyKafka": true,
                "workflow_id": "xxxx-xxxxx-xxxxx"

}
```

### License
This project is licensed under the BSD-3 Clause License. See
[LICENSE.md](https://raw.githubusercontent.com/nokia/nsp-workflow/master/LICENSE.md) file for details.
