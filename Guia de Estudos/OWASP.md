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
[OWASP Top 1](https://owasp.org/Top10/2025/A01_2025-Broken_Access_Control/)

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
[OWASP Top 2](https://owasp.org/Top10/2025/A02_2025-Security_Misconfiguration/)

Subiu do 5º para o **2º lugar**.

Essa categoria engloba falhas decorrentes de ambientes mal configurados, serviços desnecessários habilitados e políticas de segurança inadequadas.

### Problemas comuns:

- Uso de credenciais padrão
- Mensagens de erro excessivamente detalhadas
- Serviços expostos sem necessidade
- Configurações inseguras em nuvem, containers e APIs

---

### 3. A03:2025 – Software Supply Chain Failures (Falhas na Cadeia de Suprimentos de Software)
[OWASP Top 3](https://owasp.org/Top10/2025/A03_2025-Software_Supply_Chain_Failures/)

Expandiu seu escopo para incluir qualquer compromisso no processo de construção ou distribuição de software.

Foi a categoria **mais votada pela comunidade** como uma preocupação de segurança.

### Principais riscos:

- Dependências comprometidas
- Bibliotecas de terceiros vulneráveis
- Ataques ao pipeline de CI/CD
- Publicação de pacotes maliciosos

---

### 4. A04:2025 – Cryptographic Failures (Falhas Criptográficas)
[OWASP Top 4](https://owasp.org/Top10/2025/A04_2025-Cryptographic_Failures/)

Foca na falta ou fraqueza da criptografia, expondo dados sensíveis.

Relaciona-se ao uso incorreto ou inexistente de mecanismos criptográficos para proteção de dados sensíveis.

### Exemplos frequentes:

- Uso de algoritmos obsoletos, como MD5 e SHA-1
- Criptografia fraca ou mal implementada
- Gerenciamento inadequado de chaves
- Armazenamento inseguro de senhas

---

### 5. A05:2025 – Injection (Injeção)
[OWASP Top 5](https://owasp.org/Top10/2025/A05_2025-Injection/)

Continua entre as vulnerabilidades mais exploradas do mundo e concentra o **maior número de CVEs registrados**.

Ocorre quando dados não confiáveis são interpretados como comandos por bancos de dados, sistemas operacionais ou aplicações.

### Tipos comuns:

- SQL Injection
- Command Injection
- NoSQL Injection
- LDAP Injection

---

### 6. A06:2025 – Insecure Design (Design Inseguro)
[OWASP Top 6](https://owasp.org/Top10/2025/A06_2025-Insecure_Design/)

Foca em falhas arquiteturais.

Diferencia-se de falhas de implementação, pois um design inseguro não pode ser corrigido por uma codificação perfeita se os controles necessários nunca foram criados.

### Exemplos:

- Ausência de modelagem de ameaças
- Fluxos críticos sem validação de segurança
- Falta de segregação de funções
- Regras de negócio vulneráveis

---

### 7. A07:2025 – Authentication Failures (Falhas de Autenticação)
[OWASP Top 7](https://owasp.org/Top10/2025/A07_2025-Authentication_Failures/)

Refere-se a fraquezas que permitem a invasores assumir identidades legítimas.

### Problemas comuns:

- Ausência de autenticação multifator (MFA)
- Políticas fracas de senha
- Sessões previsíveis ou mal gerenciadas
- Tokens inseguros ou expirados incorretamente

---

### 8. A08:2025 – Software or Data Integrity Failures (Falhas de Integridade de Software ou Dados)
[OWASP Top 8](https://owasp.org/Top10/2025/A08_2025-Software_or_Data_Integrity_Failures/)

Foca no tratamento de código ou infraestrutura que não protege contra:

### Exemplos:

- Execução de código não verificado
- Atualizações sem assinatura digital
- Desserialização insegura
- Manipulação maliciosa de dados

---

### 9. A09:2025 – Security Logging & Alerting Failures (Falhas de Log e Alerta de Segurança)
[OWASP Top 9](https://owasp.org/Top10/2025/A09_2025-Security_Logging_and_Alerting_Failures/)

O nome foi alterado para enfatizar que **logs sem alertas** possuem valor mínimo para identificar incidentes em tempo real.

### Problemas principais:

- Ausência de logs críticos
- Logs incompletos ou inconsistentes
- Falta de alertas em tempo real
- Monitoramento ineficaz de incidentes

---

### 10. A10:2025 – Mishandling of Exceptional Conditions (Manipulação Incorreta de Condições Excepcionais)
[OWASP Top 10](https://owasp.org/Top10/2025/A10_2025-Mishandling_of_Exceptional_Conditions/)

Nova categoria introduzida na OWASP 2025, focada em falhas relacionadas ao tratamento inadequado de erros e comportamentos inesperados do sistema.

### Exemplos:

- Erros lógicos
- Falhas ao lidar com situações anômalas
- Erros de sistema que revelam informações sensíveis
- Sistemas que “falham abertos” (*fail open*)

---

## X01:2025 — Falta de Resiliência da Aplicação
[OWASP NEXT STEPS](https://owasp.org/Top10/2025/X01_2025-Next_Steps/)

Esse tipo de falha acontece quando a aplicação não consegue lidar bem com estresse, erros ou condições inesperadas. Em vez de se recuperar, ela degrada ou falha completamente. Isso pode resultar principalmente em indisponibilidade, mas também pode causar corrupção de dados, vazamento de informações sensíveis e até falhas em cascata que afetam outros sistemas.

As causas estão relacionadas a classes conhecidas de vulnerabilidades, como consumo descontrolado de recursos (CWE-400), problemas com dados altamente comprimidos (CWE-409), recursão sem controle (CWE-674) e loops infinitos (CWE-835). Em conjunto, elas mostram que o problema está em como a aplicação lida com limites e exceções.

## Como prevenir

A prevenção passa por projetar sistemas assumindo que falhas vão acontecer. Isso significa impor limites claros de uso de recursos, como CPU, memória e conexões, além de proteger operações mais pesadas para que não fiquem expostas sem necessidade.

Também é essencial validar entradas de forma rigorosa, limitar o tamanho das respostas e evitar retornar dados brutos diretamente ao cliente. O sistema deve adotar uma postura mais segura por padrão, rejeitando o que não for explicitamente permitido.

Outro ponto importante é evitar chamadas bloqueantes e síncronas em excesso, preferindo abordagens assíncronas com timeouts e controle de concorrência. Além disso, padrões de resiliência como circuit breaker, bulkheads, retry controlado e degradação gradual ajudam o sistema a continuar funcionando mesmo sob falhas parciais.

Testes de carga, performance e até chaos engineering ajudam a identificar problemas antes que eles ocorram em produção. Monitoramento e observabilidade também são fundamentais para detectar comportamento anormal rapidamente.

Por fim, medidas contra abuso, como bloqueio de bots, limitação de sessões, proof-of-work e controle de comportamento, ajudam a reduzir ataques automatizados e consumo excessivo de recursos.

## Cenários de ataque

Na prática, os ataques mais comuns envolvem a exaustão de recursos do sistema, como memória, CPU ou conexões, levando à queda do serviço. Outro cenário é o uso de entradas maliciosas ou malformadas que exploram falhas de lógica e quebram o funcionamento da aplicação. Também é comum atacar dependências externas (APIs e serviços), o que pode derrubar a aplicação mesmo que ela esteja funcionando corretamente.

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
