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

state & backends
```bash
# use local fs, pointed to ~/.pulumi
pulumi login -l
# use local fs, with path
pulumi login file:///path/to/backend
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

# stacks

commands
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
```

stack output
stack references

# Topology

outputs
secrets