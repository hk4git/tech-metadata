# AI
## AI General
### AI Prompt
**ChatGPT Enterprise** is designed for work. Unlike public AI tools, it's built to securely use our own data—such as documents, messages, and schedules—only when we choose to connect them. ChatGPT Connectors let you securely link your ORG apps—such as SharePoint, Outlook, Calendar, and Teams—to ChatGPT Enterprise so it can reference your internal information while you work. The connection steps are simple and consistent, making it easy to enable the tools you need without extra setup or technical knowledge.

**Six Ways AI Can Support Our Work**: 1) UNDERSTAND, 2) CLARIFY, 3) IMPROVE, 4) PREPARE, 5) ADAPT, 6) DECIDE

- **AI Slop**: AI output might look structured and professional, it can lack quality and substance. This type of output is known as AI Slop.
- The Five Principles:
  - Be Specific and Clear: AI thrives on clarity!
  - Provide Context: Context sets the direction.
  - Set Constraints: Constraints create focus.
  - Assign a Role: Roles shape perspective.
  - Iterate & Refine: Great prompts are built, not written.


# Microsoft 
## IQ
- Microsoft IQ (intelligence, tools): Work IQ (chat, mail), Fabric IQ (databases), Foundry IQ (AI), Web IQ (bing, search)
- Agent365: Identity, data, security, threat protection, endpoint, registration, observability etc. 

### M365 Copilot:
Enabling developer mode: To enable developer mode, in Copilot Chat, type `-developer on`. To disable developer mode, type `-developer off`.
<br /> https://learn.microsoft.com/en-us/collections/p11pb18wmq6xqq
<br /> https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/api-plugin-debug-local
- API plugins enable declarative agents in Microsoft 365 Copilot to call REST APIs to retrieve data and perform tasks. However, these APIs must be hosted on servers that are addressable over the internet in order for Microsoft 365 Copilot to reach them.
- Use `/share` on agent chat to share debug session details with M365 support team.

###### M365 Declarative agent requires OpenAPI url are available over internet so local url will not work, Use `DevTunnel` to expose local url to make it available over internet.

### Teams Agents:
https://www.youtube.com/watch?v=7bL_kaA9cag
https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/api-plugin-confirmation-prompts

OpenAPI:
- only https is allowed, http is not supported.

https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/api-plugin-debug-local

### Example
Sample instructions for Declarative Agent format can be used:
```
# OBJECTIVE

# RESPONSE RULES
- rules

# WORKFLOW

## Step 1: Evaluate Query for `OneDriveAndSharePoint`
- **Goal:** goals
- **Action:** 
  - action
    - take action
  - Example: example
- **Transition:** Keyword found → `OneDriveAndSharePoint`. Otherwise → Step 2.

## Step 2: Route to `get_answer` (Default)
- **Goal:** goal 2
- **Action:** action 2:
- **Transition:** Execute query and present results.

# OUTPUT FORMATTING
- output

# EXAMPLES

## Valid Routing Examples

### → `OneDriveAndSharePoint`:
**User:** "user ask"
**Action:** Route to `OneDriveAndSharePoint`

### → `get_answer`:
- sample question

## Invalid Routing Examples
- example

# ERROR HANDLING
- example

# CONVERSATIONAL CONTEXT
- example

# DATA SOURCE INTEGRITY
- example
```

Sample instruction for Semantic Kernel plugin:
```
# Instructions

## Purpose

## Guidelines

## Execution Steps
1. Read the original content.

## Input
- Data: {{$Data}}


## Output
- output

## Example Output 

Example 1:
Example 2:
```


### MCP
- run inspector command - `npx @modelcontextprotocol/inspector`

# Explore
- LLMOps / MLOps frameworks
- Harmful AI Content filter for CEA (Custom Engine Agent)
- Explore WorkIQ - to read Teams Chat/Messages etc.
- AI Lend Engineering 20% target
- Agency for team
- RAI | SDL | Privacy Review | Threat Model | TrIP
  

