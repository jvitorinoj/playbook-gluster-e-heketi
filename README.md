# Gluster

Automatiza a instalação do glusterfs com heketi. O cluster criado pode ser utilizado como storage do kubernetes.

Atividades feitas por esse playbook
  - Instalação do gluster 
  - Instalação do heketi
  - Configuração do heketi para conexão ao gluster


##  Pre-requisitos

  - O host no grupo *[heketi]* dever ter um usuário que possa acessar todos os hosts no grupo *[gluster_servers]* sem senha através de ssh
  - O cluster deve possuir no minimo 3 nos (grupo *[gluster_servers]*) 
  - os hosts no grupo *[gluster_servers]* devem possuir discos não formatadas disponiveis, o tamanho e a quantidade de discos depende do [tipo de volume](https://docs.gluster.org/en/latest/Administrator%20Guide/Setting%20Up%20Volumes/) que deseja.
  - Esse playbook foi feito para execução em S.O baseados em Red Hat, para os baseados em Debian é necessário alteração principalmente em [](./roles/glusterfs/tasks/main.yaml)


## Arquivos a serem modificados antes da execução

  - [hosts](./hosts)
  
  - [heketi/defaults/main.yml](./heketi/defaults/main.yml)
  >  - Configura nome dos hosts, IP e quais discos estão disponiveis

  - [roles/heketi/files/heketi.json](./roles/heketi/files/heketi.json#L36-47)
  >  Para ambientes de produtivos, alterar o `executor` de mock para ssh ou kubernetes 
  
  - [main.yml](./main.yml)
  > Alterar as variaveis de acordo com a versão do heketi e com os pre-requisitos descritos acima
  > Senhas não podem conter caracteres especiais.
  


### Execução

Exemplo de execução do script

```sh
$ mkdir gluster-playbook && cd gluster-playbook
$ git clone $this_repo . 
$ Editar arquivos
$ ansible-playbook -i hosts main -u login_ap -k -vv --become
```

### Referências

- Baseado no artigo de Josphat Mutai em [computingforgeeks.com](https://computingforgeeks.com/setup-glusterfs-storage-with-heketi-on-centos-server/)
- [Documentação do Gluster](https://docs.gluster.org/en/latest/)
- [heketi](https://github.com/heketi/heketi)
- [Configurando Gluster na unha](https://joao.vitorino.net.br/2020/04/18/elementor-22/)


