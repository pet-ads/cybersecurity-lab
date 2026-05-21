# OWASP

O **Open Worldwide Application Security Project (OWASP)** é uma comunidade aberta e sem fins lucrativos dedicada a capacitar organizações para desenvolver e manter aplicações e APIs confiáveis.

---

## Visão Geral da Organização

A OWASP atua de forma independente de pressões comerciais, fornecendo informações imparciais e práticas sobre segurança de aplicações. Quase todos os seus membros são **voluntários** que produzem ferramentas, padrões e pesquisas de forma colaborativa e transparente.

A fundação defende que a segurança deve ser abordada como uma combinação de:

- **Pessoas**
- **Processos**
- **Tecnologia**

---

## O OWASP Top 10:2025

A edição de **2025** é o oitavo lançamento deste projeto, que lista os dez riscos de segurança mais críticos para aplicações web.

A metodologia utiliza dados de mais de **2,8 milhões de aplicações**. A lista prioriza a **causa raiz** das vulnerabilidades em vez de apenas os sintomas, agrupando centenas de *Common Weakness Enumerations* (CWEs) em dez categorias principais.

---

## As 10 Categorias de Risco para 2025

### 1. A01:2025 – Broken Access Control (Controle de Acesso Quebrado)

Permanece em **1º lugar**.  
100% das aplicações testadas apresentaram falhas nesta categoria, onde usuários agem fora de suas permissões.

Esse problema ocorre quando usuários conseguem executar ações além das permissões previstas, comprometendo dados, funções administrativas e recursos sensíveis.

### Principais exemplos:

- Quebra do princípio do menor privilégio (*Least Privilege*)
- Acesso indevido a recursos de outros usuários
- Manipulação de parâmetros e metadados
- Escalada horizontal ou vertical de privilégios

---

### 2. A02:2025 – Security Misconfiguration (Configuração Incorreta de Segurança)

Subiu do 5º para o **2º lugar**.

Essa categoria engloba falhas decorrentes de ambientes mal configurados, serviços desnecessários habilitados e políticas de segurança inadequadas.

### Problemas comuns:

- Uso de credenciais padrão
- Mensagens de erro excessivamente detalhadas
- Serviços expostos sem necessidade
- Configurações inseguras em nuvem, containers e APIs

---

### 3. A03:2025 – Software Supply Chain Failures (Falhas na Cadeia de Suprimentos de Software)

Expandiu seu escopo para incluir qualquer compromisso no processo de construção ou distribuição de software.

Foi a categoria **mais votada pela comunidade** como uma preocupação de segurança.

### Principais riscos:

- Dependências comprometidas
- Bibliotecas de terceiros vulneráveis
- Ataques ao pipeline de CI/CD
- Publicação de pacotes maliciosos

---

### 4. A04:2025 – Cryptographic Failures (Falhas Criptográficas)

Foca na falta ou fraqueza da criptografia, expondo dados sensíveis.

Relaciona-se ao uso incorreto ou inexistente de mecanismos criptográficos para proteção de dados sensíveis.

### Exemplos frequentes:

- Uso de algoritmos obsoletos, como MD5 e SHA-1
- Criptografia fraca ou mal implementada
- Gerenciamento inadequado de chaves
- Armazenamento inseguro de senhas

---

### 5. A05:2025 – Injection (Injeção)

Continua entre as vulnerabilidades mais exploradas do mundo e concentra o **maior número de CVEs registrados**.

Ocorre quando dados não confiáveis são interpretados como comandos por bancos de dados, sistemas operacionais ou aplicações.

### Tipos comuns:

- SQL Injection
- Command Injection
- NoSQL Injection
- LDAP Injection

---

### 6. A06:2025 – Insecure Design (Design Inseguro)

Foca em falhas arquiteturais.

Diferencia-se de falhas de implementação, pois um design inseguro não pode ser corrigido por uma codificação perfeita se os controles necessários nunca foram criados.

### Exemplos:

- Ausência de modelagem de ameaças
- Fluxos críticos sem validação de segurança
- Falta de segregação de funções
- Regras de negócio vulneráveis

---

### 7. A07:2025 – Authentication Failures (Falhas de Autenticação)

Refere-se a fraquezas que permitem a invasores assumir identidades legítimas.

### Problemas comuns:

- Ausência de autenticação multifator (MFA)
- Políticas fracas de senha
- Sessões previsíveis ou mal gerenciadas
- Tokens inseguros ou expirados incorretamente

---

### 8. A08:2025 – Software or Data Integrity Failures (Falhas de Integridade de Software ou Dados)

Foca no tratamento de código ou infraestrutura que não protege contra:

### Exemplos:

- Execução de código não verificado
- Atualizações sem assinatura digital
- Desserialização insegura
- Manipulação maliciosa de dados

---

### 9. A09:2025 – Security Logging & Alerting Failures (Falhas de Log e Alerta de Segurança)

O nome foi alterado para enfatizar que **logs sem alertas** possuem valor mínimo para identificar incidentes em tempo real.

### Problemas principais:

- Ausência de logs críticos
- Logs incompletos ou inconsistentes
- Falta de alertas em tempo real
- Monitoramento ineficaz de incidentes

---

### 10. A10:2025 – Mishandling of Exceptional Conditions (Manipulação Incorreta de Condições Excepcionais)

Nova categoria introduzida na OWASP 2025, focada em falhas relacionadas ao tratamento inadequado de erros e comportamentos inesperados do sistema.

### Exemplos:

- Erros lógicos
- Falhas ao lidar com situações anômalas
- Erros de sistema que revelam informações sensíveis
- Sistemas que “falham abertos” (*fail open*)

---

## Metodologia e Prevenção

A OWASP utiliza o **Risk Score**, uma fórmula que pondera:

- Taxa de incidência
- Cobertura de testes
- Impacto técnico

Tudo baseado nas pontuações **CVSS** (v2 e v3).

---

## Estratégias de Prevenção Recomendadas

### Negar por padrão

O acesso deve ser concedido apenas conforme necessário.

### Criptografar dados sensíveis

Aplicar criptografia tanto:

- Em repouso
- Em trânsito

### Modelagem de Ameaças

Integrar a segurança desde a fase de requisitos e design.

### Autenticação Robusta

Implementar:

- MFA
- Sistemas de gerenciamento de identidade bem testados

### Falhar com Segurança (Fail Closed)

Em caso de erro, o sistema deve retornar a um estado seguro e nunca permitir acesso não autorizado.

---

## Conclusão

O OWASP Top 10 2025 demonstra uma evolução clara das ameaças modernas, com destaque para riscos ligados à cadeia de suprimentos, design inseguro e falhas operacionais.

Mais do que corrigir vulnerabilidades isoladas, o foco atual da segurança deve estar em:

- Arquitetura segura desde o início (*Security by Design*)
- Automação de validações de segurança
- Monitoramento contínuo
- Gestão de dependências e cadeia de suprimentos
- Implementação consistente de controles de acesso e autenticação

Esse cenário reforça que segurança não é apenas uma etapa do desenvolvimento, mas parte essencial de todo o ciclo de vida do software.
