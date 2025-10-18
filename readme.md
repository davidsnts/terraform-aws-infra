# Infraestrutura AWS Completa com Terraform

Este projeto utiliza **Terraform** para provisionar uma infraestrutura robusta na **Amazon Web Services (AWS)**. A configuração cria uma **Rede Virtual Privada (VPC)** com alta disponibilidade, um **Servidor Web (EC2)**, um **Balanceador de Carga (ALB)** e um **Banco de Dados Gerenciado (RDS - PostgreSQL)**.

---

## Arquitetura do Projeto

* **VPC em `us-east-1`**: A base da rede, com o bloco CIDR `10.0.0.0/16`.
* **Subnets Públicas**: Duas subnets (`10.0.1.0/24` e `10.0.2.0/24`) distribuídas em **duas Zonas de Disponibilidade (us-east-1a e us-east-1b)** para garantir tolerância a falhas.
* **Internet Gateway (IGW)** e **Tabela de Rotas**: Permitem que o tráfego das subnets se comunique com a Internet.
* **Security Group (`ec2-sg`)**: Atua como firewall, permitindo **tráfego SSH (porta 22)** e **HTTP (porta 80)** de qualquer lugar (`0.0.0.0/0`).
* **Instância EC2 (`t2.micro`)**: Servidor web executando **Amazon Linux 2**, com Apache instalado via `user-data` para servir uma página de teste na porta 80.
* **Application Load Balancer (ALB)**: Distribui o tráfego HTTP entre as subnets A e B, apontando para o Servidor Web através de um **Target Group**.
* **RDS PostgreSQL (`db.t3.micro`)**: Um banco de dados gerenciado em duas subnets para alta disponibilidade, com acesso público habilitado (configuração **apenas para desenvolvimento/teste**).

---

## Pré-requisitos
Para rodar este projeto, você precisará ter instalado:

1.  **Terraform** (versão 1.0 ou superior).
2.  **AWS CLI** configurada com credenciais de acesso válidas (usuário com permissões de administrador/provisionamento de recursos).

---

## Como Executar a Implantação

1.  **Inicialize o Terraform:**
    terraform init
    
2.  **Planeje a Implantação:**
    terraform plan

3.  **Aplique a Configuração:**
   
    terraform apply

---

## Como Destruir a Infraestrutura

Para evitar custos e limpar todos os recursos provisionados na AWS, execute o comando:

terraform destroy