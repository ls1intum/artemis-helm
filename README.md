# artemis-helm
Helm chart for Artemis - Early Development

# Installation 

## Install Chart via Repository 

```bash
helm repo add artemis https://ls1intum.github.io/artemis-helm/
helm repo ls 
```

Create a `values.yml` file with all the desired artemis configurations. See `./artemis/values.yaml` for all options.

```bash
helm upgrade --install artemis-test artemis/artemis \
        --create-namespace \
        --namespace $NAMESPACE \
        -f $VALUESFILE
```

## Install Chart for development: 
Prerequisits: 
- Working kubernetes cluster
- Helm and `kubectl` installed on local machine 
- Working `kubeconfig` for `kubectl`
- Helm `artemis-values.yml` file 

Change directory to `./artemis/`

Install (and upgrade) helm release `artemis-test` from `.`:

```bash
helm upgrade --install artemis-test . \
        --debug \
        --create-namespace \
        --namespace artemis-dev \
        -f artemis-values.yml
```


# Artemis Helm chart todo list: 


- [x] Single Artemis Instance Deployment 
  - [x] Artemis Deployment
  - [x] Artemis Service 
  - [x] Artemis Ingress
  - [x] Shared Persistent Volume
- [x] Bundled Database Deployment 
- [ ] All important Artemis configurations (`application.yml` and `application-prod.yml`) as Helm Values ([See Artemis ansible collectioni](https://github.com/ls1intum/artemis-ansible-collection/blob/main/roles/artemis/defaults/main.yml))
  - [ ] Artemis Server URL
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
    - [ ] LDAP
  - [ ] Registry
  - [ ] Broker
  - [ ] Database
    - [ ] External Database
    - [ ] Database Name
    - [ ] Database User 
    - [ ] Database Password
  - [ ] Artemis Config
    - [ ] Internal Admin User and Password
    - [ ] Artemis git SSH key
    - [ ] Test Server Flag 
    - [ ] Artemis Email 
    - [ ] Login Info text/Password Reset 
- [ ] jHipster Registry Deployment
- [ ] Message Broker Deployment 
  - [ ] Single Broker deployment 
  - [ ] HA Broker deployment 
- [ ] Scalable Artemis Deployment 
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

