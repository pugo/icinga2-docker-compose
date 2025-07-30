# Docker-compose files for Icinga2 docker images

This project contains docker-compose files for the official Icinga2 docker images.

## File separation

The files are split to currently four different compose files:

 * `icinga-master-compose.yml`: The icinga-master container.
 * `icinga-db-compose.yml`: All required databases (Redis, MariaDB and the icingadb container.
 * `icinga-web-compose.yml`: The icingaweb2 container.

 * `icinga-agent-compose.yml`: The icinga-agent container for other hosts.

## Configuration

The different compose files maps configuration from the `data` directory into respective containers.

The `data` directory contains subdirectories for respective container:

* `master`: The main location for any master related config. This likely means your main Icinga2 config.
* `web`: Config for the icingaweb2.
* `agent`: Config for icinga2 agents.


## Running

To bring up for example the three necessary docker-compose files for the server, run as follows.

```
$ docker-compose -f icinga-master-compose.yml up
$ docker-compose -f icinga-db-compose.yml up
$ docker-compose -f icinga-web-compose.yml up
```

To bring up for the docker-compose files for a stand-alone agent, run as follows.

```
$ docker-compose -f icinga-agent-compose.yml up
```


## Interaction

To for example run a command in the master container:

```
$ docker exec -it icinga-master <command>
```

To generate a ticket from the master, to add an agent:

```
$ docker exec -it icinga-master icinga2 pki ticket --cn icinga-agent > icinga-agent.ticket
```
