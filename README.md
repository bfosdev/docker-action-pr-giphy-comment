# docker-action-pr-giphy-comment

This repository contains a custom GitHub Action designed to automatically comment on pull requests with a randomly selected "Thank You" GIF from Giphy. It's implemented using a Docker container and a shell script.



📁 Repository Structure
.github/workflows/

main.yml: Defines the workflow that triggers the custom action.

Dockerfile: Sets up the Docker environment for the action.

action.yml: Metadata file that defines the inputs, outputs, and main entrypoint for the action.

entrypoint.sh: Shell script executed by the Docker container to perform the action's logic.

README.md: Provides a brief description of the repository.



⚙️ Workflow: .github/workflows/main.yml
Trigger: The workflow is triggered on pull_request events.

Jobs:

add-giphy-comment:

Runs-on: ubuntu-latest

Steps:

Checkout Repository:

Uses actions/checkout@v4 to clone the repository.

Run Custom Action:

Uses the custom action defined in the repository (uses: ./.).

Passes the following inputs:

GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

GIPHY_API_KEY: ${{ secrets.GIPHY_API_KEY }}




🐳 Dockerfile
The Dockerfile sets up the environment for the custom action:

Base Image: alpine:3.18

Installs:

curl: For making HTTP requests.

jq: For parsing JSON responses.

Copies:

entrypoint.sh into the container.

Entrypoint:

Sets entrypoint.sh as the default command to run.




📝 action.yml
Defines the custom action's metadata:

Name: Add Giphy Comment

Description: Adds a random "Thank You" GIF comment to a pull request.

Inputs:

GITHUB_TOKEN: Required. Used for authentication with the GitHub API.

GIPHY_API_KEY: Required. Used to fetch GIFs from Giphy.

Runs:

Using: docker

Image: Dockerfile




🔧 entrypoint.sh
Shell script that performs the action's main logic:

Retrieve Inputs:

Reads GITHUB_TOKEN and GIPHY_API_KEY from the action's inputs.

Extract Pull Request Number:

Parses the GitHub event payload to get the PR number.

Fetch Random GIF:

Uses the Giphy API to fetch a random "Thank You" GIF.

Post Comment:

Constructs a comment containing the GIF.

Posts the comment to the pull request using the GitHub API.




🔑 Secrets Required
GITHUB_TOKEN: Automatically provided by GitHub Actions. Used for authentication with the GitHub API.

GIPHY_API_KEY: Must be added to the repository's secrets. Used to authenticate requests to the Giphy API.




🧪 Usage
Add the Workflow:

Create a .github/workflows/main.yml file with the workflow configuration as shown above.

Set Secrets:

Add GIPHY_API_KEY to your repository's secrets.

Trigger the Workflow:

Open or update a pull request to trigger the workflow and see the GIF comment.
