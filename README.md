# kuadrant-test-drive
Scripts Ansible para preparar ambiente de TD de quadrant 

### Pre-reqs
* Credenciais da aws salvas em ~/aws/credentials.
* Um cluster OpenShift
* Ansible instalado

### Managed Zone
Supondo que voce esteja usando o ambiente de demo aws open da Red Hat, voce deve ter recebido nas instrucoes um dominio tipo sandbox1198.opentlc.com ou algo parecido. Tenha esse dominio como o seu <top domain>. Vamos criar um managed.<top domain>.

Para isso, exporte a variavel AWSTOPDOMAIN com o dominio que voce recebeu no demo.redhat.com. Ex:
```bash
export AWSTOPDOMAIN=sandbox1198.opentlc.com
```
Vai precisar também exportar sua chave e secret aws assim como seu email para rodar o instalador depois

```bash
export EMAILCERT=seuemail@algo.com
export AWSKEY=suachaveaws
export AWSSECRET=suasecretaws
```


Depois rode o playbook que ira fazer a criacao do dominio.

```bash
ansible-playbook cria_managed_zone.yaml
```

Este playbook já cria a managed zone, obtem o id, e já popula o arquivo inventory.template. 

Agora basta clonar o repositorio https://github.com/rh-soln-pattern-connectivity-link/connectivity-link-ansible

```bash
git clone https://github.com/rh-soln-pattern-connectivity-link/connectivity-link-ansible
cp inventory.template connectivity-link-ansible/operator-setup/inventories
cd connectivity-link-ansible/operator-setup/
ansible-playbook playbooks/ocp4_workload_connectivity_link.yml -e ACTION=create -i inventories/inventory.template
```


