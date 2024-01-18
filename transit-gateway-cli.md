---

copyright:
  years: 2020, 2024
lastupdated: "2024-01-10"

keywords: command line interface, commands, CLI

subcollection: transit-gateway-cli

---

{{site.data.keyword.attribute-definition-list}}

# Transit Gateway CLI
{: #transit-gateway-cli}

The {{site.data.keyword.cloud}} Transit Gateway command line provides an interface into the Transit Gateway service. You can use the CLI to create and manage gateways and connections and list available locations for gateways.
{: shortdesc}

## Before you begin
{: #cli-ref-prereqs}

Follow these instructions to use the Transit Gateway Command Line Interface, which is implemented as an {{site.data.keyword.cloud_notm}} CLI plug-in.

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli#install-ibmcloud-cli){: external}.
1. Install the `tg-cli/tg` CLI plug-in to the {{site.data.keyword.cloud_notm}} CLI.

   To install:

   ```sh
   ibmcloud plugin install tg
   ```
   {: pre}

If you are going to use the CLI with a Virtual Private Endpoint (VPE), you must set the following variable:

```bash
export IBMCLOUD_TG_API_ENDPOINT=private.transit.cloud.ibm.com
```

## `ibmcloud plugin show tg`
{: #show-plugin-info}

Show Transit Gateway CLI plug-in information.

```sh
ibmcloud plugin show tg
```
{: pre}

---

## `ibmcloud tg --help`
{: #command-help}

Get help on Transit Gateway commands.

```sh
ibmcloud tg -h|--help
```

---

## Locations
{: #locations}

This section provides information about CLI commands for location functions.

### `ibmcloud tg locations`
{: #list-locations}

Use this command to list possible locations to create a gateway.

```sh
ibmcloud tg locations|locs [--output json] [-h, --help]
```

#### Command options
{: #list-locations-options}

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

---

### `ibmcloud tg location`
{: #location-detail}

Retrieves specific information for this location.

```sh
ibmcloud tg location|loc NAME [--output json] [-h, --help]
```

#### Command options
{: #location-detail-options}

`NAME`
:   Name of the location you want details for.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #location-detail-examples}

Request details for location `us-south`.

```sh
ibmcloud tg location us-south
```
{: pre}

---

## Gateways
{: #gateways}

This section provides information about CLI commands for gateway functions.

### `ibmcloud tg gateways`
{: #list-gateways}

List transit gateways.

```sh
ibmcloud tg gateways|gws [--output json] [-h, --help]
```

#### Command options
{: #list-gateways-options}

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

Other commands require a gateway ID. Save the ID as an environment variable so you can use it later, for example:

```text
gateway="bdf8fa2b-c518-9999-9028-f3c9ece86159"
```
{: screen}

---

### `ibmcloud tg gateway`
{: #gateway-details}

Retrieve details about a specific gateway.

```sh
ibmcloud tg gateway|gw GATEWAY_ID [--output json] [-h, --help]
```

#### Command options
{: #gateway-details-options}

`GATEWAY_ID`
:   ID of the gateway you want details for.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #gateway-details-examples}

Request details for gateway.

```sh
ibmcloud tg gw $gateway
```
{: pre}

---

### `ibmcloud tg gateway-create`
{: #gateway-create}

Create a transit gateway.

```sh
ibmcloud tg gateway-create|gwc --name NAME --location LOCATION [--routing ROUTING] [--resource-group-id RES_GROUP_ID] [--output json] [-h, --help]
```

#### Command options
{: #gateway-create-options}

`--name`
:   Name for the new gateway.

`--location`
:   Location of the gateway (see possible values by using `ibmcloud tg locations`)

`--routing`
:   Gateway routing of resources (`global` | `local`). Select `global` to connect resources across regions. The default value is `local`.

`--resource-group-id`
:   Optional: Gateway resource group ID. Uses default resource group, if not specified.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #gateway-create-examples}

Create a gateway that is named `myGateway` in `us-south` with `local` routing and that uses default resource group.

```sh
ibmcloud tg gwc --name myGateway --location us-south
```
{: pre}

---

### `ibmcloud tg gateway-update`
{: #gateway-update}

Update properties on an existing gateway.

```sh
ibmcloud tg gateway-update|gwu GATEWAY_ID [--name NAME] [--routing ROUTING] [--output json] [-h, --help]
```

#### Command options
{: #gateway-update-options}

`GATEWAY_ID`
:   ID of the gateway you want to update.

`--name`
:   Optional: New name of the gateway.

`--routing`
:   Optional: Gateway routing of resources (`global` | `local`). Select global to connect resources across regions. Changing routing from `global` to `local` requires all existing connections to be `local`.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #gateway-update-examples}

Update the gateway with a routing value of `global`.

```sh
ibmcloud tg gwu $gateway --routing global
```
{: pre}

---

### `ibmcloud tg gateway-delete`
{: #gateway-delete}

Delete an existing gateway.

```sh
ibmcloud tg gateway-delete|gwd GATEWAY_ID [-f, --force] [-h, --help]
```


#### Command options
{: #gateway-delete-options}

`GATEWAY_ID`
:   ID of the gateway you want to delete.

`--force | -f`
:   Optional: Force the delete without confirmation.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #gateway-delete-examples}

Delete gateway with no confirmation.

```sh
ibmcloud tg gwd $gateway -f
```
{: pre}

---

## Connections
{: #connections}

This section provides information about CLI commands for connection functions.


### `ibmcloud tg connections`
{: #list-connections}

List connections on the transit gateway.

```sh
ibmcloud tg connections|cs GATEWAY_ID [--output json] [-h, --help]
```


#### Command options
{: #list-connections-options}

`GATEWAY_ID`
:   ID of the gateway you want connections for.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #list-connections-examples}

List the connections on the gateway.

```sh
ibmcloud tg cs $gateway
```
{: pre}

Other commands require a connection ID. Save the ID as an environment variable so you can use it later, for example:

```text
connection="4892849f-368e-9999-bb58-8888fb21e513"
```
{: screen}

---

### `ibmcloud tg connection`
{: #connection-details}

Retrieve details about a specific connection.

```sh
ibmcloud tg connection|c GATEWAY_ID CONNECTION_ID [--output json] [-h, --help]
```


#### Command options
{: #connection-details-options}

`GATEWAY_ID`
:   ID of the gateway the connection is on.

`CONNECTION_ID`
:   ID of the connection you want details for.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #connection-details-examples}

Request details for a specific connection ID.

```sh
ibmcloud tg c $gateway $connection
```
{: pre}

---

### `ibmcloud tg connection-create`
{: #connection-create}

Create a connection on the transit gateway.

```sh
ibmcloud tg connection-create|cc GATEWAY_ID --name NAME --network-type NETWORK_TYPE --network-id NETWORK_ID --network-account-id NETWORK_ACCOUNT_ID [--output json] [-h, --help]
```

#### Command options
{: #connection-create-options}

`GATEWAY_ID`
:   ID of the gateway that the new connection is on.

`--name`
:   Name for the new connection.

`--network-type`
:   Network type of the connection. Values are `classic`, `vpc`, `directlink`, or `power_virtual_server`.

`--network-id`
:   ID of the network connection. For `classic`, do not set a value. Use the CRN for all other network types. For example, to find the CRN of a VPC:

   ```sh
   ibmcloud is vpc VPC_ID --json
   ```

`--network-account-id`
:   ID of the IBM Cloud account to use for creating a classic connection. Only used with `classic` type, when the account of the connection is different than the gateway's account.

`--default-prefix-filter`
:   Optional: Default prefix filter of the connection (`permit` | `deny`).

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #connection-create-example}

Create a VPC connection that is named `vpc-connection` and uses `vpcCRN="crn:v1:bluemix:public:is:us-south:a/3aa0a9999a1a46258064d84f7f447920::vpc:r134-f87014d5-87d2-46d1-9999-24683082f6bc"`

```sh
ibmcloud tg cc $gateway --name vpc-connection --network-id $vpcCRN --network-type vpc
```
{: pre}

Create a Classic connection named `classic-conn`.

```sh
ibmcloud tg cc $gateway --name classic-conn --network-type classic
```
{: pre}

---

### `ibmcloud tg connection-create-gre`
{: #connection-create-gre}

Create a Generic Routing Encapsulation (GRE) tunnel or unbound GRE connection on the transit gateway.

```sh
ibmcloud tg connection-create-gre|ccgre GATEWAY_ID --name NAME --zone ZONE --local-gateway-ip LOCAL_GATEWAY_IP --local-tunnel-ip LOCAL_TUNNEL_IP --remote-gateway-ip REMOTE_GATEWAY_IP --remote-tunnel-ip REMOTE_TUNNEL_IP [--base-connection-id BASE_CONNECTION_ID] [--base-network-type BASE_NETWORK_TYPE] [--network-type NETWORK_TYPE] [--network-account-id NETWORK_ACCOUNT_ID] [--remote-bgp-asn REMOTE_BGP_ASN] [--default-prefix-filter DEFAULT_PREFIX_FILTER] [--output json]
```
{: pre}

#### Command options
{: #connection-create-gre-options}

`GATEWAY_ID`
ID of the gateway where the new connection is bound.

`--name`
:   Name of the new connection.

`--zone`
:   Availability zone for the GRE tunnel. Example: `us-south-1`

`--local-gateway-ip`
:   Local gateway IP address for the GRE tunnel connection.

`--local-tunnel-ip`
:   Local tunnel IP address for the GRE tunnel connection.

`--remote-gateway-ip`
:   Remote gateway IP address for the GRE tunnel connection.

`--remote-tunnel-ip`
:   Remote tunnel IP address for the GRE tunnel connection.

`--base-connection-id`
:    Optional: ID of the classic network connection that is the underlay for the GRE tunnel. This option is for use only with the `gre_tunnel` network type.

`--base-network-type`
:   Network type of the base connection (`classic`). This option is for use only with the `unbound_gre_tunnel` network type.

`--network-type`
:   Optional: Network type of the GRE connection. Values are `gre_tunnel` or `unbound_gre_tunnel`. The default value is `gre_tunnel`.

`--network-account-id`
:   Optional: ID of account to connect to a classic connection. Use only with `classic` type when the account of the connection is different than gateway's account.

`--remote-bgp-asn`
:   Optional: If the remote BGP ASN is not specified, one is generated.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Examples
{: #connection-create-gre-examples}

Create a GRE tunnel connection that is named `gre-connection` and uses classic connection `9037f710-8dfb-4948-a2bd-847c8dde96d3` as the base connection.

```sh
ibmcloud tg connection-create-gre $gateway --name gre-connection --base-connection-id 9037f710-8dfb-9999-a2bd-847c8dde96d3  --zone us-south-2 --local-gateway-ip 192.168.100.1 --local-tunnel-ip 192.168.101.1 --remote-gateway-ip 10.242.63.12 --remote-tunnel-ip 192.168.101.2
```
{: pre}

---

### `ibmcloud tg connection-update`
{: #connection-update}

Update properties on an existing connection.

```sh
ibmcloud tg connection-update|cu GATEWAY_ID CONNECTION_ID --name NAME [--output json] [-h, --help]
```

#### Command options
{: #connection-update-options}

`GATEWAY_ID`
:   ID of the gateway that the connection is being updated is on.

`CONNECTION_ID`
:   ID of the connection to update.

`--name`
:   New name of the connection.

`--default-prefix-filter`
:   Optional: Default prefix filter of the connection (`permit` | `deny`).

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #connection-update-examples}

Update name of connection to `MyConn2`.

```sh
ibmcloud tg cu $gateway $connection --name MyConn2
```
{: pre}

---

### `ibmcloud tg connection-approve`
{: #connection-approve}

Approve a connection from another account as the network owner.

```sh
ibmcloud tg connection-approve|ca GATEWAY_ID CONNECTION_ID [-h, --help]
```


#### Command options
{: #connection-approve-options}

`GATEWAY_ID`
:   ID of the gateway the connection is on.

`CONNECTION_ID`
:   ID of the connection you are approving.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #connection-approve-examples}

Approve the connection request.

```sh
ibmcloud tg ca $gateway $connection
```
{: pre}

---

### `ibmcloud tg connection-reject`
{: #connection-reject}

Reject a connection from another account as the network owner.

```sh
ibmcloud tg connection-reject|cr GATEWAY_ID CONNECTION_ID [-h, --help]
```


#### Command options
{: #connection-reject-options}

`GATEWAY_ID`
:   ID of the gateway the connection is on.

`CONNECTION_ID`
:   ID of the connection you are rejecting.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #connection-reject-examples}

Reject the connection request.

```sh
ibmcloud tg cr $gateway $connection
```
{: pre}

---


### `ibmcloud tg connection-delete`
{: #connection-delete}

Delete an existing connection.

```sh
ibmcloud tg connection-delete|cd GATEWAY_ID CONNECTION_ID [-f, --force] [-h, --help]
```

#### Command options
{: #connection-delete-options}

`GATEWAY_ID`
:   ID of the gateway of the connection that is being deleted.

`CONNECTION_ID`
:   ID of the connection that is being deleted.

`--force | -f`
:   Optional: Force the delete without confirmation.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #connection-delete-examples}

Delete connection without confirmation.

```sh
ibmcloud tg cd $gateway $connection -f
```
{: pre}

## Route reports
{: #route-report}

This section provides information about CLI commands for route report functions.

### `ibmcloud tg route-reports`
{: #list-routereports}

Use this command to list route reports available on a gateway.

```sh
ibmcloud tg route-reports|rrs GATEWAY_ID [--output json] [-h, --help]
```

#### Command options
{: #list-routereports-options}

`GATEWAY_ID`
:   ID of the gateway to list route reports for.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #list-routereports-examples}

List the route reports on the gateway.

```sh
ibmcloud tg rrs $gateway
```
{: pre}

Other commands require a route report ID. Save the ID as an environment variable so you can use it later, for example:

```text
report="4892849f-368e-9999-4444-8888fb21e513"
```
{: screen}

---

### `ibmcloud tg route-report`
{: #routereport-details}

Retrieve details about a specific route report.

```sh
ibmcloud tg route-report|rr GATEWAY_ID REPORT_ID [--output json] [-h, --help]
```

#### Command options
{: #routereport-details-options}

`GATEWAY_ID`
:   ID of the gateway the route report is from.

`REPORT_ID`
:   ID of the route report you want details for.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #routereport-details-examples}

Request details for a route report.

```sh
ibmcloud tg rr $gateway $report
```
{: pre}

---

### `ibmcloud tg route-report-create`
{: #routereport-create}

Create a route report.

```sh
ibmcloud tg route-report-create|rrc GATEWAY_ID [--output json] [-h, --help]
```

#### Command options
{: #routereport-create-options}

`GATEWAY_ID`
:   ID of the gateway the route report is created for.

`--output json`
:   Optional: Specify whether you want the output that is displayed in JSON format.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #routereport-create-examples}

Create a route report for a gateway.

```sh
ibmcloud tg rrc $gateway
```
{: pre}

---

### `ibmcloud tg route-report-delete`
{: #routereport-delete}

Delete an existing route report.

```sh
ibmcloud tg route-report-delete|rrd GATEWAY_ID REPORT_ID [-f, --force] [-h, --help]
```

#### Command options
{: #routereport-delete-options}

`GATEWAY_ID`
:   ID of the gateway the report is for.

`REPORT_ID`
:   ID of the report you want to delete.

`--force | -f`
:   Optional: Force the delete without confirmation.

`--help | -h`
:   Optional: Get help on this command.

#### Example
{: #routereport-delete-examples}

Delete route report with no confirmation.

```sh
ibmcloud tg rrd $gateway $report -f
```
{: pre}

---

### `ibmcloud tg prefix-filter-create`
{: #prefix-filter-create}

Add prefix filter to connection.

```sh
ibmcloud tg prefix-filter-create GATEWAY_ID CONNECTION_ID --prefix PREFIX --action ACTION [--le LE] [--ge GE] [--before BEFORE] [--output json]
```

#### Command options
{: #prefix-filter-create-options}

`GATEWAY_ID`
:   ID of the gateway the prefix filter is being applied to.

`CONNECTION_ID`
:   ID of the connection the prefix filter is being applied to.

`--prefix`
:   Network prefix that the filter is applied to.

`--action`
:   Action to take on the specified prefix (`permit` | `deny`).

`--le`
:   Optional: Prefix filter that is applied to a subnet mask less than or equal to this value.

`--ge`
:   Optional: Prefix filter that is applied to a subnet mask greater than or equal to this value.

`--before`
:   Optional: Identifier of the prefix filter this filter should be applied before.  If empty, this filter is applied last.

`--output`
:   Optional: Specify output format; Only `json` is supported.

##### Examples
{: #prefix-filter-create-examples}

Add prefix filter for `10.0.250.0/24` to gateway `9f559c43-63f4-4da5-b312-b525a8dce185`, connection `6c1bdc19-4adb-4760-8cdc-ef3b74b626f7` with the action `permit`.

```sh
ibmcloud tg pfc 9f559c43-63f4-4da5-b312-b525a8dce185 6c1bdc19-4adb-4760-8cdc-ef3b74b626f7 --prefix 10.0.250.0/24 --action permit
```
{: pre}

---

### `ibmcloud tg prefix-filter-delete`
{: #prefix-filter-delete}

Delete prefix filter from connection.

```sh
ibmcloud tg prefix-filter-delete GATEWAY_ID CONNECTION_ID FILTER_ID [-f, --force]
```

#### Command options
{: #prefix-filter-delete-options}

`GATEWAY_ID`
:   ID of the gateway that the prefix filter is deleted from.

`CONNECTION_ID`
:   ID of the connection that the prefix filter is deleted from.

`FILTER_ID`
:   ID of the prefix filter being deleted.

`--force, -f`
:   Force the deletion operation without confirmation.

##### Examples
{: #prefix-filter-delete-examples}

Delete prefix filter ID `b4dbe0a6-c52d-4128-cc32-6f53d86bc82b` from gateway `9f559c43-63f4-4da5-b312-b525a8dce185` and connection `6c1bdc19-4adb-4760-8cdc-ef3b74b626f7`

```sh
ibmcloud tg pfd 9f559c43-63f4-4da5-b312-b525a8dce185 6c1bdc19-4adb-4760-8cdc-ef3b74b626f7 b4dbe0a6-c52d-4128-cc32-6f53d86bc82b
```
{: pre}
