### Создаю cloud
Configure Clouds:  
&nbsp;&nbsp;Docker Host URI `unix://var/run/docker.sock`  
&nbsp;&nbsp;Container Cap `2`  
Docker Agent templates  
&nbsp;&nbsp;Labels `ansible_docker`  
&nbsp;&nbsp;Docker Image `aragast/agent:7`  
&nbsp;&nbsp;Pull strategy `Pull once and update latest`
## Freestyle
### Настраиваю джобу
Git::Repository URL::`https://github.com/ottvladimir/example-playbook.git`
```bash
ansible-vault decrypt secret --vault-password-file vault_pass
mkdir ~/.ssh
ssh-keyscan -t rsa github.com | tee github-key-temp | ssh-keygen -lf -
cat github-key-temp >> ~/.ssh/known_hosts
mv ./secret ~/.ssh/id_rsa
chmod 400 ~/.ssh/id_rsa
ansible-galaxy install -r requirements.yml -p roles
ansible-playbook site.yml -i inventory/prod.yml
ls -lah roles
```
## Declarative
```groovy
pipeline {
    agent any

    stages {
        stage('CLONE_GIT_REPO') {
            steps {
                sh 'git clone https://github.com/ottvladimir/example-playbook.git'
                }
        }
        stage('ADD_SSH_SETTINGS') {
            steps {
                sh 'mkdir ~/.ssh'
                sh 'ssh-keyscan -t rsa github.com | tee github-key-temp | ssh-keygen -lf -'
                sh 'cat github-key-temp >> ~/.ssh/known_hosts'
                }
        }
        stage('DECRYPT_VAULT') {
            steps {
                dir("example-playbook"){
                    sh 'ansible-vault decrypt secret --vault-password-file vault_pass'
                    sh 'mv ./secret ~/.ssh/id_rsa'
                    sh 'chmod 400 ~/.ssh/id_rsa'
                }
            }
        }
        stage('RUN_ANSIBLE') {
            steps {
                dir("example-playbook"){
                    sh 'ansible-galaxy install -r requirements.yml -p roles'
                    sh 'ansible-playbook site.yml -i inventory/prod.yml'
                }
            }
        }
        stage('RUN_SOMETHING') {
            steps {
                sh 'ls -lah example-playbook/roles'
            }
        }    
    }
}
```
## Scripted 
```groovy
node("ansible_docker"){
    stage("Git checkout"){
        git credentialsId: 'jenkins_script', url: 'git@github.com:ottvladimir/example-playbook.git'
    }
    stage("Check ssh key"){
        secret_check=true
    }
    stage('ADD_SSH_SETTINGS') {
        sh 'ssh-keyscan -t rsa github.com | tee github-key-temp | ssh-keygen -lf -'
        sh 'cat github-key-temp >> ~/.ssh/known_hosts'
        sh 'ansible-vault decrypt secret --vault-password-file vault_pass'
        sh 'mv ./secret ~/.ssh/id_rsa && chmod 400 ~/.ssh/id_rsa'
    }
    stage("Run playbook"){
        if (secret_check){
            sh 'ansible-galaxy install -r requirements.yml -p roles'
            sh 'ansible-playbook site.yml -i inventory/prod.yml'
        }
        else{
            echo 'no more keys'
        }
    }
}
```
