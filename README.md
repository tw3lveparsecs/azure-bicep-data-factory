# Azure Data Factory
This module will create an Azure Data Factory.

You can optionally configure system/user assigned identities, Git configuration, managed virtual network and integration runtime, diagnostics and resource lock.
## Usage

### Example 1 - Data Factory with Azure DevOps Git configuration
``` bicep
param deploymentName string = 'adf${utcNow()}'
param location string = resourceGroup().location

module dataFactory 'datafactory.bicep' = {
  name: deploymentName
  params: {
    dataFactoryName: 'myDataFactoryName'    
    location: location        
    configureGit: true
    gitRepoType: 'FactoryVSTSConfiguration'
    gitAccountName: 'MyDevOpsOrgName'
    gitProjectName: 'MyDevOpsProjectName'
    gitRepositoryName: 'MyDevOpsRepoName'
  }
}
```

### Example 2 - Data Factory with GitHub Git configuration
``` bicep
param deploymentName string = 'adf${utcNow()}'
param location string = resourceGroup().location

module dataFactory 'datafactory.bicep' = {
  name: deploymentName
  params: {
    dataFactoryName: 'myDataFactoryName'    
    location: location        
    configureGit: true    
    gitRepoType: 'FactoryGitHubConfiguration'
    gitAccountName: 'MyGitHubUsername'
    gitRepositoryName: 'MyGitHubReponame'
  }
}
```

### Example 3 - Data Factory with managed virtual network, managed virtual network integration runtime and no public access
``` bicep
param deploymentName string = 'adf${utcNow()}'
param location string = resourceGroup().location

module dataFactory 'datafactory.bicep' = {
  name: deploymentName
  params: {
    dataFactoryName: 'myDataFactoryName'
    enableManagedVirtualNetwork: true
    location: location
    enableManagedVnetIntegrationRuntime: true
    publicNetworkAccess: false
  }
}