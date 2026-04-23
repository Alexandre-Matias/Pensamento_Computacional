
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

