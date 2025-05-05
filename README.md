# MACN_Projetcs_DIO_LAB3
Lab 3 do Bootcamb de MACN (Microsoft Azure Cloud Native)

#### Aviso: Este código foi fornecido pelo instrutor do curso de Microsoft Azure Cloud Native na plataforma DIO. O código original foi fornecido pelo instrutor Henrique Eduardo Souza e pode ser acessado no seguinte repositório:https://github.com/digitalinnovationone/Microsoft_Application_Platform

Publicando seu App no Azure Container Apps com Azure CLI
Este guia mostra como subir uma imagem Docker para o Azure Container Registry (ACR) e executá-la no Azure Container Apps.

✅ Pré-requisitos
Docker instalado e a imagem blog-renato-app:latest criada localmente.

Azure CLI instalado e autenticado com az login.

1. 🔐 Login no Azure
```powershell
az login
```

2. 🗂️ Criar um Resource Group
```powershell
az group create --name containerappslab03 --location eastus
```

3. 🗃️ Criar o Azure Container Registry (ACR)
```powershell
az acr create --resource-group containerappslab03 --name blogrenatoacr --sku Basic
```

4. 🔐 Logar no ACR
```powershell
az acr login --name blogrenatoacr
```

5. 🏷️ Taggear a imagem Docker local
```powershell
docker tag blog-renato-app:latest blogrenatoacr.azurecr.io/blog-renato-app:latest
```

6. ⬆️ Enviar a imagem para o ACR
```powershell
docker push blogrenatoacr.azurecr.io/blog-renato-app:latest
```

7. 🌐 Criar um ambiente para Container App
```powershell
az containerapp env create \
  --name blog-renato-env \
  --resource-group containerappslab03 \
  --location eastus
```

8. 🚀 Criar o Container App
```powershell
az containerapp create \
  --name blog-renato-app \
  --resource-group containerappslab03 \
  --image blogrenatoacr.azurecr.io/blog-renato-app:latest \
  --environment blog-renato-env \
  --target-port 80 \
  --ingress external \
  --registry-server blogrenatoacr.azurecr.io \
  --registry-username blogrenatoacr \
  --registry-password <SUA-SENHA-DO-ACR>
```

## Insights e Possibilidades de uso com o Container Apps

### Escalabilidade automática
O Azure Container Apps é superinteligente quando se trata de escalabilidade. Ele pode aumentar ou diminuir a quantidade de instâncias dos seus contêineres automaticamente, dependendo do uso de recursos como CPU e memória, ou até mesmo do volume de requisições. Isso significa que você não precisa se preocupar em ajustar manualmente o número de contêineres — o sistema faz isso por você.

### Microserviços e simplicidade
Se você está trabalhando com uma arquitetura de microserviços, o Azure Container Apps é um ótimo parceiro. Ele facilita a comunicação entre os diferentes serviços e a execução de múltiplos contêineres. E o melhor de tudo: você pode começar com uma abordagem simples, sem a complexidade de algo como o Kubernetes. Caso precise de mais flexibilidade no futuro, ele também integra bem com outras ferramentas como o Azure Kubernetes Service (AKS).

### Integração com outros serviços
O Azure Container Apps se conecta com outras ferramentas da Microsoft, como o Azure Functions, Azure Logic Apps, e Event Grid. Isso facilita a criação de fluxos de trabalho complexos e permite que seus contêineres respondam a eventos ou mudanças de dados de forma dinâmica e eficiente. Além disso, você pode configurar seu ambiente de execução de forma simples, sem precisar de muita configuração manual.

### Aplicações versáteis
Não importa se você está rodando um simples site, uma API ou até mesmo processamentos em segundo plano, o Azure Container Apps é flexível o suficiente para rodar todos esses tipos de carga de trabalho. Ele também pode ser ótimo para tarefas que precisam rodar em momentos específicos, como processamento de dados ou execução de jobs agendados.

### Segurança e redes
Você pode configurar seus contêineres para rodar em redes privadas, garantindo uma camada extra de segurança. Isso é útil se você precisar que seus serviços se comuniquem de forma segura e isolada. Além disso, o Azure Container Apps integra-se bem com o Azure Virtual Network, permitindo que você se conecte de maneira segura aos seus bancos de dados e outros recursos privados.

### Preço sob demanda
E talvez uma das melhores características seja o modelo de pagamento por uso. Você paga apenas pelo tempo que seus contêineres estão em execução. Isso é perfeito para quem tem cargas de trabalho intermitentes ou variáveis, pois você pode reduzir custos quando a aplicação não estiver em uso, escalando para zero quando não houver tráfego.

### Monitoramento simplificado
Para quem quer ficar de olho no que está acontecendo, o Azure Container Apps se integra de forma simples com o Azure Monitor e Application Insights, permitindo que você veja métricas como uso de CPU, memória e requisições em tempo real. Isso ajuda a otimizar a aplicação e detectar problemas rapidamente.

## Principais Tópicos Aprendidos no Curso

- Funcionamento de Release Canário e Blue-Green
- Docker Básico
- Comandos Azure CLI
- Git básico


## OBS: Adicionar prints da ferramenta em produção no diretório /Prints
