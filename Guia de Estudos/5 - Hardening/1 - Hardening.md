# Hardening e Defesa em Profundidade

## Introdução

Após compreender as principais vulnerabilidades que afetam aplicações e infraestruturas digitais, como **SQL Injection**, **Cross-Site Scripting (XSS)**, **Cross-Site Request Forgery (CSRF)**, **Session Hijacking**, **Clickjacking** e outras ameaças modernas, torna-se fundamental entender como proteger sistemas contra esses ataques.

A segurança cibernética moderna não depende de uma única solução. Em vez disso, utiliza múltiplas camadas de proteção que trabalham em conjunto para prevenir, detectar e responder a incidentes de segurança. Essa estratégia é conhecida como **Defesa em Profundidade (Defense in Depth)**.

Nesse contexto, o **Hardening** desempenha um papel essencial, reduzindo a superfície de ataque e dificultando a exploração de vulnerabilidades por agentes maliciosos.

---

# O que é Hardening?

O **Hardening** (endurecimento) é o processo de fortalecimento de sistemas, aplicações, servidores, dispositivos e redes por meio da redução de vulnerabilidades, remoção de componentes desnecessários e aplicação de configurações seguras.

Seu principal objetivo é minimizar a **superfície de ataque**, reduzindo as oportunidades de exploração por invasores.

## Conceito Prático

Imagine um castelo medieval:

- Muros altos representam os **firewalls**;
- Portões reforçados representam a **autenticação**;
- Guardas representam o **monitoramento e auditoria**;
- Áreas restritas representam o **controle de acesso**;
- Torres de vigilância representam os sistemas de **detecção de intrusão (IDS)**.

Quanto mais protegidas forem essas camadas, mais difícil será comprometer o ambiente.

## Objetivos do Hardening

- Reduzir riscos de invasão;
- Minimizar vulnerabilidades;
- Limitar impactos de incidentes;
- Garantir a confidencialidade dos dados;
- Preservar a integridade das informações;
- Aumentar a disponibilidade dos serviços;
- Atender requisitos de conformidade e auditoria.

---

# Redução da Superfície de Ataque

A **superfície de ataque** representa todos os pontos que podem ser explorados por um invasor.

Quanto maior a quantidade de serviços, aplicações, APIs, usuários e portas expostas, maior será o risco de comprometimento.

## Boas Práticas

### Remoção de Serviços Desnecessários

Exemplos:

- Telnet;
- FTP sem criptografia;
- Servidores de teste;
- Serviços legados;
- Aplicações não utilizadas.

### Exclusão de Contas Inutilizadas

Contas abandonadas frequentemente possuem:

- Senhas fracas;
- Permissões excessivas;
- Ausência de monitoramento.

### Fechamento de Portas Não Utilizadas

Somente portas estritamente necessárias devem permanecer abertas.

| Serviço | Porta |
|----------|--------|
| HTTP | 80 |
| HTTPS | 443 |
| SSH | 22 |

Todas as demais devem ser avaliadas e bloqueadas quando possível.

### Remoção de Softwares Obsoletos

Softwares antigos frequentemente possuem vulnerabilidades conhecidas e exploráveis.

---

# Princípio do Menor Privilégio (PoLP)

O **Princípio do Menor Privilégio (Principle of Least Privilege - PoLP)** estabelece que usuários, processos e aplicações devem possuir apenas as permissões necessárias para executar suas funções.

## Exemplo

### ERRADO
Usuário comum com privilégios administrativos.

### CERTO
Usuário comum com acesso apenas aos recursos necessários para seu trabalho.

## Benefícios

- Redução do impacto de contas comprometidas;
- Menor risco de movimentação lateral;
- Diminuição do escalonamento de privilégios;
- Melhor rastreabilidade das ações.

---

# Controle de Acesso

O controle de acesso determina quem pode acessar quais recursos e sob quais condições.

## Autenticação

Responsável por verificar a identidade do usuário.

### Exemplos

- Senha;
- PIN;
- Biometria;
- Token;
- Certificado digital.

## Autorização

Define o que o usuário autenticado pode fazer.

| Perfil | Permissões |
|----------|-------------|
| Usuário | Leitura |
| Editor | Leitura e alteração |
| Administrador | Controle total |

## Modelos de Controle de Acesso

### RBAC (Role-Based Access Control)

Permissões são atribuídas com base em funções.

Exemplo:

- Analista;
- Gerente;
- Administrador.

### ABAC (Attribute-Based Access Control)

Permissões são concedidas com base em atributos como:

- Cargo;
- Localização;
- Horário;
- Dispositivo utilizado.

---

# Autenticação Multifator (MFA)

A **Autenticação Multifator (Multi-Factor Authentication)** adiciona camadas extras de proteção.

## Fatores de Autenticação

### Algo que você sabe

- Senha;
- PIN.

### Algo que você possui

- Smartphone;
- Aplicativo autenticador;
- Token físico.

### Algo que você é

- Impressão digital;
- Reconhecimento facial;
- Reconhecimento de íris.

## Benefícios

Mesmo que uma senha seja comprometida, o invasor ainda precisará do segundo fator de autenticação.

---

# Cabeçalhos HTTP de Segurança

Os **Security Headers** instruem os navegadores a aplicar políticas de segurança automaticamente.

## Content Security Policy (CSP)

Protege contra:

- XSS;
- Injeção de scripts;
- Conteúdo malicioso.

### Exemplo

```http
Content-Security-Policy:
default-src 'self';
script-src 'self';
```

### Benefícios

- Bloqueia scripts não autorizados;
- Restringe fontes de conteúdo;
- Reduz impactos de vulnerabilidades XSS.

---

## HTTP Strict Transport Security (HSTS)

Força o uso exclusivo de HTTPS.

### Exemplo

```http
Strict-Transport-Security:
max-age=31536000;
includeSubDomains
```

### Benefícios

- Impede downgrade para HTTP;
- Mitiga ataques MITM;
- Protege sessões autenticadas.

---

## X-Frame-Options

Protege contra Clickjacking.

### Exemplo

```http
X-Frame-Options: DENY
```

### Benefício

Impede que a página seja carregada dentro de iframes maliciosos.

---

## X-Content-Type-Options

### Exemplo

```http
X-Content-Type-Options: nosniff
```

Impede que navegadores interpretem arquivos de maneira incorreta.

---

## Referrer-Policy

### Exemplo

```http
Referrer-Policy: strict-origin-when-cross-origin
```

Controla quais informações de navegação serão compartilhadas com outros sites.

---

# Proteção Contra CSRF

O **Cross-Site Request Forgery (CSRF)** explora a confiança que um sistema possui em um usuário autenticado.

## CSRF Tokens

Principal mecanismo de defesa.

```html
<input type="hidden"
       name="csrf_token"
       value="TOKEN_ALEATORIO">
```

O servidor valida o token antes de processar a requisição.

## Cookies SameSite

```http
Set-Cookie:
sessionid=abc123;
SameSite=Strict;
Secure;
HttpOnly
```

### Modos

| Modo | Proteção |
|--------|-----------|
| Strict | Máxima |
| Lax | Intermediária |
| None | Sem proteção CSRF |

## Validação de Origin e Referer

O servidor verifica os cabeçalhos:

- Origin;
- Referer.

Caso a origem não seja confiável:

Requisição rejeitada.

---

# Proteção de Sessões

A segurança das sessões é essencial para evitar **Session Hijacking**.

## Cookies Seguros

```http
Set-Cookie:
Secure;
HttpOnly;
SameSite=Strict
```

## Expiração de Sessão

Sessões não devem permanecer ativas indefinidamente.

## Rotação de Sessão

Gerar um novo identificador após:

- Login;
- Alteração de senha;
- Mudança de privilégios.

---

# Criptografia

A criptografia protege a confidencialidade dos dados.

## Dados em Trânsito

Utilizar:

- HTTPS;
- TLS 1.2 ou TLS 1.3.

Protege contra:

- Interceptação;
- Espionagem;
- Manipulação de tráfego.

## Dados em Repouso

Criptografar:

- Bancos de dados;
- Backups;
- Discos;
- Arquivos sensíveis.

### Exemplos

- AES-256;
- BitLocker;
- LUKS.

## Armazenamento Seguro de Senhas

Nunca armazenar senhas em texto puro.

Utilizar:

- Argon2;
- bcrypt;
- PBKDF2.

---

# Segmentação de Rede

A segmentação reduz a propagação de ataques.

## Exemplo

```text
Internet
    │
Firewall
    │
DMZ
    │
Servidor Web
    │
Banco de Dados
```

Mesmo que o servidor web seja comprometido, outras camadas continuam protegendo o banco de dados.

---

# Atualizações e Gerenciamento de Patches

Grande parte das invasões explora vulnerabilidades já conhecidas.

## Boas Práticas

- Atualizações automáticas;
- Inventário de ativos;
- Gestão de vulnerabilidades;
- Monitoramento de versões obsoletas;
- Testes de compatibilidade antes da implantação.

---

# Logs, Auditoria e Monitoramento

A segurança não termina após a implementação das proteções.

É necessário monitorar continuamente o ambiente.

## Registrar

- Logins;
- Alterações de privilégios;
- Falhas de autenticação;
- Ações administrativas;
- Eventos críticos.

## Ferramentas Comuns

- SIEM;
- IDS;
- IPS;
- EDR;
- XDR;
- SOAR.

---

# Zero Trust

O modelo **Zero Trust** segue o princípio:

> "Nunca confie, sempre verifique."

Todo acesso deve ser validado continuamente, independentemente da origem.

## Princípios

- Verificação contínua;
- MFA obrigatório;
- Menor privilégio;
- Monitoramento constante;
- Microsegmentação.

---

# Defesa em Profundidade

A **Defesa em Profundidade** utiliza múltiplas camadas de proteção para reduzir riscos.

## Exemplo

```text
Firewall
    ↓
IDS/IPS
    ↓
WAF
    ↓
MFA
    ↓
Controle de Acesso
    ↓
CSP
    ↓
CSRF Token
    ↓
Criptografia
    ↓
Logs e Monitoramento
```

Se uma camada falhar, as demais continuam protegendo o ambiente.

---

# Resumo Geral

O Hardening é um processo contínuo que busca reduzir riscos e fortalecer sistemas contra ameaças cibernéticas.

## Principais Medidas

### Redução da superfície de ataque

### Princípio do menor privilégio

### Controle de acesso e MFA

### Cabeçalhos HTTP de segurança

### Proteção contra CSRF

### Segurança de sessões

### Criptografia de dados

### Segmentação de rede

### Atualizações e gerenciamento de patches

### Logs, auditoria e monitoramento

### Modelo Zero Trust

### Defesa em Profundidade

---

# Conclusão

O Hardening constitui uma das práticas mais importantes da Cybersegurança moderna. Quando combinado com monitoramento contínuo, criptografia, autenticação forte, segmentação de rede e Defesa em Profundidade, cria um ambiente significativamente mais resiliente contra ataques cibernéticos.

A segurança não deve ser vista como um produto ou uma configuração única, mas como um processo contínuo de melhoria, avaliação de riscos e adaptação às novas ameaças.

<br>

[![➡ Próxima Seção](https://img.shields.io/badge/-➡_Próxima_Seção-blue?style=for-the-badge&color=007BFF)](https://github.com/pet-ads/cybersecurity-lab/blob/main/Guia%20de%20Estudos/4%20-%20Vulnerabilidade%20Cr%C3%ADticas/3%20-%20CSRF.md)


## LINKS EXTRAS

-[Utilizando Políticas de Segurança de Conteúdo)](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Guides/CSP)

-[#81 - Hardening Aula 1 - O que é Hardening?](https://youtu.be/93sW8GmW8ug?si=7_kvm8owsUm53OSz)

-[Hardening: o que é, pilares, vantagens e como aplicar](https://www.totvs.com/blog/negocios/hardening/)

