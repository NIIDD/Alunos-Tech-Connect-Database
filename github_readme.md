# Alunos Tech Connect - Enterprise Database Architecture

[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16%2B-blue?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![PL/pgSQL](https://img.shields.io/badge/PL%2FpgSQL-Procedural-green?style=for-the-badge)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)]()

Repositório dedicado à modelagem, otimização e programação do subsistema de banco de dados relacional desenvolvido para a plataforma corporativa **Alunos Tech Connect**. Este projeto faz parte do PIM VIII (Projeto Integrado Multidisciplinar) do curso superior de Tecnologia em Análise e Desenvolvimento de Sistemas.

---

## Sobre o Projeto

A **Alunos Tech Connect** é uma plataforma corporativa integrada desenhada para centralizar o gerenciamento de serviços digitais, clientes corporativos, solicitações de suporte, equipes operacionais e tarefas em campo. 

Como **Administrador de Banco de Dados (DBA) / Arquiteto de Dados**, minha responsabilidade concentrou-se em projetar uma arquitetura de persistência robusta em **PostgreSQL**, garantindo alta performance analítica, segurança estrita de dados, trilhas de auditoria automatizadas, controle de concorrência e total conformidade com a LGPD.

---

## Modelagem Relacional & Entidades (11 Core Entities)

O esquema relacional foi rigorosamente normalizado para evitar redundâncias e assegurar integridade referencial (*ACID*):

1. **`perfil`**: Papéis de acesso ao sistema (Gestor, Colaborador, Administrativo, Cliente, Admin de TI).
2. **`usuario`**: Cadastro centralizado de operadores e credenciais de segurança.
3. **`cliente`**: Diretório corporativo de clientes (com validação fiscal e sinalizadores LGPD).
4. **`servico`**: Catálogo de serviços com prazos contratuais de SLA.
5. **`cliente_servico`**: Relociação N:N de serviços contratados por cliente.
6. **`equipe`**: Agrupamentos operacionais supervisionados por gestores.
7. **`usuario_equipe`**: Tabela associativa para alocação flexível de colaboradores em múltiplas equipes.
8. **`solicitacao`**: Chamados de suporte abertos por clientes, controlando ciclos de status e prioridades.
9. **`tarefa`**: Desdobramento operacional das solicitações direcionadas aos colaboradores em campo (*Mobile*).
10. **`comentario`**: Histórico de interações transparentes nas solicitações.
11. **`notificacao`**: Central de alertas em tempo real e monitoramento de SLA.
12. **`log_acesso`**: Trilha de auditoria imutável para ações sensíveis de segurança.

---

## Diferenciais Técnicos & Objetos Programáveis (PL/pgSQL)

O repositório contém scripts avançados desenvolvidos em PostgreSQL:

* **Triggers de Auditoria Automática (US08):** Gatilhos em PL/pgSQL que capturam alterações críticas na base de dados (`INSERT`, `UPDATE`, `DELETE`) e registram logs imutáveis com rastreabilidade de IP e timestamp.
* **Funções de Cálculo de SLA (US05/US09):** Funções procedurais otimizadas para o cálculo automático de prazos limite com base nas horas contratuais do serviço.
* **Stored Procedures Transacionais (US09):** Procedimentos para a triagem e conversão atômica de solicitações em tarefas operacionais para equipes de campo.
* **Controle de Concorrência Otimista (US10):** Mecanismo baseado em controle de versão de linha (`versao_concorrencia`) para impedir sobrescrita de dados (*Lost Update*) em atualizações simultâneas via aplicativo móvel.
* **Governança de Dados e LGPD (US15):** Procedure dedicada ao mascaramento reversível de dados pessoais de clientes solicitantes, garantindo conformidade regulatória sem corromper as chaves estrangeiras relacionais.
* **Otimização de Consultas (US13):** Índices não clusterizados (`CREATE INDEX`) estrategicamente posicionados nas chaves estrangeiras e campos de filtro frequente para acelerar o painel de indicadores gerenciais.

---

## Como Executar os Scripts

1. Certifique-se de ter o **PostgreSQL 16+** e o **pgAdmin 4** instalados em sua máquina.
2. Crie uma nova base de dados chamada `alunos_tech_db`:
   ```sql
   CREATE DATABASE alunos_tech_db;
   ```
3. Execute o script DDL de criação de tabelas e índices.
4. Execute os blocos de funções, triggers e procedures em PL/pgSQL para habilitar a lógica de negócio no servidor.

---

## Autor

Desenvolvido por **Cainã Lopes Gonçalves / NIIDD** como parte do ecossistema técnico do PIM VIII - Análise e Desenvolvimento de Sistemas.