# Docker Commands

## Images

| Images    | Description                                                              |
| --------- | ------------------------------------------------------------------------ |
| `images`  | **List images**                                                          |
| `rmi`     | **Remove one or more images**                                            |
| `pull`    | **Pull an image or a repository from a registry**                        |
| `push`    | **Push an image or a repository to a registry**                          |
| `commit`  | Create a new image from a container's changes                            |
| `history` | Show the history of an image                                             |
| `save`    | Save one or more images to a tar archive (streamed to STDOUT by default) |
| `load`    | Load an image from a tar archive or STDIN                                |
| `tag`     | Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE                    |
| `version` | Show the Docker version information                                      |

## Containers

| Containers | Description                                                          |
| ---------- | -------------------------------------------------------------------- |
| `run`      | **RUN A COMMAND IN A NEW CONTAINER**                                 |
| `start`    | **Start one or more stopped containers**                             |
| `stop`     | **Stop one or more running containers**                              |
| `rm`       | **Remove one or more containers**                                    |
| `ps`       | **List containers**                                                  |
| `exec`     | **Run a command in a running container**                             |
| `kill`     | **Kill one or more running containers**                              |
| `restart`  | **Restart one or more containers**                                   |
| `top`      | Display the running processes of a container                         |
| `port`     | List port mappings or a specific mapping for the container           |
| `rename`   | Rename a container                                                   |
| `pause`    | Pause all processes within one or more containers                    |
| `unpause`  | Unpause all processes within one or more containers                  |
| `update`   | Update configuration of one or more containers                       |
| `wait`     | Block until one or more containers stop, then print their exit codes |

| Advanced  | Description                                                                       |
| --------- | --------------------------------------------------------------------------------- |
| `attach`  | **Attach local standard input, output, and error streams to a running container** |
| `cp`      | Copy files/folders between a container and the local filesystem                   |
| `create`  | Create a new container                                                            |
| `diff`    | Inspect changes to files or directories on a container's filesystem               |
| `events`  | Get real time events from the server                                              |
| `export`  | Export a container's filesystem as a tar archive                                  |
| `import`  | Import the contents from a tarball to create a filesystem image                   |
| `info`    | Display system-wide information                                                   |
| `inspect` | Return low-level information on Docker objects                                    |

## Others

| DockerHUB | Description                                                     |
| --------- | --------------------------------------------------------------- |
| `search`  | **Search the Docker Hub for images**                            |
| `login`   | Log in to a Docker registry                                     |
| `logout`  | Log out from a Docker registry                                  |
| `logs`    | Fetch the logs of a container                                   |
| `stats`   | Display a live stream of container(s) resource usage statistics |

| Dockerfile | Description                      |
| ---------- | -------------------------------- |
| `build`    | Build an image from a Dockerfile |

## Remove all images at once

```sh
docker rmi $(docker images -q)
```

- `-q ` is a option is used to provide to return the unique IDs.
- `-q ` the quiet option to provide only container numeric IDs, rather than a whole table of information about container

# Containers

## Remove container

`docker rm` removes containers by their **name** or **ID**.

When you have Docker containers running, you first need to stop them before deleting them.

- Stop all running containers: `docker stop $(docker ps -a -q)`
- Delete all stopped containers: `docker rm $(docker ps -a -q)`

## Remove all containers from specific image

The command is:

```sh
docker rm $(docker ps -a | grep <image-name> | cut -d ' ' -f 1)
```

### How it works

1. List all containers with `docker ps -a`

```sh
[broch-pc broch]> docker ps -a
CONTAINER ID   IMAGE            COMMAND                  CREATED          STATUS                      PORTS     NAMES
7f66a25605ba   dpage/pgadmin4   "/entrypoint.sh -e P…"   33 minutes ago   Exited (1) 33 minutes ago             youthful_faraday
efc539dbf95a   dpage/pgadmin4   "/entrypoint.sh -e P…"   33 minutes ago   Exited (1) 33 minutes ago             serene_archimedes
9a9a5a7fb4a4   dpage/pgadmin4   "/entrypoint.sh -e P…"   33 minutes ago   Exited (1) 33 minutes ago             beautiful_merkle
4dc49f5eaccf   dpage/pgadmin4   "/entrypoint.sh -e P…"   34 minutes ago   Exited (1) 34 minutes ago             strange_thompson
57c5134d0967   dpage/pgadmin4   "/entrypoint.sh -e P…"   35 minutes ago   Exited (1) 35 minutes ago             distracted_torvalds
7e0641340993   dpage/pgadmin4   "/entrypoint.sh -e P…"   36 minutes ago   Exited (1) 36 minutes ago             pensive_allen
8dcca5f5b516   dpage/pgadmin4   "/entrypoint.sh -e P…"   36 minutes ago   Exited (1) 36 minutes ago             elegant_haslett
6afa92b01ec0   dpage/pgadmin4   "/entrypoint.sh PGAD…"   37 minutes ago   Exited (1) 37 minutes ago             gifted_moser
19392297e7ec   dpage/pgadmin4   "/entrypoint.sh"         43 minutes ago   Exited (1) 43 minutes ago             eloquent_dijkstra
7cd5863687c5   ubuntu           "bash"                   4 days ago       Exited (0) 4 days ago                 ubuntu
8c1d8ea33d1f   postgres         "docker-entrypoint.s…"   9 days ago       Exited (0) 2 days ago                 postgresdb
```

2. We'll remove all containers from `dpage/pgadmin4` image. Selecting with `grep dpage`

```sh
[broch-pc broch]> docker ps -a | grep dpage
7f66a25605ba   dpage/pgadmin4   "/entrypoint.sh -e P…"   37 minutes ago   Exited (1) 37 minutes ago             youthful_faraday
efc539dbf95a   dpage/pgadmin4   "/entrypoint.sh -e P…"   37 minutes ago   Exited (1) 37 minutes ago             serene_archimedes
9a9a5a7fb4a4   dpage/pgadmin4   "/entrypoint.sh -e P…"   37 minutes ago   Exited (1) 37 minutes ago             beautiful_merkle
4dc49f5eaccf   dpage/pgadmin4   "/entrypoint.sh -e P…"   37 minutes ago   Exited (1) 37 minutes ago             strange_thompson
57c5134d0967   dpage/pgadmin4   "/entrypoint.sh -e P…"   38 minutes ago   Exited (1) 38 minutes ago             distracted_torvalds
7e0641340993   dpage/pgadmin4   "/entrypoint.sh -e P…"   40 minutes ago   Exited (1) 39 minutes ago             pensive_allen
8dcca5f5b516   dpage/pgadmin4   "/entrypoint.sh -e P…"   40 minutes ago   Exited (1) 40 minutes ago             elegant_haslett
6afa92b01ec0   dpage/pgadmin4   "/entrypoint.sh PGAD…"   41 minutes ago   Exited (1) 41 minutes ago             gifted_moser
19392297e7ec   dpage/pgadmin4   "/entrypoint.sh"         46 minutes ago   Exited (1) 46 minutes ago             eloquent_dijkstra
```

3. Select first colunm, which is the container's unique id, with `cut -d ' ' -f 1`

```sh
[broch-pc broch]> docker ps -a | grep  'page' | cut -d ' ' -f 1
7f66a25605ba
efc539dbf95a
9a9a5a7fb4a4
4dc49f5eaccf
57c5134d0967
7e0641340993
8dcca5f5b516
6afa92b01ec0
19392297e7ec
```

4. Now we have all containers IDs, let's delete it.

```sh
docker rm $(docker ps -a | grep page | cut -d ' ' -f 1)
```

5. All containers from `dpage/pgadmin4` image have been deleted.

```sh
[broch-pc broch]> docker ps -a
CONTAINER ID   IMAGE      COMMAND                  CREATED      STATUS                  PORTS     NAMES
7cd5863687c5   ubuntu     "bash"                   4 days ago   Exited (0) 4 days ago             ubuntu
8c1d8ea33d1f   postgres   "docker-entrypoint.s…"   9 days ago   Exited (0) 2 days ago             postgresdb

```
