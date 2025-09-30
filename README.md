# 🧱 Bootstrap Kubernetes – Cluster Setup Inicial (Hack SOAT)

Este repositório contém os recursos essenciais de **bootstrap** do cluster Kubernetes para o projeto **Sistema de Processamento de Vídeos – FIAP X**.  
Ele prepara o cluster com componentes fundamentais, garantindo que os microsserviços possam ser implantados de forma segura, escalável e automatizada.

---

## 📦 Visão Geral

O bootstrap é executado **antes do deploy da infraestrutura de microsserviços** e provisiona:

- 🎛️ **Ingress Controller (NGINX)** – roteamento de tráfego externo.  
- 🔐 **External Secrets** – integração com gerenciadores de segredos (ex.: AWS Secrets Manager).  
- 🤖 **Integração com GitHub Actions** – via `aws-creds-secret.yaml` para deploys automatizados.  
- 🗂️ **ClusterSecretStore** – sincronização de segredos externos para pods.  
- ⚙️ **Workflows de automação** – pipelines definidos em `.github/workflows/*.yml`.  

---

## 🛠️ Tecnologias Utilizadas

- **Kubernetes** (cluster provisionado previamente)  
- **kubectl** – gerenciamento do cluster  
- **Helm** (opcional para instalação de pacotes)  
- **Ingress NGINX**  
- **External Secrets Operator**  
- **Secrets Manager** (ex.: AWS)  
- **GitHub Actions** – CI/CD  

---

## 🧩 Pré-requisitos

- Cluster Kubernetes já provisionado (ex.: via Terraform do repositório de infraestrutura).  
- [kubectl](https://kubernetes.io/docs/tasks/tools/) instalado e configurado.  
- Acesso a um repositório GitHub com permissões de CI/CD.  
- Permissões de acesso ao provedor cloud (EKS + Secrets Manager no caso da AWS).  

---

## 🚀 Como Utilizar

### 1. Aplicar Ingress Controller

```bash
kubectl apply -f ingress/ingress.yml
```

### 2. Criar Segredos de Acesso ao Provedor

```bash
kubectl apply -f templates/aws-creds-secret.yaml
```

Esse recurso é consumido pelos workflows do GitHub Actions para autenticação no provedor.

### 3. Configurar External Secrets Operator

```bash
kubectl apply -f external-secrets/cluster-secret-store.yaml
```

Esse recurso conecta o cluster ao gerenciador de segredos e os disponibiliza como variáveis em pods.

---

## ⚙️ Workflows Automatizados

Os workflows definidos em `.github/workflows/*.yml` permitem:

- Deploy contínuo de segredos.  
- Validação automática da configuração do cluster.  
- Atualização dos componentes de bootstrap.  

---

## 👨‍💻 Autores

Projeto desenvolvido pelo grupo SOAT 67 para o Hackaton - Pós-Graduação em Arquitetura de Software (FIAP).
