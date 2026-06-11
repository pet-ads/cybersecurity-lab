# Oque é SQL Injection

**SQL Injection (SQLi)** é uma das vulnerabilidades mais críticas em aplicações web.

Ela ocorre quando uma aplicação:
> insere dados fornecidos pelo usuário diretamente em comandos SQL sem validação ou separação adequada.

Isso permite que o atacante:
- altere consultas
- acesse dados indevidos
- execute comandos no banco
- comprometa o sistema inteiro

---

## Problema central

o problema surge quando o sistema não consegue diferenciar corretamente o que é dado e o que é comando. Assim, uma entrada maliciosa pode ser interpretada como parte da instrução SQL e executada diretamente no banco de dados.


---

# Como SQL Injection acontece (raiz do problema)

## Concatenação insegura

Exemplo clássico:

```python
query = "SELECT * FROM users WHERE email = '" + email + "'"
```

Se o usuário envia:

```
' OR '1'='1
```

A query vira:

```sql
SELECT * FROM users WHERE email = '' OR '1'='1'
```

Resultado: retorna todos os usuários

---

## Falhas comuns que causam SQLi

- Falta de validação de entrada  
- Uso de concatenação de strings  
- Queries dinâmicas sem proteção  
- Uso de usuário admin no banco  
- Exposição de erros SQL  

---

# Tipos de SQL Injection

Os ataques de SQLi podem ocorrer de várias formas, dependendo de como a aplicação se comporta.

Uma das formas mais comuns é o bypass de autenticação, onde o atacante manipula um campo de login para fazer a consulta sempre retornar verdadeira, permitindo acesso sem credenciais válidas. Isso acontece porque a entrada fornecida é incorporada diretamente na query. Outra técnica bastante comum é o uso do operador UNION, que permite ao atacante combinar resultados da consulta original com dados de outras tabelas, podendo expor informações sensíveis como usuários e senhas. Também existem os ataques conhecidos como stacked queries, onde o invasor consegue encerrar uma instrução SQL e iniciar outra, podendo executar comandos destrutivos como exclusão de tabelas. Além disso, há os ataques baseados em erros do banco de dados, onde mensagens de erro são exploradas para revelar informações internas, como estrutura de tabelas ou versão do banco. Em cenários mais avançados, existe ainda o Blind SQL Injection, onde o atacante não vê os dados diretamente, mas infere informações através do comportamento da aplicação.

---

## Authentication Bypass

Explora login:

```sql
' OR '1'='1' --
```

📌 Resultado:
- ignora senha
- autentica como primeiro usuário

---

## UNION-based SQLi

Permite juntar dados de outras tabelas:

```sql
UNION SELECT username, password FROM users
```

Impacto:
- vazamento de credenciais
- extração de dados sensíveis

---

## Stacked Queries

Permite múltiplas instruções:

```sql
'; DROP TABLE users; --
```

Impacto:
- destruição de dados
- execução de comandos adicionais

---

## Error-based SQLi

Explora mensagens de erro do banco:

- nomes de tabelas
- estrutura do banco
- colunas internas

---

## Blind SQL Injection

Sem retorno visível de dados.

O atacante infere informações por:

- tempo de resposta (time-based)
- respostas booleanas (true/false)

Exemplo conceitual:
- resposta rápida → condição verdadeira  
- resposta lenta → condição falsa  

---

# Impactos (visão real de cibersegurança)

SQL Injection é classificado como **CRÍTICO (OWASP Top 10)**.

---

## Consequências:

- Vazamento de dados pessoais (LGPD violada)
- Roubo de credenciais
- Alteração de dados bancários
- Exclusão de tabelas inteiras
- Escalação de privilégios
- Acesso administrativo ao sistema
- Execução de comandos no sistema operacional (casos avançados)

---

## Impacto real

Em sistemas reais, SQLi pode levar a:

> comprometimento total da aplicação + infraestrutura

---

# Defesa em profundidade (modelo moderno)

A prevenção contra SQL Injection depende principalmente de boas práticas de desenvolvimento seguro e uma arquitetura bem configurada.

**Segurança NÃO é uma única camada.**

---

# Camada de Aplicação (DEV SECURE)

---

## Prepared Statements (ESSENCIAL)

Inseguro:

```python
query = "SELECT * FROM users WHERE email = '" + email + "'"
```

---

Seguro:

```python
cursor.execute(
    "SELECT * FROM users WHERE email = %s",
    (email,)
)
```

---

Por que funciona?

- separa código de dados
- impede interpretação de input como SQL

---

## ORM (boa prática moderna)

Evita SQL manual:

- SQLAlchemy (Python)
- Hibernate (Java)
- Sequelize (Node.js)

Benefício:
- reduz risco humano
- abstrai queries inseguras

---

## Validação de entrada (Allow-list)

Aceitar apenas formatos esperados:

| Campo | Regra |
|------|------|
| email | regex email |
| id | apenas números |
| nome | letras + espaço |

---

# Camada de Banco de Dados

---

## Princípio do menor privilégio

A aplicação NÃO deve usar admin.

Separar permissões:

- SELECT apenas
- INSERT apenas
- UPDATE controlado
- DELETE restrito

---

## Remover funções perigosas

- execução de shell
- procedures administrativas desnecessárias
- comandos internos expostos

---

# Camada de infraestrutura

---

## WAF (Web Application Firewall)

Detecta padrões de ataque:

- SQL keywords suspeitas
- payloads maliciosos
- comportamento anormal

Exemplos:
- Cloudflare
- AWS WAF

---

## Ocultação de erros

Errado:

```
SQL syntax error near DROP
```

Correto:

```
Erro interno no servidor
```

Motivo:
Evita vazamento de estrutura do banco

---

## Logs e monitoramento

Detectar:

- tentativas repetidas de SQLi
- padrões anormais de query
- picos de requisição
- comportamento automatizado (bot attack)

---

# DevSecOps (segurança contínua)

---

## Pipeline seguro:

- Code review obrigatório
- SAST (Static Analysis)
- DAST (Dynamic Testing)
- Pentest periódico
- CI/CD com segurança integrada

---

## Ferramentas:

- OWASP ZAP
- Burp Suite
- SonarQube
- Nikto

---

# Como identificar SQL Injection

---

## sinais típicos:

- `' OR 1=1`
- `--` ou `#`
- múltiplos erros SQL
- resposta lenta (blind SQLi)
- tráfego anormal em endpoints

---

# Mitigação (Checklist profissional)

✔ Prepared Statements sempre  
✔ ORM corretamente configurado  
✔ Validação de entrada (allow-list)  
✔ Usuário do banco limitado  
✔ Logs e auditoria ativos  
✔ Erros ocultos ao usuário  
✔ WAF configurado  
✔ Revisão de código contínua  
✔ Testes de segurança automatizados  

---

# Resumo

| Item | Descrição |
|------|----------|
| SQLi | injeção de comandos SQL via input |
| Causa | concatenação insegura |
| Exploração | manipulação de queries |
| Impacto | crítico (OWASP Top 10) |
| Defesa principal | prepared statements |
| Defesa moderna | DevSecOps + WAF + least privilege |

---

# Arquitetura segura (visão profissional)

Uma aplicação segura deve seguir:

- 🔹 Input sanitization (camada de entrada)
- 🔹 Query parameterization (camada de aplicação)
- 🔹 Least privilege (camada de banco)
- 🔹 WAF (camada de rede)
- 🔹 Monitoring (camada de observabilidade)

---

# Conclusão

SQL Injection não é apenas uma falha de código.

É uma falha de arquitetura de segurança.

Sistemas modernos precisam de:

- defesa em profundidade
- validação em múltiplas camadas
- monitoramento contínuo
- cultura de DevSecOps

---

>  Um sistema seguro não depende de uma única proteção — ele depende de camadas trabalhando juntas.

## LINK EXTRAS

-[SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)

-[Injeção SQL para iniciantes: exemplos e prevenção](https://hackerdna.com/pt-br/blog/tutorial-injecao-sql)

-[SQL Injection (Do Ataque a Prevenção)](https://www.devmedia.com.br/sql-injection/6102)

-[SQL Injection (Do Ataque a Prevenção) // Dicionário do Programador](https://www.youtube.com/watch?si=7H8xm7QbLOSAEJHf&v=jN8QGOxdhvM&feature=youtu.be)