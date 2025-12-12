# Building AI Agents with KAgent and AgentGateway
## Josh Donaldson 991675118, December 2025

### Introduction
Project 1 involves spinning up a lightweight Docker container simulating a Kubernetes cluster. The Kind tool allows us to do this; making local Kubernetes deployments possible as the Kind clusters are more efficient with their utilization yield. We will also take the time to download an Ollama model and its binaries so we can hook it up to our Kind environment. This model will be the basis of Kagent; which will also be configured to port-forward a local web UI for agent interaction. This agent allows users to access local AI models within a DevOps environment or network. There is litle to no reliance on cloud LLM providers-- which means tighter control over data and authorization-based access controls.
However, this doesn't come without limitations. Using certain local models may warrant outdated model/training data and worse scalability. You also need to worry about bandwidth and cluster networking if you plan on deploying a large scale environment.

### Challenges encountered
There were quite a few challenges encountered in project 1. Many were syntax based. Here are a few that were a bit deeper than that:
- Port 80 was already being used by an unforseen apache service. Stopped the service then ran the kind create cluster command again
- Port forwarded using 8080:8080 instead of the lab port
- When running the OLLAMA_POD command, Kubernetes kept trying to talk to the default API server port of 8080, instead of where it was created (40827). This is because the kubeconfig file was in my root directory, instead of the home directory where it should be read from. I fixed this by copying the contents of the config file and placing it in/creating a new ~/.kube/config location.
- The kgateway-agent pod was stuck in a perpetual state of pending, due to “insufficient memory” (lab was performed on laptop). I never got around this as I did not want to play with custom memory args for the deployments
- Initial Ollama download command would not work. downloaded ollama binary, downloaded the model using “ollama run llama3.2:1b”, and tweaked the ollama modelconfig yaml to hit the host "http://ollama.ollama.svc.cluster.local:11434/v1"
