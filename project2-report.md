# Building AI Agents with KAgent and AgentGateway
## Josh Donaldson 991675118, December 2025

### Introduction
Project 2 involves using Agentgateway to secure AI agent operations within a local environment. We would set up a dedicated gateway, create an authorization policy and set up specific tools to handle routes. This gateway exists to allow for policy and identity aware communications between clients and AI agents. The authorization policy gives the gateway auth logic to handle traffic, like which tools can be accessed by which agents.
Using a gateway can offer many benfits over just direct connection, especially for the reasons stated above. You can even go as deep as rate limiting and configuring certain types of traffic for even more control over how agents are handled within your cluster.

### Challenges encountered
There were a lot of challenges encountered in project 2. Many were syntax based. Here are a few that were a bit deeper than that:
- agentgateway install w/ helm commands were wrong. Correct commands to bring everything up, including the controller were: "helm upgrade -i kgateway oci://cr.kgateway.dev/kgateway version v2.1.2 --namespace kgateway-system --create-namespace --set gatewayClass.create=true --set gatewayClass.name=kgateway --set dataplane.type=agentgateway". This was done after grabbing the correct CRDs
- The MCP gateway server would not initialize and throw HTTP errors. I tried changing ports from 3000 to 9977 which was where kagent gateway pod was running at but that didn't help. I threw in the towel here

### Learning
I learned that managing agents in a cluster can be extremely granular. Controllers are separate from pods, and they handle the logic to how the pods execute workflows. I learned that namespaces within Kubernetes are 'security zones' and proprietary tasks are carried out within each namespace. I learned that agent gateways are not just fancy software routers, but logic stations that can handle agent traffic and bound it to identities, which is pretty cool. I can see why DevOps guys are going crazy over this new implementation of technology

GitHub Repo (filedump): https://github.com/thejoshdonaldson/KAgent-final-assignment/tree/main
Resources: Kagent, Kind, and Kgateway-Dev repos. https://ollama.com/download/linux also used for grabbing Ollama model when OpenAI default command would not work. ChatGPT used for mild troubleshooting/syntax formatting
