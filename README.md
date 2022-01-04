# robolaunch :rocket:

:warning: This project is only for development environment for a moment.

[robolaunch](https://www.robolaunch.io) is a cloud based robotics simulation and development platform which supports variety of simulation environments, ROS/ROS2 and multiple software languages with an opportunity to run large scale of simulations in parallel.

## Deployment

You could reach helm chart of deployment from this page.
[Source Code Repo](https://github.com/robolaunch/robolaunch)

## Prerequisite

Dependencies:

- Temporal + ElasticSearch
- Istio

Also you must add following `SearchAttributes` to Temporal

```bash
tctl admin cluster asa --name DeploymentName --type Keyword
tctl admin cluster asa --name DeploymentNamespace --type Keyword
```

## Installation

Clone robolaunch-deploy repository.

```bash
git clone https://github.com/robolaunch/robolaunch-deploy.git
```

If you want to activate end-user auth you must configure **.Values.auth.issuer** and **.Values.auth.jwksUri** paramaters in values.yaml.

```yaml
auth:
  enable: true
  issuer: ""
  jwksUri: ""
```

Create namespace that has `istio-injection: enabled` label.

```bash
kubectl create ns <namespace>
kubectl label namespace <namespace> istio-injection=enabled
```

After create namespace you can deploy robolaunch chart

```bash
cd helm-robolaunch; helm install --<namespace> helmbot <release-name> .
```
