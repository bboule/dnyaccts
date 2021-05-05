# Dynamic accounts to be configured with gitops style Spinnaker
  - This url of this repo is fed into default/profiles/spinnakerconfig.yaml file that is present in https://github.com/OpsMx/gitops-hal-sample
  - Credentials to access this repo is fed via secret (opsmx-gitops-secret) in oes helm chart.
  

## Add K8s accounts
- First, this git repo uri is added to spinnakerconfig.yml using secret(opsmx-gitops-secret) in oes helm chart.
- clouddriver-local.yml file in this repo contains all the accounts, under kubernetes
  section, an account shall be added and corresponding kubeconfig file should be added
  to kubecfgsDir

## Add Jenkins accounts
- Encrypted credentials of Jenkins shall be placed under igor-local.yml

      jenkins:
        username: '{cipher}<ENCRYPTED_JENKINS_USERNAME>'
        password: '{cipher}<ENCRYPTED_JENKINS_PASSWORD>'

- Below section shall be added to ~/.hal/config
  ci:
    jenkins:
      enabled: true
      masters:
      - name: opsmx-jenkins-master
        permissions: {}
        address: http://my-jenkins-master-url
        username: ${jenkins.username}
        password: ${jenkins.password}

## Add AWS, ECS accounts
- Encrypted access-key and secret-key of AWS shall be put in clouddriver-local.yml and add AWS, ECS accounts in clouddriver-local.yml

## Process to encrypt credentials
- Follow the detailed instructions in below link
  https://www.opsmx.com/blog/managing-secrets-in-spinnaker-encryption-using-symmetric-key/
