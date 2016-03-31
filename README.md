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

## Documentation
```js
{
  "key": "A unique identifier for this service - may only contain lowercase alpha-numeric characters",
  "label": "How this service should appear in the UI",
  "image": "A docker image, formatted as repository/image:version",
  "description": "A short description of what this service does that will appear in the UI",
  "access": "external if browser needs to access, internal if other services need to access, none otherwise",
  "display": "stack if it should be displayed at the top-level in the UI, standalone if it should be displayed under the 'Show Standalones' checkbox in the UI, none otherwise",
  "depends": [
    {
      "key": "The key of another service that this spec depends on",
      "required": "True if this dependency is required. False if it is optional",
      "shareConfig": "True if any config from the dependency should be copied into this one"
    },
      ...
  ],
  "config": [
    {
      "name": "Name of the environment variable to set inside of this container",
      "value": "Value of the environment variable",
      "label": "The label for this property that will appear in the UI",
      "isPassword": "True if this variable reprents a password - this tells the UI to generate a password box and to allow the user to generate a random value for this field",
      "canOverride": "True if this variable can be overridden by the user, if they so desire"
    },
      ...
  ],
  "ports": [
    {
      "port": "A port number to expose",
      "protocol": "The protocol of this exposed port  must be lowercase (i.e. http, tcp, udp, etc)"
    },
      ...
  ],
  "volumeMounts": [
    {
      "name": "The unique identifier of this volume mount - this must match an existing volume",
      "mountPath": "The absolute path of the destination inside of the container"
    },
      ...
  ]
}
```

For more information about the specs: [NDS Labs Service Specification](https://opensource.ncsa.illinois.edu/confluence/display/NDS/NDS+Labs+Service+Specification).

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
