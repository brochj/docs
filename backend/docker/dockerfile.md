# Docker file

[Dockerfile Reference](https://docs.docker.com/engine/reference/builder)

## CMD

[CMD - Dockerfile Reference](https://docs.docker.com/engine/reference/builder/#cmd)

**The main purpose of a `CMD` is to provide defaults for an executing container**

- `CMD` commands will only be utilized **when command-line arguments are missing**

The `CMD` instruction has three forms:

- `CMD ["executable","param1","param2"]` (exec form, this is the preferred form)
- `CMD ["param1","param2"]` (as default parameters to ENTRYPOINT)
- `CMD command param1 param2` (shell form)

**There can only be one `CMD` instruction in a `Dockerfile`**. If you list more than one `CMD` then only the last `CMD` will take effect.

## ENTRYPOINT

[ENTRYPOINT - Dockerfile Reference](https://docs.docker.com/engine/reference/builder/#entrypoint)

ENTRYPOINT has two forms:

- `ENTRYPOINT ["executable", "param1", "param2"]` (exec form, which is the preferred form)
- `ENTRYPOINT command param1 param2 ` (shell form)

# CMD vs ENTRYPOINT

[cmd vs entrypoint](https://www.bmc.com/blogs/docker-cmd-vs-entrypoint/#)

They both specify programs that execute when the container starts running, but:

- `CMD` commands are ignored by Daemon when there are parameters stated within the `docker run` command.

- `ENTRYPOINT` instructions are not ignored but instead are appended as command line parameters by treating those as arguments of the command.

## Using `ENTRYPOINT` or `CMD`

Both `ENTRYPOINT` and `CMD` are essential for building and running Dockerfiles—it simply depends on your use case. As a general rule of thumb:

- Opt for `ENTRYPOINT` instructions when building an executable Docker image using commands that always need to be executed.
- Opt for `ENTRYPOINT` instructions when there is a need for a specific **command to always run when the container starts**.

- `CMD` instructions are best for an additional set of arguments that act as default instructions till there is an explicit command line usage when a Docker container runs.

## Using `CMD` & `ENTRYPOINT` instructions together

While there are fundamental differences in their operations, CMD and ENTRYPOINT instructions are not mutually exclusive. Several scenarios may call for the use of their combined instructions in a Dockerfile.

A very popular use case for blending them is to automate container startup tasks. In such a case, the ENTRYPOINT instruction can be used to define the executable while using CMD to define parameters.

Example

```dockerfile
FROM centos:7
RUN    apt-get update
RUN     apt-get -y install python
COPY ./opt/source code
ENTRYPOINT ["echo", "Hello"]
CMD [“Darwin”]
```

If we run the container without CLI parameters (`docker run Darwin`), it will echo the message `Hello, Darwin`.

Appending the command with a parameter, such as Username, will override the CMD instruction, and execute only the ENTRYPOINT instruction using the CLI parameters as arguments.

```sh
docker run Darwin User_JDArwin
```

will return the output:

```sh
Hello User_JDArwin
```

This is because the ENTRYPOINT instructions cannot be ignored, while with CMD, the command line arguments override the instruction.