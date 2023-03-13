# coder workspaces policy-template

Set workspace policy template

### Synopsis

Set workspace policy template or restore to default configuration. This feature
is for site admins only.

```text
coder workspaces policy-template [flags]
```

### Options

```text
      --default           Restore policy template to default configuration
      --dry-run           skip setting policy template, but view errors/warnings about how this policy template would impact existing workspaces
  -f, --filepath string   full path to local policy template file.
  -h, --help              help for policy-template
      --scope string      scope of impact for the policy template. Supported values: site (default "site")
```

### Options inherited from parent commands

```text
  -v, --verbose   show verbose output
```

### SEE ALSO

- [coder workspaces](coder_workspaces.md) - Interact with Coder workspaces
