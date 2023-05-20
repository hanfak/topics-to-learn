# GitOps

## What?

- A process of doing Kubernetes cluster management and application delivery, by using Git as a single source of truth.
  - for defining and managing infrastructure and application deployments
  -  for implementing continuous delivery for cloud-native applications that emphasizes the use of version control and declarative definitions of infrastructure and application configurations.
- entails using Git and pull requests to manage all stages of modern software development.
- All instructions, ie deployments, K8s infrastructure is written in declarative manner.
- you no longer tell your servers and clusters what to run, they instead ask what’s there for us to run

## How?

- An K8 operator, pulls from the git repo, and compares with current state, and applies the changes.
- Changes are made as pull request, reviewed, and pushed to master. Where it is picked up by the operator and applied the cluster

## Benefits

- Continuous Syncing is the paradigm shift where the deployment of the desired environment state is not a once-off process.
- Full Audit and reporting Trail
  - All history is in git
- No cap on deployment parallelism
- Minimise configurational drift
  - Environments should not deviate away from the desired state. Ideally, they should also prevent or rollback any changes that are not declared in the source control.
- With GitOps, I am a lot more likely to be using GitHub to assess the state of my environments then use kubectl to achieve the same.
- Don’t give CI/CD wildcard access to your environments
- Easy to roll back state to a previous version that is known to work
  - reducing your meantime to recovery (MTTR) from hours to minutes.
- By codifying everything — i.e. infrastructure, security, monitoring, CI/CD — you can automate everything and move even faster with lower friction
- Every change (pull request) can be validated automatically and blocked if needed before merging into a production environment.
- GitOps provides the advantages of having only a single tool to work with, while still offering flexibility to use the tool in different ways.
- you have consistent end-to-end workflows across your entire organization. Not only are your continuous integration and continuous deployment pipelines all driven by pull request, but your operations tasks are also fully reproducible through Git.

## Drawbakcs

- Restarts
  - Each time you change a Secret or a ConfigMap without modifying the deployment itself, you are presented with a challenge of making sure that your application picks up the latest metadata.
- Broken YAML
  - a CIOps pipeline or even kubectl apply -f has an advantage. Feedback about broken YAML is very timely. With GitOps broken manifests will break a GitOps tool of choice (Flux in our case), but unless you actively monitor and alert on logs in the GitOps tool, this problem might remain unnoticed for longer.
- API throttling
  - GitOps is constantly polling git repo. Ensure that your provider has a generous allowance on polling. Additionally, tools like Flux are scanning your container registries for changes, and you might hit the API limits there as well.
- GitOps can’t deny you from doing outright silly things like kubectl apply -f from your machine.
-

### FluxCD

- https://fluxcd.io/

## Links

- https://www.weave.works/technologies/gitops/
- https://dzone.com/articles/what-is-gitops-really
