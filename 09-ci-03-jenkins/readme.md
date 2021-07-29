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
```bash
ansible-vault decrypt secret --vault-password-file vault_pass
mkdir ~/.ssh
mv ./secret ~/.ssh/id_rsa
chmod 400 ~/.ssh/id_rsa
ansible-galaxy install -r requirements.yml -p roles
ansible-playbook site.yml -i inventory/prod.yml
ls -lah roles
```
## Declarative
