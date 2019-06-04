---
title: Working with Inputs Advanced
author: Grant Orchard
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - YAML
  - Inputs
  - Advanced
date: 2019-05-15
permalink: /inputsadvanced/
description: 'AWorking with Inputs Advanced'
---

### Input Schema

**const** - (Optional) Used with oneOf as the real value associated with the user friendly title.
**default** - (Optional) Sets a default value for the parameter. If used with enum, must be a valid value contained in the array of options.
**description** - (Optional) A tooltip that will be rendered on the form at time of deployment. Should be used to provide additional context for the input to the requesting user.
**encrypted** - (Optional) Hides the user keystrokes behind asterisks in the form. Only supported with the string type. Not compatible with enum.
**enum** - (Optional) Used to provide a pre-defined selection of options. Supports string, integer, and number as stand-alone types, but not within an array or object. Allows the use of dual-list and multi-select in Service Broker custom forms.
**format** - (Optional) Sets the expected format for the input. Currently (25/04/19) supports 'date-time'. Allows the use of the date picker in Service Broker custom forms.
**items** - (Optional) Used to declare items within an array. Can contain strings, numbers, integers, booleans, or objects.
**maxItems** - (Optional) Used to constrain the maximum number of selectable items within an array.
**maxLength** - (Optional) Used to constrain the maximum length of the field for string, integer, and number types. Setting this value to 256 or more renders the input field into a text area, though not when used in concert with encrypted: true.
**maximum** - (Optional) Used with integer and number types to constrain the permissable maximum value.
**minItems** - (Optional) Used to constrain the minimum number of selectable items within an array.
**minLength** - (Optional) Used to constrain the minimum length of the field for  string, integer, and number types.
**minimum** - (Optional) Used with integer and number types to constrain the permissable minimum value.
**oneOf** - (Optional) Allows the use of a friendly name (title) for a less friendly value (const). The title will be rendered in the form, while const will be the value used. Valid for use with strings, integers, and numbers. If setting a default value, you need to set the const value, and not the title.
**pattern** - (Optional) Sets a regex pattern to be used for field validation. Only compatible with strings, numbers, and integers.
**properties** - (Optional) Used to declare the key:value properties block for objects.
**readOnly** - (Optional) Used to provide a label only.
**title** - (Optional) Can be used to provide a friendly name that is rendered on the form at time of deployment for an input or a oneof input value.
**type** - (Required) One of string, number, integer, boolean, or object.
**writeOnly** - (Optional) Hides the user keystrokes behind asterisks in the form. Not compatible with enum. Renders as a password field in Service Broker custom forms.



### Example Usage

#### String with enumeration
```yaml
  image:
    type: string
    title: Operating System
    description: The operating system version to use.
    enum:
      - ubuntu 16.04
      - ubuntu 18.04
    default: ubuntu 16.04
```

```yaml
  shell:
    type: string
    title: Default shell
    Description: The default shell that will be configured for the created user.
    enum:
      - /bin/bash
      - /bin/sh
```

#### Integer with minimum and maximum
```yaml
  count:
    type: integer
    title: Machine Count
    description: The number of machines that you want to deploy.
    maximum: 5
    minimum: 1
    default: 1
```

#### Array of objects
```yaml
  tags:
    type: array
    title: Tags
    description: Tags that you want applied to the machines.
    items:
      type: object
      properties:
        key:
          type: string
          title: Key
        value:
          type: string
          title: Value
```

#### String with friendly names
```yaml
  platform:
    type: string
    oneOf:
      - title: AWS
        const: platform:aws
      - title: Azure
        const: platform:azure
      - title: vSphere
        const: platform:vsphere
    default: platform:aws
```

#### String with pattern validation
```yaml
  username:
    type: string
    title: Username
    description: The name for the user that will be created when the machine is provisioned.
    pattern: ^[a-zA-Z]+$
```

#### String as password
```yaml
  password:
    type: string
    title: Password
    description: The initial password that will be required to logon to the machine. Will be set to reset on first login.
    writeOnly: true
```

#### String as text area
```yaml
  ssh_public_key:
    type: string
    title: SSH public key
    maxLength: 256
```

#### Boolean
```yaml
  public_ip:
    type: boolean
    title: Assign public IP address
    description: Choose whether your machine should be internet facing.
    default: false
```

#### Full blueprint

{% gist cc7759f662d068c49374c15f6b8bee62 %}

### Updating a Deployment with Inputs
While we often look at inputs during our initial request, there is a another very inportant function that inputs provide - allowing you to modify a Deployment as a Day 2 action. This is not to be confused with modifying the blueprint itself, which can also be used as a mechanism for changing a deployment.

In the image below, you will note that the screen title is "Update", as I have used the Day 2 update action from the Deployments screen. The input values from my request are all preserved, all render on screen (although you can only see a few on screen in my screenshot), and can all be modified to change your deployment. You could add tags, which would update the deployment, or you could change the operating system which would trigger a re-deploy of the machine in question.

{% lightbox /assets/images/cas/cloudassembly/blueprint-inputs/update.png --title="Update a Deployment Using Inputs" --alt="Update Cloud Assembly Deployment Using Inputs" --data="blueprint-inputs" --img-style="max-width:80%" %}

### Blueprint Inputs via API
Finally (or should that have been firstly?) we have the API.
You can query the URI below to get the input schema for the blueprint you are intending to request.

GET https://api.mgmt.cloud.vmware.com/blueprint/api/blueprints/{blueprint_id}/inputs-schema

```json
{
    "type": "object",
    "required": [
        "tags",
        "platform",
        "username",
        "ssh_public_key",
        "password"
    ],
    "properties": {
        "image": {
            "type": "string",
            "title": "Operating System",
            "default": "ubuntu 16.04",
            "enum": [
                "ubuntu 16.04",
                "ubuntu 18.04"
            ]
        },
        "count": {
            "type": "integer",
            "minimum": 2,
            "maximum": 5,
            "title": "Machine Count",
            "default": 2
        },
        "size": {
            "type": "string",
            "title": "Machine size",
            "description": "Resource requirements for your workload.",
            "default": "small",
            "enum": [
                "small",
                "medium"
            ]
        },
        "tags": {
            "type": "array",
            "items": {
                "type": "object",
                "encrypted": false,
                "computed": false,
                "recreateOnUpdate": false,
                "ignoreOnUpdate": false,
                "properties": {
                    "key": {
                        "type": "string",
                        "encrypted": false,
                        "computed": false,
                        "recreateOnUpdate": false,
                        "ignoreOnUpdate": false,
                        "title": "Key"
                    },
                    "value": {
                        "type": "string",
                        "encrypted": false,
                        "computed": false,
                        "recreateOnUpdate": false,
                        "ignoreOnUpdate": false,
                        "title": "Value"
                    }
                }
            },
            "title": "Tags",
            "description": "Freeform tags that you would like attached to the provisioned resources."
        },
        "platform": {
            "type": "string",
            "oneOf": [
                {
                    "encrypted": false,
                    "computed": false,
                    "recreateOnUpdate": false,
                    "ignoreOnUpdate": false,
                    "title": "AWS",
                    "const": "platform:aws"
                },
                {
                    "encrypted": false,
                    "computed": false,
                    "recreateOnUpdate": false,
                    "ignoreOnUpdate": false,
                    "title": "Azure",
                    "const": "platform:azure"
                },
                {
                    "encrypted": false,
                    "computed": false,
                    "recreateOnUpdate": false,
                    "ignoreOnUpdate": false,
                    "title": "vSphere",
                    "const": "platform:vsphere"
                }
            ],
            "title": "Deploy to"
        },
        "username": {
            "type": "string",
            "pattern": "^[a-zA-Z0-9]+$",
            "title": "User Account",
            "description": "Name of the user account to be created. Can only contain letters and numbers."
        },
        "shell": {
            "type": "string",
            "title": "Default Shell",
            "default": "/bin/bash",
            "enum": [
                "/bin/bash",
                "/bin/sh"
            ]
        },
        "ssh_public_key": {
            "type": "string",
            "title": "SSH public key"
        },
        "password": {
            "type": "string",
            "writeOnly": true,
            "title": "Password",
            "description": "The initial password that will be required to logon to the machine. Will be set to reset on first login."
        },
        "public_ip": {
            "type": "boolean",
            "title": "Assign public IP address",
            "description": "Choose whether your machine should be internet facing.",
            "default": false
        }
    }
}
```

The request itself is a POST to https://api.mgmt.cloud.vmware.com/blueprint/api/blueprints-requests/ and the inputs are included in the payload as shown below.


```json
{
  "blueprintId" : "73b91a7e-ddf7-4393-a857-08b6870fa474",
  "deploymentName" : "working with inputs via api",
  "description" : "",
  "plan" : false,
  "content" : null,
  "inputs" : {
    "image" : "ubuntu 16.04",
    "count" : 2,
    "size" : "small",
    "tags" : [
      {
        "key" : "blogging",
        "value" : "finally"
      }
    ],
    "platform" : "platform:aws",
    "username" : "grant",
    "shell" : "/bin/bash",
    "ssh_public_key" : "not really your business",
    "password" : "VMware!",
    "public_ip" : false
  },
  "simulate" : false
}
```
Happy blueprinting!
