# Deploy using Docker

You can use MindsDBs Docker container assuming that you have <a href="https://docs.docker.com/install" target="_blank">docker</a> installed on your machine. To make sure Docker is successfully installed on your machine, run:

```
docker run hello-world
```

You should see the `Hello from Docker!` message displayed. If not, check the <a href="https://www.docker.com/get-started" target="_blank">get started</a> documentation.


### Run MindsDB container

MindsDB images are uploaded to the <a href="https://hub.docker.com/u/mindsdb" target="_blank">MindsDB repo on docker hub</a> after each release.

#### Pull image

First, run the below command to pull our latest production image:

```
docker pull mindsdb/mindsdb
```

Or, to try out the latest beta version, pull the beta image:

```
docker pull mindsdb/mindsdb_beta
```

#### Start container

Next, run the below command to start the container:

```
docker run -p 47334:47334 mindsdb/mindsdb
```

![Docker run](/assets/docker-install.gif)

That's it. MindsDB should automatically start the Studio on your default browser.

!!! info "Publish ports"
    Note that you must publish a container’s port to the host `-p 47334:47334`, which is used by the MindsDB GUI and HTTP API. Also, to use MindsDB MySQL API publish `-p 47335:47335` and for MongoDB API `-p 47336:47336` port.

!!! warning "MKL Issues"
	Note that If you experience issue related to MKL or if training process does not finish, please add env var or start Docker with this command:
	```
	docker run --env MKL_SERVICE_FORCE_INTEL=1 -it -p 47334:47334 mindsdb/mindsdb
	```

#### Extend config.json

If you want to extend the default configuration, you will be able to send the config.json value as JSON string argument to the MDB_CONFIG_CONTENT as:

```
docker run -e MDB_CONFIG_CONTENT='{"api":{"http": {"host": "0.0.0.0","port": "47334"}}}' mindsdb/mindsdb
```

Or, you can pipe `<`  the content of the file to the MDB_CONFIG_CONTENT.
