# Criatura lendária: Tiamat

**Projeto final da disciplina ATP-203 — Aprendizado de Máquina**

**Autor(es):** Angelo Quadros Zampieri
**Instituição:** Ilum Escola de Ciência  
**Professor:** Daniel R. Cassar

## Sobre o trabalho

Este repositório contém um estudo de **classificação binária** para prever se um cliente de um banco português
aderirá a um **depósito a prazo** após uma ligação de telemarketing, usando o conjunto de dados real
*Bank Marketing* (`bank-additional-full`, UCI; Moro, Cortez e Rita, 2014).

O problema é fortemente desbalanceado (~11% de adesões). O trabalho:

- faz uma análise exploratória (apenas no conjunto de treino);
- remove o atributo `duration`, que só é conhecido depois da ligação (vazamento de informação do futuro);
- divide os dados em treino e teste **agrupando exemplos idênticos**, para evitar vazamento por dados redundantes;
- treina um **baseline** e compara **5 algoritmos/pipelines** (regressão logística, k-NN, árvore de decisão,
  floresta aleatória e gradient boosting), cada um com **100 tentativas de otimização no `optuna`** e validação
  cruzada estratificada e agrupada;
- deixa o `optuna` controlar também o **pré-processamento** (tipo de normalizador e uso de PCA);
- avalia o modelo escolhido no teste (AP, AUC-ROC, limiar de decisão, curva de ganho) e o explica com
  **importância por permutação** e **gráficos de dependência parcial**.

A narrativa do notebook usa a lore da disciplina: cada algoritmo é uma das cinco cabeças de Tiamat.

## Estrutura do repositório

```
tiamat.ipynb          # relatório científico: todo o trabalho, de cima para baixo
bank-additional-full.csv   # conjunto de dados (UCI Bank Marketing)
estudos_optuna/       # estudos do optuna (.db), criados ao rodar o notebook
requirements.txt      # dependências
.gitignore
README.md
```

## Como reproduzir

1. Crie um ambiente e instale as dependências:

   ```bash
   python -m venv .venv
   source .venv/bin/activate        # no Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. Abra o notebook e execute **todas as células, de cima para baixo**:

   ```bash
   tiamat.ipynb

   ```

> **Tempo de execução:** 5 algoritmos x 100 tentativas x validação cruzada de 5 folds leva de dezenas de minutos
> a algumas horas, dependendo do computador. Os estudos ficam salvos em `estudos_optuna/`; se o notebook for
> reexecutado, as tentativas já feitas são reaproveitadas (só rodam as que faltam para completar 100).
> Para um teste rápido, altere `NUM_TENTATIVAS` (seção 2 do notebook) para um valor pequeno e apague
> a pasta `estudos_optuna/` depois.

## Dados e referências principais

- Moro, S.; Cortez, P.; Rita, P. *A data-driven approach to predict the success of bank telemarketing.*
  Decision Support Systems, 62:22-31, 2014.
- UCI Machine Learning Repository, *Bank Marketing*: https://archive.ics.uci.edu/dataset/222/bank+marketing

A lista completa de referências está na seção 15 do notebook.

## Uso de IA

O uso de ferramentas de IA neste trabalho está descrito na seção 14 do notebook.

