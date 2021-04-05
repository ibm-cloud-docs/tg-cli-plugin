---

copyright:
  years: 2020, 2021
lastupdated: "2021-03-15"

keywords: command line interface, commands, CLI

subcollection: transit-gateway
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Transit Gateway CLI reference
{: #transit-gateway-cli}

The {{site.data.keyword.cloud}} Transit Gateway command-line interface (CLI) provides an additional interface into the Transit Gateway service. You can use the CLI to create and manage gateways and connections and list available locations for gateways.   
{: shortdesc}

## Before you begin
{: #cli-ref-prereqs}

Follow these instructions to use the Transit Gateway Command Line Interface, which is implemented as an {{site.data.keyword.cloud_notm}} CLI plug-in.

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli#install-ibmcloud-cli){: external}.
1. Install the `tg-cli/tg` CLI plug-in to the {{site.data.keyword.cloud_notm}} CLI.

   To install:

   ```
   ibmcloud plugin install tg
   ```
   {: pre}
   
**Note**: If you are going to use the CLI with a Virtual Private Endpoint (VPE), you must set the following variable:

```bash
export IBMCLOUD_TG_API_ENDPOINT=private.transit.cloud.ibm.com
```
For more information, see [Integrating with Virtual Private Endpoint for VPC](/docs/transit-gateway?topic=transit-gateway-vpe-for-ibm-cloud-transit-gateway).


## ibmcloud plugin show tg
{: #show-plugin-info}

Show Transit Gateway CLI plug-in information.

```
ibmcloud plugin show tg
```
{: pre}

---

## ibmcloud tg --help
{: #command-help}

Get help on Transit Gateway commands.

```
ibmcloud tg -h|--help
```

---

## Locations

This section provides information about CLI commands for location functionality.

### ibmcloud tg locations
{: #list-locations}

Use this command to list possible locations to create a gateway.

```
ibmcloud tg locations|locs [--output json] [-h, --help]
```

#### Command options
{: #list-locations-options}

- **--output json**: Optional: Specify if you want the output displayed in JSON format.

- **--help | -h**: Optional: Get help on this command.

---

### ibmcloud tg location  
{: #location-detail}

Retrieves specific information for this location.

```
ibmcloud tg location|loc NAME [--output json] [-h, --help]
```

#### Command options
{: #location-detail-options}

- **NAME**: Name of the location you want details for.

- **--output json**: Optional: Specify if you want the output displayed in JSON format.

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #location-detail-examples}

Request details for location `us-south`.

```
ibmcloud tg location us-south
```
{: pre}
---

## Gateways

This section provides information about CLI commands for gateway functionality.


### ibmcloud tg gateways
{: #list-gateways}

List transit gateways.

```
ibmcloud tg gateways|gws [--output json] [-h, --help]
```

#### Command options
{: #list-gateways-options}

- **--output json**: Optional: Specify if you want the output displayed in JSON format.

- **--help | -h**: Optional: Get help on this command.

Other commands will require a gateway ID, save the ID as an environment variable so you can use it later, for example:

```
gateway="bdf8fa2b-c518-9999-9028-f3c9ece86159"
```

---

### ibmcloud tg gateway
{: #gateway-details}

Retrieve details about a specific gateway.

```
ibmcloud tg gateway|gw GATEWAY_ID [--output json] [-h, --help]
```

#### Command options
{: #gateway-details-options}

- **GATEWAY_ID**: ID of the gateway you want details for.

- **--output json**: Optional: Specify if you want the output displayed in JSON format.

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #gateway-details-examples}

Request details for gateway.

```
ibmcloud tg gw $gateway
```
{: pre}

---

### ibmcloud tg gateway-create
{: #gateway-create}

Create a transit gateway.

```
ibmcloud tg gateway-create|gwc --name NAME --location LOCATION [--routing ROUTING] [--resource-group-id RES_GROUP_ID] [--output json] [-h, --help]
```

#### Command options
{: #gateway-create-options}

- **--name**: Name for the new gateway.

- **--location**: Location of the gateway (see possible values by using : `ibmcloud tg locations`)

- **--routing**: Gateway routing of resources (global | local). Select 'global' to connect resources across regions. Default value is 'local'.

- **--resource-group-id**: Optional: Gateway resource group ID. Uses default resource group, if not specified.

- **--output json**: Optional: Specify if you want the output displayed in JSON format.  

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #gateway-create-examples}

Create gateway named 'myGateway' in `us-south` with `local` routing and using default resource group.

```
ibmcloud tg gwc --name myGateway --location us-south
```
{: pre}

---

### ibmcloud tg gateway-update
{: #gateway-update}

Update properties on an existing gateway.

```
ibmcloud tg gateway-update|gwu GATEWAY_ID [--name NAME] [--routing ROUTING] [--output json] [-h, --help]
```

#### Command options
{: #gateway-update-options}

- **GATEWAY_ID**: ID of the gateway you want to update.

- **--name**: Optional: New name of the gateway.

- **--routing**: Optional: Gateway routing of resources (global | local). Select global to connect resources across regions. Changing routing from global to local requires all existing connections to be local.

- **--output json**: Optional: Specify if you want the output displayed in JSON format.  

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #gateway-update-examples}

Update gateway with a routing value of `global`.

```
ibmcloud tg gwu $gateway --routing global
```
{: pre}

---

### ibmcloud tg gateway-delete
{: #gateway-delete}

Delete an existing gateway.

```
ibmcloud tg gateway-delete|gwd GATEWAY_ID [-f, --force] [-h, --help]
```


#### Command options
{: #gateway-delete-options}

- **GATEWAY_ID**: ID of the gateway you want to delete.

- **--force | -f**: Optional: Force the delete without confirmation.

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #gateway-delete-examples}

Delete gateway with no confirmation.

```
ibmcloud tg gwd $gateway -f
```
{: pre}

---

## Connections

This section provides information about CLI commands for connections functionality.


### ibmcloud tg connections
{: #list-connections}

List connections on the given transit gateway.

```
ibmcloud tg connections|cs GATEWAY_ID [--output json] [-h, --help]
```


#### Command options
{: #list-connections-options}

- **GATEWAY_ID**: ID of the gateway you want connections for.

- **--output json**: Optional: Specify if you want the output displayed in JSON format.

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #list-connections-examples}

List the connections on the gateway.

```
ibmcloud tg cs $gateway
```
{: pre}

Other commands will require a connection ID, save the ID as an environment variable so you can use it later, for example:

```
connection="4892849f-368e-9999-bb58-8888fb21e513"
```

---

### ibmcloud tg connection
{: #connection-details}

Retrieve details about a specific connection.

```
ibmcloud tg connection|c GATEWAY_ID CONNECTION_ID [--output json] [-h, --help]
```


#### Command options
{: #connection-details-options}

- **GATEWAY_ID**: ID of the gateway the connection is on.

- **CONNECTION_ID**: ID of the connection you want details for.

- **--output json**: Optional: Specify if you want the output displayed in JSON format.

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #connection-details-examples}

Request details for a specific connection ID.

```
ibmcloud tg c $gateway $connection
```
{: pre}

---

### ibmcloud tg connection-create
{: #connection-create}

Create a connection on the given transit gateway.

```
ibmcloud tg connection-create|cc GATEWAY_ID --name NAME --network-type [vpc | classic] --network-id NETWORK_ID --network-account-id NETWORK-ACCOUNT-ID [--output json] [-h, --help]
```

#### Command options
{: #connection-create-options}

- **GATEWAY_ID**: ID of the gateway that the new connection will be on.

- **--name**: Name for the new connection.

- **--network-type**: Network type of the connection. Values are `vpc` or `classic`.

- **--network-id**: ID of the network connection. For classic, do not set a value. For VPC, use the VPC's CRN. To find the CRN of a VPC:

   ```
   ibmcloud is vpc VPC_ID --json
   ```

- **--network-account-id**: ID of the IBM Cloud account to use for creating a classic connection. Only used with 'classic' type, when the account of connection is different than the gateway's account.

- **--output json**: Optional: Specify if you want the output to display in JSON format.

- **--help | -h**: Optional: Get help on this command.

#### Examples
{: #connection-create-examples}

Create VPC connection named `vpc-connection` using `vpcCRN="crn:v1:bluemix:public:is:us-south:a/3aa0a9999a1a46258064d84f7f447920::vpc:r134-f87014d5-87d2-46d1-9999-24683082f6bc"`

```
ibmcloud tg cc $gateway --name vpc-connection --network-id $vpcCRN --network-type vpc
```
{: pre}

Create Classic connection named `classic-conn`.

```
ibmcloud tg cc $gateway --name classic-conn --network-type classic
```
{: pre}

---

### ibmcloud tg connection-update
{: #connection-update}

Update properties on an existing connection.

```
ibmcloud tg connection-update|cu GATEWAY_ID CONNECTION_ID --name NAME [--output json] [-h, --help]
```


#### Command options
{: #connection-update-options}

- **GATEWAY_ID**: ID of the gateway the connection being updated is on.

- **CONNECTION_ID**: ID of the connection to update.

- **--name**: New name of the connection.

- **--output json**: Optional: Specify if you want the output displayed in JSON format.

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #connection-update-examples}

Update name of connection to `MyConn2`.

```
ibmcloud tg cu $gateway $connection --name MyConn2
```
{: pre}

---

### ibmcloud tg connection-approve
{: #connection-approve}

Approve a connection from another account as the network owner.

```
ibmcloud tg connection-approve|ca GATEWAY_ID CONNECTION_ID [-h, --help]
```


#### Command options
{: #connection-approve-options}

- **GATEWAY_ID**: ID of the gateway the connection is on.

- **CONNECTION_ID**: ID of the connection you are approving.

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #connection-approve-examples}

Approve the connection request.

```
ibmcloud tg ca $gateway $connection
```
{: pre}

---

### ibmcloud tg connection-reject
{: #connection-reject}

Reject a connection from another account as the network owner.

```
ibmcloud tg connection-reject|cr GATEWAY_ID CONNECTION_ID [-h, --help]
```


#### Command options
{: #connection-reject-options}

- **GATEWAY_ID**: ID of the gateway the connection is on.

- **CONNECTION_ID**: ID of the connection you are rejecting.

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #connection-reject-examples}

Reject the connection request.

```
ibmcloud tg cr $gateway $connection
```
{: pre}

---


### ibmcloud tg connection-delete
{: #connection-delete}

Delete an existing connection.

```
ibmcloud tg connection-delete|cd GATEWAY_ID CONNECTION_ID [-f, --force] [-h, --help]
```


#### Command options
{: #connection-delete-options}

- **GATEWAY_ID**: ID of the gateway of the connection being deleted.

- **CONNECTION_ID**: ID of the connection being deleted.

- **--force | -f**: Optional: Force the delete without confirmation.

- **--help | -h**: Optional: Get help on this command.

#### Example
{: #connection-delete-examples}

Delete connection without confirmation.

```
ibmcloud tg cd $gateway $connection -f
```
{: pre}
