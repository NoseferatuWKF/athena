# Brief Comparison

| Terraform                        | Pulumi                           | Crossplane                         |
| -------------------------------- | -------------------------------- | ---------------------------------- |
| Declarative                      | *Imperative                      | Declarative                        |
| Agnostic                         | Agnostic                         | Kubernetes native                  |
| Medium                           | Easy                             | Hard                               |
| Good documentation and community | Good documentation and community | Decent documentation and community |
| More boilerplate                 | Less boilerplate                 | More boilerplate                   |

# Getting Started

installation
```bash
curl -fsSL https://get.pulumi.com | sh
# check installation, may need to restart shell
pulumi version
```

tldr
```bash
# local only
pulumi login -l
# create new pulumi project, with premade stack
pulumi new
# create a new stack
pulumi stack init <name>
# dry run
pulumi preview
# deploy
pulumi up
```

login
```bash
# use pulumi cloud
pulumi login
# use local fs, pointed to ~/.pulumi
pulumi login -l
# use local fs, with path
pulumi login file:///path/to/backend
# GCP backend
pulumi login gs://<bucket>
```

config
```bash
pulumi config set <key> <value>
pulumi config get <key>
# set structured value
pulumi config set --path 'parent.child' <value>
# set secret with path
pulumi config set --secret --path 'sql.dbPassword' <value>
```

refresh
```bash
# only show the preview without changing the local state
pulumi refresh --preview-only
# show detailed diffs
pulumi refresh --diff
# print error if there is drift
pulumi refresh --expect-no-changes
```

state
```bash
# delete a resource in a stack
pulumi state delete <urn> 
# rename a resource
pulumi state rename <urn>
# move resource to a different stack
pulumi state move <urn> --source <from> --dest <to>
```

stack
```bash
# create new stack with fully qualified name
pulumi stack init orgName/projectName/stackName
# list stacks under current project
pulumi stack ls
# change active stack
pulumi stack select orgName/projectName/stackName
# check current selected stack
pulumi stack
# deploy/update stack
pulumi up
# get output values from stack
pulumi stack output --json
# get decrypted secret output
pulumi stack output <name> --show-secrets
# import stack deployment
pulumi stack import --file /path/to/stack.json
# export stack deployment
pulumi stack export --file /path/to/stack.json
# destroy stack resources
pulumi destroy
# remove stack
pulumi stack rm
# change secret provider
pulumi stack change-secrets-provider <provider>
```

[Pulumi.yaml](https://www.pulumi.com/docs/iac/concepts/projects/project-file/#pulumi-project-file-reference)
```yaml
name: Example Pulumi project file with all possible attributes
runtime: yaml
description: An example project with all attributes
main: example-project/
stackConfigDir: config/
backend:
  url: https://pulumi.example.com
options:
  refresh: always
template:
  displayName: Example Template
  description: An example template
  config:
    aws:region:
      description: The AWS region to deploy into
      default: us-east-1
      secret: true
  metadata:
    cloud: aws
plugins:
  providers:
    - name: aws
      path: ../../bin
  languages:
    - name: yaml
      path: ../../../pulumi-yaml/bin
      version: 1.2.3
```

# Stack

valid naming convention
- `orgName/projectName/stackName`
- `orgName/stackName`
- `stackName`

get stack name
```go
stack := ctx.Stack()
```

stack output
```go
ctx.Export("x", pulumi.String("hello"))
```

reading output from stack references
```go
infra, err := pulumi.NewStackReference(ctx, ...)
if err != nil {
    return err
}
ip := infra.GetOutput("privateIp")
logKey := ip.ApplyT(func(ip string) string {
    return fmt.Sprintf("logs/%s.log", ip)
}).(StringOutput)
logFile := s3.NewBucketObject(ctx, "log", &s3.BucketObjectArgs{
    // ...
    Key: logKey,
})
```

# Use Case

existing resources
>[!hint]
>Usually theres are import section on the provider documentation with an example command
```bash
pulumi import <type> <name> <id>
# copy the code generated and run
pulumi up
# to remove the existing resource, first need to remove protection
pulumi state unprotect <urn>
# or directly unprotect the resource during importing
pulumi import --protect false <type> <name> <id>
```

migrating between backends
```bash
# switch to the backend/stack we want to export
pulumi login -l
pulumi stack select my-app-production
# export the stack's state to a local file
pulumi stack export --show-secrets --file my-app-production.stack.json
# logout and login to the desired new backend
pulumi logout
pulumi login # default to Pulumi Cloud
# create a new stack with the same name on pulumi.com
pulumi stack init my-app-production
# import the new existing state into pulumi.com
pulumi stack import --file my-app-production.stack.json
```

stack output
stack references

# Topology

outputs
secrets

[Organizing Projects Stacks](https://www.pulumi.com/docs/iac/using-pulumi/organizing-projects-stacks/)
