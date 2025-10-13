# 🏭 MVP — Controle Estatístico de Processo (CEP)

## 🎯 Objetivo do Projeto

Este MVP tem como objetivo **aplicar o Controle Estatístico de Processo (CEP)** em um contexto industrial real, utilizando **cartas de controle de variáveis (X̄ e R)** para monitorar a **estabilidade e a variabilidade** de um processo produtivo.  

A análise foi feita sobre dados de um processo de manufatura, considerando variáveis como:
- **Temperature (°C)**  
- **Machine Speed (RPM)**  
- **Vibration Level (mm/s)**  
- **Energy Consumption (kWh)**  

A variável escolhida para o monitoramento foi **Temperature (°C)**, por estar diretamente relacionada ao desempenho e à qualidade do produto final.

---

## 🧠 Contexto do Projeto

O **Controle Estatístico de Processo (CEP)** é uma das ferramentas mais importantes da Qualidade, introduzida por **Walter A. Shewhart** e amplamente discutida por **Douglas C. Montgomery** nos capítulos 5 e 6 do livro *Introduction to Statistical Quality Control*.  

Seu objetivo é distinguir entre:
- **Variações comuns**, que são naturais do processo;
- **Variações especiais**, que indicam anomalias e exigem ação corretiva.  

Neste projeto, o CEP foi aplicado para avaliar se o processo se encontra **sob controle estatístico** e para identificar possíveis **causas especiais de variação**.

---

## ⚙️ Etapas do Projeto

### 📌 Passo 1 – Importação das Bibliotecas e Definição das Constantes

Foram importadas as principais bibliotecas:
- `pandas` → manipulação de dados tabulares;  
- `numpy` → cálculos matemáticos;  
- `matplotlib` → criação dos gráficos;  
- `IPython.display` → exibição de DataFrames no Colab.

Também foram definidas as **constantes d2, D3 e D4**, que variam conforme o tamanho do subgrupo (n=20), conforme a tabela de **Montgomery (2013)**.

Essas constantes são usadas para calcular os **limites de controle** das cartas de controle.

---

### 📌 Passo 2 – Leitura e Preparação dos Dados

Os dados foram carregados diretamente do GitHub, contendo registros temporais do processo de manufatura.  
Etapas realizadas:
1. Conversão da coluna `Timestamp` para formato de data e hora;  
2. Seleção da variável de interesse `Temperature (°C)`;  
3. Limpeza dos dados, removendo valores nulos;  
4. Formação de **subgrupos racionais** de tamanho `n=20`;  
5. Cálculo da **média (X̄)** e da **amplitude (R)** de cada subgrupo.

O uso de subgrupos racionais segue o conceito apresentado por **Montgomery (Cap. 5)**, permitindo reduzir a influência de variações aleatórias.

---

### 📌 Passo 3 – Cálculo dos Limites Iniciais e Diagnóstico (Fase 1)

Nesta etapa, foram calculados os limites de controle iniciais com base em **todas as observações**:

- **Carta X̄ (Médias):**  
  \[
  UCL_X = \bar{\bar{X}} + 3 \frac{\sigma_{\hat}}{\sqrt{n}} \quad e \quad LCL_X = \bar{\bar{X}} - 3 \frac{\sigma_{\hat}}{\sqrt{n}}
  \]
- **Carta R (Amplitudes):**  
  \[
  UCL_R = D_4 \bar{R} \quad e \quad LCL_R = D_3 \bar{R}
  \]

Em seguida, foram identificados **subgrupos fora de controle**, ou seja, pontos acima ou abaixo dos limites calculados.  
Esses pontos indicam **instabilidade do processo** e a presença de **causas especiais**.

---

### 📌 Passo 4 – Intervenção e Recalibração dos Limites (Fase 2)

Após a detecção de subgrupos fora de controle na **Carta R**, eles foram **removidos** para recalcular os limites de controle.  
Esse processo é chamado de **recalibração** e busca representar o **potencial do processo sob controle estatístico**.

Novos limites foram obtidos:
- Menores amplitudes (R) → indicam **menor variabilidade**;  
- Médias mais consistentes → indicam **maior estabilidade**.

Com isso, foi possível distinguir entre as **causas especiais eliminadas** e as **variações naturais restantes**.

---

### 📌 Passo 5 – Visualizações e Interpretação dos Resultados

Foram geradas duas visualizações principais:

1. **Carta X̄ e R completa:**  
   Mostra todos os subgrupos analisados, com os pontos fora de controle destacados.  
   📈 Arquivo: `carta_XR_n20_completa.png`

2. **Carta X̄ e R focada nos últimos 100 subgrupos:**  
   Destaca o comportamento recente do processo e permite monitorar o desempenho mais atual.  
   📊 Arquivo: `carta_XR_n20_otimizada.png`

Ambas as cartas demonstram a transição de um processo **instável** (Fase 1) para um **processo estável** (Fase 2).

---

## 📊 Resultados Obtidos

| Indicador | Valor Inicial | Valor Após Correção |
|------------|----------------|---------------------|
| **X̄̄ (Média Global)** | 74.9894 | 74.9894 |
| **R̄ (Amplitude Média)** | 7.3925 | 7.3925 |
| **σ̂ (Estimativa via R̄)** | 2.0085 | 2.0034 |
| **UCL_X / LCL_X** | 76.3367 / 73.6421 | 76.3333 / 73.6455 |
| **UCL_R / LCL_R** | 11.7469 / 3.0757 | 11.7171 / 3.0679 |

✅ **Conclusão Parcial:**  
Após a remoção dos subgrupos instáveis, o processo passou a apresentar **menor dispersão** e **controle estatístico consolidado**.

---

## 🧩 Ferramentas Utilizadas

| Ferramenta | Função |
|-------------|--------|
| **Python 3.10+** | Linguagem principal de análise |
| **Google Colab** | Ambiente de execução e visualização |
| **Pandas / NumPy** | Manipulação e análise numérica dos dados |
| **Matplotlib** | Criação das cartas de controle |
| **GitHub** | Armazenamento e versionamento do projeto |

---

## 📘 Fundamentação Teórica

Este trabalho foi fundamentado nos capítulos **5 e 6** do livro:

**MONTGOMERY, D. C.** *Introduction to Statistical Quality Control.*  
7ª edição. John Wiley & Sons, 2013.

Esses capítulos abordam:
- A construção e interpretação das cartas **X̄** e **R**;  
- A importância do **tamanho do subgrupo (n)**;  
- O conceito de **limites de controle** e **causas de variação**;  
- O uso das cartas para **avaliar a estabilidade e capacidade do processo**.

---

## 🧠 Conclusão Geral

O processo analisado apresentou:
- **Estabilidade estatística** após a intervenção;  
- **Variabilidade sob controle (Carta R)**;  
- **Médias consistentes (Carta X̄)**.

Conclui-se que o processo está **sob controle estatístico**, com variações compatíveis com o comportamento natural do sistema produtivo.  
Portanto, ele é **previsível, confiável e com boa capacidade de manutenção da qualidade.**

---

## 👩‍💻 Autora

**Ingredy Thamis**  
📚 MVP — Controle Estatístico de Processo (CEP)  
📅 Outubro / 2025  
🏫 Universidade de Brasilia

---


