---
title: "TODO"
author: [Sébastien Traber]
syntax: markdown
date: "TODO"
keywords: [TODO]
tags: [TODO]

---
    
# Archidep

## CommandLine

# Introduction

## [Command line](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/cli?home=MediaComem%2Fcomem-archidep%23readme)

### What a command line interface is, what a command is, and general command syntax.

__CLI (command line interface)__
un outils permettatn d'intéragir avec un ordinateur au moyen commandes textuelles permettant de se passer de la souris

__Commande__

Une commande est un mot qu'il faut entrer dans un CLI pour indiquer à l'ordinateur quoi faire.

```bash
nomDelaCommande argument1 argument2 argument3 ...
```
__Option vs argument__

Les options spécifie comment une commande doit se comporter. Par convention elles sont précédés par `-` ou `--` lorsque disponible.

```bash
man -h -v
man --help -version
man -hv
```

__Option avec valeur__

Certaines options requière une valeur. Dans cette exemple `compressed.tar.gz` est la valeur de l'option `-f`

```bash
tar -c -v -f compressed.tar.gz filename
```

### What the Unix paths `.`, `..` and `~` are.
### The difference between a relative and an absolute path.
### What the `PATH` is and how it works.
### What the following commands do and their basic syntax (not their options): `cd`, `ls`, `pwd`.

## [Secure Shell (SSH)](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/ssh?home=MediaComem%2Fcomem-archidep%23readme)
### What SSH is and what is is used for.
### The fact that establishing the secure channel and authenticating are 2 separate processes.
### The basic syntax of the SSH command: `ssh user@hostname`.
### The difference between password authentication and public key authentication,
### That when SSH warns you that host authenticity cannot be established the

# Version control

## [Version control with Git](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/git?home=MediaComem%2Fcomem-archidep%23readme)

### What version control is.
### What Git is and what its basic components are
### The basic Git workflow.
### The purpose (but not the syntax or options) of the main Git subcommands used to perform that workflow:

#### `git checkout`

#### `git add`

#### `git commit`

### The purpose (but not the syntax or options) of the other basic Git subcommands:

#### `git init`

#### `git log`

#### `git status`

### How to ignore files with Git.

## [Git branching](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/git-branching?home=MediaComem%2Fcomem-archidep%23readme)

### What Git branching is and why it is useful.
### That any repository has a main branch (usually called `main` or `master`).

## [Collaborating with Git](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/git-collaborating?home=MediaComem%2Fcomem-archidep%23readme)

### What a Git remote is.
### The purpose (but not the syntax or options) of the Git subcommands used to work with remotes:

#### `git clone`

#### `git push`

#### `git pull`

### The reasons why GitHub may refuse a push

# Security

## [Open Web Application Security Project][owasp]

## [OWASP Top 10 - The Ten Most Critical Web Application Security Risks][owasp-top10]

### That the OWASP Top 10 list exists and that it lists the ten most critical web application security risks.

# Basic deployment

## [Cloud computing](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/cloud?home=MediaComem%2Fcomem-archidep%23readme)

### What a client and a server is.
### The difference between types of web hosting
### What cloud computing is and why it is useful.
### What a public cloud is.
### What are the 3 most popular cloud service models (IaaS, PaaS and SaaS),

## [Linux](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/linux?home=MediaComem%2Fcomem-archidep%23readme)

### What Linux is and how it relates to Unix.
### That Ubuntu is a Linux operating system.

## [Unix basics & administration](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/unix-admin?home=MediaComem%2Fcomem-archidep%23readme)

### That Linux uses a case-sensitive file system by default.
### That Unix-like systems use a rooted file system and that the path of the root directory is `/`.
### What are users, groups and the superuser in a Unix-like system.
### How file permissions are represented (`r`, `w`, `x` and the concept of owner, group and others).
### What the `sudo` command is and how to use it.
### What the `/etc/sudoers` file is in principle.
### What the `chmod` and `chown` commands are in principle.

## [Unix processes](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/unix-processes?home=MediaComem%2Fcomem-archidep%23readme)

### What a process is.
### What a process ID is and what the `ps` command does.
### What an exit status is and what is the difference between and exit status
### What a Unix pipeline is and the syntax used to pipe commands together.
### What a Unix signal is and what the `kill` command does.

## [Unix networking](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/unix-networking?home=MediaComem%2Fcomem-archidep%23readme)

### What HTTP and TCP are and how they are related.
### What an IP address and a port is, and how they are related to TCP.
### What is the hostname `localhost` and the IP address `127.0.0.1`.
### What the standard HTTP(S) ports.
### What a well-known port or system port is and how they are different from other ports.
### What the Domain Name System (DNS) is.

## [APT](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/apt?home=MediaComem%2Fcomem-archidep%23readme)

### What APT is.

# Advanced deployment

## [Twelve-factor app][12factor]

### Why it is a good practice to store configuration in the environment rather

## [Unix environment variables](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/unix-env-vars?home=MediaComem%2Fcomem-archidep%23readme)

### What environment variables are and why they are useful.

## [Linux process management](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/linux-process-management?home=MediaComem%2Fcomem-archidep%23readme)

### What a process manager is and that operating systems usually have one built in.
### That Systemd is the standard process management tool on many Linux systems like Ubuntu.
### That Systemd uses unit files to configure process management.
### That you can use Systemd to control processes (start them, stop them, restart them, etc).

## [Domain Name System (DNS)](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/dns?home=MediaComem%2Fcomem-archidep%23readme)

### What the Domain Name System (DNS) is.
### What a DNS zone and a DNS zone file is.

## [Reverse proxying](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/reverse-proxy?home=MediaComem%2Fcomem-archidep%23readme)

### What a reverse proxy is.
### The main uses of a reverse proxy (hiding internal architecture or
### That nginx is a web server and reverse proxy.

## [TLS/SSL certificates](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/ssl?home=MediaComem%2Fcomem-archidep%23readme)

### What a TLS certificate is and what is is used for.
### Why a TLS certificate is considered valid or invalid.
### What a self-signed TLS certificate is.
### What a chain of trust is in the context of TLS certificates.
### What a root TLS certificate is.

#### What a trusted root certificate is.

### What domain validation is.

#### At least one method of domain validation.

### What Let's Encrypt and Certbot are in principle.

# Automated deployment

## [Shell scripting](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/shell-scripting?home=MediaComem%2Fcomem-archidep%23readme)

### What a shell script is.
### What a shebang is.

## [Git hooks](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/git-hooks?home=MediaComem%2Fcomem-archidep%23readme)

### What a Git hook is.

# Platform-as-a-Service (PaaS)

## [Heroku](https://mediacomem.github.io/comem-archidep/2021-2022/subjects/heroku?home=MediaComem%2Fcomem-archidep%23readme)

### What Heroku is and how the platform works on principle.
### That you can configure environment variables for your Heroku applications.

# Drawing a simple diagram
