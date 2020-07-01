# Azure Pipelines
## Introduction
What initially started as having a collection of Azure DevOps Pipelines Task Groups has changed to Step Templates.  These templates can be referenced from various pipelines (including Azure Pipelines YAML build files in various Repos).

## Using
The simplist way to reference these templates is to use the following in your YAML files (e.g., azure-pipelines.yml):

```
resources:
  repositories:
    - repository: templates
      type: github
      name: daikinapplied/Azure-Pipelines
      endpoint: my-service-connect-to-github # Azure DevOps service connection

steps:
- template: replace-token.yml@templates
  parameters:
    DisplayName: '[Replace Token: SQL Connection String]'
    FileWithPath: 'webapp\web.config'
    BackupFileExtension: 'original'
    RestoreBackup: 'no'
    TokenString: '$DBCONNSTR'
    TokenValue: '$(my-app-connectionstring)' # Could come from Azure Vault or Variable in Pipeline Build or Release
```

Some additional notes:
1. The **name** referencing *daikinapplied/Azure-Pipelines* within the resources is the GitHub company and repo
2. The **repository** *templates* is cross-referenced within the template mentioned with the yml file

## Resources
[Microsoft Documentation on Pipelines Step Templates](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/templates?view=azure-devops)
