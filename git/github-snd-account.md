# Using a second Github account

## Setting up Git and github

### First method

Go inside project's folder

`git remote set-url origin https://github.com/freeconhecimento/freebr.git/`

`git config --get remote.origin.url`

`git config user.name <second-account-username>`

`git config user.email <second-account-username>`

`git config credential.username <second-account-username>`


### Second method

Change config file inside `.git` folder

```git
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[remote "origin"]
        url = https://github.com/broch/freebs.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
        remote = origin
        merge = refs/heads/main
```

Add the new user name and email

```
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[user]
        name = freeconhecimento
        email = culturafitblog@gmail.com
[remote "origin"]
        url = https://github.com/freeconhecimento/freebr.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
        remote = origin
        merge = refs/heads/main

```

`git config credential.username <second-account-username>`