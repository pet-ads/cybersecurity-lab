## Tokens

Em aplicações web, um **token** funciona como uma credencial digital que substitui o envio constante de login e senha.

Ele é usado para:

- Identificar o usuário
- Definir permissões de acesso (autorização)
- Manter autenticação em requisições subsequentes

### Vantagens

- Reduz validações constantes no banco de dados  
- Melhora desempenho da aplicação  
- Aumenta a segurança ao evitar envio repetido de credenciais  

### Tipos comuns de tokens

- **Access Token** → usado para acessar APIs (geralmente via `Authorization: Bearer`)  
- **OTP (One-Time Password)** → senha de uso único para validação temporária  

---

## JWT (JSON Web Token)

O **JWT** é um padrão aberto para transmissão segura de informações entre partes.

Ele é:

- Leve  
- Independente de linguagem  
- Autocontido (contém todas as informações necessárias)  

### Estrutura de um JWT

Um JWT é composto por três partes separadas por ponto (`.`):

```
.Header
.Payload
.Signature
```

---

### Header

Define:

- Tipo do token (JWT)  
- Algoritmo de assinatura (ex: HMAC SHA256, RSA)  

---

### Payload

O payload contém as chamadas **claims**, que são as informações do usuário, como ID, email e permissões. Também pode incluir dados como tempo de expiração., como:

- ID do usuário  
- Email  
- Permissões (roles)  
- Expiração do token (`exp`)  

Importante:  
O payload **não é criptografado**, apenas codificado em Base64.  
Nunca armazene senhas aqui.

---

### Signature

A assinatura garante a integridade do token.

Ela é gerada usando:

- Header + Payload  
- Uma chave secreta do servidor  

Isso impede alterações não autorizadas no token.

---

## Refresh Token e controle de sessão

Access tokens possuem **curta duração** (minutos ou horas) para reduzir riscos em caso de vazamento.

### Como funciona:

1. Usuário faz login  
2. Recebe:
   - Access Token (curta duração)  
   - Refresh Token (longa duração)  
3. Access token expira  
4. Cliente usa refresh token para solicitar um novo access token  

---

### Boas práticas

- Armazenar refresh token com segurança (preferencialmente no servidor)  
- Permitir revogação (logout / bloqueio de conta)  
- Usar **rotação de refresh tokens** (cada uso gera um novo)  

---

## CORS (Cross-Origin Resource Sharing)

O **CORS** é um mecanismo de segurança dos navegadores que controla requisições entre diferentes origens.

### O que é uma origem?

Uma origem é composta por:

- Protocolo (http / https)  
- Domínio  
- Porta  

Se qualquer um for diferente → origem diferente.

---

### O problema

Por padrão, navegadores bloqueiam requisições entre origens diferentes.

---

### Solução

O servidor precisa permitir explicitamente o acesso via headers:

```
Access-Control-Allow-Origin
```

---

### Preflight Request

Para requisições mais complexas, o navegador envia uma verificação prévia:

- Método: `OPTIONS`  
- Objetivo: verificar se o servidor permite a requisição  

---

## Fundamentos de cibersegurança aplicada

###  Segurança de senhas

Senhas nunca devem ser armazenadas em texto puro.

Solução:
**utiliza-se técnicas de hashing**
- Hashing com algoritmos seguros:
  - bcrypt  
  - Argon2  
  - scrypt  

---

###  Comunicação segura

O uso de **HTTPS (TLS)** garante:

- Criptografia dos dados em trânsito  
- Proteção contra interceptação (MITM)  

---




## Resumo geral

Esses conceitos trabalham juntos para garantir a segurança de aplicações modernas:

- **Tokens e JWT** → autenticação e autorização  
- **Refresh Tokens** → continuidade segura de sessão  
- **CORS** → controle de acesso entre domínios  
- **Hashing + HTTPS** → proteção de dados sensíveis  
- **OWASP + boas práticas** → prevenção de vulnerabilidades  

---

##  Conclusão

Segurança em aplicações web não depende de um único recurso, mas da combinação de múltiplas camadas de proteção.

Quanto mais camadas (defense in depth), mais difícil se torna explorar vulnerabilidades em um sistema.

<br>

[![➡ Próxima Seção](https://img.shields.io/badge/-➡_Próxima_Seção-blue?style=for-the-badge&color=007BFF)](https://github.com/pet-ads/cybersecurity-lab/blob/main/Guia%20de%20Estudos/4%20-%20Vulnerabilidade%20Cr%C3%ADticas/1%20-%20SQL%20Injection.md)

## LINKS EXTRAS

-[Token // Dicionário do Programador](https://youtu.be/LtVb9rhU41c?si=0M0fK2r-UwBcrQcQ)

-[REFRESH TOKEN DA FORMA CERTA](https://youtu.be/t5iumvSNbgM?si=M_Cq0YUkl-uydUIk)

-[Implementando Refresh Token utilizando JWT](https://youtu.be/5LaGTbPyZcc?si=gJMGK3JCYWHUie3I)

-[JWT (JSON Web Token - Autenticação e Segurança) // Dicionário do Programador](https://youtu.be/Gyq-yeot8qM?si=vROGNmsTrDRdQlDO)

-[CORS (Cross-Origin Resource Sharing em 6 minutos) // Dicionário do Programador](https://youtu.be/GZV-FUdeVwE?si=58-RrXdXRSTzBhsF)

-[COMO FUNCIONA O CORS NA PRÁTICA](https://youtu.be/1V1qkh6K8Gg?si=2YQieO3VlAUFkpDN)