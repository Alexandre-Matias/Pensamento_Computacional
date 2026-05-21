# Erros Identificados — Calculadora Matemática

> Laboratório Prático de Tratamento de Erros | Prof. Kadidja Valéria | 07/05/2026  
> Baseado em Santos (2021) e nos conceitos apresentados na aula "A Arquitetura da Resiliência"

---

## Algoritmo original (com erros)

O código abaixo é a versão **imperfeita** da calculadora, contendo erros propositais de sintaxe, lógica e execução para análise:

```python
# calculadora.py — VERSÃO COM ERROS

def somar(a, b):
    return a + b

def subtrair(a, b):
    return a - b

def multiplicar(a, b):
    return a * b

def dividir(a, b):
    return a / b                          # ERRO 1

def calcular_porcentagem(valor, percent):
    resultado = valor / percent * 100     # ERRO 2
    return resultado

def exibir_menu():
    print("=== CALCULADORA ===")
    print("1. Somar")
    print("2. Subtrair")
    print("3. Multiplicar")
    print("4. Dividir")
    print("5. Porcentagem")
    print("6. Sair")

def main():
    while True:
        exibir_menu()
        opcao = input("Escolha uma opção: ")

        if opcao == "6":
            print("Encerrando...")
            break

        a = float(input("Digite o primeiro número: "))
        b = float(input("Digite o segundo número: "))

        if opcao == "1":
            print(f"Resultado: {somar(a, b)}")
        elif opcao == "2":
            print(f"Resultado: {subtrair(a, b)}")
        elif opcao == "3":
            print(f"Resultado: {multiplicar(a, b)}")
        elif opcao == "4":
            print(f"Resultado: {dividir(a, b)}")
        elif opcao == "5":
            print(f"Resultado: {calcular_porcentagem(a, b)}")
        else:
            print("Opção inválida!")   # ERRO 3

main()                                 # ERRO 4
```

---

## Mapeamento dos Erros

---

### Erro 1 — Divisão por zero sem tratamento

**Tipo:** Execução (o programa trava em tempo real ao receber entrada inválida)  
**Localização:** `calculadora.py`, função `dividir()`, linha 12  
**Descrição:** A função realiza `a / b` sem verificar se `b` é igual a zero. Em Python, dividir qualquer número por zero lança a exceção `ZeroDivisionError`, encerrando o programa abruptamente.

**Trecho com erro:**
```python
def dividir(a, b):
    return a / b
```

**Impacto:** Se o usuário digitar 0 como segundo número na operação de divisão, o programa exibe uma mensagem de erro do Python e encerra sem aviso amigável ao usuário. Viola o princípio de **Ação Defensiva** apresentado na aula: o sistema deve prever falhas e preparar estados seguros.

---

### Erro 2 — Falha de prioridade operacional no cálculo de porcentagem

**Tipo:** Lógico-Matemático (o código executa sem travar, mas retorna resultado matematicamente falso)  
**Localização:** `calculadora.py`, função `calcular_porcentagem()`, linha 16  
**Descrição:** A fórmula correta para calcular X% de um valor é `valor * percent / 100`. O código inverte a operação: faz `valor / percent * 100`, o que produz um resultado completamente diferente e matematicamente incorreto.

**Trecho com erro:**
```python
def calcular_porcentagem(valor, percent):
    resultado = valor / percent * 100
    return resultado
```

**Exemplo do problema:**
- Esperado: 10% de 200 → `200 * 10 / 100` = **20,0**
- Obtido com o erro: `200 / 10 * 100` = **2000,0**

**Impacto:** O sistema não quebra, mas entrega um resultado numericamente falso — exatamente o tipo de **Falha de Prioridade Operacional** apresentada na aula (slide 4): o desconto é calculado com precedência errada e o resultado é matematicamente inválido.

---

### Erro 3 — Ausência de continuidade do loop após opção inválida

**Tipo:** Lógico (Conflito de Regras / comportamento inesperado do fluxo)  
**Localização:** `calculadora.py`, função `main()`, bloco `else`, linha 42  
**Descrição:** Quando o usuário digita uma opção inválida (por exemplo, a letra "A"), o programa exibe a mensagem "Opção inválida!" mas em seguida ainda solicita dois números (`a` e `b`) antes de retornar ao menu. Isso acontece porque a validação da opção ocorre **após** a coleta dos números, e o bloco `else` fica dentro do fluxo errado.

**Trecho com erro:**
```python
        a = float(input("Digite o primeiro número: "))  # executa antes de validar a opção
        b = float(input("Digite o segundo número: "))

        if opcao == "1":
            ...
        else:
            print("Opção inválida!")   # já pediu os números antes de chegar aqui
```

**Impacto:** Comportamento confuso para o usuário — ele digita uma opção inválida, mas o sistema pede números antes de informar que a opção não existe. Caracteriza um **Erro Lógico por Conflito de Regras**: o código funciona, mas a regra de negócio (validar antes de pedir dados) é violada.

---

### Erro 4 — Chamada de função fora do bloco de proteção `if __name__`

**Tipo:** Sintaxe / Estrutura (má prática que causa execução indesejada ao importar o módulo)  
**Localização:** `calculadora.py`, última linha  
**Descrição:** A função `main()` é chamada diretamente no escopo global, sem a proteção condicional `if __name__ == "__main__":`. Isso faz com que o programa seja executado automaticamente sempre que o arquivo for importado por outro módulo, comportamento indesejado em Python.

**Trecho com erro:**
```python
main()   # chamada sem proteção
```

**Impacto:** Se outro arquivo fizer `import calculadora`, o programa inicia automaticamente — causando efeitos colaterais indesejados. É uma falha estrutural que compromete a **escalabilidade** do projeto.
