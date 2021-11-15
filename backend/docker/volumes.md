# Docker volumes

Create a folder where all github projects will be storaged

example `myprojects` folder

Create a ubuntu container using current directory as its volume

```sh
broch-pc pj/myprojects/: docker run -it --name mycontainer --entrypoint=bash  -v "$(pwd):/home/" -w "/home/" ubuntu
```

Now update the ubuntu image and install gsit

```sh
# bash running inside container
root@20af6441e212:/home# apt update
root@20af6441e212:/home# apt install git -y

```

Now `myprojects` folder is the "same" folder as `/home` which is inside the container.


```sh
# Entering into container's bash
[broch-pc myprojects]: docker exec -it mycontainer bash

# inside the container
root@20af6441e212:/home# ls
some-github-project

# Creating a folder 
root@20af6441e212:/home# mkdir test

# Exiting from container
root@20af6441e212:/home# exit

# Checking if the test folder was created
[broch-pc myprojects]: ls
some-github-project  test

# Removing the test folder
[broch-pc myprojects]: rm -r test
[broch-pc myprojects]: ls
some-github-project

# Entering into container's bash again
[broch-pc myprojects]: docker exec -it mycontainer bash

# Checking if test folder was deleted
root@20af6441e212:/home# ls
some-github-project
# test folder was deleted
```