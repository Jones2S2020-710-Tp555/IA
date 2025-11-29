# Detecção Não Supervisionada de Anomalias em Telemetria LEO com LSTM-AE e VAE

Este repositório contém os códigos, notebooks e figuras do artigo:

> **“Análise Comparativa entre Autoencoders Recorrentes baseados em LSTM e Autoencoders Variacionais (VAE) na Detecção Não Supervisionada de Anomalias em Séries Temporais de Telemetria de Satélites LEO”**  
> Autor: *Jones Márcio Nambundo (UNIFEI)*

O objetivo é comparar duas arquiteturas de aprendizado profundo baseadas em reconstrução:

- **LSTM Autoencoder (LSTM-AE)**  
- **Variational Autoencoder (VAE)**  

Aplicadas à detecção **não supervisionada** de anomalias em séries temporais de telemetria de satélites em órbita baixa (LEO), utilizando dados reais da missão **OPS-SAT / OPSSAT-AD (ESA)**.

---

## 1. Visão geral da metodologia

A pipeline implementada segue os passos:

1. **Carregamento da telemetria** de um arquivo `segments.csv` (OPS-SAT).
2. **Pré-processamento**:
   - filtro por canal e rótulos `train` / `anomaly`;
   - seleção apenas de dados normais para treino (`train = 1`, `anomaly = 0`);
   - normalização do valor de telemetria com `StandardScaler`.
3. **Janelamento deslizante** com tamanho fixo `w = 60` amostras:
   - geração de `X_train` (dados normais);
   - geração de `X_test` e rótulos de janela `y` (janela é anômala se alguma amostra tiver `anomaly = 1`).
4. **Treinamento dos modelos**:
   - **LSTM-AE** com duas camadas LSTM no encoder e duas no decoder;
   - **VAE** recorrente com espaço latente Gaussiano e regularização KL.
5. **Cálculo do erro de reconstrução (MSE)** por janela e busca de um **limiar ótimo** baseado nos quantis do MSE de treino.
6. **Avaliação e comparação**:
   - F1-score, precisão, recall;
   - AUC-ROC (Área sob a Curva Receiver Operating Characteristic);
   - AUC-PR (Área sob a Curva Precision–Recall);
   - MSE médio por classe (normal vs anômalo);
   - figuras de ROC, Precision–Recall e histogramas do MSE.

---

## Como Rodar com Google Colab
. Faça o download dos seguintes arquivos:
- dataset.csv
- segments.csv
- Código do modelo (arquivo .ipynb ou .py)

## Como Rodar com Google Colab
Acesse : https://colab.research.google.com/

## Envie o Dataset e Segments para o Colab
icone 🗂️ "Files" → Upload → selecione dataset.csv e segments.csv

## Execute o código
Clique em Runtime → Run all
ou execute célula por célula até o final.

