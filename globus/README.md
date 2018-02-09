# Globus Connect Personal Endpoint
This application starts up a personal Globus endpoint with data served out
of the user's home directory.

## Setup
Before the application can be launched, the user must acquire a Globus endpoint
setup key by visiting [https://www.globus.org/app/endpoints/create-gcp](https://www.globus.org/app/endpoints/create-gcp). The generated key should be copied and pasted into the application's
`SETUP_KEY` property value.

Once this is done just launch the application. After the application reports
_Ready_ the endpoint is active and users can initiate transfers to and from the
using the Globus [_Transfer Files_](https://www.globus.org/app/transfer) page.
