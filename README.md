# ConductorSample

To run Conductor (using docker), do:
1. Ensure you have docker and docker composer installed
1. Clone Conductor's code: 
```git clone https://github.com/Netflix/conductor.git``` or use the repo cloned by me (conductor folder inside this repo)
1.  Build the docker-compose file:
```cd conductor/docker``` and after: <br />
```docker-compose build```
1. Start the service: ```docker-compose up``` <br />
Please beware that at least 16gb ram are needed. Some additional 
services will also be started (as: elasticsearch, redis, rabbitmq and more)
1. On ```localhost:8080``` will be the conductor server application (which is an API). On ```localhost:5000``` 
will be available the conductor ui (web app to help managing the Conductor services) <br />
----
<br />

## Definition of a workflow: <br />

![A conductor workflow](/imgs/workflow-definition.png "Workflow") <br />
### The json definition of the Workflow:
```
{
  "createTime": 1680122442352,
  "updateTime": 1680190663514,
  "accessPolicy": {},
  "name": "WorkflowSample",
  "description": "Edit or extend this sample workflow. Set the workflow name to get started",
  "version": 5,
  "tasks": [
    {
      "name": "fetch some data",
      "taskReferenceName": "   ",
      "inputParameters": {
        "http_request": {
          "uri": "https://datausa.io/api/data?drilldowns=Nation&measures=Population",
          "method": "GET"
        }
      },
      "type": "HTTP",
      "startDelay": 0,
      "optional": false,
      "asyncComplete": false
    },
    {
      "name": "call microservice x",
      "taskReferenceName": "  ",
      "inputParameters": {
        "http_request": {
          "uri": "https://datausa.io/api/data?drilldowns=Nation&measures=Population",
          "method": "GET"
        }
      },
      "type": "HTTP",
      "startDelay": 0,
      "optional": false,
      "asyncComplete": false
    },
    {
      "name": "call microservice y",
      "taskReferenceName": " ",
      "inputParameters": {
        "http_request": {
          "uri": "https://datausa.io/api/data?drilldowns=Nation&measures=Population",
          "method": "GET"
        }
      },
      "type": "HTTP",
      "startDelay": 0,
      "optional": false,
      "asyncComplete": false
    }
  ],
  "inputParameters": [],
  "outputParameters": {
    "data": "${get_population_data.output.response.body.data}",
    "source": "${get_population_data.output.response.body.source}"
  },
  "schemaVersion": 2,
  "restartable": true,
  "workflowStatusListenerEnabled": false,
  "ownerEmail": "example@email.com",
  "timeoutPolicy": "ALERT_ONLY",
  "timeoutSeconds": 0,
  "variables": {},
  "inputTemplate": {}
}
```
-----
## Example of a workflow execution
![A conductor workflow execution](/imgs/workflow-execution.png "Workflow execution") <br />

---- 
## Available actions on a running workflow
![A conductor workflow possible actions](/imgs/workflow-actions.png "Workflow actions") <br />

