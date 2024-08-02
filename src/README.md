## Definições
- EKS: Elastic Kubernetes Service

## Criação ambiente
- AWS > Login console > EC2 > Launch Instance > "Escolher imagem" e avançar escolhendo as opções que atendam ao projeto

## Conexão
- Instâncias > Selecionar instância > Conectar > No terminal, utilizar exemplo apresentado apontando para o diretório em que a chave `SSH` foi baixada
- `sudo passwd root` definir senha de root

## Instalações
- [Kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
- [Docker](https://www.docker.com/)
- [Minikube](https://kubernetes.io/docs/tasks/tools/#minikube)
    >Necessário ter instalado o Kubectl e Hypervisor (KVM, VirtualBox, etc)

- `su -` acessar root
- `minikube start --vm-driver=none` iniciar minikube sem VirtualBox