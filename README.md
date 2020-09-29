# Setting up Apache Cassandra in Docker and Visual Studio Code

For more information check [Cassandra on Docker Hub](https://hub.docker.com/_/cassandra "Cassandra on Docker Hub")

***

## How to run Apache Cassandra on Docker

First download the image:

### Cassandar version 4.0

$ `docker pull cassandra:4.0`

### Cassandar version 3.11.8

$ `docker pull cassandra:3.11.8`

Then create a running server container named `cassandra-server`:

$ `docker run --name cassandra-server -p 9042:9042 -e CASSANDRA_CLUSTER_NAME=cassandra-cluster -e CASSANDRA_ENDPOINT_SNITCH=GossipingPropertyFileSnitch -e CASSANDRA_DC=cassandra-datacenter -d cassandra:3.11.8`

To ensure the container is running:

$ `docker ps`

If the container is not running:

$ `docker start cassandra-server`

***

## Connect to Cassandra from `cqlsh`

$ `docker exec -it cassandra-server cqlsh`

To close, press `Ctrl+D`

***

## Use Cassandra Workbench

First install [Cassandra Workbench](https://marketplace.visualstudio.com/items?itemName=kdcro101.vscode-cassandra) in Visual Studio Code. Open workspace [`Ctrl+Shift+P`] (workspace path is needed for configuration to generate), activate extension by running command from palette `Cassandra Workbench: Generate configuration`. This will generate .cassandraWorkbench.jsonc configuration file. Edit the configuration file as follow:

```jsonc
[
    // AllowAllAuthenticator
    {
        "name": "Cluster AllowAllAuthenticator",
        "contactPoints": ["127.0.0.1:9042"]
    },
    //PasswordAuthenticator
    {
        "name": "Cluster PasswordAuthenticator",
        "contactPoints": ["127.0.0.1:9042"],
        "authProvider": {
            "class": "PasswordAuthenticator",
            "username": "Your Username",
            "password": "Your Password"
        }
    }
]
```

***

## Save the container

First stop the running container

$ `docker stop cassandra-server`

Then, save the container

$ `docker commit cassandra-server cassandra-sample-image`

To ensure the image is saved, check docker images:

$ `docker images`

### How to remove stopped container or commited image

To remove a container, first you have to stop it. then in order to remove stopped container:

$ `docker rm cassandra-server`

And to remove commited image:

$ `docker rmi cassandra-sample-image`

***

## Documentation

For more information, read [Apache Cassandra Documentation](https://cassandra.apache.org/doc/latest/) (version 4 at the time of writing this documentation).

To see the version 3 documentation, open [Cassandra version 3.11.8 Documentation](https://cassandra.apache.org/doc/3.11.8/).

***

## Useful articles

[What is the Cassandra database used for?](https://www.quora.com/What-is-the-Cassandra-database-used-for)

[Cassandra use cases](https://blog.pythian.com/cassandra-use-cases/)

[Is Apache Cassandra really the Database you need?](https://blog.knoldus.com/is-apache-cassandra-really-the-database-you-need/)

[The Not-So-fictional tale of Cassandra and MongoDB for IoT Data Storage](https://medium.com/clovity/the-not-so-fictional-tale-of-cassandra-and-mongodb-for-iot-data-storage-2979726ff64c)

***
