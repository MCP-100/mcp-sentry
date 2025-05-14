[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/mcp-100-mcp-sentry-badge.png)](https://mseep.ai/app/mcp-100-mcp-sentry)

# mcp-sentry: A Sentry MCP server

[![smithery badge](https://smithery.ai/badge/@qianniuspace/mcp-sentry)](https://smithery.ai/server/@qianniuspace/mcp-sentry)

## Overview

A Model Context Protocol server for retrieving and analyzing issues from Sentry.io. This server provides tools to inspect error reports, stacktraces, and other debugging information from your Sentry account.

### Tools

1. `get_sentry_issue`
   - Retrieve and analyze a Sentry issue by ID or URL
   - Input:
     - `issue_id_or_url` (string): Sentry issue ID or URL to analyze
   - Returns: Issue details including:
     - Title
     - Issue ID
     - Status
     - Level
     - First seen timestamp
     - Last seen timestamp
     - Event count
     - Full stacktrace
2. `get_list_issues`
   - Retrieve and analyze Sentry issues by project slug
   - Input:
     - `project_slug` (string): Sentry project slug to analyze
     - `organization_slug` (string): Sentry organization slug to analyze
   - Returns: List of issues with details including:
     - Title
     - Issue ID
     - Status
     - Level
     - First seen timestamp
     - Last seen timestamp
     - Event count
     - Basic issue information

### Prompts

1. `sentry-issue`
   - Retrieve issue details from Sentry
   - Input:
     - `issue_id_or_url` (string): Sentry issue ID or URL
   - Returns: Formatted issue details as conversation context

## Installation

### Installing via Smithery

To install mcp-sentry for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@qianniuspace/mcp-sentry):

```bash
npx -y @smithery/cli install @qianniuspace/mcp-sentry --client claude
```

### Using uv (recommended)

When using [`uv`](https://docs.astral.sh/uv/) no specific installation is needed. We will
use [`uvx`](https://docs.astral.sh/uv/guides/tools/) to directly run *mcp-sentry*.

### Using PIP

Alternatively you can install `mcp-sentry` via pip:

```
pip install mcp-sentry
```

or use uv
```
uv pip install -e .
```

After installation, you can run it as a script using:

```
python -m mcp_sentry
```

## Configuration

### Usage with Claude Desktop

Add this to your `claude_desktop_config.json`:

<details>
<summary>Using uvx</summary>

```json
"mcpServers": {
  "sentry": {
    "command": "uvx",
    "args": ["mcp-sentry", "--auth-token", "YOUR_SENTRY_TOKEN","--project-slug" ,"YOUR_PROJECT_SLUG", "--organization-slug","YOUR_ORGANIZATION_SLUG"]
  }
}
```
</details>


<details>
<summary>Using docker</summary>

```json
"mcpServers": {
  "sentry": {
    "command": "docker",
    "args": ["run", "-i", "--rm", "mcp/sentry", "--auth-token", "YOUR_SENTRY_TOKEN","--project-slug" ,"YOUR_PROJECT_SLUG", "--organization-slug","YOUR_ORGANIZATION_SLUG"]
  }
}
```
</details>

<details>

<summary>Using pip installation</summary>

```json
"mcpServers": {
  "sentry": {
    "command": "python",
    "args": ["-m", "mcp_sentry", "--auth-token", "YOUR_SENTRY_TOKEN","--project-slug" ,"YOUR_PROJECT_SLUG", "--organization-slug","YOUR_ORGANIZATION_SLUG"]
  }
}
```
</details>

### Usage with [Zed](https://github.com/zed-industries/zed)

Add to your Zed settings.json:

<details>
<summary>Using uvx</summary>

For Example Curson ![mcp.json](.cursor/mcp.json) 

```json
"context_servers": [
  "mcp-sentry": {
    "command": {
      "path": "uvx",
      "args": ["mcp-sentry", "--auth-token", "YOUR_SENTRY_TOKEN","--project-slug" ,"YOUR_PROJECT_SLUG", "--organization-slug","YOUR_ORGANIZATION_SLUG"]
    }
  }
],
```
</details>

<details>
<summary>Using pip installation</summary>

```json
"context_servers": {
  "mcp-sentry": {
    "command": "python",
    "args": ["-m", "mcp_sentry", "--auth-token", "YOUR_SENTRY_TOKEN","--project-slug" ,"YOUR_PROJECT_SLUG", "--organization-slug","YOUR_ORGANIZATION_SLUG"]
  }
},
```
</details>

<details>
<summary>Using pip installation with custom path</summary>

```json
"context_servers": {
  "sentry": {
      "command": "python",
      "args": [
        "-m",
        "mcp_sentry",
        "--auth-token",
        "YOUR_SENTRY_TOKEN",
        "--project-slug",
        "YOUR_PROJECT_SLUG",
        "--organization-slug",
        "YOUR_ORGANIZATION_SLUG"
      ],
      "env": {
        "PYTHONPATH": "path/to/mcp-sentry/src"
      }
    }
},
```


</details>







## Debugging

You can use the MCP inspector to debug the server. For uvx installations:

```
npx @modelcontextprotocol/inspector uvx mcp-sentry --auth-token YOUR_SENTRY_TOKEN --project-slug YOUR_PROJECT_SLUG --organization-slug YOUR_ORGANIZATION_SLUG
```

Or if you've installed the package in a specific directory or are developing on it:

```
cd path/to/servers/src/sentry
npx @modelcontextprotocol/inspector uv run mcp-sentry --auth-token YOUR_SENTRY_TOKEN --project-slug YOUR_PROJECT_SLUG --organization-slug YOUR_ORGANIZATION_SLUG  
```
or in term
```
npx @modelcontextprotocol/inspector uv --directory /Volumes/ExtremeSSD/MCP/mcp-sentry/src run mcp_sentry --auth-token YOUR_SENTRY_TOKEN
--project-slug YOUR_PROJECT_SLUG --organization-slug YOUR_ORGANIZATION_SLUG
```
![Inspector-tools](./images/Inspector-tools.png)

## Fork From
- [https://github.com/modelcontextprotocol/servers/tree/main/src/sentr](https://github.com/modelcontextprotocol/servers/tree/main/src/sentry)
## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.
