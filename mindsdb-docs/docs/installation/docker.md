# Install with Docker

You can run MindsDB in a docker container assuming that you have [docker](https://docs.docker.com/install/) installed in your machine. To make sure Docker is successfully installed on your machine run:

```
docker run hello-world
```

You should see the `Hello from Docker!` message displayed.


### Run MindsDB container

MindsDB images are uploaded to [MindsDB repo on docker hub](https://hub.docker.com/u/mindsdb) after each release.

#### Pull image

First, run the bellow command to pull our latest production image:

```
docker pull mindsdb/mindsdb
```

Or, to try out the latest beta version pull the beta image:

```
docker pull mindsdb/mindsdb_beta
```

#### Start container

Next, run the bellow command to start the container:

```
docker run -p 47334:47334 mindsdb/mindsdb
```

!!! info "Publish ports"

    Note that, you must publish a container’s port to the host `-p 47334:47334` which is used by MindsDB GUI and HTTTP API. Also, to use MindsDB MySQL API or MongoDB API publish `-p 47335:47335 -p 47336:47336` too.