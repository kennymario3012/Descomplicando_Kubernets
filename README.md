Este repósitorio do Descomplicado Kubernets faz parte do treinamento [PICK 2024](https://github.com/leandrohv/pick2024) da [Linux Tips](https://github.com/badtuxx/DescomplicandoKubernetes). aqui apresentou as instruções para configurar um cluster de Kubernetes com dois nós usando o Minikube e a CLI do Linux, bem como os manifestos yaml utilizado durante os dias do programa.

# Configuração de um Cluster de Dois Nós no Minikube

## Pré-requisitos

- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
- [Docker](https://docs.docker.com/engine/install/ubuntu/)

- Para esse caso vamos installar o Minikube em docker para evitar termos de criar um maquina vituall aonde teriamde de ter a virtualização habilitada na sua máquina (por exemplo, VirtualBox, KVM)

## Passos para Configurar o Cluster

### 1. Instale o Minikube e o Kubectl

Siga as instruções de instalação para Minikube e Kubectl nos links fornecidos nos pré-requisitos.

### 2. Inicie o Minikube com Configurações de Multi-Node

Para iniciar o Minikube com um cluster de dois nós, você pode usar o seguinte comando:

```bash
minikube start --nodes 2 minikube
```

### 3. Verifique os Nós do Cluster

Depois que o Minikube estiver em execução, você pode verificar os nós do cluster com o comando:

```bash
kubectl get nodes
```

Você deve ver a saída indicando dois nós, um master e um worker:

```plaintext
NAME           STATUS   ROLES    AGE   VERSION
minikube       Ready    master   2m    v1.28.3
minikube-m02   Ready    <none>   1m    v1.28.3
```

### 4. Executar um Pod no Cluster

Agora para testar o nosso cluster bem como o nosso yaml vamos executat utilizadno esse comado.:

```bash
kubectl apply -f giropops/pod.yaml
```

### 5. Exponha o Pod

Depois de criar o nosso pod, devemos expor por intermedio de um serviçis para poder acessalo.

```bash
kubectl expose pod giropops --type=NodePort
```

### 6. Acesse o Serviço

Recupere a URL para acessar o serviço:

```bash
minikube service giropops --url
```

Acesse a URL fornecida no seu navegador para verificar se o serviço está funcionando corretamente.

## Problemas Comuns

### 1. Minikube Não Inicia

Certifique-se de que a virtualização está habilitada na BIOS do seu sistema e que você possui um hipervisor compatível instalado.

### 2. Nodes Não Mostram Status "Ready"

Se os nós não mostrarem o status "Ready", pode ser necessário mais tempo para o cluster se configurar. Você também pode verificar logs para diagnosticar problemas:

```bash
kubectl describe nodes
```

## Limpeza

Para parar e excluir o cluster Minikube:

```bash
minikube stop
minikube delete
```

## Conclusão

Parabes configuramos com sucesso um cluster de Kubernetes com dois nós usando Minikube. Agora podemos explorar mais recursos do Kubernetes e implantar as nossas próprias aplicações no cluster. Somso Zikass de mais.

## Referências

- [Documentação do Minikube](https://minikube.sigs.k8s.io/docs/)
- [Documentação do Kubernetes](https://kubernetes.io/docs/home/)
- [Documentação do Descomplicado Kubernets](https://github.com/badtuxx/DescomplicandoKubernetes)
```