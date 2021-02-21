## webMethods Integration Server Administration

wmisa is a command line client for administering webMethods Integration Server. Use it to perform operations on administrative resources and execute administrative actions such as restarting the server, installing a package or enabling a cache manager.

## Installation
wmisa requires [Node.js](https://nodejs.org) v 10.15 or later.

    npm install -g @softwareag/wmisa

## Usage

There are three categories of commands.
| Category |Description |
|:--|:--|
|Server Commands  | Perform administrative operations and actions. |
|Help Commands | Discover types of resources, the operations they support and their inputs and outputs. |
|Default Commands | View and modify default values for command line options. |


### Server Commands
Server commands are sent to the Integration Server identified by the `--host` command line option. There are two types of server commands: CRUD commands and action commands.

**CRUD commands** are used to view and modify the configuration of an Integration Server. Not all types of resources support all CRUD operations. For example, the server resource can be used to read high-level information about the server. It cannot be used to create a new server or delete and existing one.

*CRUD Command Formats and Examples* 

    wmisa read <resource-type>
Lists all instances of a type of resource. When combined with the `--expand` option, the details of each resource is displayed. Not all resource types support this operation.
&ensp;&ensp;Example: List all keystore aliases. `wmisa read keystore`
&ensp;&ensp;Example: List details for all keystore aliases. `wmisa read keystore --expand`

    wmisa read <resource-type> <resource-id>
Displays a resource.
&ensp;&ensp;Example: Displays the remote server wmrestoneng01. `wmisa read remoteserver vmrestoneng01`

    wmisa create <resource-type>
Creates a new instance of a resource. Requires a payload defining the state of the resource. You can put the payload a file and use the `--file` option or enter it on the command line with the `--entity` option.
&ensp;&ensp;Example: Create a cache manager named Purchasing from a file. 
&ensp;&ensp;&ensp;&ensp;`wmisa create cachemanager Purchasing --file ./newcachemgr.json`
&ensp;&ensp;Example: Create a cache named Orders in the Purchasing cache manager from a file.
&ensp;&ensp;&ensp;&ensp;`wmisa create cachemanager Purchasing cache Orders --file ./newcache.json`

    wmisa update <resource-type> <resource-id>
Updates an existing resource. The payload of changes to make to the resource must be supplied to this command. You can put the payload in a file and use the `--file` option or enter it on the command line with the `--entity` option.
&ensp;&ensp;Example: Update the user btaylor's password. `wmisa update user btaylor --entity "password=S3cre7!"`

    wmisa delete <resource-type> <resource-id>
Deletes a resource.
&ensp;&ensp;Example: Delete the trusted JWT issuer IdProvider01. `wmisa delete jwt issuer IdProvider01`


**Action commands** perform administrative actions on server resources. Each type of resource has its own set of actions. Use the help command to discover them. Most action commands include `name=value` sub-commands. In DOS, these must be surrounded by double quotes.

