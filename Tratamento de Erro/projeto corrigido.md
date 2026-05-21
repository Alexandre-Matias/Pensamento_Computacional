# Projeto Corrigido — Calculadora Matemática

> Versão refatorada com justificativas técnicas para cada alteração realizada.  
> Disciplina: Pensamento Computacional | Prof. Kadidja Valéria | UDF, 2026

---

## Código corrigido completo

```python
# calculadora.py — VERSÃO CORRIGIDA

def somar(a, b):
    return a + b

def subtrair(a, b):
    return a - b

def multiplicar(a, b):
    return a * b

def dividir(a, b):
    # Correção 1: verificação defensiva antes de executar a divisão
    if b == 0:
        return "Erro: divisão por zero não é permitida."
    return a / b

def calcular_porcentagem(valor, percent):
    # Correção 2: fórmula corrigida para precedência matemática adequada
    resultado = valor * percent / 100
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

        # Correção 3: validação da opção ANTES de solicitar os números
        if opcao not in ["1", "2", "3", "4", "5"]:
            print("Opção inválida! Por favor, escolha entre 1 e 6.")
            continue

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

# Correção 4: proteção do ponto de entrada com if __name__
if __name__ == "__main__":
    main()
```

---

## Justificativas técnicas por correção

---

### Correção 1 — Tratamento da divisão por zero

**O que foi alterado:**  
Adicionada uma pré-condição dentro da função `dividir()` que verifica se o divisor (`b`) é igual a zero antes de executar a operação. Se for, a função retorna uma mensagem de erro amigável em vez de lançar uma exceção.

**Antes:**
```python
def dividir(a, b):
    return a / b
```

**Depois:**
```python
def dividir(a, b):
    if b == 0:
        return "Erro: divisão por zero não é permitida."
    return a / b
```

**Justificativa técnica:**  
Esta correção aplica o princípio de **Ação Defensiva** apresentado na aula: "Divisão por zero? Crie uma pré-condição para impedir." O sistema não deve esperar o erro acontecer — ele deve antecipar a falha e preparar um estado seguro. Ao retornar uma mensagem ao invés de deixar o Python lançar `ZeroDivisionError`, o programa mantém o controle do fluxo e oferece uma experiência segura e compreensível ao usuário.

---

### Correção 2 — Fórmula de porcentagem com precedência correta

**O que foi alterado:**  
A fórmula de cálculo de porcentagem foi reescrita para respeitar a precedência matemática correta: `valor * percent / 100`.

**Antes:**
```python
def calcular_porcentagem(valor, percent):
    resultado = valor / percent * 100
    return resultado
```

**Depois:**
```python
def calcular_porcentagem(valor, percent):
    resultado = valor * percent / 100
    return resultado
```

**Justificativa técnica:**  
Este erro corresponde exatamente ao exemplo de **Falha de Prioridade Operacional** exibido na aula (slide 4): a operação era executada na ordem errada, produzindo resultado matematicamente falso sem que o sistema quebrasse. A lição é que erros lógico-matemáticos são os mais perigosos precisamente porque o código executa normalmente — o problema só aparece ao verificar o resultado. A correção exige conhecimento da fórmula correta e atenção à precedência dos operadores.

---

### Correção 3 — Validação da opção antes da coleta de dados

**O que foi alterado:**  
A verificação de opção inválida foi movida para **antes** da solicitação dos números `a` e `b`. Quando a opção não é reconhecida, o programa exibe uma mensagem e usa `continue` para reiniciar o loop sem pedir dados desnecessários.

**Antes:**
```python
        a = float(input("Digite o primeiro número: "))
        b = float(input("Digite o segundo número: "))

        if opcao == "1":
            ...
        else:
            print("Opção inválida!")
```

**Depois:**
```python
        if opcao not in ["1", "2", "3", "4", "5"]:
            print("Opção inválida! Por favor, escolha entre 1 e 6.")
            continue

        a = float(input("Digite o primeiro número: "))
        b = float(input("Digite o segundo número: "))
```

**Justificativa técnica:**  
Este é um caso de **Erro Lógico por Conflito de Regras** (slide 4): o código funcionava, mas a regra de negócio era violada — o sistema pedia informações antes de verificar se a opção era válida. A correção aplica o princípio do **Filtro de Validação** (slide 7): verificar o tipo e formato dos dados antes de processá-los. O uso de `continue` garante que o fluxo retorne ao início do loop de forma limpa.

---

### Correção 4 — Proteção do ponto de entrada com `if __name__`

**O que foi alterado:**  
A chamada direta `main()` foi substituída pela estrutura condicional padrão do Python `if __name__ == "__main__": main()`.

**Antes:**
```python
main()
```

**Depois:**
```python
if __name__ == "__main__":
    main()
```

**Justificativa técnica:**  
Em Python, quando um arquivo é executado diretamente, a variável `__name__` recebe o valor `"__main__"`. Quando o mesmo arquivo é importado por outro módulo, `__name__` recebe o nome do arquivo — e a condição falha, impedindo a execução automática. Sem essa proteção, qualquer módulo que importasse `calculadora.py` iniciaria o programa interativo inadvertidamente. Esta correção está alinhada ao princípio de **Simplicidade na Solução** (Ferragina e Luccio, 2018): soluções simples e bem estruturadas geram inerentemente menos espaço para erros ocultos.
