# 🧪 Plano de Teste — Sistema **InfoBairro**

---

## 1. Escopo

Este plano de teste tem como objetivo validar as funcionalidades do sistema **InfoBairro**, garantindo que os módulos principais operem conforme os **requisitos funcionais** e as **regras de negócio** estabelecidas.

### 📌 Módulos que serão testados

* **Autenticação** *(cadastro, login e controle de acesso)*
* **Gerenciamento de usuários**
* **Gerenciamento de bairros** *(cadastro, edição e exclusão)*
* **Visualização de bairros no mapa**
* **Sistema de avaliações**
* **Sistema de comentários**
* **Moderação de comentários**
* **Filtro e pesquisa de bairros**

### 🚫 Fora do escopo

* Testes internos da **API do Google Maps**
* Testes de **infraestrutura de hospedagem** *(servidor externo)*

---

## 2. Objetivo

O objetivo deste plano é:

* Verificar se o sistema atende aos **Requisitos Funcionais (RF)**
* Validar as **Regras de Negócio (RN)**
* Garantir que os diferentes perfis de usuário possuam **permissões corretas**
* Identificar falhas antes da entrega final
* Assegurar a **estabilidade do sistema** antes da implantação

---

## 3. Estratégia de Teste

Serão aplicados os seguintes tipos de teste:

### 🔹 Testes Funcionais

Validação de todas as funcionalidades descritas nos requisitos funcionais:

* Cadastro e login
* Cadastro, edição e exclusão de bairros
* Avaliação por critérios
* Publicação e visualização de comentários
* Curtidas em comentários
* Filtro por nome e categoria

### 🔹 Testes de Permissão *(Controle de Acesso)*

Verificação das permissões para os perfis:

* **ADMIN MASTER**
* **ADMIN**
* **USER**

### 🔹 Testes de Integração

* Integração com a **API do Google Maps**
* Integração entre módulos

  * Exemplo: exclusão de bairro removendo avaliações e comentários

### 🔹 Testes de Validação

* Verificação de **e-mail único**
* Validação de **senha**
* Limite de caracteres em comentários
* Bloqueio de conteúdo proibido

### 🔹 Testes de Moderação

* Verificação automática de comentários
* Encaminhamento para status **“pendente”**
* Aprovação e rejeição por administrador

---

## 4. Ambiente

Os testes serão realizados no seguinte ambiente:

* **Aplicação Web** *(versão de homologação)*
* **Navegadores**

  * Google Chrome
  * Microsoft Edge
* **Banco de Dados:** MySQL
* Integração com **API do Google Maps**
* Sistema executado em **ambiente local** ou **servidor de testes**

---

## 5. Critérios de Entrada

Os testes poderão ser iniciados quando:

* O desenvolvimento das funcionalidades estiver concluído
* O banco de dados estiver configurado
* A API do Google Maps estiver integrada e funcionando
* Os requisitos funcionais estiverem documentados
* A versão de testes estiver disponível

---

## 6. Critérios de Saída

Os testes serão considerados concluídos quando:

* **100%** dos requisitos funcionais forem testados
* Nenhum erro **crítico** estiver presente
* Erros **médios ou baixos** estiverem documentados
* As permissões de usuários estiverem funcionando corretamente
* A navegação no mapa estiver operando sem falhas

---

## 7. Responsáveis

### 👨‍💻 Execução de Testes Funcionais

**Responsáveis:** Gabriel Oliveira & Leandro Rivas
*Foco na garantia de que todas as funcionalidades operam conforme o esperado.*

### 📋 Validação de Regras de Negócio

**Responsáveis:** Arthur Michelangelo, Enya Sofia & Nicolly Brito
*Garantia de que as restrições e lógicas do sistema (RN) estão sendo cumpridas.*

### ✅ Revisão Final e Validação Geral

**Equipe Completa:**

* Arthur Michelangelo
* Enya Arruda
* Gabriel Oliveira
* Leandro Rivas
* Nicolly Brito

*Homologação final e controle de qualidade do projeto.*

---

> **Observação:** Este plano de teste visa assegurar a qualidade, confiabilidade e estabilidade do sistema **InfoBairro** antes de sua implantação final.
