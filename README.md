# Ambiente para validar os playbooks Ansible da plataforma Dojot

Este projeto consiste em prover um ambiente controlado e isolado para validar os playbooks Ansible criado para o projeto [`Dojot`](https://github.com/dojot).

## Pré-requisitos

- [VirtualBox](https://www.virtualbox.org/) >= 6.1
- [Vagrant](https://www.vagrantup.com/) >= 2.2.19

## Como utilizar este projeto

Inicialize a VM executando o comando abaixo:
```bash
vagrant up
```

Após inicializada a VM, execute o playbook de configuração do ambiente.
```bash
ansible-playbook playbook.yaml
```

O playbook acima contém algumas `tags` que ajudam a desacoplar, se preciso, a configuração do ambiente.

* **filesystem**: formata e configura os discos adicionais utilizados pelo `Docker`e `K3s`;
* **docker**: instal o `Docker Engine`;
* **docker_compose**: instala o [`Docker Compose`](https://docs.docker.com/compose/);
* **k3s**: instala e inicializa o cluster kubernetes baseado no [`k3s`](https://k3s.io/);
* **kubectl**: instala o [`https://kubernetes.io/docs/tasks/tools/`];
* **helm**: instala o [`Helm`](https://helm.sh/);

## Acessando a máquina virtual

Estando no diretório do projeto, basta executar o comando abaixo:
```bash
vagrant ssh
```
> O usuário padrão dessa VM se chama `vagrant` na qual já possui privilégios de sudo.

## Informações Importantes

* Ajuste os recursos da máquina virtual no arquivo `Vagrantfile`;
* Para encerrar a maquina virtual execute o comando a seguir: `vagrant halt --force && vagrant --destroy --force`;
* Para saber o estado da máquina virtual, execute `vagrant status` ou `vagrant global-status`;

