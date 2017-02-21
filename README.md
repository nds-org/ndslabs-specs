# NDS Labs Service Catalog
This repository contains specifications for services supported in the National Data Service [NDS Labs](https://github.com/nds-org/ndslabs) platform. Service specifications include the following information:

* Unique key used to identify the service
* A label and description used for display and searching
* Associated Docker image
* Attributes controlling how the service is deployed in NDSLabs.
* Required and optional dependencies
* Configuration options
* Storage requirements
* Ports and networking configuration

Specifications for a given service stack are organized into subdirectories. 

## Example specification

```js
{
    "id": "uniqueid",
    "logo": "URL",
    "key": "shortname",
    "label": "My Service Display Name",
    "maintainer": "Maintainer name and email",
    "image": {
        "registry" : "docker.io",
        "name" : "ndslabs/myimage",
        "tags" : [ "latest", "v1", "v2", "v3" ]
    },
    "display": "stack",
    "access": "external",
    "description": "Description of my service",
    "depends": [
        {
            "key": "dependencykey",
            "required": true,
            "shareConfig": false
        }
    ],
    "config":  [
        {
            "name": "ENV_VAR",
            "value": "value",
            "label": "Label",
            "canOverride": true,
            "isPassword": true
        }
    ],
    "command": [ "somecommand" ],
    "args" : [
        "-someargument"
    ],
    "ports": [
        {
            "port": 80,
            "protocol": "http"
        },
        {
            "port": 8000,
            "protocol": "http"
        }
    ],
    "repositories":  [
        {
            "url": "https://github.com/golang/example",
            "type": "git"
        }
    ],
    "developerEnvironment" : "devenvId",
    "volumeMounts":[
       { 
            "name": "data",
            "mountPath": "/data"
       },
       {
            "name": "other",
            "mountPath": "/other"
       }   
    ],
    "readinessProbe" : {
        "type" : "http",
        "path" : "/favicon.ico",
        "port" : 80,
        "initialDelay": 10,
        "timeout" : 600
    },
    "resourceLimits": {
        "cpuMax": 1000,
        "cpuDefault": 100,
        "memMax": 1024,
        "memDefault": 512
    },
    "tags": [
        "tagId1",
        "tagId2"
    ]
}
```

## Documentation

### Service
|Field|Type|Description|
|:---|:---|:---|
|key|string|Unique identifier for the service (alpha-numeric only, lowercase)|
|label|string|Label used for display|
|description|string|Description used for display|
|maintainer|string|maintainer name and email|
|info|string|Optional URL to help page for this service|
|logo|string|Optional URL to logo for service|
|image|ServiceImage|Docker image information (see below)|
|display|string|	"stack" => show this service as a top-level stack; "standalone" => show this service as a standalone (hidden behind the checkbox in the UI) otherwise, do not display this service; only allow it to be added to other stacks|
|access|string|"internal" => allow this service to receive requests only from within the cluster;  "external" => allow this service to receive requests from outside of the cluster (usually a browser); otherwise, do not allow any communication to be received by this service|
|depends|ServiceDepencency[]|List of dependencies (see below)|
|config|Config[]|List of configuration options (see below)|
|command|string[]|Optional commands to be passed to the container.|
|args|string[]|	Optional arguments to be passed to the container|
|ports|Port[]|List of ports exposed by this service (see below)|
|repositories|Repository[]|List of source code repositoriues associated with service|
|volumeMounts|VolumeMount[]|Defines volume requirements for the service. Currently only one mount is supported per service.|
|readinessProbe|ReadyProbe|Probe used to determine when a service is ready to receive traffic|
|resourceLimits|ResourceLimit[]|Required CPU and memory requirements for application.|
|developerEnvironment|string|Unique key of associated developer environment|
|tags|string[]|List of tags|

### ServiceImage
|Field|Type|Description|
|:---|:---|:---|
|registry|string|Registry URL (for now, only docker)|
|name|string|Docker image name|
|tags|string[]|List of tags|

### ServiceDependency
|Field|Type|Description|
|:---|:---|:---|
|key|string|Unique ID of dependency|
|required|bool|Whether dependency is required (default: false)|
|shareConfig|bool|Whether config is shared with other services (default:false)

### Config
|Field|Type|Description|
|:---|:---|:---|
|name|string|Environment variable name|
|value|string|Environment variable value|
|label|string|Label to display in UI|
|canOverride|bool|Whether user can override value|
|isPassword|bool|Whether value is a password|

### Port
|Field|Type|Description|
|:---|:---|:---|
|port|int|Port number|
|protocol|string|Procotol (http or tcp)

### VolumeMount
|Field|Type|Description|
|:---|:---|:---|
|name|string|Unique name for volume|
|mountPath|string|Mount path in container|

### ReadyProbe
|Field|Type|Description|
|:---|:---|:---|
|type|string|Probe type: must be one of "http" or "tcp"|
|path|string|Probe path for HTTP probes|
|port|int|Probe port|
|initialDelay|int|How long to wait before starting probe|
|timeout|int|How long to wait before timing out|

### Repository
|Field|Type|Description|
|:---|:---|:---|
|url|string|Respository URL|
|type|string|Repository type (git, svn or hg)|

### ResourceLimit
Individual NDS Labs projects are configured with specific memory and CPU limits. Because of this, all services must declare memory and CPU requirements to enable scheduling and resource constraint enforcement. These values relate directly to Kubernetes limit ranges and resource requests.

|Field|Type|Description|
|:---|:---|:---|
|cpuMax	|String	|Maximum expected CPU utilization in millicores|
|cpuDefault	|String	|Initial CPU utilization in millicores |
|memMax	|String	|Maximum memory in Mb|
|memDefault	|String	|Initial memory in Mb|



## Adding a New Spec
To add a new service to NDS Labs, you only need:
* a Docker Image
* a Docker Hub account (required to push your image)
* a JSON object describing your image that conforms to the above specification

For some tutorials on how to add a new spec to a running instance of NDS Labs, see [developer-tutorial](https://github.com/nds-org/developer-tutorial).

## Contributing a Spec
Have you created and tested a spec of your own? Want to see it end up in NDS Labs for others to use?

That's great!

### Share Your Spec
Share the JSON spec you have created with other users of NDS Labs!

This will enable them to add the JSON spec using the CLI:
```bash
ndslabsctl add service -f path/to/spec/file.json
```

They will then be able to run your custom service using your pushed Docker image.

### Make a Pull Request
To contribute your service back to our code base:
* Fork this repository
* Add your service spec
* Create a pull request

We will review and give feedback on your pull request before merging it in.

For more information on our Developer Workflows, see [Developer Workflows](https://opensource.ncsa.illinois.edu/confluence/display/NDS/Developer+Workflows).

## See Also
* https://github.com/nds-org/ndslabs-clowder
* https://github.com/nds-org/ndslabs-dataverse
* https://github.com/nds-org/ndslabs-elk
* https://github.com/nds-org/ndslabs-irods
