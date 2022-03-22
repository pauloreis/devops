Install Kubectl:
    https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

Install Minikube:
    https://minikube.sigs.k8s.io/docs/start/

Install Virtual Box:
    https://www.virtualbox.org/wiki/Linux_Downloads
    sudo dpkg -i virtualbox-6.1_6.1.32-149290_Ubuntu_eoan_amd64.deb
    https://mundodacomputacaointegral.blogspot.com/2019/05/resolvendo-o-problema-kernel-driver-not.html

Create or Load a local cluster:
    ~$ minikube start --vm-driver=virtualbox

Visualize clusters:
    ~$ kubectl get nodes

- Forma Imperativa:

    Criação de um POD
        ~$ kubectl run [node-do-pod] --image=[nome-imagem:versao]
        ~$ kubectl run nginx-pod --image=nginx:latest

    Visualise Pods:
        ~$ kubectl get Pods
        ~$ kubectl get Pods -- watch
        ~$ kubectl get pods -o wide

    Visualise Descrição de um Pod:
        ~$ kubectl describe pod [node-do-pod]
        ~$ kubectl describe pod nginx-pod

    Atualizando configurações de um Pod:
        ~$ kubectl edit pod [node-do-pod]
        ~$ kubectl edit pod nginx-pod

    Removendo Pod:
        ~$ kubectl delete pod nginx-pod



- Forma Declarativa:

    ver arquivo: primeiro-pod.yaml
    ~$ kubectl apply -f [nome-arquivo.yaml]
    ~$ kubectl apply -f primeiro-pod.yaml

    Remover POD baseado no arquivo de definição:
    ~$ kubectl delete -f primeiro-pod.yaml

- Executar bash dentro do POD.
    ~$ kubectl exec -it portal-noticias -- bash
    CTRL + D para sair do POD


- Service
    ~$ kubectl get svc
    ~$ kubectl apply -f svc-pod-2.yaml

    para testar se o service vinculada ao Pod2
    nos conectamos pelo bash do pod1
    ~$ kubectl exec -it pod-1 -- bash
    enviamos uma requisicao para o pod 2 usando o IP da service

- NodePort
    Abre comunicação para fora do cluster
    Funciona dentro do cluster como um ClusterIP
    No windows é feito o bind para localhost
    No linux é preciso ver qual o ip do nó:
    
    ~$ kubectl get nodes -o wide

- LoadBalancer
    ClusterIP que permite a comuicação para o mundo externo ao cluster
    mas usando o load balancer do provedor clound.
    

Entendimento Geral

    Cluster é o local onde ficam os PODS.
    
    Um POD pode ter 1 ou vários containers.
    
    A principio é preciso ter uma imagem do docker para configurar 
    esta imagem em um container dentro do POD.

    Cada vez que um POD é criado ele recebe um IP.

    Para expor serviços e peritir a comunicação entre PODs utilizamos a SERVICE

    SERVICE:
        Abtração para expor aplicações executando 1 ou mais PODS
        Prove IP fixo para comunicação
        Prove DNS para os PODS
        Promove o balanceamento de carga

    Para vincular a Service ao Pod utilizamos as Labels.
    - setamos a label na Service
    - no pod vinculamos via spec.selector

