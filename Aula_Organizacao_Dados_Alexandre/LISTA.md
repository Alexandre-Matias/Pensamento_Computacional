# Lista — Sequência de Chamada da Turma

## 📋 O que é uma Lista?

Uma **lista** é a estrutura de organização linear. É uma sequência ordenada de elementos onde a **posição** (índice) dita a ordem de acesso. Não existem ramificações nem conexões cruzadas — apenas um elemento após o outro.

> **Vantagem:** Simplicidade de implementação e leitura direta.  
> **Uso cotidiano:** Agenda telefônica, listas de tarefas, fila de reprodução de músicas.

---

## 📌 Conjunto: Alunos da Turma de Pensamento Computacional

**Representação:** Lista de chamada em ordem alfabética (posição 0 a 5)

---

### Representação Textual

```
Índice | Nome do Aluno      | Matrícula
-------|--------------------|-----------
  0    | Ana Souza          | 2025001
  1    | Bruno Lima         | 2025002
  2    | Carlos Mendes      | 2025003
  3    | Daniela Ferreira   | 2025004
  4    | Eduardo Costa      | 2025005
  5    | Fernanda Oliveira  | 2025006
```

---

### Representação em Pseudocódigo

```
lista_chamada = [
  "Ana Souza",
  "Bruno Lima",
  "Carlos Mendes",
  "Daniela Ferreira",
  "Eduardo Costa",
  "Fernanda Oliveira"
]

Para cada aluno em lista_chamada:
    chamar(aluno)
```

---

### Representação Visual (ASCII)

```
[0: Ana] → [1: Bruno] → [2: Carlos] → [3: Daniela] → [4: Eduardo] → [5: Fernanda]
```

---

## 🔍 Por que a Lista é adequada aqui?

A chamada da turma é um exemplo perfeito de lista porque:

- A **ordem importa** (primeiro ao último)
- O acesso é **sequencial** — chamamos do índice 0 ao 5
- Não há relações entre os alunos nesta representação; o que importa é a **posição**
- É simples e direta: ideal para registro e chamada

---

*Estrutura: Lista | Foco: Ordem e Sequência | Disciplina: Pensamento Computacional — UDF*
