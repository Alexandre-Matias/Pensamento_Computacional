# Atividade - Lógica de Algoritmos

## Controle de Acesso em Sala de Aula

### 📌 Descrição do Problema

O objetivo desta atividade é desenvolver um algoritmo em pseudocódigo para controlar a entrada de alunos em uma sala de aula.

O sistema deve:

* Verificar se o aluno está na lista oficial
* Permitir entrada se estiver
* Negar entrada caso não esteja
* Repetir o processo para todos os alunos da fila

---

### 🧠 Lógica Utilizada

O algoritmo utiliza:

* Estrutura de repetição (**ENQUANTO**) para percorrer a fila
* Estrutura de decisão (**SE-SENÃO**) para validar a entrada
* Estrutura de repetição (**PARA**) para buscar o nome na lista

---

### 💻 Pseudocódigo

```text
INICIO

Definir listaOficial com os nomes:
    "Ana", "Bruno", "Carlos", "Daniela", "Eduardo"

Ler nomeAluno

ENQUANTO nomeAluno ≠ "FIM" FAÇA
    encontrado ← falso

    PARA cada nome na listaOficial FAÇA
        SE nomeAluno = nome ENTÃO
            encontrado ← verdadeiro
            PARAR
        FIMSE
    FIMPARA

    SE encontrado ENTÃO
        Exibir "Entrada PERMITIDA para " + nomeAluno
    SENÃO
        Exibir "Entrada NEGADA! Nome não encontrado."
    FIMSE

    Ler próximo nomeAluno
FIMENQUANTO

FIM
```

---

### ⚙️ Funcionamento

1. O sistema recebe o nome de um aluno
2. Verifica se ele está na lista oficial
3. Se estiver → entrada permitida
4. Se não estiver → entrada negada
5. O processo se repete até que seja digitado **"FIM"**


