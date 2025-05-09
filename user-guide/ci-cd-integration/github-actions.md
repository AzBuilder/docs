# Github Actions

Integrate Terrakube with GitHub Actions is easy and you can handle your workspace from GitHub.

The GIT repository will represent a Terrakube Organization and each folder inside the repository will be a new workspace.

There is an example available in the following [link](https://github.com/AzBuilder/terraform-sample-repository)

### Configuration

Add the following snippet to the script section of your github actions file:

#### Pull Request example

To run a terraform plan using Terrakube templates use the following example:

> File: .github/workflows/pull\_request.yml

```
name: Terrakube Plan

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  build:
    runs-on: ubuntu-latest
    name: "Running Terrakube Plan"
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - uses: AzBuilder/terrakube-action-github@main
        with:
          TERRAKUBE_TOKEN:  ${{ secrets.TERRAKUBE_PAT }} 
          TERRAKUBE_TEMPLATE: "Terraform-Plan"
          TERRAKUBE_ENDPOINT: ${{ secrets.TERRAKUBE_ENDPOINT }}  
          TERRAKUBE_BRANCH: ${{ github.head_ref }}
          TERRAKUBE_ORGANIZATION: "terrakube_organization_name"
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          SHOW_OUTPUT: true
```

> A new workspace will be created for each folder with the file "terrakube.json". For each PR only new folders or folders that has been updated will be evaluated inside Terrakube.

#### Push Main branch

To run a terraform apply using Terrakube templates use the following example:

> File: .github/workflows/push\_main.yml

```
name: Terrakube Apply

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    name: "Running Terrakube Apply"
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - uses: AzBuilder/terrakube-action-github@main
        with:
          TERRAKUBE_TOKEN:  ${{ secrets.TERRAKUBE_PAT }} 
          TERRAKUBE_TEMPLATE: "Terraform-Plan/Apply"
          TERRAKUBE_ENDPOINT: ${{ secrets.TERRAKUBE_GITPOD }}  
          TERRAKUBE_BRANCH: "main"
          TERRAKUBE_ORGANIZATION: "terrakube_organization_name"
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          SHOW_OUTPUT: false
```

### Terrakube Variables

To define terrakube variables to connect to cloud providers it is recommended to use Global Variables inside the organization using the UI. Terraform variables could be define inside a terraform.tfvars inside each folder or you can define inside the Terrakube UI after the workspace creation.

### GitHub Action Inputs

| Variable                     | Usage                                                                                |
|------------------------------| ------------------------------------------------------------------------------------ |
| TERRAKUBE\_TOKEN (\*)        | Terrakube Personal Access Token                                                      |
| TERRAKUBE\_TEMPLATE (\*)     | Terrakube template name                                                              |
| TERRAKUBE\_ENDPOINT (\*)     | Terrakbue api endpoint                                                               |
| TERRAKUBE\_ORGANIZATION (\*) | Terrakbue organization                                                               |
| TERRAKUBE\_BRANCH (\*)       | Github Branch when running a job                                                     |
| TERRAKUBE\_SSH\_KEY\_NAME    | ssh key name define in the terrakube organization to connect to private repositories |
| GITHUB\_TOKEN (\*)           | Github Token                                                                         |
| SHOW\_OUTPUT (\*)            | Show terrakube logs inside PR comments                                               |

_(\*) = required variable._

### Terraform Workspace Configuration

Create a file called "terrakube.json"; includes workspace name and the terraform version that will be used for the job execution.

```
{
    "workspace": "workspaceA"
    "terraform": "1.2.9"
}
```

### Build GitHub Action

To build the github action in your local machine use the following.

```
git clone https://github.com/AzBuilder/terrakube-action-github.git
yarn install
yarn build
```

