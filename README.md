# Redfish Mockup Server

Copyright 2016-2020 DMTF. All rights reserved.

## About

The Redfish Mockup Server serves Redfish requests against a Redfish mockup. The server runs at a specified IP address and port or at `127.0.0.1:8000`, which is the default IP address and port.

You can find DMTF-published sample mock-ups at [All Published Versions of DSP2043](https://www.dmtf.org/dsp/DSP2043 "https://www.dmtf.org/dsp/DSP2043"). To create a mockup from a service, use the [Redfish-Mockup-Creator](https://github.com/DMTF/Redfish-Mockup-Creator "https://github.com/DMTF/Redfish-Mockup-Creator").

## Requirements

If running the mockup server natively on your system:

* Install [Python 3](https://www.python.org/downloads/ "https://www.python.org/downloads/") and [pip](https://pip.pypa.io/en/stable/installing/ "https://pip.pypa.io/en/stable/installing")
* Install required Python packages: `pip install -r requirements.txt`

If running the mockup server as a Docker container:

* Install [Docker](https://www.docker.com/get-started "https://www.docker.com/get-started")
* See [Docker container](#docker-container)

## Usage

```
Redfish Mockup Server, version 1.1.4
usage: redfishMockupServer.py [-h] [-H HOST] [-p PORT] [-D DIR] [-E] [-X]
                              [-t TIME] [-T] [-s] [--cert CERT] [--key KEY]
                              [-S] [-P]

Serve a static Redfish mockup.

optional arguments:
  -h, --help            show this help message and exit
  -H HOST, --host HOST, --Host HOST
                        hostname or IP address (default 127.0.0.1)
  -p PORT, --port PORT, --Port PORT
                        host port (default 8000)
  -D DIR, --dir DIR, --Dir DIR
                        path to mockup dir (may be relative to CWD)
  -E, --test-etag, --TestEtag
                        (unimplemented) etag testing
  -X, --headers         load headers from headers.json files in mockup
  -t TIME, --time TIME  delay in seconds added to responses (float or int)
  -T                    delay response based on times in time.json files in
                        mockup
  -s, --ssl             place server in SSL (HTTPS) mode; requires a cert and
                        key
  --cert CERT           the certificate for SSL
  --key KEY             the key for SSL
  -S, --short-form, --shortForm
                        apply short form to mockup (omit filepath /redfish/v1)
  -P, --ssdp            make mockup SSDP discoverable
```

## Example

The mockup server starts an HTTP server at the *HOST* name or IP address and *PORT* port. The mockup server provides Redfish resources in the *DIR* mockup directory. If the mockup does not contain the representation of the `/redfish` resource, you must provide the *short-form* argument. If you omit the mockup, the mockup server serves DMTF's `public-rackmount1` mockup.

```bash
python redfishMockupServer.py -D /home/user/redfish-mockup
```

## Docker container

If running as a Docker container, use one of these actions to pull or build the container:

| Action | Command |
| :----- | :------ |
| Pull the container from Docker Hub | `docker pull dmtf/redfish-mockup-server:latest` |
| Build a container from local source | `docker build -t dmtf/redfish-mockup-server:latest .` |
| Build a container from GitHub | `docker build -t dmtf/redfish-mockup-server:latest https://github.com/DMTF/Redfish-Mockup-Server.git` |

The following command runs the container with the built-in `public-rackmount1` mockup:

```bash
docker run --rm dmtf/redfish-mockup-server:latest
```

The following command runs the container with a specified mockup, where `<PathToMockup>` is the path to the mockup directory:

```bash
docker run --rm -v <PathToMockup>:/mockup dmtf/redfish-mockup-server:latest -D /mockup
```

## Release process

To publish a new version, run the `release.sh` script:

```bash
sh release.sh <NewVersion>
```

When prompted, type the release notes. To indicate the end of notes, enter an an empty line.
