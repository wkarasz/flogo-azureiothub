---
title: AWS IoT
weight: 4605
---

# AWS IoT
This activity allows you to update a device shadow on AWS.

## Installation
### Flogo Web
This activity comes out of the box with the Flogo Web UI
### Flogo CLI
```bash
flogo add activity github.com/TIBCOSoftware/flogo-contrib/activity/awsiot
```

## Schema
Inputs and Outputs:

```json
{
  "input":[
    {
      "name": "thingName",
      "type": "string",
      "required": true
    },
    {
      "name": "awsEndpoint",
      "type": "string",
      "required": true
    },
    {
      "name": "desired",
      "type": "params"
    },
    {
      "name": "reported",
      "type": "params"
    }
  ]
}
```

## Settings
| Setting     | Required | Description |
|:------------|:---------|:------------|
| thingName   | True     | The name of the "thing" in Aws IoT |         
| awsEndpoint | True     | The Aws Iot Endpoint for the account  |
| desired     | False    | The desired state to update |
| reported    | False    | The reported state to update |

## Configuration
### Certificate Installation
The activity looks for the AWS device certificates in a "things" directory relative to where the engine was started.  Download the [root CA certificate](https://www.symantec.com/content/en/us/enterprise/verisign/roots/VeriSign-Class%203-Public-Primary-Certification-Authority-G5.pem) file and save it as "things/root-CA.pem.crt". Now place the cert and private key generated by Aws IoT for your thing under "things/[thingName]" as device.pem.crt and device.pem.key respectively.

### Flow Configuration
Configure a task in flow to update the device shadow of 'raspberry-pi' with a reported temp of "50".

```json
{
  "id": "awsiot_1",
  "name": "Update AWS Device Shadow",
  "description": "Simple AWS IoT",
  "activity": {
    "ref": "github.com/TIBCOSoftware/flogo-contrib/activity/awsiot",
    "input": {
      "thingName": "raspberry-pi",
      "awsEndpoint": "A3CWMRYOWXFD7I.iot.us-west-2.amazonaws.com",
      "reported": { "temp":"50" }
    }
  }
}
```