# Configuração Segura de Servidores

## Introdução

A configuração segura de servidores é uma das etapas mais importantes da **Cybersegurança**. Um servidor mal configurado pode permitir acessos não autorizados, vazamento de informações, indisponibilidade de serviços e comprometimento de toda a infraestrutura.

Para reduzir esses riscos, é necessário aplicar diversas camadas de proteção, seguindo o princípio da **Defesa em Profundidade (Defense in Depth)**. Isso significa que, mesmo que uma camada seja comprometida, outras continuarão protegendo o ambiente.

Este material apresenta as principais técnicas utilizadas para aumentar a segurança de servidores Linux e Unix, explicando seu funcionamento, vantagens, exemplos práticos e boas práticas.

---

# 1. Chaves SSH

O **SSH (Secure Shell)** é um protocolo utilizado para realizar acesso remoto seguro a servidores. Diferentemente do Telnet, o SSH criptografa toda a comunicação entre cliente e servidor, protegendo credenciais e dados contra interceptação.

Uma das formas mais seguras de autenticação é através das **chaves SSH**, que substituem o uso de senhas.

## Como funciona

A autenticação utiliza um par de chaves criptográficas:

* **Chave privada:** permanece somente no computador do usuário e nunca deve ser compartilhada.
* **Chave pública:** é copiada para o servidor e utilizada para validar a identidade do cliente.

Quando uma conexão é iniciada, o servidor verifica se a chave privada correspondente à chave pública cadastrada está sendo utilizada. Caso a validação seja bem-sucedida, o acesso é concedido.

Como apenas o proprietário possui a chave privada, torna-se extremamente difícil que um invasor consiga autenticar-se.

## Vantagens

* Elimina a necessidade de memorizar senhas.
* Praticamente impossibilita ataques de força bruta.
* Permite automatizar acessos de forma segura.
* Possui criptografia muito mais forte do que senhas tradicionais.
* É compatível com autenticação multifator.

## Exemplo de geração da chave

```bash
ssh-keygen -t ed25519 -C "usuario@exemplo.com"
```

Depois, copie a chave pública para o servidor:

```bash
ssh-copy-id usuario@servidor
```

## Boa prática

Após confirmar que o acesso por chave está funcionando, desative a autenticação por senha no arquivo:

```text
/etc/ssh/sshd_config
```

Alterando:

```text
PasswordAuthentication no
```

Em seguida reinicie o serviço SSH.

Essa simples configuração elimina a maioria dos ataques automatizados contra servidores.

---

# 2. Firewalls

Um **firewall** controla quais conexões podem entrar ou sair de um servidor.

Seu principal objetivo é reduzir a **superfície de ataque**, permitindo apenas o tráfego realmente necessário.

Imagine um servidor Web.

Ele precisa aceitar conexões HTTP e HTTPS, mas não existe motivo para que o banco de dados fique acessível pela internet.

Um firewall resolve exatamente esse problema.

## Funcionamento

O firewall analisa cada pacote recebido e verifica regras como:

* origem;
* destino;
* protocolo;
* porta;
* interface de rede.

Dependendo dessas regras, o pacote pode ser:

* permitido;
* bloqueado;
* rejeitado.

## Exemplo

Servidor Web:

| Serviço    | Porta |   Deve ficar pública?  |
| ---------- | ----: | :--------------------: |
| SSH        |    22 | Apenas administradores |
| HTTP       |    80 |           Sim          |
| HTTPS      |   443 |           Sim          |
| PostgreSQL |  5432 |           Não          |
| Redis      |  6379 |           Não          |

Nesse cenário, apenas as portas **80** e **443** ficam abertas para qualquer usuário.

As demais permanecem restritas.

## Ferramentas comuns

* UFW (Ubuntu)
* iptables
* nftables
* firewalld
* CSF (ConfigServer Security & Firewall)

## Boa prática

A estratégia mais segura é:

> Bloquear tudo por padrão e liberar apenas o que for necessário.

---

# 3. VPNs e Redes Privadas

Nem todo serviço precisa estar disponível na internet.

Na maioria das empresas, apenas o servidor Web fica público.

Serviços internos, como bancos de dados e APIs administrativas, permanecem em **redes privadas**.

Quando administradores precisam acessar esses recursos remotamente, utiliza-se uma **VPN (Virtual Private Network)**.

## O que é uma VPN?

Uma VPN cria um **túnel criptografado** entre o computador do usuário e a rede da empresa.

Todo o tráfego passa por esse túnel protegido.

Mesmo que alguém intercepte os dados durante a transmissão, eles estarão criptografados.

## Benefícios

* Protege dados em redes públicas.
* Oculta serviços internos da internet.
* Permite acesso remoto seguro.
* Reduz significativamente a exposição da infraestrutura.

## Exemplo

Sem VPN:

```text
Internet
      │
Banco de Dados
```

Qualquer pessoa pode tentar acessar o banco.

Com VPN:

```text
Internet
      │
Servidor VPN
      │
Rede Privada
      │
Banco de Dados
```

Agora apenas usuários autenticados conseguem acessar os serviços internos.

---

# 4. Infraestrutura de Chaves Públicas (PKI) e SSL/TLS

A **PKI (Public Key Infrastructure)** é o conjunto de processos responsáveis pela criação, emissão, validação e revogação de certificados digitais.

Esses certificados são utilizados pelo protocolo **SSL/TLS**, responsável por proteger comunicações na internet.

Hoje, praticamente todos os sites utilizam HTTPS graças ao TLS.

## Como funciona

Cada servidor possui um certificado digital emitido por uma Autoridade Certificadora (CA).

Quando um cliente acessa o servidor:

1. recebe o certificado;
2. verifica sua autenticidade;
3. cria uma chave de sessão;
4. toda a comunicação passa a ser criptografada.

## Benefícios

* Garante confidencialidade.
* Garante autenticidade.
* Protege contra ataques Man-in-the-Middle (MITM).
* Impede alterações no conteúdo transmitido.

## Exemplos de uso

* HTTPS
* APIs REST
* SMTP seguro
* LDAP seguro
* VPNs
* Comunicação entre microsserviços

## Desafios

Administrar certificados exige:

* emissão;
* renovação;
* revogação;
* armazenamento seguro das chaves privadas.

Em grandes empresas essa tarefa costuma ser automatizada.

---

# 5. Auditoria de Serviços

Quanto menos serviços estiverem em execução, menor será a possibilidade de exploração por invasores.

Por isso, é importante realizar auditorias periódicas.

## Objetivos

Descobrir:

* quais serviços estão ativos;
* quais portas estão abertas;
* quais protocolos estão sendo utilizados;
* quais processos iniciam automaticamente.

Muitas distribuições Linux instalam serviços que talvez nunca sejam utilizados.

Cada serviço desnecessário representa um possível ponto de vulnerabilidade.

## Ferramentas

Verificar portas abertas:

```bash
ss -tuln
```

ou

```bash
netstat -tuln
```

Verificar processos:

```bash
ps aux
```

Verificar serviços:

```bash
systemctl list-units --type=service
```

## Boa prática

Desative qualquer serviço que não seja essencial para o funcionamento do servidor.

---

# 6. Auditoria de Arquivos e Sistemas de Detecção de Intrusão (IDS)

Mesmo que um invasor consiga acesso ao servidor, é importante detectar rapidamente qualquer modificação realizada.

É exatamente essa a função da auditoria de arquivos.

Essas ferramentas criam uma "fotografia" inicial do sistema contendo informações como:

* tamanho;
* permissões;
* proprietário;
* hash criptográfico.

Posteriormente essas informações são comparadas com o estado atual.

Qualquer alteração gera um alerta.

## Ferramentas

### AIDE

Advanced Intrusion Detection Environment.

Leve e bastante utilizado em servidores Linux.

### Tripwire

Ferramenta tradicional para monitoramento da integridade de arquivos críticos.

## O que pode ser detectado?

* alteração de binários;
* modificação de bibliotecas;
* inclusão de malware;
* criação de usuários ocultos;
* alteração de arquivos de configuração.

## Limitação

Sempre que um software legítimo é atualizado, a base de referência precisa ser atualizada.

Caso contrário, alterações legítimas também serão reportadas.

---

# 7. Ambientes de Execução Isolada

Uma das melhores estratégias de segurança é impedir que um problema em um serviço afete todo o servidor.

Isso é feito através do isolamento.

Cada aplicação executa em um ambiente separado.

Caso uma delas seja comprometida, o invasor encontra muito mais dificuldades para acessar os demais componentes.

Essa estratégia segue o princípio do **menor impacto possível**.

## Tipos de isolamento

### chroot

Isola um processo dentro de um diretório específico.

É uma solução simples, porém limitada.

### Contêineres

Ferramentas como **Docker** e **Podman** executam aplicações em ambientes isolados.

Cada contêiner possui:

* sistema de arquivos próprio;
* bibliotecas próprias;
* processos isolados;
* rede própria.

### Máquinas Virtuais

Cada aplicação executa em um sistema operacional independente.

Possuem maior isolamento, porém consomem mais recursos.

### Servidores físicos dedicados

É o maior nível de isolamento.

Mesmo que um servidor seja comprometido, os demais permanecem protegidos.

## Analogia

Imagine um navio dividido em vários compartimentos estanques.

Se um compartimento for inundado, os demais permanecem secos e o navio continua flutuando.

O isolamento de aplicações funciona exatamente dessa maneira.

---

# Boas Práticas para Configuração Segura de Servidores

Uma infraestrutura segura não depende de apenas uma tecnologia, mas da combinação de diversas medidas de proteção. Entre as principais recomendações estão:

* Utilizar autenticação por **chaves SSH** e desabilitar login por senha.
* Manter o sistema operacional e os softwares sempre atualizados.
* Configurar um **firewall** com política de negar tudo por padrão, liberando apenas os serviços necessários.
* Restringir serviços internos por meio de **redes privadas** ou **VPNs**.
* Utilizar **SSL/TLS** para proteger todas as comunicações sensíveis.
* Remover ou desativar serviços e portas que não são utilizados.
* Monitorar continuamente a integridade dos arquivos com ferramentas como **AIDE** ou **Tripwire**.
* Executar aplicações em ambientes isolados, como contêineres ou máquinas virtuais.
* Aplicar o **Princípio do Menor Privilégio**, concedendo apenas as permissões indispensáveis para usuários e processos.
* Realizar auditorias periódicas, registrar eventos em logs e monitorar atividades suspeitas.

---

# Resumo

A segurança de servidores é construída por meio da combinação de diferentes mecanismos de proteção. Chaves SSH fortalecem a autenticação e eliminam a dependência de senhas; firewalls reduzem a superfície de ataque ao controlar o tráfego de rede; VPNs e redes privadas protegem comunicações internas; a infraestrutura de chaves públicas (PKI) e o protocolo TLS garantem autenticação e criptografia; auditorias de serviços identificam processos desnecessários; ferramentas de monitoramento de integridade detectam alterações indevidas em arquivos; e o isolamento por contêineres, máquinas virtuais ou servidores dedicados limita o impacto de possíveis invasões.

Nenhuma dessas medidas é suficiente de forma isolada. Quando aplicadas em conjunto, elas formam múltiplas camadas de defesa, tornando a infraestrutura significativamente mais resistente a ataques e alinhada às boas práticas modernas de Cybersegurança.

<br>

[![➡ Próxima Seção](https://img.shields.io/badge/-➡_Próxima_Seção-blue?style=for-the-badge&color=007BFF)](https://github.com/pet-ads/cybersecurity-lab/blob/main/Guia%20de%20Estudos/4%20-%20Vulnerabilidade%20Cr%C3%ADticas/3%20-%20CSRF.md)


## LINKS EXTRAS

-[7 Medidas de Segurança para Proteger Seus Servidores](https://www.digitalocean.com/community/tutorials/7-medidas-de-seguranca-para-proteger-seus-servidores-pt)

-[Configuração de segurança do Windows Server e boas práticas](https://www.hostragons.com/pt/blog/configuracao-de-seguranca-do-servidor-windows/)



