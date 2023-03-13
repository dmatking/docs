# coder workspaces create

create a new workspace.

### Synopsis

Create a new Coder workspace.

```text
coder workspaces create [workspace_name] [flags]
```

### Examples

```text
# create a new workspace using default resource amounts
coder workspaces create my-new-workspace --image ubuntu
coder workspaces create my-new-powerful-workspace --cpu 12 --disk 100 --memory 16 --image ubuntu
```

### Options

```text
      --container-based-vm   deploy the workspace as a Container-based VM
  -c, --cpu float32          number of cpu cores the workspace should be provisioned with.
  -d, --disk int             GB of disk storage a workspace should be provisioned with.
      --enable-autostart     automatically start this workspace at your preferred time.
      --follow               follow buildlog after initiating rebuild
  -g, --gpus int             number GPUs a workspace should be provisioned with.
  -h, --help                 help for create
  -i, --image string         name of the image to base the workspace off of.
  -m, --memory float32       GB of RAM a workspace should be provisioned with.
  -o, --org string           name of the organization the workspace should be created under.
      --provider string      name of Workspace Provider with which to create the workspace
  -t, --tag string           tag of the image the workspace will be based off of. (default "latest")
      --user string          Specify the user whose resources to target. This flag can only be used by admins and managers. Input an email or user id. (default "me")
```

### Options inherited from parent commands

```text
  -v, --verbose   show verbose output
```

### SEE ALSO

- [coder workspaces](coder_workspaces.md) - Interact with Coder workspaces
