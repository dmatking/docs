# coder workspaces edit-from-config

change the template a workspace is tracking

### Synopsis

Edit an existing Coder workspace using a workspace template.

```text
coder workspaces edit-from-config [flags]
```

### Examples

```text
# edit a new workspace from git repository
coder workspaces edit-from-config dev-env --repo-url https://github.com/cdr/m --ref my-branch
coder workspaces edit-from-config dev-env --filepath coder.yaml
```

### Options

```text
  -f, --filepath string   path to local template file.
      --follow            follow buildlog after initiating rebuild
  -h, --help              help for edit-from-config
```

### Options inherited from parent commands

```text
  -v, --verbose   show verbose output
```

### SEE ALSO

- [coder workspaces](coder_workspaces.md) - Interact with Coder workspaces
