# Developer Knowledge Extension

This extension connects Gemini CLI with the Developer Knowledge MCP server.

## Install

To use this extension, you must enable the Developer Knowledge API and MCP
service on your Cloud project.

1. Create a Google Cloud project.

2. Enable the Developer Knowledge API on your project:

  ```
  gcloud services enable developerknowledge.googleapis.com --project=$PROJECT_ID
  ```

3. Enable the Developer Knowledge MCP service:

  ```
  gcloud beta services mcp enable developerknowledge.googleapis.com --project=$PROJECT_ID
  ```

4. Log in with `gcloud` with the required scopes:

  ```
  gcloud auth application-default login --scopes=https://www.googleapis.com/auth/devprofiles.full_control,https://www.googleapis.com/auth/cloud-platform
  ```

5. Install the extension.

## Disclaimer

This is not an officially supported Google product. This project is not
eligible for the [Google Open Source Software Vulnerability Rewards
Program](https://bughunters.google.com/open-source-security).

