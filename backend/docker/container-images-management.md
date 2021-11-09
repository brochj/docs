# Images

## List all images

```sh
docker images
```

## Remove image

```sh
docker rmi <image-name>
```

## Remove multiple images

```sh
docker rmi <your-image-id1> <your-image-id2> ...
```

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
