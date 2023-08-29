# ApiJobsVariables

## Pipeline Requirements

The setVariable pipeline requires the following parameters to be defined:
Paramaters:


| Name  | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| appDeploymentTarget | string | | | Required | |
| key | string | | | Required | |
| apiJobBatchSchedulerAKSApps | string | | | Optional | |
| apiJobBatchSchedulerWorkloadName | string | | | Optional | |
| apiJobEventDispatcherAKSApps | string | | | Optional | |
| apiJobEventDispatcherWorkloadName | string | | | Optional | |
| apiJobEventReprocessAKSApps | string | | | Optional | |
| apiJobEventReprocessWorkloadName | string | | | Optional | |
| apiJobClaimsMigrationUtilityJobAKSApps | string | | | Optional | |
| apiJobClaimsMigrationUtilityJobWorkloadName | string | | | Optional | |
| apiJobClaimsMigrationUtilityPurgeJobAKSApps | string | | | Optional | |
| apiJobClaimsMigrationUtilityPurgeJobWorkloadNam | string | | | Optional | |
| apiJobDiagnosticServiceAKSApps | string | | | Optional | |
| apiJobDiagnosticServiceWorkloadName | string | | | Optional | |
| apiJobClaimsAssignmentHistoryPurgeJobAKSApps | string | | | Optional | |
| apiJobClaimsAssignmentHistoryPurgeJobWorkloadName | string | | | Optional | |
| enableApiJobsVariables | boolean | 'true' | 'true'/'false' | Required | |

  These parameters provide multiple use case options for the setvariables templates pipeline, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

### Direct use of a template

You can directly call a particular template as per the requirement. for example: 

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name:  your_username/Repo_name
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'



  steps:
  # passing the parameters
  - template: templates/setApiJobsVariables.yml@Template
      parameters:
        appDeploymentTarget: ${{parameters.appDeploymentTarget}}
        key: ${{parameters.key}}
        apiJobBatchSchedulerAKSApps: ${{ parameters.apiJobBatchSchedulerAKSApps}}
        apiJobBatchSchedulerWorkloadName: ${{ parameters.apiJobBatchSchedulerWorkloadName}}
        apiJobEventDispatcherAKSApps: ${{ parameters.apiJobEventDispatcherAKSApps}}
        apiJobEventDispatcherWorkloadName: ${{ parameters.apiJobEventDispatcherWorkloadName}}
        apiJobEventReprocessAKSApps: ${{ parameters.apiJobEventReprocessAKSApps}}
        apiJobEventReprocessWorkloadName: ${{ parameters.apiJobEventReprocessWorkloadName}}
        apiJobClaimsMigrationUtilityJobAKSApps: ${{ parameters.apiJobClaimsMigrationUtilityJobAKSApps}}
        apiJobClaimsMigrationUtilityJobWorkloadName: ${{ parameters.apiJobClaimsMigrationUtilityJobWorkloadName}}
        apiJobClaimsMigrationUtilityPurgeJobAKSApps: ${{ parameters.apiJobClaimsMigrationUtilityPurgeJobAKSApps}}
        apiJobClaimsMigrationUtilityPurgeJobWorkloadName: ${{ parameters.apiJobClaimsMigrationUtilityPurgeJobWorkloadName}}
        apiJobDiagnosticServiceAKSApps: ${{ parameters.apiJobDiagnosticServiceAKSApps}}
        apiJobDiagnosticServiceWorkloadName: ${{ parameters.apiJobDiagnosticServiceWorkloadName}}
        apiJobClaimsAssignmentHistoryPurgeJobAKSApps: ${{ parameters.apiJobClaimsAssignmentHistoryPurgeJobAKSApps}}
        apiJobClaimsAssignmentHistoryPurgeJobWorkloadName: ${{ parameters.apiJobClaimsAssignmentHistoryPurgeJobWorkloadName}}

  # passing the variables as parameters
  - template: templates/setApiJobsVariables.yml@Template
      parameters:
        appDeploymentTarget: ${{parameters.appDeploymentTarget}}
        key: ${{parameters.key}}
        apiJobBatchSchedulerAKSApps: claims-batch-apijob-$(claims.batchScheduler.blueGreenEnv)
        apiJobBatchSchedulerWorkloadName: claims-batch-apijob
        apiJobEventDispatcherAKSApps: claims-ep-apijob-$(claims.eventDispatcher.blueGreenEnv)
        apiJobEventDispatcherWorkloadName: claims-ep-apijob
        apiJobEventReprocessAKSApps: claims-epreprocess-apijob-$(claims.eventReprocess.blueGreenEnv)
        apiJobEventReprocessWorkloadName: claims-epreprocess-apijob
        apiJobClaimsMigrationUtilityJobAKSApps: claims-migrationapi-apijob-$(claims.migrationUtilityJob.blueGreenEnv)
        apiJobClaimsMigrationUtilityJobWorkloadName: claims-migrationapi-apijob
        apiJobClaimsMigrationUtilityPurgeJobAKSApps: claims-migrationpurgeapi-apijob-$(claims.migrationUtilityPurgeJob.blueGreenEnv)
        apiJobClaimsMigrationUtilityPurgeJobWorkloadName: claims-migrationpurgeapi-apijob
        apiJobDiagnosticServiceAKSApps: claims-diagservice-apijob-$(claims.diagservice.blueGreenEnv)
        apiJobDiagnosticServiceWorkloadName: claims-diagservice-apijob
        apiJobClaimsAssignmentHistoryPurgeJobAKSApps: claims-assignmenthistorypurge-apijob-$(claims.assignmentHistoryPurgeJob.blueGreenEnv)
        apiJobClaimsAssignmentHistoryPurgeJobWorkloadName: claims-assignmenthistorypurge-apijob
  
 

Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.

  ```
