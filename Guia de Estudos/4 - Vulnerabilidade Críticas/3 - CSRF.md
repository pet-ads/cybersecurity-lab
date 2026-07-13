# O que é CSRF?

O **CSRF (Cross-Site Request Forgery)** é uma vulnerabilidade de segurança em aplicações web que permite que um atacante induza um usuário autenticado a executar ações indesejadas sem perceber.

Isso acontece porque o navegador automaticamente envia credenciais válidas, como cookies de sessão, em requisições feitas para um site confiável.

**Em outras palavras, o CSRF não explora a senha do usuário, mas sim a confiança que o servidor deposita no navegador autenticado.**

---

# Como o ataque funciona

O CSRF se torna possível devido a três características comuns em aplicações web:

- o usuário já está autenticado em um site legítimo  
- o navegador envia cookies automaticamente em requisições  
- o servidor não valida corretamente a origem da requisição  

A partir disso, o ataque acontece de forma simples. O usuário realiza login em um site confiável, como um banco, e mantém sua sessão ativa. Em seguida, ele acessa um site malicioso sem perceber.

Esse site malicioso dispara requisições escondidas para o sistema legítimo, e como o navegador envia automaticamente os cookies de sessão, o servidor interpreta a requisição como legítima e executa a ação.

---

# Exemplos de ataque CSRF

O CSRF pode ser explorado de diferentes formas, dependendo do tipo de requisição.

---

## CSRF via GET

Um exemplo clássico é o uso de uma imagem maliciosa:

```html
<img src="https://bank.com/transfer?to=attacker&amount=1000" />
```

Se o usuário estiver autenticado, essa requisição pode ser executada automaticamente sem interação.

---

## CSRF via POST oculto

Também é possível simular formulários invisíveis:

```html
<form action="https://bank.com/transfer" method="POST">
  <input type="hidden" name="to" value="attacker">
  <input type="hidden" name="amount" value="1000">
</form>

<script>
  document.forms[0].submit();
</script>
```

---

## CSRF de login

Outro tipo comum força o usuário a ser autenticado em uma conta controlada pelo atacante, permitindo manipulações futuras da sessão.

---

# O que NÃO protege contra CSRF (mitos comuns)

Existem muitas ideias incorretas sobre proteção contra CSRF.

Algumas medidas isoladas não são suficientes, como:

- usar apenas requisições POST  
- confiar apenas em cookies de sessão  
- usar HTTPS (que protege dados, não origem)  
- validar apenas Referer ou Origin sem estratégia adicional  

📌 Nenhuma dessas medidas, isoladamente, impede CSRF de forma eficaz.

---

# Proteções eficazes (boas práticas modernas)

A segurança contra CSRF depende de múltiplas camadas combinadas.

---

## CSRF Token (padrão ouro)

O servidor gera um token único e imprevisível associado à sessão ou requisição.

Esse token é enviado junto com as requisições e validado pelo servidor.

```html
<input type="hidden" name="csrf_token" value="RANDOM123ABC">
```

Se o token não for válido, a requisição é rejeitada.

---

## Cookies com SameSite

Uma das proteções mais importantes atualmente é o atributo `SameSite`.

- `SameSite=Strict` → bloqueia quase todas requisições cross-site  
- `SameSite=Lax` → permite alguns casos controlados  
- `SameSite=None; Secure` → permite uso cross-site com HTTPS  

📌 Essa proteção reduz significativamente ataques CSRF modernos.

---

## Validação de Origin e Referer

O servidor pode verificar a origem da requisição usando headers como:

- `Origin` (mais confiável)  
- `Referer` (menos confiável)  

Se a origem não for confiável, a requisição deve ser rejeitada.

---

## Double Submit Cookie

Nesse modelo, o token CSRF é enviado em dois lugares:

- em um cookie  
- em um campo da requisição  

O servidor compara ambos antes de aceitar a requisição.

---

## Frameworks seguros

Muitos frameworks já implementam proteção automática contra CSRF, como:

- Spring Security (Java)  
- Django (Python)  
- Laravel (PHP)  
- ASP.NET Core  
- Ruby on Rails  

---

# Boas práticas de segurança (visão geral)

A proteção contra CSRF deve ser aplicada junto de outras práticas de segurança.

---

## Segurança de sessões

- expiração curta de sessão  
- regeneração de sessão após login  
- cookies seguros (`HttpOnly`, `Secure`, `SameSite`)  

---

## Validação de entrada

- sanitização de dados  
- proteção contra XSS (que pode amplificar CSRF)  
- escape de conteúdo dinâmico  

---

## Controle de acesso

- validação no backend (não no frontend)  
- princípio do menor privilégio  

---

## Monitoramento

- logs de ações sensíveis  
- detecção de padrões anormais  
- alertas para operações críticas (transferências, senhas)  

---

# Impacto do CSRF

Os impactos variam de acordo com o sistema comprometido.

---

## Usuários comuns

- transferências bancárias não autorizadas  
- alteração de senha ou e-mail  
- perda de controle da conta  

---

## Sistemas administrativos

- criação de usuários admin  
- manipulação de dados críticos  
- comprometimento total da aplicação  

---

# Relação com outras vulnerabilidades

O CSRF frequentemente aparece combinado com outras falhas:

- **XSS** → pode roubar tokens CSRF  
- **Session Hijacking** → compromete sessões ativas  
- **Clickjacking** → induz ações invisíveis  

---

# Conclusão

O CSRF não explora uma falha direta no usuário, mas sim na forma como o navegador e o servidor confiam automaticamente nas requisições autenticadas.

A proteção moderna exige defesa em camadas, combinando:

- tokens CSRF  
- cookies com SameSite  
- validação de origem  
- frameworks seguros  
- boas práticas de sessão e autenticação  

---

> Em segurança web, confiança nunca deve ser implícita — sempre deve ser validada.

<br>

[![➡ Próxima Seção](https://img.shields.io/badge/-➡_Próxima_Seção-blue?style=for-the-badge&color=007BFF)](https://github.com/pet-ads/cybersecurity-lab/blob/main/Guia%20de%20Estudos/4%20-%20Vulnerabilidade%20Cr%C3%ADticas/3%20-%20CSRF.md)

## LINKS EXTRAS

-[Cross Site Request Forgery (CSRF)](https://owasp.org/www-community/attacks/csrf)