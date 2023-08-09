# Run a Sophos Factory Pipeline

A GitHub Action for triggering a Sophos Factory pipeline.

This action runs Sophos Factory pipelines right from GitHub Actions, enabling you to execute pipelines as a result of GitHub commits, pull requests, and other GitHub triggers.

## Prerequisites

* An existing GitHub repository for which you want to use this Action.
* An existing Sophos Factory project containing a pipeline and an associated job.
* A Sophos Factory API token.
    * API tokens can be generated from the Sophos Factory application by visiting the Account Settings page.
    * Add the token as a [GitHub Secret in your repository](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository) (e.g. with name `API_TOKEN`) and supply this secret to the GitHub Action environment as demonstrated in the example below.

## Example Usage

```yaml
on:
  pull_request:
    branches:
      - master
  push:
    branches:
      - master

jobs:
  test:
    runs-on: ubuntu-latest
    name: Run Sophos Factory pipeline
    steps:
      - uses: actions/checkout@v3
      - uses: sophos/factory-run-pipeline@master
        with:
          project_id: # Your Project ID
          job_id: # Your Job ID
          api_token: ${{ secrets.API_TOKEN }}
          variables: '{ "my_var": "value" }'
```

## Inputs

| Input        | Description                                                                                                             | Required |              Default              |
| ------------ | ----------------------------------------------------------------------------------------------------------------------- | :------: | :-------------------------------: |
| `project_id` | ID of the project containing the job to run.                                                                            |   yes    |                 -                 |
| `job_id`     | ID of the Job to run                                                                                                    |   yes    |                 -                 |
| `api_token`  | Sophos Factory API token                                                                                                |   yes    |                 -                 |
| `variables`  | Input variables for the Job. The variables must be in a form of stringified JSON object, e.g. `'{ "my_var": "value" }'` |    no    |                 -                 |
| `api_url`    | Sophos Factory API base URL. Most users will not need to set this value.                                                |    no    | https://api.factory.sophos.com/v1 |

## Outputs

The Action will report if the job run was successful. If the job run fails, the Action will report a failure. The output events from the run are streamed to the Action console.

## Terms of Use

Please see [Sophos Services Agreement](https://www.sophos.com/en-us/legal/sophos-services-agreement.aspx) and [Sophos Privacy Notice](https://www.sophos.com/en-us/legal/sophos-group-privacy-notice.aspx).

