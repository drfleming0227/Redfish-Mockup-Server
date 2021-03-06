<<<<<<< HEAD
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
=======
Copyright 2016-2020 DMTF. All rights reserved.

# The Redfish mockup server

The Redfish mockup server, `redfishMockupServer.py`, serves Redfish `GET`, `PATCH`, `POST`, and `DELETE` requests against a Redfish mockup bundle, and implements the `SubmitTestEvent` action.

The server runs at either:

* An IP address and port that you specify when you start the server.
* The default IP address and port, `127.0.0.1:8000`.

<a id="server-form"></a>The server runs in *tall* or *short* form, which indicates what the server expects at the top of the mockup directory structure:

* **Tall**. (Default.) The mockup directory structure, the version resource, `/redfish`.
* **Short**. The mockup directory structure, the service root resource, `/redfish/v1/`. 

    > **Note:** To run in short form, specify the `-S` option when you start the server.

## Contents

* [Run the Redfish mockup server inside docker](#run-the-redfish-mockup-server-inside-docker)
* [Run the Redfish mockup server outside docker: Prerequisite software](#run-the-redfish-mockup-server-outside-docker-prerequisite-software)
    + [Python 3](#python-3)
    + [pip](#pip)
    + [Python packages](#python-packages)
    + [Redfish mockup server](#redfish-mockup-server)
    + [Redfish Mockup Bundle](#redfish-mockup-bundle)
* [Start the Redfish mockup server](#start-the-redfish-mockup-server)
* [redfishMockupServer usage](#redfishmockupserver-usage)
* [Release process](#release-process)

## Run the Redfish mockup server inside docker

```
$ docker build -t redfish-mockup-server:latest .
$ docker run --rm -it -v /absolute/path-to-mockup/directory:/mymockup redfish-mockup-server:latest -D /mymockup
```

## Run the Redfish mockup server outside docker: Prerequisite software

You must install [Python 3](#python-3), [pip](#pip), and [Python packages](#python-packages).

Then, you must [clone the Redfish mockup server](#clone-the-redfish-mockup-server) and [save the Redfish Mockup Bundle](#save-the-redfish-mockup-bundle) to your local machine.

### Python 3

1. Verify your Python installation:

    ```bash
    $ python --version
    ```

1. If Python 3.4 or later is not installed, download [Python](https://www.python.org/downloads/ "https://www.python.org/downloads/") for your operating system and verify the Python installation again:

    ```bash
    $ python --version
    ```

1. Ensure that Python is in your path:

    ```bash
    $ echo $PATH
    ```

### pip

1. Verify your pip installation:

    ```bash
    $ pip --version
    ```

1. If pip is not installed, install it:

    ```bash
    $ curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
    $ python3 get-pip.py
    ```

1. Upgrade pip and verify the installation again:

    ```bash
    $ pip install --upgrade pip
    $ pip --version
    ```

### Python packages

1. Install Python packages:

    ```bash
    $ pip install -r requirements.txt
    ```

<a id="clone-the-redfish-mockup-server"></a>

### Redfish mockup server

Clone the [Redfish mockup server repository](https://github.com/dmtf/Redfish-Mockup-Server "https://github.com/dmtf/Redfish-Mockup-Server"):

```bash
$ git clone git@github.com:DMTF/Redfish-Mockup-Server.git
```

<a id="save-the-redfish-mockup-bundle"></a>
 
### Redfish mockup bundle

DSP2043 *Redfish Mockup Bundle* provides mockups of various Redfish service implementations that show typical Redfish examples.

Go to the [All Published Versions of DSP2043](https://www.dmtf.org/dsp/DSP2043 "https://www.dmtf.org/dsp/DSP2043") page and in the **Title** column, click the **Redfish Mockup Bundle** link and save the ZIP file to your preferred location.

## Start the Redfish mockup server

The server runs at either:

* An IP address and port that you specify when you start the server.
* The default IP address and port, `127.0.0.1:8000`.

1. Get the latest Redfish mockup server usage information:

    ```bash
    $ python3 redfishMockupServer.py --help
    ```

1. Start the server in [*short* form](#server-form) against the mockup in `-D <DIR>`:

    ```bash
    $ python3 redfishMockupServer.py -S -D <DIR>
    ```

    > **Note:** If you omit the `-S` option, the server runs in tall form by default.

For example, if you copy the `DSP2043_2019.1` bundle to a `DSP2043_2019.1` directory that is parallel with the `Redfish-Mockup-Server` directory, you can start the server in short form on port 8000, as follows:

```bash
$ cd Redfish-Mockup-Server
$ python3 redfishMockupServer.py -S -D ../DSP2043_2019.1/public-localstorage
```

## redfishMockupServer usage
>>>>>>> 8b374d8054ce53178335549f4a0774bd2aedf24a

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

<<<<<<< HEAD
When prompted, type the release notes. To indicate the end of notes, enter an an empty line.
=======
1. Update `CHANGELOG.md` with the list of changes since the last release.
1. Update the `tool_version` variable in `redfishMockupServer.py` to the new version of the tool.
1. Push changes to GitHub.
1. Create a release in GitHub.
>>>>>>> 8b374d8054ce53178335549f4a0774bd2aedf24a
