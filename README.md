<!--
---
name: Remote MCP  using Azure API Management (Experimental)
description: Use Azure API Management as the AI Gateway for MCP Servers using Azure Functions  
page_type: sample
languages:
- python
- bicep
- azdeveloper
products:
- azure-api-management
- azure-functions
- azure
urlFragment: remote-mcp-apim-functions-python
---
-->

# Secure Remote MCP Servers using Azure API Management (Experimental)

![Diagram](mcp-client-authorization.gif)

Azure API Management acts as the [AI Gateway](https://github.com/Azure-Samples/AI-Gateway) for MCP servers. 

This sample implements the latest [MCP Authorization specification](https://modelcontextprotocol.io/specification/2025-03-26/basic/authorization#2-10-third-party-authorization-flow)

This is a [sequence diagram](infra/app/apim-oauth/diagrams/diagrams.md) to understand the flow.

## Deploy Remote MCP Server to Azure

1. Register `Microsoft.App` resource provider.
    * If you are using Azure CLI, run `az provider register --namespace Microsoft.App --wait`.
    * If you are using Azure PowerShell, run `Register-AzResourceProvider -ProviderNamespace Microsoft.App`. Then run `(Get-AzResourceProvider -ProviderNamespace Microsoft.App).RegistrationState` after some time to check if the registration is complete.

2. Run this [azd](https://aka.ms/azd) command to provision the api management service, function app(with code) and all other required Azure resources

    ```shell
    azd up
    ```

### MCP Inspector

1. In a **new terminal window**, install and run MCP Inspector

    ```shell
    npx @modelcontextprotocol/inspector
    ```

1. CTRL click to load the MCP Inspector web app from the URL displayed by the app (e.g. http://127.0.0.1:6274/#resources)
1. Set the transport type to `SSE`
1. Set the URL to your running API Management SSE endpoint displayed after `azd up` and **Connect**:

    ```shell
    https://<apim-servicename-from-azd-output>.azure-api.net/mcp/sse
    ```

5. **List Tools**.  Click on a tool and **Run Tool**.  



