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
    >Setar as permissões sugeridas após instalação
    >Alterar caminho do usuário de root para home/ubuntu, por exemplo, no arquivo .kube/config

- `su -` acessar root
- `minikube start --vm-driver=none` iniciar minikube sem VirtualBox
- `minikube status` verificar status
- `kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080` executar imagem de exemplo
- `kubectl expose deployment <nome-deployment> --type=NodePort` expor aplicação
    >Configurar Security Groups do tipo _Custom TCP Rule_, com origem _My IP_, para a porta exposta e associar à instância (Actions > Networking > Change Security Groups)
    >Testar acesso por meio do endereço da instância (Public DNS)