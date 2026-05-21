# Avaliação da Solução Final

> Reflexão crítica sobre a eficiência e clareza da calculadora após o processo de correção.  
> Disciplina: Pensamento Computacional | Prof. Kadidja Valéria | UDF, 2026

---

## 1. Clareza

**Avaliação do grupo:**

A versão corrigida apresenta clareza satisfatória. Cada operação matemática está encapsulada em uma função própria com nome descritivo (`somar`, `subtrair`, `multiplicar`, `dividir`, `calcular_porcentagem`), o que torna o código legível mesmo para alguém que não participou do desenvolvimento.

Os comentários inseridos durante a refatoração explicam o **porquê** de cada decisão — não apenas o **o quê** foi feito. Isso está alinhado ao conceito de **Planejamento com Pseudocódigo** (Riley e Hunt, 2014): documentar o comportamento antes e durante a implementação previne que outros desenvolvedores repitam os mesmos erros.

**Ponto de melhoria identificado:** as mensagens de erro retornadas pela função `dividir()` poderiam ser padronizadas como exceções Python (`raise ValueError`) em vez de strings, o que tornaria o código mais alinhado às boas práticas da linguagem.

---

## 2. Eficiência

**Avaliação do grupo:**

A solução é eficiente para o escopo proposto. Cada função realiza exatamente uma operação (princípio da responsabilidade única), sem cálculos redundantes ou variáveis desnecessárias.

A validação de opção inválida com `continue` evita que o programa execute etapas desnecessárias (solicitar `a` e `b`) quando a entrada já é inválida — reduzindo processamento e melhorando a experiência do usuário.

A aplicação do **Gráfico de Pareto** como raciocínio de priorização (slide 11) guiou a ordem das correções: os erros de execução (divisão por zero) e de lógica matemática (porcentagem) foram tratados primeiro por terem maior impacto no resultado final, enquanto o erro estrutural (`if __name__`) foi corrigido em seguida por ser uma boa prática de escalabilidade.

---

## 3. Escalabilidade

**Avaliação do grupo:**

A arquitetura modular da calculadora — com funções independentes para cada operação — permite adicionar novas funcionalidades sem reescrever o código existente. Para incluir, por exemplo, uma operação de radiciação, basta criar uma função `radiciacao(a, b)` e adicionar uma nova opção no menu, sem alterar as funções já existentes.

A proteção `if __name__ == "__main__"` é o elemento mais crítico para a escalabilidade: ela permite que o arquivo `calculadora.py` seja importado como módulo por outros programas futuros, reutilizando suas funções sem efeitos colaterais indesejados.

**Limitação identificada:** a interface atual é exclusivamente por terminal. Uma evolução natural seria separar a lógica de cálculo (funções matemáticas) da interface com o usuário (menu e `input`), o que tornaria ainda mais fácil migrar para uma interface gráfica ou web no futuro.

---

## 4. Lição aprendida pelo grupo

O processo de identificar, corrigir e avaliar os erros revelou algo fundamental que a aula destacou desde o início: **o objetivo não é apenas encontrar se existe erro, mas qual é o erro e onde ele está.**

O erro mais difícil de detectar foi o da porcentagem (Erro 2) — exatamente porque o programa executava normalmente. Não havia mensagem de erro, não havia travamento. O resultado simplesmente estava errado. Isso demonstrou na prática por que erros lógico-matemáticos são os mais perigosos em sistemas reais: eles passam despercebidos até que alguém verifique o resultado com atenção.

A Regra de Ouro da aula ficou clara: **quanto mais cedo o erro é descoberto, menor a chance de ele se transformar em um bug letal.** Testar cada função isoladamente — antes de integrar tudo — teria revelado o erro da porcentagem na primeira execução.

Como concluiu a professora: um programador de verdade não é aquele que escreve código sem errar, mas aquele que organiza seu pensamento para **prever, testar, corrigir e melhorar** seus sistemas antes que os erros causem danos.

---

## Resumo dos erros corrigidos

| # | Erro | Tipo | Impacto | Princípio aplicado |
|---|------|------|---------|-------------------|
| 1 | Divisão por zero | Execução | Programa encerra com exceção | Ação Defensiva |
| 2 | Fórmula de porcentagem invertida | Lógico-Matemático | Resultado matematicamente falso | Prioridade Operacional |
| 3 | Validação após coleta de dados | Lógico (Conflito de Regras) | Fluxo confuso para o usuário | Filtro de Validação |
| 4 | Chamada direta de `main()` | Estrutural | Execução indesejada ao importar | Simplicidade na Solução |
