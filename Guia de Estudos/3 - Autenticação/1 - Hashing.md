# Hashing

O hashing é um dos conceitos mais importantes tanto em estruturas de dados quanto em segurança da informação. Ele aparece em dois contextos diferentes, mas com objetivos bem distintos: na computação, ele é usado para melhorar a eficiência de busca e armazenamento de dados; já na cibersegurança, ele é fundamental para proteger informações sensíveis, especialmente senhas.

Em termos de eficiência, o hashing se destaca porque permite que buscas sejam feitas, em média, em tempo constante, ou seja, **O(1)**. Isso é muito mais rápido do que a busca sequencial, que cresce linearmente com o tamanho dos dados (**O(n)**), ou até mesmo a busca binária, que apesar de eficiente, depende de uma estrutura ordenada e opera em **O(log n)**. Essa performance é possível graças às tabelas hash, estruturas que organizam dados com base em uma função de mapeamento.

# Como funciona hash?
Uma tabela hash funciona como um conjunto de pares chave-valor, onde cada chave identifica de forma única um valor armazenado. A chave é processada por uma função hash, que transforma esse dado (pode ser uma string, número ou outro tipo complexo) em um índice válido dentro de um vetor. Esse índice é onde o valor será armazenado ou procurado. As operações principais envolvem inserir um par chave-valor, buscar um valor a partir da chave e remover elementos da estrutura.

Um exemplo prático disso pode ser visto em dicionários de linguagens como Python:

```python
usuarios = {
    "ana": 25,
    "joao": 30
}

print(usuarios["ana"])  # acesso direto via hash
```

Aqui, o Python usa internamente uma tabela hash para acessar o valor associado à chave `"ana"` sem precisar percorrer todos os elementos.

---

## Como a tabela hash funciona na prática

O ponto central desse processo é a função hash, representada como **h(k)**. Ela é responsável por converter a chave em um número inteiro dentro do intervalo da tabela. Um exemplo comum é pegar a soma dos valores ASCII dos caracteres de uma string, mas esse método é fraco, pois gera muitas colisões, especialmente com palavras diferentes que produzem somas semelhantes.

Uma abordagem mais eficiente é considerar a posição de cada caractere, utilizando potências de números primos, como 31 ou 37, o que melhora significativamente a distribuição dos dados. No final, aplica-se a operação de módulo para garantir que o valor gerado caiba dentro do tamanho da tabela:

```
h(k) mod n
```

### Exemplo simples de função hash

```python
def hash_simples(chave):
    return sum(ord(c) for c in chave)

print(hash_simples("ana"))
```

**Problema:** `"ana"` e `"naa"` podem gerar valores iguais → colisão.

---

## Colisão

Apesar de todo esse cuidado, um problema inevitável é a colisão, que ocorre quando duas chaves diferentes geram o mesmo índice. Esse é um dos principais desafios das tabelas hash.

Para lidar com isso, existem estratégias como:
- **Encadeamento (chaining)**: múltiplos elementos são armazenados em uma lista na mesma posição.
- **Endereçamento aberto**: a tabela procura outra posição disponível.

Outro fator importante para reduzir colisões é o uso de números primos no tamanho da tabela, o que ajuda a evitar padrões repetitivos na distribuição dos dados. Além disso, manter um fator de carga baixo também é essencial para preservar a eficiência da estrutura.

---

## Hashing em cibersegurança

Enquanto na estrutura de dados o foco é desempenho, na cibersegurança o hashing assume um papel completamente diferente: ele passa a ser uma ferramenta de proteção. Nesse contexto, o objetivo não é facilitar buscas rápidas, mas sim tornar os dados irreversíveis, ou seja, impossíveis de serem reconstruídos a partir do resultado do hash.

Esse é o caso do armazenamento de senhas. Em sistemas seguros, senhas nunca devem ser armazenadas em texto puro. Em vez disso, elas são convertidas em hashes criptográficos.

No entanto, apenas aplicar uma função hash simples não é suficiente, pois ataques modernos conseguem quebrar muitos desses valores usando tabelas pré-computadas ou força bruta.

---

# Salt, Pepper e bcrypt

Para aumentar a segurança no armazenamento de senhas, utiliza-se o conceito de **salt**, que é um valor aleatório adicionado à senha antes do hashing. Isso garante que duas senhas iguais nunca gerem o mesmo hash, dificultando ataques baseados em tabelas pré-computadas.

Em sistemas ainda mais robustos, pode-se usar o **pepper**, que é um valor secreto adicionado ao processo de hashing, mas armazenado separadamente do banco de dados. Isso significa que, mesmo que o banco seja comprometido, o atacante ainda não terá acesso completo ao processo de geração do hash.

Além dessas técnicas, um dos algoritmos mais importantes na prática é o **bcrypt**. Ele não é apenas uma função hash simples, mas um algoritmo projetado especificamente para senhas.

O bcrypt já inclui automaticamente o uso de salt e ainda possui um **fator de custo configurável**, que define o quanto o processo será lento — e isso é intencional. Quanto maior o custo, mais difícil se torna realizar ataques de força bruta, pois cada tentativa de senha exige mais tempo computacional.

---

## Exemplo prático com bcrypt em Python

```python
import bcrypt

senha = "minha_senha_segura".encode()

# Gerando hash com salt automático
hash_senha = bcrypt.hashpw(senha, bcrypt.gensalt())

print(hash_senha)
```

### Explicação do exemplo:

- A senha é convertida para **bytes** usando `.encode()`
- O bcrypt gera automaticamente um **salt**
- O resultado é um **hash seguro e irreversível**

---

##  Verificando senha com bcrypt

Na prática, não comparamos hashes manualmente. O próprio bcrypt faz essa verificação:

```python
senha_digitada = "minha_senha_segura".encode()

if bcrypt.checkpw(senha_digitada, hash_senha):
    print("Senha correta!")
else:
    print("Senha incorreta!")
```

### Como funciona:

- A senha digitada é convertida para bytes
- O bcrypt compara internamente o hash armazenado com o valor gerado
- Se forem equivalentes, a senha é validada com sucesso

---

## Algoritmos modernos de hashing

Algoritmos modernos de hashing para senhas são projetados para serem lentos de propósito. Isso é uma defesa importante contra ataques de força bruta.

Um dos exemplos mais utilizados é o **bcrypt**, que permite ajustar um fator de custo, aumentando o tempo necessário para calcular o hash. Quanto maior esse custo, mais difícil se torna tentar milhões de combinações em pouco tempo.

Algoritmos antigos como **MD5** e **SHA-1** já não são considerados seguros para senhas, pois são rápidos demais e vulneráveis a colisões e ataques modernos.

Hoje, recomenda-se o uso de algoritmos como:
- bcrypt  
- scrypt  
- Argon2  

---

<br>

[![➡ Próxima Seção](https://img.shields.io/badge/-➡_Próxima_Seção-blue?style=for-the-badge&color=007BFF)](https://github.com/pet-ads/cybersecurity-lab/blob/main/Guia%20de%20Estudos/3%20-%20Autentica%C3%A7%C3%A3o/2%20-%20Sess%C3%B5es.md)

## LINKS EXTRAS

-[Estruturas de Dados - Conceitos de Tabela Hash](https://youtu.be/jQ0r7P8rC1M?si=kRn_R8rpZmSmEr_4)

-[What is Hashing? Hash Functions Explained Simply](https://youtu.be/2BldESGZKB8?si=mRf9ZKYKcwm55kPC)

-[O que é bcrypt](https://flammadesign.com.br/glossario/o-que-e-bcrypt-entenda-o-algoritmo-de-hashing/)