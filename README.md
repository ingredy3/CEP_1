# 🏭 MVP — Controle Estatístico de Processo (CEP)

## 🎯 Objetivo do Projeto

Este MVP tem como objetivo **aplicar o Controle Estatístico de Processo (CEP)** em um contexto industrial real, utilizando **cartas de controle de variáveis** (X̄ e R) para monitorar a **estabilidade e variabilidade** de um processo produtivo.  

A análise foi feita sobre dados reais de manufatura, com variáveis como:
- **Temperature (°C)**  
- **Machine Speed (RPM)**  
- **Vibration Level (mm/s)**  
- **Energy Consumption (kWh)**  

A variável principal analisada foi **Temperature (°C)**, por estar diretamente relacionada ao desempenho e qualidade do processo produtivo.

---

## 🧠 Contexto do Projeto

O **Controle Estatístico de Processo (CEP)** é uma das principais ferramentas da qualidade, introduzida por **Walter Shewhart** e amplamente detalhada por **Montgomery (Capítulos 5 e 6)**.  
Ele permite distinguir entre **variações comuns (inerentes ao processo)** e **variações especiais (anomalias que exigem ação corretiva)**.

Neste estudo, foi implementado o **monitoramento do processo via cartas X̄ e R**, que indicam se o processo está **em controle estatístico**.

---

## ⚙️ Etapas do Projeto

### 📌 Passo 1 – Importação das Bibliotecas e Definição das Constantes

Foram importadas bibliotecas essenciais:
- `pandas` → manipulação dos dados  
- `numpy` → cálculos numéricos  
- `matplotlib` → visualização gráfica  

Também foram definidas **constantes de controle (d2, D3, D4)** de acordo com **Montgomery (n=20)**, fundamentais para o cálculo dos limites das cartas X̄ e R.

---

### 📌 Passo 2 – Leitura e Tratamento dos Dados

A base foi carregada diretamente do **GitHub**, contendo dados de produção industrial.  
Etapas:
- Conversão da coluna `Timestamp` para formato de data e hora  
- Seleção da variável `Temperature (°C)`  
- Agrupamento dos dados em **subgrupos racionais de tamanho n=20**  
- Cálculo da **média (X̄)** e **amplitude (R)** de cada subgrupo  

Esse agrupamento permite reduzir a variabilidade aleatória e identificar padrões de instabilidade.

---

### 📌 Passo 3 – Cálculo dos Limites Iniciais e Diagnóstico (Fase 1)

Com os subgrupos formados, foram calculados os limites iniciais:

- **Carta X̄ (Médias):**  
  \[
  UCL_X = \bar{\bar{X}} + 3 \frac{\sigma_{\hat}}{\sqrt{n}}, \quad LCL_X = \bar{\bar{X}} - 3 \frac{\sigma_{\hat}}{\sqrt{n}}
  \]

- **Carta R (Amplitudes):**  
  \[
  UCL_R = D_4 \bar{R}, \quad LCL_R = D_3 \bar{R}
  \]

Nesta etapa, foram identificados **subgrupos fora dos limites**, sinalizando **instabilidade no processo (causas especiais)**.

---

### 📌 Passo 4 – Intervenção e Recalibração dos Limites (Fase 2)

Após identificar os subgrupos instáveis na carta R, eles foram **removidos** para recalcular o **potencial do processo**.

O objetivo dessa etapa é estimar **limites mais realistas**, representando o **processo sob controle estatístico**.

Novos limites foram obtidos e aplicados em todas as observações, mostrando **redução da variabilidade e estabilidade** nas médias.

---

### 📌 Passo 5 – Visualização Completa e Foco nos Últimos Subgrupos

Foram geradas duas visualizações principais:

1. **Carta X̄ e R completa:**  
   Mostra a evolução de todos os subgrupos, destacando pontos fora de controle e limites ajustados.  
   📈 `carta_XR_n20_completa.png`

2. **Carta com foco nos últimos 100 subgrupos:**  
   Permite analisar a estabilidade recente do processo.  
   📊 `carta_XR_n20_otimizada.png`

---

## 📊 Resultados

| Indicador | Valor Inicial | Valor Após Correção |
|------------|----------------|---------------------|
| **X̄̄ (Média Global)** | 74.9894 | 74.9894 |
| **R̄ (Amplitude Média)** | 7.3925 | 7.3925 |
| **σ̂ (Estimativa via R̄)** | 2.0085 | 2.0034 |
| **UCL_X / LCL_X** | 76.3367 / 73.6421 | 76.3333 / 73.6455 |
| **UCL_R / LCL_R** | 11.7469 / 3.0757 | 11.7171 / 3.0679 |

✅ **Conclusão:**  
Após a remoção dos subgrupos fora de controle, o processo mostrou **estabilidade estatística**.  
As variações observadas são **naturais e controladas**, sem sinais de causas especiais ativas.

---

## 🧩 Ferramentas e Tecnologias Utilizadas

| Ferramenta | Função Principal |
|-------------|------------------|
| **Python 3.10+** | Linguagem principal |
| **Google Colab** | Ambiente de execução |
| **Pandas / NumPy** | Manipulação e análise de dados |
| **Matplotlib** | Visualização e plotagem das cartas |
| **GitHub** | Armazenamento e versionamento do projeto |

---

## 📘 Fundamentação Teórica

O trabalho se baseia no livro:

**MONTGOMERY, D. C.** *Introduction to Statistical Quality Control*, 7ª Edição, John Wiley & Sons, 2013.  
Capítulos 5 e 6 — *Control Charts for Variables* e *Process Capability Analysis.*

Esses capítulos explicam:
- Como construir e interpretar as cartas X̄ e R.  
- O conceito de **limites de controle** e **amostras racionais**.  
- A distinção entre **causas comuns** e **causas especiais de variação**.

---

## 🧠 Conclusão Geral

O processo analisado demonstra:
- **Estabilidade estatística** após a remoção de causas especiais.  
- **Controle adequado da variabilidade** (Carta R estável).  
- **Médias consistentes** próximas ao valor central do processo.  

Portanto, o processo está **sob controle estatístico**, apresentando **desempenho previsível** e **baixo risco de não conformidades**.

---

## 👩‍💻 Autora

**Ingredy Thamis**  
📚 MVP — Controle Estatístico de Processo (CEP)  
📅 Outubro / 2025  
🏫 Universidade [coloque o nome da sua instituição]

---

## 📜 Licença

Uso acadêmico e educativo.  
Reprodução permitida mediante citação da autora e referência à disciplina de CEP.

---

## 🌐 Repositório do Projeto

🔗 [Clique aqui para acessar o código no Google Colab](#)  
🔗 [Repositório GitHub](https://github.com/ingredy3/CEP_1)

---
