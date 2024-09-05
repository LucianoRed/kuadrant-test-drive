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

