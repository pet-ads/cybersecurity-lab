# Variáveis de Ambiente

## Introdução

Durante o desenvolvimento de aplicações, é comum a necessidade de utilizar informações como senhas, chaves de API, tokens de autenticação e credenciais de bancos de dados. Embora seja possível armazenar esses dados diretamente no código-fonte, essa prática representa um grande risco de segurança, pois qualquer pessoa com acesso ao código poderá visualizar informações sensíveis.

Para resolver esse problema, os desenvolvedores utilizam as **variáveis de ambiente**, um recurso presente nos sistemas operacionais que permite armazenar configurações e credenciais fora da aplicação. Além de aumentar a segurança, essa abordagem facilita a configuração do software em diferentes ambientes, como desenvolvimento, testes e produção.

Neste material, serão apresentados os conceitos fundamentais sobre variáveis de ambiente, sua utilização em Python e sua importância dentro das boas práticas de Cybersegurança.

---

# O que são Variáveis de Ambiente?

Uma variável de ambiente é um valor armazenado pelo sistema operacional e associado a um nome específico. Esses valores ficam disponíveis para programas em execução e podem ser utilizados para configurar o comportamento de uma aplicação sem a necessidade de modificar seu código-fonte.

Em outras palavras, as variáveis de ambiente funcionam como configurações externas que podem variar de um computador para outro ou entre diferentes servidores.

Alguns exemplos comuns incluem:

```text
DB_HOST=localhost
DB_PORT=5432
API_KEY=abc123xyz
APP_ENV=production
```

Nesse exemplo, uma aplicação pode utilizar essas informações para se conectar a um banco de dados ou identificar em qual ambiente está sendo executada.

---

# Por que Utilizar Variáveis de Ambiente?

O uso de variáveis de ambiente tornou-se uma prática fundamental no desenvolvimento moderno por oferecer benefícios tanto para a segurança quanto para a organização dos projetos.

## Proteção de Informações Sensíveis

Um dos principais motivos para utilizar variáveis de ambiente é evitar que informações confidenciais sejam armazenadas diretamente no código.

Considere o seguinte exemplo:

```python
senha = "MinhaSenha123"
api_key = "abc123xyz"
```

Embora o código funcione normalmente, qualquer pessoa que tenha acesso ao projeto poderá visualizar essas informações. Além disso, caso o código seja enviado para um repositório público, as credenciais poderão ser expostas na internet.

Uma alternativa mais segura consiste em armazenar esses valores fora do código:

```python
import os

senha = os.getenv("SENHA")
api_key = os.getenv("API_KEY")
```

Dessa forma, as credenciais permanecem protegidas no ambiente onde a aplicação está sendo executada.

---

## Facilidade de Configuração

Outro benefício importante é a possibilidade de utilizar diferentes configurações sem alterar o código-fonte.

Por exemplo, durante o desenvolvimento, uma aplicação pode utilizar um banco de dados local:

```text
APP_ENV=development
DEBUG=True
```

Já em produção:

```text
APP_ENV=production
DEBUG=False
```

Com isso, o mesmo código pode ser utilizado em diferentes cenários, bastando alterar os valores das variáveis de ambiente.

---

## Portabilidade

As variáveis de ambiente também contribuem para a portabilidade da aplicação.

Um projeto pode ser executado no computador do desenvolvedor, em um servidor Linux, em containers Docker ou em serviços de computação em nuvem utilizando exatamente o mesmo código. Apenas as configurações externas são alteradas conforme a necessidade.

---

# A Relação entre Variáveis de Ambiente e Cybersegurança

Dentro da Cybersegurança, a proteção de credenciais é uma preocupação constante. Senhas, tokens e chaves de acesso são considerados ativos críticos e devem ser protegidos adequadamente.

Por esse motivo, uma das recomendações mais importantes é:

> Nunca armazenar segredos diretamente no código-fonte.

Essa prática faz parte do conceito conhecido como **Gerenciamento de Segredos (Secrets Management)**, que consiste em controlar de forma segura informações sensíveis utilizadas pelas aplicações.

Entre os principais tipos de segredos digitais estão:

- Senhas de usuários;
- Chaves de API;
- Tokens de autenticação;
- Credenciais de banco de dados;
- Certificados digitais;
- Chaves criptográficas.

O uso de variáveis de ambiente reduz significativamente o risco de exposição dessas informações.

---

## Princípio do Menor Privilégio

Outra prática importante de Cybersegurança é o **Princípio do Menor Privilégio**.

Segundo esse princípio, uma aplicação deve possuir apenas as permissões estritamente necessárias para realizar suas atividades.

Por exemplo, se uma aplicação precisa apenas consultar dados de um banco de dados, não faz sentido fornecer a ela uma conta com permissões administrativas completas.

Caso uma credencial seja comprometida, os danos serão limitados pelas permissões reduzidas.

---

## Defesa em Profundidade

Embora as variáveis de ambiente sejam importantes para a proteção de credenciais, elas não devem ser consideradas a única medida de segurança.

A estratégia recomendada é conhecida como **Defesa em Profundidade (Defense in Depth)**, que consiste na utilização de múltiplas camadas de proteção.

Essas camadas podem incluir:

- Variáveis de ambiente;
- Criptografia;
- Controle de acesso;
- Autenticação multifator (MFA);
- Firewalls;
- Monitoramento de logs;
- Sistemas de detecção de intrusão;
- Gestão centralizada de segredos.

Quanto mais camadas forem implementadas, mais difícil será para um atacante comprometer o sistema.

---

# Utilizando Variáveis de Ambiente em Python

Python oferece suporte nativo para acesso às variáveis de ambiente por meio da biblioteca `os`.

Primeiramente, é necessário importar a biblioteca:

```python
import os
```

Após a importação, é possível acessar as variáveis configuradas no sistema.

Uma forma simples é utilizar o método `getenv()`:

```python
usuario = os.getenv("USUARIO")
```

Também é possível definir um valor padrão caso a variável não exista:

```python
usuario = os.getenv("USUARIO", "Visitante")
```

Essa abordagem é recomendada porque evita erros caso a variável não esteja configurada.

---

# Trabalhando com Arquivos .env

Em projetos Python, especialmente durante o desenvolvimento local, é comum utilizar arquivos `.env`.

Esses arquivos armazenam variáveis de ambiente em formato simples de texto.

Exemplo:

```text
DB_HOST=localhost
DB_USER=admin
DB_PASSWORD=minhaSenhaSegura
API_KEY=123456789
```

Para que o Python consiga carregar essas informações automaticamente, utiliza-se a biblioteca `python-dotenv`.

A instalação pode ser realizada com:

```bash
pip install python-dotenv
```

Depois disso, basta carregar o arquivo:

```python
from dotenv import load_dotenv
import os

load_dotenv()

api_key = os.getenv("API_KEY")
```

Com isso, as variáveis passam a estar disponíveis para a aplicação como se tivessem sido configuradas diretamente no sistema operacional.

---

# Protegendo o Arquivo .env

Apesar de facilitar o desenvolvimento, o arquivo `.env` geralmente contém informações sensíveis e, por esse motivo, não deve ser compartilhado.

Uma prática essencial é adicioná-lo ao arquivo `.gitignore`:

```gitignore
.env
```

Isso impede que o arquivo seja enviado acidentalmente para repositórios Git.

Ao compartilhar um projeto, recomenda-se criar um arquivo chamado `.env.example`, contendo apenas os nomes das variáveis necessárias:

```text
DB_HOST=
DB_USER=
DB_PASSWORD=
API_KEY=
```

Dessa forma, outros desenvolvedores saberão quais configurações precisam criar sem que as credenciais reais sejam expostas.

---

# Boas Práticas de Segurança

Ao utilizar variáveis de ambiente, algumas práticas ajudam a aumentar ainda mais a segurança da aplicação.

- Nunca armazenar senhas diretamente no código.
- Nunca enviar arquivos `.env` para repositórios públicos.
- Utilizar credenciais com permissões mínimas necessárias.
- Realizar a troca periódica de senhas e chaves de acesso.
- Monitorar possíveis vazamentos de credenciais.
- Utilizar ferramentas de gerenciamento de segredos em ambientes corporativos.

Soluções como HashiCorp Vault, AWS Secrets Manager, Azure Key Vault e Google Secret Manager oferecem recursos avançados para armazenamento seguro de credenciais, incluindo criptografia, auditoria e controle de acesso.

---

# Conclusão

As variáveis de ambiente representam uma das práticas mais importantes para o desenvolvimento seguro de aplicações modernas. Além de separar configurações do código-fonte, elas ajudam a proteger informações sensíveis, facilitam a implantação em diferentes ambientes e contribuem para a adoção de boas práticas de Cybersegurança.

Quando combinadas com conceitos como Gerenciamento de Segredos, Princípio do Menor Privilégio e Defesa em Profundidade, as variáveis de ambiente tornam-se uma ferramenta fundamental para a construção de sistemas mais seguros, confiáveis e alinhados às exigências atuais de segurança da informação.

<br>

[![➡ Próxima Seção](https://img.shields.io/badge/-➡_Próxima_Seção-blue?style=for-the-badge&color=007BFF)](https://github.com/pet-ads/cybersecurity-lab/blob/main/Guia%20de%20Estudos/6%20-%20Infraestrutura/3%20-%20Configura%C3%A7%C3%A3o%20segura%20de%20servidor.md)

## LINKS EXTRAS

-[O Que São Variáveis de Ambiente no Python e Como Usá-las?](https://youtu.be/yVP50NsY_FQ?si=Oj351P0EhtEP_3-J)


