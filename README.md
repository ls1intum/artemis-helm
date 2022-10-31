# artemis-helm
Helm chart for Artemis - Early Development - Not recommended for production use!

# Installation 

Create a `values.yml` file with all the desired artemis configurations. See `./artemis/values.yaml` for all options.

__Prerequisites:__
- Working Kubernetes cluster
- Helm and `kubectl` installed on local machine 
- Working `kubeconfig` for `kubectl`
- Helm `values.yml` file 

## Install Chart via Repository 

Add and update the helm repository to your cluster:
```bash
helm repo add artemis https://ls1intum.github.io/artemis-helm/
helm repo update
helm repo ls 
```

Install Artemis: 
```bash
helm upgrade --install artemis-test artemis/artemis \
        --create-namespace \
        --namespace artemis \
        -f values.yml
```

## Install Chart for development: 
Clone the git repository and change to the directory `./artemis/`

Install (and upgrade) helm release `artemis-test` from `.`:

```bash
helm upgrade --install artemis-test . \
        --debug \
        --create-namespace \
        --namespace artemis-dev \
        -f artemis-values.yml
```

# Usage 
The Artemis architecture can be found [here](https://github.com/ls1intum/Artemis#architecture). This chart will deploy: 
- StatefulSets
  - Database (Only for evaluation/testing/development purposes)
  - jHipster registry
  - Artemis Application Server Scheduling Node - We use a StatefulSet for the primary Artemis Application Server instance. This instance is used for all scheduling tasks. The scheduling node must be unique in the cluster! 
- Deployments
  - [Message Broker](https://github.com/ls1intum/activemq-broker-docker)
  - Artemis Application Server - We use a deployment to scale the Artemis Application server. If you need more resources, you can scale out this deployment 


# Development Documentation
## Release Workflow
This helm chart is automatically released via github actions and github pages. A release is automatically build as soon as the `main` branch changes. 
> A new version is only released if the `version` in `./artemis/Chart.yml` is bumped!



## Artemis Helm Chart Todo List: 
This is a non exhaustive list! Feel free to contribute to this chart by implementing one of the todos, or adding new todos! You can also open github issues!

- [x] Single Artemis Instance Deployment 
  - [x] Artemis Deployment
  - [x] Artemis Service 
  - [x] Artemis Ingress
  - [x] Shared Persistent Volume
- [x] Bundled Database Deployment 
- [ ] All important Artemis configurations (`application.yml` and `application-prod.yml`) as Helm Values ([See Artemis ansible collection](https://github.com/ls1intum/artemis-ansible-collection/blob/main/roles/artemis/defaults/main.yml))
  - [x] Artemis Server URL
  - [ ] external services 
    - [x] User Management
    - [ ] Version Control
      - [x] Bitbucket
      - [ ] Gitlab
    - [ ] Continuous Integration
      - [x] Bamboo
      - [ ] Jenkins
    - [ ] LTI
    - [ ] Athene 
    - [ ] Apollon
    - [ ] Mail
    - [x] LDAP
  - [x] Registry
  - [ ] Database
    - [ ] External Database
    - [ ] Database Name
    - [ ] Database User 
    - [ ] Database Password
  - [ ] Artemis Configuration
    - [x] Internal Admin User and Password
    - [ ] Artemis git SSH key
    - [ ] Test Server Flag 
    - [ ] Artemis Email 
    - [ ] Login Info text/Password Reset 
- [x] jHipster Registry Deployment
- [ ] Message Broker Deployment 
  - [x] Single Broker deployment 
  - [ ] HA Broker deployment 
- [x] Scalable Artemis Deployment 
  - [x] Find a way to have the `scheduling` spring profile in only one pod 
- [ ] Readiness and liveness probes 
- [ ] Artemis wait on db/registry 
- [ ] Rolling Update for Artemis Deployment
- [ ] Security Contexts for all Deployments
  - [ ] Artemis
- [ ] Implement Autoscalers for all Deployments
  - [ ] Artemis
- [ ] Network Policies for all pods
  - [ ] Artemis


Long term:
- [ ] Microservice Migration 
- [ ] Kubernetes Native Monitoring 
- [ ] Scaling Artemis from the Artemis UI 

