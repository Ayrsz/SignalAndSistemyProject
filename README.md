# SignalAndSistemProject
Genre reconigtion of musics, using concepts from signals and systems lessons

## 📂 Estrutura do Projeto

- **Augmentation Audios**: Módulo relacionado à aplicação de efeitos nos áudios do dataset
- **FeatureExtract**: Responsável pela extração de características do áudio e conversão dos dados para `.csv`.
- **Model**: XGBoost

## 🔍 Extração de Features

A extração é dividida em três domínios principais:

### 1️⃣ Domínio do Tempo
#### 🔹 Low-Level Features
   - **Energy**: Mede a energia total do sinal em um determinado intervalo de tempo.
   - **Zero-Cross-Rate**: Indica a taxa de cruzamentos por zero do sinal de áudio.
   - **Amplitude Envelope**: Representa a variação da amplitude ao longo do tempo.

#### 🔹 High-Level Features
   - **Tempo (ritmo)**: Determina a pulsação principal do áudio, útil para análise rítmica.

### 2️⃣ Domínio da Frequência
#### 🔹 Low-Level Features
   - **Média das Frequências Ponderadas**: Calcula a média das frequências, ponderadas pela amplitude de cada amostra em cada quadro de análise. Utiliza a Transformada Rápida de Fourier (FFT).
   - **Bandwidth**: Calcula grau de "espalhamento" do espectro de um audio para cada frame.

#### 🔹 High-Level Feature
   - **MFCC (Mel-Frequency Cepstral Coefficients)**: Extrai os coeficientes cepstrais de frequência mel, calculando estatísticas como média e desvio padrão.

### 3️⃣ Features em Imagens de Espectrogramas
Além das características extraídas diretamente dos sinais de áudio, o projeto também analisa espectrogramas para extrair descritores baseados em **Histogram of Oriented Gradients (HOG)**.

#### 🔹 Extração de HOG de Espectrogramas
O método `get_hog(spectrogram)` realiza os seguintes passos:
   1. Redimensiona a imagem do espectrograma.
   2. Calcula os **Histogram of Oriented Gradients (HOG)**.
   3. Retorna estatísticas da feature extraída.

## 🏋️ Modelo

O modelo utilizado realiza o seguinte:

### 🎲 Carregamento e vizualização  dos dados
- Utilizando pandas, carregamos o arquivo CSV e fazemos uma vizualização dos dados em tabela, o que permite entender a estrutura e as características do arquivo.
- Após isso, fazemos um tratamento para normalizar os dados, mapeando classes em números

### 🔍 Analise exploratória
- Através de gráficos, é realizada uma análise exploratória dos dados, com tempo, RMS e envelopamento médio dos gêneros sendo exibidos nos gráficos em barra;
- Após isso utilizamos uma matriz de confusão para verificar e avaliar a precisão das predições do modelo;

### 🤖 Modelagem e Avaliação  
- Prepara os dados e divide em **treino (80%)** e **teste (20%)**.  
- Treina um modelo `GradientBoostingClassifier`.  
- Avalia **precisão** e **importância das features**

## Como rodar?
- Mudança do diretório padrão, variavel com o nome "path_root" ou "new_path", substituir pelo diretório com a pasta "Data" oferecida em https://drive.google.com/drive/folders/1vxzl9tmki-r60igYsUWLxvowS1Rzasab?usp=sharing, faça uma cópia para sua pasta pessoal. Caso dê algum erro entrar em contato com mas11@cin.ufpe.br, não é necessário rodar o "Feature extract" nem o "Augmentation" pois eles já estão sintetizados nessa pasta. As visualizações necessárias já estão no Model.ipynb.

