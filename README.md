# Azure Pipelines
## Introduction
What initially started as having a collection of Azure DevOps Pipelines Task Groups has changed to Step Templates.  These templates can be referenced from various pipelines (including Azure Pipelines YAML build files in various Repos).

## Using
The simplist way to reference these templates is to use the following in your YAML files (e.g., azure-pipelines.yml):

'''
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
'''

## Resources
[https://docs.microsoft.com/en-us/azure/devops/pipelines/process/templates?view=azure-devops](Microsoft Documentation on Pipelines Step Templates)
