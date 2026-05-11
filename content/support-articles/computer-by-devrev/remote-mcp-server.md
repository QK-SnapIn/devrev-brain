---
title: Remote MCP server
devrev_id: ART-21859
parent_directory: Computer by DevRev
translation_group: ZNqaZTsx
modified_date: "2026-05-07T10:28:06.998Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/ZNqaZTsx"
tags: []
top_category: Computer by DevRev
wiki_match: features/remote-mcp
match_score: 1.0
last_updated: 2026-05-11
related: ['features/remote-mcp']
---

# Remote MCP server

As an agent-first platform, DevRev provides a remote MCP server for work with agentic platforms such as Claude desktop and Cursor.

The DevRev remote MCP server is available at `https://api.devrev.ai/mcp/v1`.

The MCP server currently supports two modes of authentication: **OAuth** or DevRev-generated **PAT**.

Most MCP clients (such as the Claude desktop) automatically use OAuth when connecting to the server, so no configuration is required.

## Supported clients

We support a wide variety of MCP clients, most notable are the following:

* [OpenAI ChatGPT/Codex](https://platform.openai.com/docs/guides/tools-connectors-mcp)
* [Claude Code](https://code.claude.com/docs/en/mcp) (*PAT only*)
* [Claude Desktop](https://support.claude.com/en/articles/11175166-getting-started-with-custom-connectors-using-remote-mcp)
* [GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli)
* [Google Gemini](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md)
* [Amazon Quick Suite](https://docs.aws.amazon.com/quicksuite/latest/userguide/mcp-integration.html)

The DevRev remote MCP Server also supports any **local MCP-compatible client** that can run on `localhost` and connect to the server via the `mcp-remote` proxy. This enables custom or third-party integrations that follow the MCP specification.

For detailed setup instructions, refer to your client's own MCP documentation or built-in assistant.

## Authenticate with OAuth

DevRev MCP server supports **OAuth authentication** in **Claude Desktop** and **Cursor IDE**. These clients complete authentication via a browser-based OAuth flow.

**Claude Code does not support OAuth.** When using Claude Code, you must authenticate using a **personal access token (PAT)**, as described in the section below.

### Configure for Claude Desktop

Installing a DevRev connector to Claude requires **Admin** permissions. You must first add the connector to your team; only then can team members connect to it.

OAuth authentication is available only in **Claude** (both the desktop and web apps).

1. In the Claude app, navigate to **Settings > Connectors**, then click **Browse connectors** and search for **DevRev**.

![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316211&key=3653f2d3d7e23e3742f85034947d129fcd4cf776f31681db5ad3579db5a5317a)2. Select **DevRev** from the results and click **Add to your team**. The DevRev connector will appear in the list of available connectors. Click **Connect** to begin the setup process. A new browser tab opens, prompting you to enter your organization’s **slug**.

The **slug** is the string that follows `https://app.devrev.ai/` in your DevRev URL. For example, if your URL is `https://app.devrev.ai/acme/`, the slug is `acme`.

![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316213&key=41f91f07aa8fc3c2dbc98476f1009baee8d40a673e1a2a6dbabd09f4d129db25)

3. Click **Continue** to proceed to the next step, where you must review and confirm the access permissions required by Claude.

![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316210&key=fce03db677cbb09d75ade69f28bcdc467bc25e6df6d67a5fee70e7718bd5b55b)

After the connection is complete, the DevRev connector status changes to **Connected**. Clicking the connector shows additional details, including the list of available tools.

![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316217&key=70c843151a76d1cf50747e8f6d89c87be91c3f1e027d9fa0e94e44547eb0a580)

### Configure for Cursor

You can connect the DevRev MCP server to Cursor IDE using OAuth in **two ways**. Both methods ultimately require the same configuration and authentication steps.

**Option 1: Add DevRev MCP from the Cursor Website**

1. **Install from Cursor’s MCP directory**  
   Go to Cursor’s official MCP directory and locate the **DevRev MCP server**.  
   Click **“+ Add to Cursor”**.

   ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316218&key=18ad3167140e0231103f948bd1413d1d0d50c4418501b48c6d86fb04c1d5f739)
2. **Confirm installation in Cursor**  
   Your browser will open Cursor IDE and display a confirmation modal.  
   Click **Confirm / Install** to proceed.

   ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316215&key=4ab6fd820850b859ea59e30308e8e701372ba792ab1dec2a1d372d1a515dd84d)
3. **Initial connection attempt (expected to fail)**  
   After installation, Cursor will automatically try to connect to the DevRev MCP server.  
   This connection will **fail**, because the required OAuth configuration is not yet complete.

   ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316219&key=d0c1c0359e88f464265c8f9e2d10773cebb4f30b10f77a458c209f394262a8a2)
4. **Edit the MCP configuration**  
   Click the **Edit** button for the DevRev MCP server.  
   Add your **CLIENT\_ID** to the configuration file.

   Example configuration:

   ```
   {
     "mcpServers": {
       "DevRev": {
         "url": "https://api.devrev.ai/mcp/v1",
         "auth": {
           "CLIENT_ID": "AB0hoKlvrU1rh3rBF4jkb2rbOd6T2qDR"
         }
       }
     }
   }
   ```
5. **Reconnect the server**  
   Save the configuration and click **Connect** again.
6. **Authenticate with DevRev**  
   A browser window will open, prompting you to enter your **DevRev organization slug**.  
   Enter the slug and click **Continue**.

   The **slug** is the string that follows `https://app.devrev.ai/` in your DevRev URL. For example, if your URL is `https://app.devrev.ai/acme/`, the slug is `acme`.

   ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316216&key=744fbf5b445a531f322f7a11e8ec768c450a81870bfb0bd11d930e313129a19d)
7. **Connection successful**  
   You will be redirected back to Cursor IDE.  
   The DevRev MCP server will now show as **connected**, and all available DevRev tools will be accessible.

   ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316214&key=22edb3001be97c0c43fb09d6380757f7bb65aeaaf6731764c0d8bfe48dd53b02)

### Option 2: Add DevRev MCP manually from Cursor IDE

1. **Open MCP settings in Cursor**  
   In Cursor IDE, open **Settings → Cursor Settings →Tools & MCP**.
2. **Add a custom MCP server**  
   Click **“Add Custom MCP”**.

   ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9316212&key=ef1b41596066e2cd4224d0cbde72b91139b85cea702f796dcecca961aa008046)
3. **Provide the MCP configuration**  
   Paste the same configuration shown below, making sure to include your **CLIENT\_ID**:

   ```
   {
     "mcpServers": {
       "DevRev": {
         "url": "https://api.devrev.ai/mcp/v1",
         "auth": {
           "CLIENT_ID": "YOUR_CLIENT_ID_HERE"
         }
       }
     }
   }
   ```
4. **Connect and authenticate**  
   Click **Connect**.  
   A browser window will open asking for your **DevRev organization slug**.

   Enter the slug and click **Continue**.

   The **slug** is the string that follows `https://app.devrev.ai/` in your DevRev URL. For example, if your URL is `https://app.devrev.ai/acme/`, the slug is `acme`.
5. **Finish setup**  
   After successful authentication, you will be redirected back to Cursor, and the DevRev MCP server will be connected and ready to use.

Once connected, you can immediately start using the DevRev MCP tools within Cursor IDE.

## Authenticate with PAT

### Configure for Claude Code

Claude Code currently only supports **DCR** OAuth flows, which presents a compatibility limitation with our existing authentication infrastructure. Until broader OAuth support is available in Claude Code, we recommend authenticating with our remote MCP server using a PAT.

For configuring PAT authentication with Claude Code, we recommend following their official docs [here](https://code.claude.com/docs/en/mcp#option-1:-add-a-remote-http-server).

Below is a command for quick copying if you are already familiar with setting up MCP servers in Claude Code:

```
claude mcp add --transport http devrev https://api.devrev.ai/mcp/v1 \
  --header "Authorization: Bearer <token>"
```

**Note:** Claude code allows for scoped configurations. To avoid adding the MCP server in each Claude project/directory, append the `--scope user` option to the above command. More on scope configurations in Claude code can be found on their [official page](https://code.claude.com/docs/en/settings#configuration-scopes).

### Configure for Codex

Follow official documentation on how to configure an MCP server in Codex [here](https://developers.openai.com/codex/mcp).

**Note:** Currently Codex [does not support connecting to remote MCPs natively](https://github.com/openai/codex/issues/3696) so it is recommended to use the `mcp-remote` proxy as a workaround until support is added.

### Configure for Cursor

Cursor only allows OAuth for a curated list of MCP servers. Until DevRev is listed, PAT authentication is the only way to use the remote MCP through Cursor.

1. In Cursor, go to **Preferences** > **Cursor settings** and open the **Tools & Integrations** tab from the side menu.
2. Click **Add Custom MCP** or **New MCP Server** if you already have some registered.
3. Edit the `mcp.json` and add the following JSON object into it:

```
{
   "mcpServers":{
      "DevRev MCP":{
         "url":"https://api.devrev.ai/mcp/v1",
         "headers":{
            "Authorization":"<token>"
         }
      },
      
   }
}
```

4. Save the file to apply the addition of the remote MCP server.

## Related wiki nodes
- [[features/remote-mcp]]

## Source
- DevRev support article [Remote MCP server](https://support.devrev.ai/en-US/devrev/article/ZNqaZTsx) (ART-21859)
