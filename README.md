# 🔬 Diagnóstico de Melanomas: Segmentação e Extração de Atributos (Regra ABCD)

## 📌 Sobre o Projeto
Este projeto é o trabalho final da disciplina **ES235 - Processamento de Imagem**, do Departamento de Engenharia Biomédica da Universidade Federal de Pernambuco (UFPE). 

O objetivo principal é desenvolver um pipeline completo de processamento de imagens dermatoscópicas para **estimar a malignidade de lesões de pele**. O fluxo consiste em pré-processar as imagens, segmentar a Região de Interesse (ROI) e extrair características baseadas na **regra clínica ABCD** (Assimetria, Borda, Cor e Diâmetro).

## 🗂️ Dataset Utilizado
Os dados utilizados pertencem ao dataset do **ISIC 2017** (*Skin Lesion Analysis Towards Melanoma Detection*). 
* Cada grupo trabalhará com um subconjunto específico de **50 imagens** do conjunto de treinamento.
* O dataset inclui: a imagem original (RGB), a máscara binária de segmentação (*Ground Truth*) e o diagnóstico clínico real (Benigno/Maligno).

## 🛠️ Etapas de Desenvolvimento

O desafio técnico é dividido em duas grandes etapas:

### 1. Segmentação
Implementação de algoritmos (como Limiarização de Otsu, Crescimento de Regiões, Watershed, etc.) para isolar a lesão da pele saudável. É fortemente recomendado explorar o espaço de cores das imagens para contornar desafios como a presença de pelos e variações de iluminação.

### 2. Extração de Características (Regra ABCD)
A partir da máscara gerada na segmentação, o algoritmo deve extrair os seguintes atributos e calcular o **TDS (*Total Dermatoscopy Score*)**:
* **A (Assimetria):** Grau de assimetria da lesão em relação aos seus eixos principais.
* **B (Borda):** Irregularidade da borda (ex: índice de compacticidade, gradiente radial).
* **C (Cor):** Variância de cores e presença de matizes suspeitos (vermelho, branco, marrom, azul-acinzentado, preto).
* **D (Diâmetro):** Diâmetro relativo ou maior extensão da lesão (em pixels).

**Cálculo do Score Final (Fórmula de Stolz):**
> `TDS = 1.3 * A + 0.1 * B + 0.5 * C + 0.5 * D`

## 📊 Métricas de Avaliação

O desempenho do sistema será avaliado em duas frentes:

* **Qualidade da Segmentação:** Comparação das máscaras geradas pelo algoritmo com as máscaras padrão-ouro (*Ground Truth*) usando os índices de **Dice** e **IoU** (*Intersection over Union*).
* **Qualidade da Classificação:** Definição de um limiar (*threshold*) no valor do TDS para classificar a lesão como "Suspeita" (Maligna) ou "Não Suspeita". O resultado será avaliado calculando-se a **Sensibilidade**, **Especificidade** e **Acurácia**.