# Sessões na Web

## O problema do HTTP

Na web, tudo começa com um problema simples: o protocolo HTTP é **stateless**, ou seja, não “lembra” de nada. Cada requisição feita por um navegador para um servidor é independente da anterior, como se fosse sempre o primeiro contato. Isso significa que, sem algum mecanismo adicional, um site não conseguiria saber se você está logado, o que colocou no carrinho ou até mesmo suas preferências.

**Problema**: como manter um usuário autenticado durante a navegação?

Para resolver isso, entram dois conceitos fundamentais: cookies e sessões.


---

##  O que são Sessões?

Quando você acessa um site, o servidor precisa encontrar uma forma de te identificar nas próximas interações. Ele faz isso criando uma **sessão**, que é como um “**registro temporário**” do seu acesso. Essa sessão fica armazenada no servidor, e o usuário não acessa diretamente esses dados, assim, **mantendo o estado de um usuário entre requisições HTTP**. O que vai para o navegador é apenas um identificador único, geralmente armazenado em um cookie.

## O que são Cookies?

Os **cookies**, por sua vez, são pequenos arquivos armazenados no navegador. Eles servem para **manter informações entre requisições**, permitindo que a experiência do usuário seja contínua. Existem dois tipos principais.

Os **cookies de sessão** são temporários. Eles existem apenas enquanto o navegador está aberto e são apagados automaticamente quando ele é fechado.

Os **cookies persistentes** permanecem no dispositivo por um tempo definido, podendo durar dias, meses ou até anos, dependendo da configuração do desenvolvedor.

É graças a esse mecanismo que conseguimos ficar logados em sites, continuar com itens no carrinho de compras ou manter preferências como idioma e tema.

---

### Objetivos da sessão:
- Identificar um usuário único
- Manter autenticação ativa
- Armazenar dados temporários (ex: carrinho, preferências)
- Controlar permissões durante a navegação

---

## Como uma sessão funciona na prática

O funcionamento segue um modelo baseado em **identificador (Session ID)**:

### Fluxo simplificado:

1. Usuário faz login no sistema  
2. O servidor cria uma sessão única  
3. Um **Session ID** é gerado (aleatório e único)  
4. Esse ID é enviado ao navegador (geralmente via cookie)  
5. O navegador envia esse ID em toda requisição futura  
6. O servidor usa esse ID para recuperar os dados da sessão  

---

## O que o servidor armazena?

Ao contrário do que muitos pensam:

-O navegador NÃO guarda a sessão  
-Ele guarda apenas o **ID da sessão**

O servidor mantém algo como:

```
Session ID: abc123
{
  usuario: "ka_sil",
  autenticado: true,
  carrinho: ["mouse", "teclado"],
  role: "admin"
}
```

---

## Relação entre Sessões e Cookies

As sessões geralmente dependem de cookies.

O cookie guarda apenas:

```
sessionId=abc123
```

**Importante**:
- Cookie = identificador
- Sessão = dados no servidor

---

## Analogia simples

Imagine um cinema:

- Você faz check-in na entrada (login)
- Recebe uma pulseira (Session ID)
- A pulseira não tem informações detalhadas, só um identificador
- O sistema do cinema consulta seus dados internamente usando essa pulseira

Se alguém roubar sua pulseira → pode se passar por você

---

## Segurança em sessões

Como sessões representam identidade, elas são alvo de ataques.

### Principais riscos:

#### Session Hijacking
Roubo do Session ID e acesso à conta do usuário.

#### Fixation
Atacante força o usuário a usar um Session ID já conhecido.

#### XSS
Se cookies não forem protegidos, o Session ID pode ser roubado via JavaScript.

---

## Boas práticas

- Gerar Session ID aleatório e imprevisível
- Expirar sessões automaticamente
- Regenerar Session ID após login
- Usar HTTPS sempre (TLS)
- Marcar cookies como `HttpOnly` e `Secure`
- Limitar tempo de inatividade
- Invalidar sessão no logout

---

## Sessão vs Cookies vs JWT

| Tecnologia | Onde fica o estado | Característica |
|------------|------------------|----------------|
| Sessão     | Servidor         | Stateful        |
| Cookie     | Cliente (browser)| Armazena ID     |
| JWT        | Cliente (token)  | Stateless       |

---

## Resumo 

Sessões são um mecanismo essencial para:
- Simular “memória” no HTTP
- Manter usuários logados
- Gerenciar estado de aplicações web

Sem sessões, praticamente toda aplicação moderna (login, redes sociais, e-commerce) não funcionaria corretamente.


## LINKS EXTRAS

-[O que são sessões e cookies ](https://youtu.be/zw4duVA-ahY?si=Z0mf5veh5_8jOwtv)

-[Cookies // Dicionário do Programador](https://youtu.be/jQ0r7https://youtu.be/UPjbJWKbPSU?si=z15mMbzVSKTKbNRj)

