# 1. Contexto do Sistema

O **InfoBairro** é uma aplicação web que permite aos usuários visualizar, avaliar e comentar sobre bairros por meio de um **mapa interativo integrado à API do Google Maps**.

O sistema permite:

- Cadastro e autenticação de usuários
- Cadastro, edição e exclusão de bairros
- Visualização de bairros no mapa com pins geográficos
- Avaliação de bairros por categorias
- Comentários na aba específica de cada bairro
- Filtro e pesquisa de bairros por nome ou critérios de avaliação

O sistema será utilizado por:

- Administradores
- Administradores Master
- Usuários

---

# 2. Perfis de Usuário

O sistema possui três perfis de acesso:

- **ADMIN MASTER**
- **ADMIN**
- **USER**

## Permissões

| Operação | ADMIN MASTER | ADMIN | USER |
|---|---|---|---|
| Registrar usuário | ✔ | ✔ | ✔ |
| Visualizar informações dos bairros | ✔ | ✔ | ✔ |
| Navegar pelo mapa | ✔ | ✔ | ✔ |
| Comentar | ✔ | ✔ | ✔ |
| Curtir comentário | ✔ | ✔ | ✔ |
| Avaliar bairro | ✔ | ✔ | ✔ |
| Criar bairros | ✔ | ✔ | ✖ |
| Editar bairros | ✔ | ✔ | ✖ |
| Excluir bairro | ✔ | ✖ | ✖ |
| Moderar comentários | ✔ | ✔ | ✖ |
| Gerenciar usuários (bloquear/excluir) | ✔ | ✔ | ✖ |
| Gerenciar administradores | ✔ | ✖ | ✖ |
| Filtrar bairros por critério | ✔ | ✔ | ✔ |

---

# 3. Requisitos Funcionais (RF)

## Módulo 1 – Bairro

**RF01** – O sistema deve permitir que o **ADMIN** cadastre novos bairros.  
**RF02** – O sistema deve permitir que o **ADMIN** edite as informações de um bairro.  
**RF03** – O sistema deve permitir que usuários visualizem os bairros cadastrados no mapa.  
**RF04** – O sistema deve permitir que o **ADMIN MASTER** exclua bairros.

---

## Módulo 2 – Avaliação

**RF05** – O sistema deve permitir que o usuário avalie bairros nos seguintes critérios:

- Segurança  
- Transporte  
- Infraestrutura  
- Educação  
- Saúde  
- Comércio  
- Lazer  
- Entregas
- Apps de Corrida

**RF06** – O sistema deve calcular e exibir a **média das avaliações de cada bairro**.  

**RF07** – O sistema deve permitir que o usuário visualize as avaliações já realizadas.

---

## Módulo 3 – Comentário

**RF08** – O sistema deve permitir que o usuário publique comentários na aba de comentários de cada bairro.  

**RF09** – O sistema deve permitir que usuários visualizem os comentários publicados.  

**RF10** – O sistema deve permitir que usuários curtam comentários.  

**RF11** – O sistema deve identificar automaticamente se o usuário é **morador ou visitante do bairro** e exibir o selo correspondente no comentário.  

**RF12** – O sistema deve submeter automaticamente todos os comentários a uma **verificação baseada na Política de Comunidade**.

---

## Módulo 4 – Usuário

**RF13** – O sistema deve permitir que o usuário realize cadastro utilizando **e-mail e senha válidos**.  

**RF14** – O sistema deve permitir que o usuário realize **login utilizando e-mail e senha cadastrados**.  

**RF15** – O sistema deve permitir que **administradores gerenciem contas de usuários (bloquear ou excluir)**.

---

## Módulo 5 – Endereço

**RF16** – O sistema deve permitir que o usuário **cadastre seu endereço** para validação de morador ou visitante.  

**RF17** – O sistema deve utilizar o **endereço cadastrado** para determinar o selo exibido nos comentários.

---

# 4. Regras de Negócio (RN)

## Autenticação

**RN01** – O e-mail do usuário deve ser **único no sistema**.  

**RN02** – A senha deve possuir **no mínimo 8 caracteres** e conter pelo menos:

- 1 letra maiúscula  
- 1 letra minúscula  
- 1 número
- 1 caractere especial

**RN03** – O acesso a funcionalidades administrativas deve ser **restrito a usuários com perfil ADMIN ou ADMIN MASTER**.

---

## Bairros

**RN04** – O nome do bairro **não pode ser duplicado** no sistema.  

**RN05** – Todas as **informações obrigatórias do bairro** devem ser preenchidas no momento do cadastro.  

**RN06** – A **coordenada geográfica (latitude e longitude)** deve ser definida no momento da criação do bairro.  

**RN07** – Dois bairros **não podem possuir a mesma coordenada geográfica**.  

**RN08** – Apenas **ADMIN MASTER** pode excluir bairros.

---

## Avaliações

**RN09** – Um usuário pode realizar **apenas uma avaliação por critério em cada bairro**.  

**RN10** – A **média das avaliações** deve ser recalculada automaticamente após cada nova avaliação ou edição.

---

## Comentários

**RN11** – Comentários que violem a **Política de Comunidade** devem ser encaminhados automaticamente para **moderação**.  

**RN12** – Comentários devem respeitar o **limite máximo de 800 caracteres**.  

**RN13** – Não são permitidos comentários contendo:

- Divulgação de serviços  
- Links externos  
- Endereços de e-mail  
- Redes sociais
- Divulgação de dados pessoais

**RN14** – Comentários são exibidos de forma **anônima para outros usuários**, mantendo a identidade visível **apenas para administradores**.

# 5. Endpoints da API

## Autenticação

| Método | Endpoint | Descrição |
|---|---|---|
| POST | `/auth/register` | Registro de usuário |
| POST | `/auth/login` | Login do usuário |
| POST | `/auth/logout` | Logout do usuário |
| GET | `/auth/me` | Retorna informações do usuário autenticado |

---

## Usuários

| Método | Endpoint | Descrição |
|---|---|---|
| GET | `/users/{id}` | Buscar usuário por ID |
| PATCH | `/users/{id}` | Atualizar informações do usuário |
| DELETE | `/users/{id}` | Excluir usuário |

---

## Bairros

| Método | Endpoint | Descrição |
|---|---|---|
| POST | `/neighborhoods` | Criar novo bairro |
| GET | `/neighborhoods` | Listar bairros |
| GET | `/neighborhoods/{id}` | Buscar bairro por ID |
| PATCH | `/neighborhoods/{id}` | Atualizar bairro |
| DELETE | `/neighborhoods/{id}` | Excluir bairro |
| GET | `/neighborhoods/search?name={nome}` | Buscar bairro por nome |
| GET | `/neighborhoods/filter?criteria={categoria}&order={asc|desc}` | Filtrar bairros por critério |

---

## Avaliações

| Método | Endpoint | Descrição |
|---|---|---|
| POST | `/neighborhoods/{id}/ratings` | Criar avaliação para um bairro |
| GET | `/neighborhoods/{id}/ratings` | Listar avaliações de um bairro |
| PATCH | `/ratings/{id}` | Atualizar avaliação |
| DELETE | `/ratings/{id}` | Remover avaliação |

### Categorias de Avaliação Disponíveis

- `segurança`
- `infraestrutura`
- `lazer`
- `transporte`
- `entrega`
- `apps_de_corrida`
- `saude`
- `comercio`
- `educacao`

---

## Comentários


| Método | Endpoint | Descrição |
|---|---|---|
| POST | /neighborhoods/{id}/comments | Criar comentário |
| GET | /neighborhoods/{id}/comments | Listar comentários |
| PATCH | /comments/{id} | Editar comentário |
| DELETE | /comments/{id} | Excluir comentário |

A edição de comentários é permitida apenas ao usuário autor do comentário
ou a administradores com permissão de moderação.

Comentários editados devem ser submetidos novamente
à verificação automática da Política de Comunidade.

### Exemplo de Requisição (PATCH)

```json
{
  "texto": "Comentário atualizado pelo usuário."
}

```
---

## Moderação (Administrador)

| Método | Endpoint | Descrição |
|---|---|---|
| GET | `/admin/comments/pending` | Listar comentários pendentes |
| PATCH | `/admin/comments/{id}/approve` | Aprovar comentário |
| PATCH | `/admin/comments/{id}/reject` | Rejeitar comentário |
| GET | `/admin/users` | Listar usuários |
| PATCH | `/admin/users/{id}/block` | Bloquear usuário |
| PATCH | `/admin/users/{id}/unblock` | Desbloquear usuário |

---

## 6. Regras de Autenticação

- A autenticação é baseada em token JWT.
- O token deve ser enviado no header:

Authorization: Bearer {token}

- Requisições sem token devem retornar **401 – Unauthorized**.
- Usuário autenticado sem permissão adequada deve retornar **403 – Forbidden**.
- Tokens expirados devem retornar **401**.
- Endpoints administrativos exigem role **ADMIN ou ADMIN MASTER**,
conforme a operação e as permissões definidas.
---


# 7. Fluxos Operacionais e Integração com Mapa

## 7.1 Fluxo de Moderação de Comentários

Todo comentário publicado no sistema deve passar automaticamente por uma verificação baseada na Política de Comunidade.

Fluxo:

1. O usuário publica o comentário
2. O sistema realiza verificação automática de conteúdo
3. Caso o comentário seja identificado como suspeito, seu status deve ser definido como **"pendente"**
4. Um administrador deverá decidir pela:
   - **aprovação**
   - **rejeição**

Comentários aprovados ficam visíveis aos usuários.
Comentários rejeitados permanecem ocultos.

---

## 7.2 Exclusão de Bairro

A exclusão de bairros é permitida exclusivamente ao perfil **ADMIN MASTER**.

Ao excluir um bairro, o sistema deve remover automaticamente todos os dados associados, incluindo:

- avaliações vinculadas
- comentários vinculados

Essa remoção deve ocorrer em **cascata**, garantindo a integridade dos dados.

---

## 7.3 Integração com Mapa

| Método | Endpoint | Descrição |
|---|---|---|
| GET | /map/neighborhoods | Retorna bairros para exibição no mapa |

Este endpoint é utilizado pelo frontend para renderizar os **marcadores geográficos (pins)** no mapa interativo integrado à API do Google Maps.

A resposta deve retornar uma lista contendo:

- id
- nome
- latitude
- longitude
- resumo das avaliações
- média geral
- quantidade de avaliações

As coordenadas devem ser retornadas em formato decimal compatível com a API do Google Maps.

### Exemplo de Resposta (200 - OK)

```json
{
  "status": 200,
  "data": [
    {
      "id": 1,
      "nome": "Centro",
      "latitude": -23.55052,
      "longitude": -46.633308,
      "media_geral": 4.5,
      "quantidade_avaliacoes": 120,
      "resumo_avaliacoes": {
        "seguranca": 4.2,
        "transporte": 4.8,
        "infraestrutura": 4.6,
        "apps_de_corrida": 4.7,
        "saude": 4.3,
        "comercio": 4.1,
        "educacao": 4.0,
        "lazer": 4.4,
        "entrega": 4.6
      }
    }
  ]
}
```
---

## 8. Considerações Gerais

- Todas as respostas devem retornar **status HTTP** adequado:

  - **200 – OK**
  - **201 – Created**
  - **204 – No Content**
  - **400 – Bad Request**
  - **401 – Unauthorized**
  - **403 – Forbidden**
  - **404 – Not Found**
  - **500 – Internal Server Error**

- Em caso de erro, o sistema deve retornar **mensagem descritiva no formato JSON**.
```
{
  "status": 400,
  "error": "Bad Request",
  "message": "O nome do bairro já está cadastrado."
}
```

- A API do mapa utiliza **integração com a API do Google Maps** para exibição dos **pins dos bairros cadastrados**.

- Todos os **dados sensíveis** devem ser armazenados de forma segura:
  - Senhas com **hash e salt**

- **Logs administrativos** devem registrar ações críticas, como:
  - Exclusão de bairro
  - Bloqueio de usuário
  - Remoção de comentário

---

# 9. Estrutura Mínima das Entidades

## 9.1 Usuário

A entidade usuário deve conter, no mínimo, os seguintes campos:

| Campo | Tipo | Descrição |
|---|---|---|
| id | integer | Identificador único do usuário |
| nome | string | Nome completo do usuário |
| email | string | E-mail único do usuário |
| senha_hash | string | Senha criptografada com hash e salt |
| role | string | Perfil de acesso (ADMIN_MASTER, ADMIN, USER) |
| endereco | string | Endereço cadastrado para validação |
| status | string | Ativo, bloqueado ou excluído |
| created_at | datetime | Data de criação |
| updated_at | datetime | Data de atualização |

---

## 9.2 Bairro

A entidade bairro deve conter, no mínimo:

| Campo | Tipo | Descrição |
|---|---|---|
| id | integer | Identificador único do bairro |
| nome | string | Nome do bairro |
| descricao | string | Descrição do bairro |
| latitude | decimal | Coordenada geográfica |
| longitude | decimal | Coordenada geográfica |
| media_geral | decimal | Média geral das avaliações |
| total_avaliacoes | integer | Quantidade de avaliações |
| created_at | datetime | Data de criação |
| updated_at | datetime | Data de atualização |

---

## 9.3 Avaliação

A entidade avaliação deve conter:

| Campo | Tipo | Descrição |
|---|---|---|
| id | integer | Identificador da avaliação |
| user_id | integer | Usuário que avaliou |
| neighborhood_id | integer | Bairro avaliado |
| criteria | string | Categoria avaliada |
| score | integer | Nota atribuída (1 a 5) |
| created_at | datetime | Data da avaliação |
| updated_at | datetime | Data de atualização |

---

## 9.4 Comentário

A entidade comentário deve conter:

| Campo | Tipo | Descrição |
|---|---|---|
| id | integer | Identificador do comentário |
| user_id | integer | Usuário autor |
| neighborhood_id | integer | Bairro relacionado |
| texto | string | Conteúdo do comentário |
| selo_usuario | string | Morador ou visitante |
| status | string | Aprovado, pendente ou rejeitado |
| curtidas | integer | Número de curtidas |
| created_at | datetime | Data de criação |
| updated_at | datetime | Data de atualização |

<p align="center">
  <b>InfoBairro</b> - Documentação de Requisitos e API<br>
  Última atualização: 08 de Abril de 2026
</p>





