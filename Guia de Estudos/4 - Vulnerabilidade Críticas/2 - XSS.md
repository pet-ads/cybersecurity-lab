# O que é XSS?

O **Cross-Site Scripting (XSS)** é uma vulnerabilidade de segurança em aplicações web que permite a execução de scripts maliciosos dentro do navegador de usuários que acessam uma página confiável.

Na prática, isso acontece quando uma aplicação recebe dados do usuário e os exibe na interface sem aplicar validação, sanitização ou escape adequado. O problema central é que o navegador não consegue diferenciar o que é conteúdo legítimo do site e o que foi injetado por um atacante.

## Problema central

O navegador interpreta o código injetado como legítimo, pois ele vem de um site confiável.

Resultado: execução de código malicioso no navegador da vítima.

---

# Como um ataque XSS acontece

Um ataque XSS geralmente segue um fluxo bem definido.

Primeiro, o atacante insere um código malicioso em algum ponto da aplicação, como formulários, URLs, comentários ou até cabeçalhos HTTP. Em seguida, a aplicação processa esse conteúdo de forma insegura, sem aplicar filtros ou escape adequado, e o armazena ou reflete diretamente na página.

Quando outro usuário acessa esse conteúdo, o navegador interpreta automaticamente o script como parte legítima do site e o executa.

Isso permite que o atacante execute ações dentro do navegador da vítima sem o consentimento dela.

---

# Tipos de XSS

Existem diferentes formas de XSS, que variam principalmente na forma como o código malicioso é executado.

## XSS refletido
Aqui o payload não é armazenado no servidor. Ele é enviado na requisição e imediatamente refletido na resposta da aplicação. Esse tipo de ataque costuma ser explorado via links maliciosos, geralmente em ataques de phishing.

## XSS armazenado 
Esse é mais perigoso, pois o código malicioso é salvo no servidor, normalmente em banco de dados. Isso faz com que qualquer usuário que acesse o conteúdo infectado acabe executando o script automaticamente, tornando o ataque persistente e escalável.

## XSS baseado em DOM
Aqui que ocorre inteiramente no lado do cliente. Nesse caso, a vulnerabilidade está no JavaScript da própria aplicação, que manipula o DOM de forma insegura, inserindo dados sem validação em funções como `innerHTML`.

## Blind XSS 
Já aqui acontece quando o payload é armazenado e executado em um ambiente diferente daquele em que foi injetado, como painéis administrativos. Esse tipo é muito utilizado em testes de segurança.

---

# Consequências de um ataque XSS

Os impactos de um XSS podem ser graves, principalmente porque o ataque ocorre diretamente no navegador da vítima.

Um dos riscos mais críticos é o roubo de sessão, onde o atacante pode capturar cookies e sequestrar a conta do usuário. Além disso, o script malicioso pode realizar ações em nome da vítima, como alterar senhas, realizar compras ou enviar mensagens.

Outro impacto comum é o redirecionamento para páginas falsas, usadas em ataques de phishing para roubar credenciais. Também é possível modificar o conteúdo da página exibida ao usuário, o que pode gerar fraudes ou manipulação de informações.

Em cenários mais avançados, o XSS pode até ser usado para distribuir malware, forçando downloads ou executando scripts maliciosos automaticamente.

---

# Exemplos de payloads

Embora muitas pessoas associem XSS apenas à tag `<script>`, na prática existem várias formas de exploração.

O ataque pode ocorrer através de eventos HTML, como `onload`, `onerror` ou `onmouseover`, que executam JavaScript diretamente dentro de elementos HTML.

```html
<body onload="alert('XSS')">
```

```html
<img src="x" onerror="alert(document.cookie)">
```

```html
<a href="#" onmouseover="alert('XSS')">Passe o mouse</a>
```

Isso mostra que o XSS não depende apenas de blocos de script tradicionais, mas de qualquer ponto onde o navegador interprete entrada do usuário como código executável.

---

# Como prevenir XSS

A prevenção de XSS não depende de uma única solução, mas de várias camadas de proteção aplicadas corretamente.

O primeiro passo é validar todas as entradas recebidas pela aplicação, garantindo que apenas dados esperados sejam aceitos. No entanto, apenas validar não é suficiente.

Também é essencial sanitizar os dados, removendo ou neutralizando qualquer conteúdo potencialmente malicioso antes de armazená-lo ou exibi-lo.

Um dos pontos mais importantes é o escape de saída, que garante que caracteres especiais como `<` e `>` sejam convertidos em entidades seguras, impedindo que o navegador interprete o conteúdo como código.

Outra medida importante é o uso de cookies com a flag `HttpOnly`, que impede o acesso via JavaScript, reduzindo o impacto de ataques que tentam roubar sessões.

Além disso, o uso de Content Security Policy (CSP) adiciona uma camada extra de proteção, controlando quais scripts podem ser executados na página e bloqueando fontes não autorizadas.

Também é recomendado evitar funções perigosas como `innerHTML`, `document.write` e `eval`, que frequentemente são exploradas em ataques XSS.

---

# Visão de segurança (OWASP)

XSS é um dos principais riscos do:

> OWASP Top 10 — vulnerabilidades críticas da web

---

Mesmo sendo uma vulnerabilidade conhecida há muitos anos, ela ainda é amplamente explorada devido a falhas básicas de desenvolvimento e falta de validação adequada.

## Impacto geral

- afeta frontend e backend  
- permite controle do navegador da vítima  
- pode levar a invasão total de contas  

---

# Conclusão

O XSS não é apenas um erro simples de programação, mas uma falha na forma como a aplicação trata dados externos.

Em sistemas modernos, a segurança contra XSS depende de uma combinação de boas práticas, incluindo validação, sanitização, escape de saída e políticas de segurança no navegador.

No fim, qualquer dado vindo do usuário deve ser tratado como não confiável até que seja explicitamente validado e seguro para uso.

## LINKS EXTRAS

-[XSS Attack (Como Funciona e Como Prevenir Ataques) // Dicionário do Programador](https://youtu.be/2LYPyUk-L0k?si=KLkZ8igS_g8SoOWz)

-[Cross Site Scripting (XSS)](https://owasp.org/www-community/attacks/xss/)