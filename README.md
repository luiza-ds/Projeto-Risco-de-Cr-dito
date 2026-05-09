# 📊 Simulação de Monte Carlo: Gestão de Risco de Crédito

## 📝 Descrição do Projeto
Este projeto utiliza a **Simulação de Monte Carlo** para prever o risco de inadimplência de uma carteira de crédito bancária. O objetivo central é calcular a **Perda Esperada** e o **Capital de Segurança (Provisionamento)** necessário para cobrir eventos inesperados, utilizando métricas regulatórias de risco bancário e conceitos de estatística computacional.

---

## 🛠️ Tecnologias e Ferramentas
*   **Linguagem:** `Python 3.x`
*   **Bibliotecas:**
    *   `Pandas`: Manipulação e estruturação da base de dados.
    *   `NumPy`: Geração de números pseudoaleatórios e cálculos de percentis (VaR).
    *   `Seaborn` & `Matplotlib`: Construção de histogramas e curvas de densidade.

---

## 🧠 Conceitos de Negócio 
O modelo foi construído seguindo os pilares fundamentais do gerenciamento de risco de crédito:

| Sigla | Conceito | Descrição |
| :--- | :--- | :--- |
| **PD** | *Probability of Default* | Probabilidade de o cliente não honrar o pagamento (baseada no Score). |
| **LGD** | *Loss Given Default* | Severidade da perda real após execução de garantias (ex: FGI). |
| **EAD** | *Exposure at Default* | O valor total que o cliente deve no momento do calote. |
| **VaR** | *Value at Risk* | Métrica que define o limite máximo de perda para um nível de confiança. |

---

## 🚀 O Motor da Simulação
O código executa um processo iterativo para transformar probabilidades estáticas em cenários de perda real:

1.  **Geração de Universos:** Simulação de `10.000` cenários distintos para a carteira.
2.  **Sorteio Aleatório:** Uso da função `np.random.rand()` para gerar um número entre 0 e 1 para cada cliente.
3.  **Lógica de Calote:** 
    ```python
    calotes = (sorteio_pd < dados['PD']).astype(int)
    ```
    *Se o número sorteado for menor que a PD, o cliente é marcado com **1** (Calote), caso contrário **0** (Pagamento).*
4.  **Agregação:** Os prejuízos são calculados e armazenados via `.append()` para construir a distribuição de perdas.

---

## 📈 Análise dos Resultados

### 📊 Distribuição de Perdas (Curva de Gauss)
A Simulação de Monte Carlo gera uma **Distribuição Normal**, que mapeia a frequência de cada valor de prejuízo simulado. 

<img width="1159" height="613" alt="COM 10 MIL SIMULAÇÕES" src="https://github.com/user-attachments/assets/f4b944d1-f904-4771-b0a6-e505312aa369" />


**Entendendo o Gráfico:**
*   **A Curva (Sino):** O topo representa os cenários de perda mais prováveis de ocorrer.
*   **Linha Laranja (Média):** Indica a **Perda Esperada**. É o valor que o banco deve provisionar no custo do produto.
*   **Linha Vermelha (VaR 95%):** Indica o limite de segurança. Em 95% dos universos simulados, a perda foi igual ou menor que este valor.

### 📋 Relatório Consolidado de Risco
Valores extraídos da simulação baseados em 10.000 iterações:

| Indicador de Risco | Valor Simulado |
| :--- | :--- |
| **Valor Total Emprestado** | R$ 1.044.999.435,00 |
| **Perda Médica Esperada** | R$ 17.709.141,52 |
| **Provisionamento (VaR 95%)** | R$ 21.007.708,01 |
| **Risco Extremo (VaR 99%)** | R$ 22.495.913,18 |
| **Pior Cenário Simulado** | R$ 25.900.315,80 |
| **Melhor Cenário Simulado** | R$ 9.968.865,40 |

---

> [!IMPORTANT]
> **Insight do Projeto:** A simulação provou que o provisionamento baseado apenas na média é insuficiente para garantir a solvência do banco. O cálculo do VaR permite que a instituição identifique o capital necessário para suportar a volatilidade e eventos de "cauda" (extremos), garantindo estabilidade financeira.

---

## 📁 Estrutura do Repositório
*   `RiscoCred.ipynb`: Notebook com a lógica de programação e visualizações.
*   `DadosClientes.xlsx`: Dataset sintético com valores de empréstimo e scores.

---

## 👤 Autor
**Ana Luiza Pires Souza da Mata**  
*Estudante de Estatística — Universidade Federal de Uberlândia (UFU)*

---
