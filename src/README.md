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
- `minikube ip` obter endereço IP do cluster

## Deploy Aplicação Guestbook
- `kubectl apply -f https://raw.githubusercontent.com/ricardomerces/guestbook-app/master/redis-master-deployment.yaml` redis master
- `kubectl apply -f https://raw.githubusercontent.com/ricardomerces/guestbook-app/master/redis-master-service.yaml` serviço redis master (comunicação da app com o redis para gravação dos dados)
- `kubectl apply -f https://raw.githubusercontent.com/ricardomerces/guestbook-app/master/redis-slave-deployment.yaml` redis slave
- `kubectl apply -f https://raw.githubusercontent.com/ricardomerces/guestbook-app/master/redis-slave-service.yaml` serviço redis slave (comunicação da app com o redis para a leitura dos dados)
- `kubectl apply -f https://raw.githubusercontent.com/ricardomerces/guestbook-app/master/frontend-deployment.yaml` frontend
- `kubectl apply -f https://raw.githubusercontent.com/ricardomerces/guestbook-app/master/frontend-service.yaml` serviço frontend
- `kubectl get all` visualizar o resultado
- `kubectl version` versão Kubernetes

>Arquivos .yaml disponíveis nas pastas **app** e **db**
>Editar Security Group com a porta do pod de serviço frontend (Security Groups > <group-name> > Inbound)
>Testar acesso por meio do endereço da instância (Public DNS)

## Criação Cluster
- IAM > Roles > Criar role (autorização para utilização do EKS) > EKS
- VPC - Virtual Private Cloud (rede virtual)
- CloudFormation > Create Stack > (Specify an Amazon S3 template URL > amazon-eks-vpc-sample.yaml)
- `aws eks create-cluster --name <nome-cluster> --role-arn<role arn> --resources-vpc-config subnetIds=<subnet ID1, subnet ID2..., securityGroupsIds=<group ID>>` criar cluster no AWS CLI (ou via console AWS)
    >`role-arn` disponível na role configurada na AWS

    >`resources-vpc-config subnetIds` disponível nas subredes da VPC

    >`securityGroupsIds` disponível nos security groups da VPC

    >Caso esteja configurado Multi-Factor Authentication, não será possível seguir via console AWS, pois em determinado momento dependerá da AWS CLI