# Classificação de Imagens de Satélite: ResNet50 vs. EfficientNetB0

Projeto desenvolvido para a disciplina **Redes Neurais Artificiais**, como avaliação da **Unidade 2**, ministrada pela professora **Rosana Cibely**.

O objetivo é comparar duas arquiteturas de redes neurais convolucionais aplicadas à classificação de imagens de satélite e analisar qual delas apresenta os melhores resultados para o problema proposto.

## 🎯 Objetivo

Investigar e comparar o desempenho das arquiteturas **ResNet50** e **EfficientNetB0** na classificação de imagens de satélite. A proposta é manter o problema e o fluxo geral de treinamento semelhantes, alterando a arquitetura utilizada, e avaliar os resultados por meio de métricas de classificação.

A conclusão será baseada nos resultados obtidos durante os experimentos, sem assumir antecipadamente que uma arquitetura é superior à outra.

## 🛰️ Dataset

Foi utilizado o dataset **Satellite Image Classification**, disponibilizado por Mahmoud Reda no Kaggle:

🔗 [Acessar o dataset no Kaggle](https://www.kaggle.com/datasets/mahmoudreda55/satellite-image-classification/code)

O conjunto de dados possui quatro classes de imagens:

- **Cloudy** — áreas com nuvens;
- **Desert** — regiões desérticas;
- **Green area** — áreas verdes;
- **Water** — regiões com água.

O download do conjunto de dados é realizado nos notebooks com a biblioteca `kagglehub`.

## 🧠 Modelos avaliados

### 1. ResNet50

A ResNet50 é uma rede neural convolucional que utiliza conexões residuais (*residual connections*) para facilitar o treinamento de redes profundas. Neste projeto, é utilizada com pesos pré-treinados no ImageNet e sem a camada de classificação original (`include_top=False`).

### 2. EfficientNetB0

A EfficientNetB0 é uma arquitetura que busca equilibrar desempenho e eficiência por meio do escalonamento de profundidade, largura e resolução. Assim como na ResNet50, são utilizados pesos pré-treinados no ImageNet e uma nova camada de classificação adaptada às quatro classes do dataset.

### Camadas de classificação

Nos dois notebooks, a base pré-treinada é congelada e conectada a uma cabeça de classificação composta por:

- `GlobalAveragePooling2D`;
- camada densa com 128 neurônios e ativação ReLU;
- `Dropout(0.5)`;
- camada de saída com 4 neurônios e ativação Softmax.

A configuração usa o otimizador Adam, taxa de aprendizado inicial de `0.001` e função de perda `sparse_categorical_crossentropy`. O treinamento também utiliza parada antecipada (*Early Stopping*).

## 📓 Notebooks

| Notebook | Arquitetura | Entrada das imagens |
|---|---|---|
| `Projeto2satelite.ipynb` | ResNet50 | 128 × 128 pixels |
| `EfficientNetB0_satelite (2).ipynb` | EfficientNetB0 | 224 × 224 pixels |

Cada notebook inclui etapas de exploração do dataset, preparação das imagens, treinamento, avaliação e visualização dos resultados.

## 📊 Como os modelos serão comparados

A análise considera as seguintes métricas e recursos:

- **Acurácia no teste:** proporção total de previsões corretas;
- **Loss:** valor da função de perda durante o treinamento e a avaliação;
- **Precisão, recall e F1-score:** desempenho geral e por classe;
- **Matriz de confusão:** classes que são mais facilmente reconhecidas ou confundidas;
- **Curvas de treinamento e validação:** comportamento da acurácia e da perda ao longo das épocas;
- **Exemplos de predição:** comparação entre a classe real e a classe prevista, acompanhada da confiança estimada pelo modelo.

Os valores finais devem ser preenchidos após executar os notebooks. Não há um vencedor definido previamente: a melhor arquitetura será aquela que apresentar resultados mais adequados considerando as métricas observadas e o comportamento no conjunto de teste.

## ⚙️ Tecnologias utilizadas

- Python
- TensorFlow / Keras
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- Pillow (PIL)
- KaggleHub
- SHAP, para explorar explicações das previsões

## ▶️ Como executar

1. Abra o notebook desejado no **Google Colab** ou em um ambiente Jupyter com suporte a TensorFlow.
2. Instale as dependências necessárias caso ainda não estejam disponíveis no ambiente.
3. Execute as células na ordem apresentada.
4. Permita que o `kagglehub` baixe o dataset.
5. Aguarde o treinamento e a avaliação.
6. Registre os resultados de cada modelo e compare as métricas e os gráficos gerados.

O treinamento pode levar algum tempo, dependendo do hardware e dos recursos disponíveis.

## 👩‍🏫 Informações acadêmicas

- **Disciplina:** Redes Neurais Artificiais
- **Avaliação:** Unidade 2
- **Professora:** Rosana Cibely
- **Tema:** comparação de arquiteturas de redes neurais para classificação de imagens de satélite

---

Desenvolvido para fins acadêmicos e de estudo em aprendizado profundo.
