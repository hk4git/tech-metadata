### Useful VS Code extensions
Run terminal command: `code --list-extensions`  
Run terminal command: `Get-ChildItem "$env:USERPROFILE\.vscode\extensions" -Directory | ForEach-Object { $pkg = "$($_.FullName)\package.json"; if (Test-Path $pkg) { $json = Get-Content $pkg -Raw | ConvertFrom-Json; [PSCustomObject]@{ ID = "$($json.publisher).$($json.name)"; Name = $json.name; DisplayName = $json.displayName } } } | Sort-Object ID | Format-Table -AutoSize`

| Extension ID | Name | Display Name |
|---|---|---|
| `42Crunch.vscode-openapi` | vscode-openapi | OpenAPI (Swagger) Editor |
| `devprod.vulnerability-extension` | vulnerability-extension | WAVE AI Code Review & Analysis |
| `eamodio.gitlens` | gitlens | GitLens — Git supercharged |
| `humao.rest-client` | rest-client | REST Client |
| `ms-azure-devops.azure-pipelines` | azure-pipelines | Azure Pipelines |
| `ms-azuretools.vscode-azure-github-copilot` | vscode-azure-github-copilot | GitHub Copilot for Azure |
| `ms-azuretools.vscode-azure-mcp-server` | vscode-azure-mcp-server | Azure MCP Server |
| `ms-azuretools.vscode-azureappservice` | vscode-azureappservice | Azure App Service |
| `ms-azuretools.vscode-azureresourcegroups` | vscode-azureresourcegroups | Azure Resources |
| `ms-azuretools.vscode-bicep` | vscode-bicep | Bicep |
| `ms-dotnettools.vscode-dotnet-runtime` | vscode-dotnet-runtime | .NET Install Tool |
| `ms-python.debugpy` | debugpy | Python Debugger |
| `ms-python.python` | python | Python |
| `ms-python.vscode-pylance` | vscode-pylance | Pylance |
| `ms-python.vscode-python-envs` | vscode-python-envs | Python Environments |
| `MS-SarifVSCode.sarif-viewer` | sarif-viewer | SARIF Viewer |
| `ms-toolsai.jupyter` | jupyter | Jupyter |
| `ms-toolsai.jupyter-keymap` | jupyter-keymap | Jupyter Keymap |
| `ms-toolsai.jupyter-renderers` | jupyter-renderers | Jupyter Notebook Renderers |
| `ms-toolsai.vscode-jupyter-cell-tags` | vscode-jupyter-cell-tags | Jupyter Cell Tags |
| `ms-toolsai.vscode-jupyter-slideshow` | vscode-jupyter-slideshow | Jupyter Slide Show |
| `ms-windows-ai-studio.windows-ai-studio` | windows-ai-studio | Foundry Toolkit for VS Code |
| `redhat.vscode-yaml` | vscode-yaml | YAML |
| `shd101wyy.markdown-preview-enhanced` | markdown-preview-enhanced | *(unresolved placeholder)* |
| `TeamsDevApp.ms-teams-vscode-extension` | ms-teams-vscode-extension | Microsoft 365 Agents Toolkit |
| `TeamsDevApp.vscode-adaptive-cards` | vscode-adaptive-cards | Adaptive Card Previewer |



### Sample .rest file
```
### HK

@api=https://localhost:1234/api @token=

### GET https://localhost/api/user
Content-Type: application/json
authorization: Bearer {{token}}

### POST https://localhost/api/user
# POST https://localhost/api2/user
# POST https://localhost2/api2/user
Content-Type: application/json
Authorization: Bearer {{token}}
# X-SourceApp-Name: CustomHeader
# X-Correlation-Id: 8888
# Ocp-Apim-Subscription-Key: GUID

{
"data": ""
}
```
