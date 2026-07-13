# HTTP, HTTPS e Cybersegurança

## Introdução

A comunicação entre usuários e servidores na Internet ocorre por meio de protocolos de rede. Entre eles, o **HTTP (Hypertext Transfer Protocol)** é o principal responsável pela troca de informações entre navegadores e servidores web.

Com o crescimento das ameaças cibernéticas, surgiu a necessidade de proteger essa comunicação contra interceptações, alterações maliciosas e roubo de dados. Para isso foi criado o **HTTPS (Hypertext Transfer Protocol Secure)**, que adiciona uma camada de segurança baseada em criptografia.

Compreender o funcionamento do HTTP e do HTTPS é fundamental para profissionais de **Cybersegurança**, **Desenvolvimento Web**, **Redes de Computadores** e **Administração de Sistemas**.

---

# O que é HTTP?

O **HTTP (Hypertext Transfer Protocol)** é um protocolo da camada de aplicação utilizado para comunicação entre clientes e servidores na Web.

Ele permite a transferência de diversos tipos de recursos, como:

- Páginas HTML
- Imagens
- Vídeos
- Arquivos
- Dados JSON
- Dados XML
- APIs REST

O HTTP é um protocolo **stateless** (sem estado), ou seja, cada requisição é tratada de forma independente.

---

## Funcionamento Básico

Quando um usuário acessa um site:

1. O navegador envia uma requisição ao servidor.
2. O servidor processa a solicitação.
3. O servidor retorna uma resposta.
4. O navegador interpreta e exibe o conteúdo.

Esse processo acontece constantemente durante o carregamento e utilização de uma aplicação web.

```text
Cliente (Browser)
        |
        | Request
        v
Servidor Web
        |
        | Response
        v
Cliente (Browser)
```

---

# O Modelo TCP/IP

O HTTP depende da pilha de protocolos TCP/IP para funcionar.

| Camada | Protocolo | Função |
|----------|----------|----------|
| Aplicação | HTTP / HTTPS | Comunicação Web |
| Transporte | TCP | Entrega confiável dos dados |
| Internet | IP | Endereçamento e roteamento |
| Acesso à Rede | Ethernet / Wi-Fi | Transmissão física |

---

## Exemplo de Comunicação

Ao acessar um site:

- O HTTP define o conteúdo da mensagem.
- O TCP garante a entrega correta dos dados.
- O IP encontra o caminho até o destino.
- A rede física transporta os pacotes.

---

# Comunicação HTTP: Request e Response

Toda comunicação HTTP segue o modelo:

```text
Cliente → Servidor → Cliente
```

---

## Request (Requisição)

É a mensagem enviada pelo cliente ao servidor.

### Exemplo

```http
GET /index.html HTTP/1.1
Host: exemplo.com
User-Agent: Chrome
```

---

### Componentes da Requisição

#### Método HTTP

Define a ação desejada.

| Método | Função |
|----------|----------|
| GET | Buscar informações |
| POST | Enviar dados |
| PUT | Atualizar recurso completo |
| PATCH | Atualização parcial |
| DELETE | Remover recurso |
| HEAD | Obter apenas cabeçalhos |
| OPTIONS | Consultar métodos permitidos |

---

#### Headers (Cabeçalhos)

Contêm informações adicionais:

- Navegador utilizado
- Cookies
- Idioma
- Tipo de conteúdo
- Dados de autenticação
- Controle de cache

---

#### Body (Corpo)

Utilizado principalmente em:

- POST
- PUT
- PATCH

Exemplo:

```json
{
  "usuario": "admin",
  "senha": "123456"
}
```

---

## Response (Resposta)

Mensagem enviada pelo servidor ao cliente.

### Exemplo

```http
HTTP/1.1 200 OK
Content-Type: text/html
```

---

### Componentes da Resposta

#### Linha de Status

Indica o resultado da operação.

#### Headers

Informações sobre:

- Tipo do conteúdo
- Tamanho do arquivo
- Cache
- Compressão
- Segurança

#### Body

Contém os dados retornados:

- HTML
- JSON
- XML
- Imagens
- Vídeos

---

# Métodos HTTP e Segurança

Nem todos os métodos apresentam o mesmo nível de risco.

| Método | Possível Risco |
|----------|----------|
| GET | Exposição de dados na URL |
| POST | Envio de informações sensíveis |
| PUT | Alteração de recursos |
| PATCH | Modificação parcial de dados |
| DELETE | Exclusão de informações críticas |

---

## Boas Práticas

- Nunca enviar senhas por GET.
- Implementar autenticação.
- Utilizar HTTPS.
- Validar entradas do usuário.
- Aplicar controle de acesso.
- Registrar ações críticas em logs.

---

# Códigos de Status HTTP

Os códigos HTTP indicam o resultado de uma operação.

---

## 1xx – Informativos

| Código | Significado |
|----------|----------|
| 100 | Continue |

---

## 2xx – Sucesso

| Código | Significado |
|----------|----------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |

---

## 3xx – Redirecionamento

| Código | Significado |
|----------|----------|
| 301 | Moved Permanently |
| 302 | Found |
| 304 | Not Modified |

---

## 4xx – Erro do Cliente

| Código | Significado |
|----------|----------|
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 429 | Too Many Requests |

---

## 5xx – Erro do Servidor

| Código | Significado |
|----------|----------|
| 500 | Internal Server Error |
| 502 | Bad Gateway |
| 503 | Service Unavailable |
| 504 | Gateway Timeout |

---

# 6. O Problema do HTTP

O HTTP transmite informações em **texto puro (Plain Text)**.

Isso significa que qualquer pessoa com acesso ao tráfego pode visualizar os dados transmitidos.

---

## Informações Expostas

- Usuários
- Senhas
- Cookies
- Tokens
- Dados financeiros
- Informações pessoais

---

## Ataques Possíveis

### Sniffing

Captura de pacotes trafegando na rede.

### Man-in-the-Middle (MITM)

Interceptação da comunicação entre cliente e servidor.

### Session Hijacking

Roubo de cookies de autenticação.

### Credential Theft

Roubo de credenciais transmitidas sem proteção.

---

# O que é HTTPS?

O **HTTPS (Hypertext Transfer Protocol Secure)** é a versão segura do HTTP.

Ele utiliza o protocolo **TLS (Transport Layer Security)** para proteger a comunicação.

---

## Benefícios

### Confidencialidade

Impede que terceiros visualizem os dados.

### Integridade

Garante que as informações não foram alteradas.

### Autenticação

Confirma a identidade do servidor.

---

# O Papel do TLS

O **TLS (Transport Layer Security)** é o protocolo responsável pela segurança do HTTPS.

Ele substituiu o antigo SSL, atualmente considerado inseguro.

---

## Principais Funções

### Criptografia

Protege os dados durante a transmissão.

### Integridade

Detecta alterações indevidas nas mensagens.

### Autenticação

Valida a identidade do servidor.

---

# TLS Handshake

Antes da comunicação criptografada, ocorre o processo conhecido como **TLS Handshake**.

---

## Etapas Simplificadas

1. Cliente inicia a conexão.
2. Servidor envia seu certificado digital.
3. Cliente valida o certificado.
4. As partes negociam algoritmos criptográficos.
5. É criada uma chave de sessão.
6. A comunicação passa a ser criptografada.

```text
Cliente --------> Servidor
   Client Hello

Cliente <-------- Servidor
  Server Hello
  Certificado

Cliente --------> Servidor
 Validação e Chaves

Comunicação Segura Estabelecida
```

---

# Certificados Digitais

Os certificados digitais funcionam como uma identidade eletrônica dos sites.

São emitidos por uma **Autoridade Certificadora (CA - Certificate Authority)**.

---

## Exemplos de Autoridades Certificadoras

- Let's Encrypt
- DigiCert
- Sectigo
- GlobalSign

---

## Verificações Realizadas pelo Navegador

- Autenticidade
- Validade
- Assinatura digital
- Correspondência com o domínio

Se alguma verificação falhar, o navegador exibe um alerta de segurança.

---

# Cybersegurança Aplicada ao HTTP e HTTPS

## Principais Ameaças

### Sniffing

Captura de pacotes na rede.

### Man-in-the-Middle (MITM)

Interceptação e possível alteração da comunicação.

### Session Hijacking

Sequestro de sessões autenticadas.

### Phishing

Criação de páginas falsas para roubo de credenciais.

### SSL Stripping

Ataque que tenta forçar o uso de HTTP em vez de HTTPS.

### DNS Spoofing

Redirecionamento da vítima para servidores falsos.

---

# Cabeçalhos de Segurança HTTP

Os cabeçalhos de segurança ajudam a fortalecer aplicações web.

---

## HSTS

```http
Strict-Transport-Security: max-age=31536000
```

Força o uso de HTTPS.

---

## CSP

```http
Content-Security-Policy
```

Ajuda a prevenir ataques XSS.

---

## X-Frame-Options

```http
X-Frame-Options: DENY
```

Protege contra Clickjacking.

---

## X-Content-Type-Options

```http
X-Content-Type-Options: nosniff
```

Impede interpretação incorreta de arquivos.

---

## Referrer-Policy

```http
Referrer-Policy: strict-origin-when-cross-origin
```

Controla informações enviadas no cabeçalho Referer.

---

## Permissions-Policy

Controla permissões de recursos do navegador.

Exemplos:

- Câmera
- Microfone
- Geolocalização

---

# HTTP/2 e HTTP/3

Versões modernas do protocolo HTTP que melhoram desempenho e segurança.

## HTTP/2

Recursos:

- Multiplexação
- Compressão de cabeçalhos
- Menor latência

---

## HTTP/3

Utiliza o protocolo QUIC sobre UDP.

Benefícios:

- Conexões mais rápidas
- Menor tempo de reconexão
- Melhor desempenho em redes móveis

---

# Boas Práticas de Cybersegurança

## Utilizar HTTPS em toda a aplicação

Evita transmissão de dados em texto puro.

---

## Manter Certificados Atualizados

Certificados expirados comprometem a confiança do serviço.

---

## Implementar HSTS

Reduz riscos de downgrade para HTTP.

---

## Utilizar Autenticação Forte

- MFA (Autenticação Multifator)
- Senhas robustas
- Gerenciadores de senhas

---

## Validar Entradas

Previne:

- SQL Injection
- XSS
- Command Injection
- Path Traversal

---

## Proteger Cookies

```http
Set-Cookie: sessionid=abc123;
Secure;
HttpOnly;
SameSite=Strict
```

### Atributos

| Atributo | Função |
|-----------|---------|
| Secure | Envia apenas via HTTPS |
| HttpOnly | Impede acesso via JavaScript |
| SameSite | Reduz ataques CSRF |

---

# Resumo

- HTTP é o protocolo de comunicação da Web.
- A comunicação ocorre por meio de requisições (Request) e respostas (Response).
- Os códigos HTTP indicam o resultado das operações.
- O HTTP transmite dados sem criptografia.
- O HTTPS utiliza TLS para proteger a comunicação.
- O TLS fornece confidencialidade, integridade e autenticação.
- Certificados digitais validam a identidade dos servidores.
- Cabeçalhos de segurança fortalecem aplicações web.
- HTTP/2 e HTTP/3 melhoram desempenho e eficiência.
- O uso correto do HTTPS é uma das práticas mais importantes da Cybersegurança moderna.

<br>

[![➡ Próxima Seção](https://img.shields.io/badge/-➡_Próxima_Seção-blue?style=for-the-badge&color=007BFF)](https://github.com/pet-ads/cybersecurity-lab/blob/main/Guia%20de%20Estudos/6%20-%20Infraestrutura/2%20-%20Vari%C3%A1veis%20de%20ambiente.md)

## LINKS EXTRAS

-[HTTP // Dicionário do Programador](https://youtu.be/hwttZtWkXTk?si=gsqzzBqxbVxmDYAG)

-[O que é HTTPS?](https://www.cloudflare.com/pt-br/learning/ssl/what-is-https/)

-[O que é o TLS (Transport Layer Security)?](https://www.cloudflare.com/pt-br/learning/ssl/transport-layer-security-tls/)

