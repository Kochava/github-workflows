# Kochava Github Action Workflows

This repo contains GitHub Action Workflow Templates for Kochava's various workflows

## Workflow Types

| Workflow Type | File Prefix | Tag Format        | Description                                                                                                                                                                                             |
|---------------|-------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Go App        | go_app      | go/app/{version}  | Used for Go application projects intended to be deployed as a Docker image. Tests/Lints on PRs, Creates a Release based on conventional commits when merged to main, Publishes Docker image on Release. |
| Go Library    | go_lib      | go/lib/{version}  | Used for Go library projects intended to be imported. Tests/Lints on PRs, Creates a Release based on conventional commits when merged to main.                                                          |
| PHP Library   | php_lib     | php/lib/{version} | Used for PHP library projects intended to be imported. Tests/Lints on PRs, Creates a Release based on conventional commits when merged to main.                                                         |
| Java Library   | java_app     | java/app/{version} | Used for Java application projects intended to be deployed as a Jar file. Tests/Lints on PRs, Creates a Release based on conventional commits when merged to main.                                                         |

## Versioning

In order to protect workflow users from having their workflows break, we must carefully consider versioning. Tags should be prefixed by a workflow type. 

- example: `go/app/v1.0.0`

This will allow repositories that use this templates to choose tags accordingly and know when there might be breaking changes with the way they use the worklflow by checking the major version.

There should also be tags that are updated after every update to a major version.

- example: `go/app/v1`

This will allow users to specify a major version and always be up to date with minor updates.

As such, whenever changes are made to workflow templates and a tag is to be created, the major version should increment if there are any major changes to a workflow. This is up to the discresion of the person making the tag, but some possible reasons to increment the major version include but are not limited to:
 - major behavior for a workflow is changed in a way that will no longer satisfy a user of that template
   * example: no longer publishing a docker image to a place it would have published before with the same inputs.
   * exeption example: adding a `go vet` step to the go app workflows since we may want to enforce all workflows that fail this to immediately fix their code.
 - an input/secret/output is removed
 - possible input/secret values that worked before will no longer work or result in different intended behavior.
