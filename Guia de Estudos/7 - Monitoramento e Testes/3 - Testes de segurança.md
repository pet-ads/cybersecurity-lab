# OWASP ZAP (Zed Attack Proxy)

## Introdução

O **OWASP ZAP (Zed Attack Proxy)** é uma das ferramentas de **teste de segurança para aplicações web** mais utilizadas por profissionais de cibersegurança, desenvolvedores e equipes de DevSecOps. Desenvolvido pela **OWASP (Open Worldwide Application Security Project)**, o ZAP é gratuito, de código aberto e projetado para identificar vulnerabilidades em aplicações antes que elas possam ser exploradas por invasores.

A ferramenta pode ser utilizada tanto por iniciantes quanto por especialistas em testes de penetração (*penetration testing*), oferecendo desde uma interface gráfica intuitiva até recursos avançados de automação via API. Seu principal objetivo é auxiliar na identificação de falhas de segurança durante o desenvolvimento e manutenção de aplicações web, permitindo que essas vulnerabilidades sejam corrigidas antes da implantação em produção.

---

# Como o OWASP ZAP funciona

O ZAP atua como um **proxy interceptador (Intercepting Proxy)** entre o navegador do usuário e a aplicação web.

Em vez de o navegador enviar as requisições diretamente ao servidor, todas as comunicações passam pelo ZAP. Isso permite que a ferramenta capture, visualize, modifique e reenviе requisições HTTP e HTTPS, oferecendo uma visão completa da comunicação entre cliente e servidor.

O fluxo de comunicação ocorre da seguinte forma:

```
Navegador
     │
     ▼
 OWASP ZAP
     │
     ▼
Servidor Web
```

Durante esse processo, o ZAP registra:

* Requisições HTTP e HTTPS;
* Cabeçalhos (Headers);
* Cookies;
* Tokens de autenticação;
* Parâmetros enviados pelo usuário;
* Respostas do servidor.

Essas informações permitem identificar vulnerabilidades como:

* SQL Injection (SQLi);
* Cross-Site Scripting (XSS);
* Exposição de informações sensíveis;
* Configurações inseguras;
* Cabeçalhos de segurança ausentes;
* Falhas de autenticação e gerenciamento de sessões.

Além disso, o usuário pode modificar manualmente qualquer requisição antes que ela seja enviada ao servidor, simulando ataques reais para verificar como a aplicação reage.

---

# Principais recursos do OWASP ZAP

Entre os recursos mais importantes da ferramenta estão:

* Proxy interceptador para captura de tráfego.
* Scanner Passivo.
* Scanner Ativo.
* Spider Tradicional.
* AJAX Spider.
* Fuzzer.
* Gerenciamento de Sessões.
* Testes autenticados.
* Monitoramento de WebSockets.
* Geração automática de relatórios.
* API para automação.
* Integração com pipelines de CI/CD.

Esses recursos tornam o ZAP uma plataforma completa para avaliações de segurança em aplicações web.

---

# Varredura Passiva (Passive Scan)

A **Varredura Passiva** analisa todas as requisições e respostas capturadas **sem modificar qualquer informação enviada à aplicação**.

Por não enviar ataques ou alterar dados, esse método é considerado seguro para praticamente qualquer ambiente, inclusive produção (desde que a política da organização permita).

Durante essa análise, o ZAP procura por problemas como:

* Cabeçalhos HTTP inseguros;
* Cookies sem atributos de segurança (*Secure* e *HttpOnly*);
* Informações sensíveis expostas;
* Versões de servidores divulgadas;
* Configurações inseguras.

### Vantagens

* Não altera a aplicação.
* Não gera tráfego malicioso.
* Baixo risco.
* Pode ser executada continuamente.

### Limitações

Como nenhuma tentativa de exploração é realizada, algumas vulnerabilidades não podem ser detectadas, como:

* SQL Injection;
* Command Injection;
* Path Traversal;
* Diversas falhas de lógica da aplicação.

---

# Varredura Ativa (Active Scan)

A **Varredura Ativa** realiza testes ofensivos contra a aplicação.

Nesse modo, o ZAP envia diversas requisições modificadas utilizando técnicas conhecidas de exploração para verificar se a aplicação apresenta vulnerabilidades.

Entre os testes executados estão:

* SQL Injection;
* Cross-Site Scripting (XSS);
* Command Injection;
* LDAP Injection;
* XML Injection;
* Directory Traversal;
* CRLF Injection;
* Diversas falhas listadas no OWASP Top 10.

Ao contrário do scanner passivo, o scanner ativo modifica parâmetros e insere cargas maliciosas (*payloads*) para observar como o servidor responde.

### Vantagens

* Detecta vulnerabilidades reais.
* Alta cobertura de testes.
* Simula ataques utilizados por invasores.

### Desvantagens

* Pode gerar grande quantidade de tráfego.
* Pode alterar ou excluir dados.
* Pode causar indisponibilidade em aplicações frágeis.
* Nunca deve ser executado sem autorização.

> **Importante:** Sempre obtenha autorização formal antes de executar uma varredura ativa. Em ambientes de produção, o uso inadequado pode causar interrupções de serviço, perda de dados e impactos legais.

---

# Descoberta da aplicação (Spider)

Antes de testar uma aplicação, o ZAP precisa descobrir sua estrutura.

Para isso, utiliza rastreadores chamados **Spiders**, que percorrem automaticamente as páginas e identificam:

* URLs;
* Formulários;
* Links;
* Arquivos;
* APIs;
* Parâmetros.

Quanto mais páginas forem encontradas, maior será a cobertura do scanner.

## Spider Tradicional

O Spider Tradicional percorre o código HTML da aplicação em busca de links.

É extremamente rápido e eficiente para aplicações tradicionais.

### Vantagens

* Muito rápido.
* Baixo consumo de recursos.
* Excelente para sites estáticos.

### Limitações

Não consegue navegar corretamente em aplicações modernas construídas com JavaScript.

---

## AJAX Spider

Aplicações desenvolvidas com React, Angular, Vue.js e outros frameworks carregam conteúdo dinamamente usando JavaScript.

O **AJAX Spider** executa um navegador real (headless), renderiza a página e simula a interação de um usuário.

Isso permite descobrir:

* Botões;
* Menus;
* Links dinâmicos;
* Conteúdo carregado por JavaScript;
* Rotas SPA (*Single Page Applications*).

Embora seja mais lento que o Spider Tradicional, oferece uma cobertura muito maior para aplicações modernas.

---

# Fuzzing

O **Fuzzing** é uma técnica de teste baseada no envio de grandes quantidades de entradas inesperadas para verificar como a aplicação responde.

O objetivo é encontrar comportamentos anormais, como:

* Erros internos;
* Travamentos;
* Vazamento de informações;
* Falhas de validação;
* Vulnerabilidades exploráveis.

Exemplos de entradas utilizadas:

* Strings extremamente longas;
* Caracteres especiais;
* Scripts JavaScript;
* Comandos SQL;
* Caracteres Unicode;
* Sequências aleatórias.

O OWASP ZAP possui diversas listas de **payloads** prontas e também permite importar listas personalizadas criadas pela comunidade ou pela própria equipe de segurança.

---

# Testes Autenticados

Grande parte das vulnerabilidades encontra-se em áreas protegidas por login.

O ZAP permite realizar testes autenticados, simulando usuários reais para avaliar funcionalidades internas da aplicação.

Entre os métodos suportados estão:

* Login por formulário HTML;
* Autenticação HTTP Basic;
* HTTP Digest;
* NTLM;
* JSON;
* OAuth;
* Scripts personalizados;
* Tokens JWT.

Após autenticar-se, o scanner consegue acessar páginas que normalmente estariam protegidas, aumentando significativamente a cobertura dos testes.

---

# Testando WebSockets

Muitas aplicações modernas utilizam **WebSockets** para comunicação em tempo real.

Exemplos:

* Chats;
* Jogos online;
* Sistemas financeiros;
* Painéis administrativos;
* Notificações em tempo real.

O OWASP ZAP consegue interceptar essas conexões, permitindo analisar:

* Mensagens enviadas;
* Mensagens recebidas;
* Autenticação;
* Tokens;
* Possíveis falhas de autorização;
* Exposição de informações.

Esse recurso é importante para identificar problemas que não aparecem em comunicações HTTP tradicionais.

---

# Automação com API

Além da interface gráfica, o ZAP disponibiliza uma API que permite automatizar completamente os testes de segurança.

Essa funcionalidade é amplamente utilizada em pipelines de **DevSecOps**, possibilitando que verificações de segurança sejam executadas automaticamente sempre que houver alterações no código.

Entre as vantagens da automação estão:

* Execução automática de testes;
* Integração com CI/CD;
* Geração automática de relatórios;
* Padronização dos testes;
* Identificação precoce de vulnerabilidades.

Dessa forma, a segurança passa a fazer parte do ciclo contínuo de desenvolvimento, reduzindo custos e acelerando a correção de falhas.

---

# Instalação do OWASP ZAP

O OWASP ZAP pode ser executado em diferentes sistemas operacionais.

## Pré-requisitos

Para a versão Desktop, é necessário possuir:

* Java 8 ou superior.

Na versão Docker, o Java já está incluído na imagem, dispensando instalação adicional.

## Plataformas suportadas

* Windows
* Linux
* macOS
* Docker

---

# Primeiro teste utilizando o Auto Scan

O modo **Auto Scan** é a forma mais simples de iniciar uma análise de segurança.

## Passo 1

Abra o OWASP ZAP.

---

## Passo 2

Na tela inicial, selecione a aba **Quick Start** ou **Quick Launch**.

---

## Passo 3

Escolha a opção **Automated Scan**.

---

## Passo 4

Digite a URL da aplicação que será analisada.

Exemplo:

```
http://localhost:8080
```

ou

```
https://meusite.com
```

---

## Passo 5

Escolha o tipo de Spider:

* Spider Tradicional;
* AJAX Spider.

---

## Passo 6

Clique em **Attack**.

O ZAP executará automaticamente:

1. Descoberta da aplicação.
2. Rastreamento de páginas.
3. Scanner Passivo.
4. Scanner Ativo (quando habilitado).
5. Geração dos alertas encontrados.

---

# Interpretando os resultados

Ao final da análise, o ZAP organiza as vulnerabilidades encontradas por níveis de severidade:

| Severidade     | Significado                                                               |
| -------------- | ------------------------------------------------------------------------- |
| 🔴 Alta        | Vulnerabilidades críticas que devem ser corrigidas imediatamente.         |
| 🟠 Média       | Falhas relevantes que representam riscos significativos.                  |
| 🟡 Baixa       | Problemas com menor impacto, mas que merecem correção.                    |
| 🔵 Informativa | Boas práticas, informações de configuração ou recomendações de segurança. |

Cada alerta apresenta informações detalhadas, como:

* Descrição da vulnerabilidade;
* Evidências encontradas;
* Local onde ocorreu;
* Impacto potencial;
* Forma de exploração;
* Recomendações de mitigação;
* Referências para estudo.

Essa classificação ajuda a equipe a priorizar as correções com base no risco.

---

# Boas práticas no uso do OWASP ZAP

Para obter resultados confiáveis e evitar impactos negativos, siga algumas recomendações:

* Nunca realize testes sem autorização do proprietário da aplicação.
* Prefira utilizar ambientes de desenvolvimento, homologação ou laboratório.
* Execute primeiro uma varredura passiva e, somente depois, a varredura ativa.
* Atualize frequentemente o ZAP e seus complementos (*add-ons*).
* Revise manualmente os alertas encontrados para reduzir falsos positivos.
* Automatize testes recorrentes em pipelines de CI/CD.
* Documente e acompanhe as vulnerabilidades identificadas até sua correção.

---

# Resumo

O **OWASP ZAP** é uma ferramenta essencial para testes de segurança em aplicações web. Atuando como um proxy interceptador, ele permite analisar toda a comunicação entre cliente e servidor, identificar vulnerabilidades e avaliar a robustez da aplicação. Seus recursos de varredura passiva e ativa, rastreamento com *Spiders*, *Fuzzing*, testes autenticados, análise de WebSockets e automação por API fazem dele uma solução completa para profissionais de segurança, desenvolvedores e equipes de DevSecOps.

Quando utilizado de forma ética e autorizada, o ZAP contribui significativamente para a identificação precoce de falhas, fortalecendo a segurança das aplicações e reduzindo riscos de exploração por atacantes.

<br>

[![➡ Próxima Seção](https://img.shields.io/badge/-➡_Próxima_Seção-blue?style=for-the-badge&color=007BFF)](https://github.com/pet-ads/cybersecurity-lab/tree/main/Guia%20de%20Estudos/1%20-%20Introdu%C3%A7%C3%A3o)

## LINKS EXTRAS

-[Zed Attack Proxy (ZAP)](https://www.zaproxy.org/)

-[OWASP ZAP: 6 Key Capabilities and a Quick Tutorial](https://www.hackerone.com/knowledge-center/owasp-zap-6-key-capabilities-and-quick-tutorial)



