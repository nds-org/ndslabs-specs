# NDS Labs Service Catalog
The service definitions used by [NDS Labs](https://github.com/nds-org/ndslabs).

## Documentation
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
