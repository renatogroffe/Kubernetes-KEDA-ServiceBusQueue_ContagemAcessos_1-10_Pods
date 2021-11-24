# Kubernetes-KEDA-ServiceBusQueue_ContagemAcessos_1-10_Pods
Objetos para Deployment de um Worker Service (contagem de acessos) no Kubernetes utilizando KEDA, Helm, Azure Service Bus (Queue) e um Worker criado .NET 6. Foi definido um ScaledObject com um mínimo de 1 e um máximo de 10 Pods.

Worker Service para consumo de **mensagens vinculadas a uma fila do Azure Service Bus** (imagem **renatogroffe/workercontagem-servicebusqueue-dotnet6**) - é justamente esta aplicação que será escalada via **KEDA**:

**https://github.com/renatogroffe/DotNet6-WorkerService-AzureServiceBus-SqlServer_ContagemAcessos**

Projeto que serviu de base para o **envio de mensagens a uma fila do Azure Service Bus** (imagem **renatogroffe/apicontagem-servicebusqueue-dotnet6**):

**https://github.com/renatogroffe/ASPNETCore6-REST_API-AzureServiceBus_ContagemAcessos**

No arquivo **keda-instalacao&sdot;sh** estão as instruções para instalação do KEDA **(Kubernetes Event-driven Autoscaling)** em um **cluster Kubernetes**.

Para os testes de carga que escalam a aplicação utilizei o pacote npm [**loadtest**](https://www.npmjs.com/package/loadtest). O exemplo a seguir procerá com o envio de **3 mil requisições**, simulando **50 usuários concorrentes**:

**loadtest -c 50 -n 3000 -k** ***ENDPOINT***