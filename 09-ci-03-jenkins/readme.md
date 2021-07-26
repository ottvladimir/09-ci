```bash
ansible-vault decrypt secret --valut-password-file valut_pass
mv ./secret ~/.ssh/id_rsa
chmod 400 `/.ssh/id_rsa
ansible-galaxy install -r requirements.yml -p roles
ansible-playbook site.yml -i inventory/prod.yml
ls -lah roles
```
