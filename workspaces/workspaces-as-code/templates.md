---
title: "Workspace templates"
description: "Learn how to write a template for creating workspaces."
state: beta
---

Workspaces as code (WAC) allows you to define and create new workspaces using
**workspace templates**.

Workspace templates are written as YAML and have a `.yaml` or `.yml` extension.
Coder looks for your workspace template at the following path:

```text
<repository-root>/.coder/<template-name>.yaml
```

![Template Location](../../assets/wac-location.png)

## Workspace template sample

The following is a sample workspace template that makes use of all available
fields. Depending on your use case, you may not need all of the options
available.

> Note that the fields are **case-sensitive**.

For detailed information on the fields available, see the
[subsequent sections](#workspace-template-fields) of this article

```yaml
version: 0.2
workspace:
  type: kubernetes
  spec:
    image: index.docker.io/ubuntu:18.04
    container-based-vm: true
    cpu: 4
    memory: 16
    disk: 128
    gpu-count: 1
    labels:
      com.coder.custom.hello: "hello"
      com.coder.custom.world: "world"
  configure:
    start:
      - name: "install curl"
        command: |
          apt update
          apt install -y curl
      - name: "install Go binary"
        command: "go install"
        directory: /home/coder/go/src/github.com/my-project
        shell: "bash"
        env:
          GOPATH: /home/coder/go
  devURLs:
    - name: MyWebsite
      port: 3000
      scheme: http
      access: private
    - name: PublicPort
      port: 8080
      scheme: https
      access: public
    - name: OrgWebsite
      port: 3001
      scheme: http
      access: org
    - name: AuthedSite
      port: 8081
      scheme: https
      access: authed
```

## Workspace template fields

### version

The version number of the config file being used. The current version is `0.2`.

### workspace

**Required**. The section containing all configuration information related to
the workspace.

#### workspace.type

**Required**. Determines the type of workspace to be created. Currently, the
only accepted value is `kubernetes`.

#### workspace.spec

**Required**. This section contains configuration information specific to the
`workspace.type`.

#### workspace.spec.image

**Required**. The image to use for the workspace. The image should include the
registry and (optionally) the tag, i.e. `docker.io/ubuntu:18.04`. If you omit
the tag, Coder uses the default value of `latest`.

You must have [imported the image](../../images/importing.md) into Coder,
otherwise, the workspace will fail to build.

#### workspace.spec.labels

The
[Kubernetes labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)
to be added to the workspace pod.

```yaml
workspace:
  labels:
    com.coder.custom.hello: hello
    com.coder.custom.world: world
```

#### workspace.spec.gpu-count

The number of GPUs to allocate to the workspace.

#### workspace.spec.container-based-vm

Determines whether the workspace should be created as a
[container-based virtual machine (CVM)](../cvms.md). Default is `false`.

#### workspace.spec.cpu

**Required**. The number of cores to allocate to the workspace.

#### workspace.spec.memory

**Required**. The amount of memory (in GB) to allocate to the workspace.

#### workspace.spec.disk

**Required**. The amount of disk space (in GB) to allocate to the workspace.

#### workspace.configure

This section lists the commands that run within the workspace after Coder builds
the workspace. See [Configure](../../images/configure.md) for more information.

#### workspace.configure.start

The list of commands to run when Coder _starts_ a workspace.

#### workspace.configure.start[*].command

**Required**. Runs the provided command within the workspace (Coder supports the
use of both single-line and multi-line commands).

- Single-line command:

  ```yaml
  - name: Install curl
    command: apt install -y curl
  ```

- Multi-line command:

  ```yaml
  - name: Update and install curl
    command: |
      apt update
      apt install -y curl
  ```

#### workspace.configure.start[*].name

The name of the command being run.

#### workspace.configure.start[*].shell

The shell Coder should use to run the command.

```yaml
start:
  - name: First step
    shell: /bin/bash
```

#### workspace.configure.start[*].directory

The working directory from which Coder should run the command.

```yaml
start:
  - name: First step
    directory: /home/coder
```

#### workspace.configure.start[*].env

The map of environment variables to set for the command.

```yaml
start:
  - name: First step
    env:
      HOME: /home/coder
      GOPATH: /home/coder/go
```

#### workspace.devURLs

This list allows you to provision [dev URLs](../devurls.md) using the workspaces
as code configuration file. The dev URLs will be provisioned _in addition to_
any dev URLs you create.

```yaml
devURLs:
  - name: PublicPort
    port: 8080
    scheme: https
    access: public
```

#### workspace.devURLs[*].name

The name of the dev URL to be created.

#### workspace.devURLs[*].port

The workspace port that the dev URL exposes.

#### workspace.devURLs[*].scheme

The URL scheme (protocol) to use (i.e., `http` or `https`).

#### workspace.devURLs[*].access

The permission level of the dev URL:

- **private**: Can only be accessed by the owner of the workspace
- **org**: Can be accessed by all members of the organization to which the
  workspace belongs
- **authed**: Can be accessed by all users on the Coder deployment
- **public**: Can be accessed by anyone on the internet
