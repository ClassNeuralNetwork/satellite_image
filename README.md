# Classificação de Imagens de Satélite: ResNet50 vs. EfficientNetB0

Projeto desenvolvido para a disciplina **Redes Neurais Artificiais**, como avaliação da **Unidade 2**, ministrada pela professora **Rosana Cibely**.

O objetivo é comparar duas arquiteturas de redes neurais convolucionais aplicadas à classificação de imagens de satélite, analisando seu desempenho na identificação de quatro categorias de cobertura e condições da superfície terrestre.

## Objetivo

Investigar e comparar o desempenho das arquiteturas **ResNet50** e **EfficientNetB0** na classificação de imagens de satélite. O projeto utiliza modelos pré-treinados no ImageNet por meio de *Transfer Learning* e avalia os resultados com métricas de classificação, matrizes de confusão e visualizações das previsões.

A análise busca identificar as diferenças entre os modelos nas condições experimentais adotadas, sem assumir antecipadamente que uma arquitetura é superior à outra.

## Dataset

Foi utilizado o dataset **Satellite Image Classification**, disponibilizado por Mahmoud Reda no Kaggle.

[**Acessar o dataset no Kaggle**](https://www.kaggle.com/datasets/mahmoudreda55/satellite-image-classification/code)

O conjunto possui **5.631 imagens**, distribuídas em quatro classes:

- **Cloudy** — imagens de áreas com nuvens;
- **Desert** — imagens de regiões desérticas;
- **Green area** — imagens de áreas verdes;
- **Water** — imagens de regiões com água.

As imagens apresentam diferenças de dimensão e formato de cor. Por isso, os notebooks incluem etapas de preparação e conversão para RGB, além do redimensionamento conforme a entrada exigida por cada arquitetura. O download do conjunto de dados é realizado com a biblioteca `kagglehub`.

## Modelos avaliados

### ResNet50

A **ResNet50** é uma rede neural convolucional que utiliza conexões residuais (*residual connections*) para facilitar o treinamento de redes profundas. Neste projeto, é utilizada com pesos pré-treinados no ImageNet e sem a camada de classificação original (`include_top=False`).

### EfficientNetB0

A **EfficientNetB0** é uma arquitetura que busca equilibrar desempenho e eficiência por meio do escalonamento conjunto de profundidade, largura e resolução. Assim como na ResNet50, são utilizados pesos pré-treinados no ImageNet e uma nova camada de classificação adaptada às quatro classes do dataset.

### Camadas de classificação e treinamento

Nos dois notebooks, a base convolucional pré-treinada é congelada e conectada a uma cabeça de classificação composta por:

- `GlobalAveragePooling2D`;
- camada densa com 128 neurônios e ativação ReLU;
- `Dropout(0.5)`;
- camada de saída com 4 neurônios e ativação Softmax.

A configuração de treinamento utiliza o otimizador Adam, taxa de aprendizado inicial de `0.001` e função de perda `sparse_categorical_crossentropy`. Também é utilizada parada antecipada (*Early Stopping*) para interromper o treinamento quando não há melhora na métrica monitorada, conforme a configuração do notebook.

## Notebooks

| Notebook | Arquitetura | Entrada das imagens |
|---|---|---|
| `Projeto2satelite.ipynb` | ResNet50 | 128 × 128 pixels |
| `EfficientNetB0_satelite (2).ipynb` | EfficientNetB0 | 224 × 224 pixels |

Cada notebook contém etapas de exploração do dataset, preparação das imagens, configuração e treinamento do modelo, avaliação e visualização dos resultados.

## Como os modelos serão comparados

A comparação considera diferentes aspectos do desempenho dos classificadores:

- **Acurácia no teste:** proporção de previsões corretas em relação ao total de imagens avaliadas;
- **Loss:** valor da função de perda durante o treinamento e a avaliação;
- **Precisão, recall e F1-score:** desempenho geral e desempenho individual por classe;
- **Matriz de confusão:** distribuição dos acertos e erros entre as classes;
- **Curvas de treinamento e validação:** evolução da acurácia e da perda ao longo das épocas;
- **Exemplos de predição:** comparação entre a classe real e a classe prevista, com a confiança estimada pelo modelo;
- **SHAP:** análise exploratória de regiões das imagens que contribuem para previsões selecionadas.

Os resultados devem ser interpretados considerando as configurações de cada experimento, incluindo as diferentes resoluções de entrada. A comparação também depende de garantir que os conjuntos de treinamento, validação e teste sejam independentes. Não há um vencedor definido previamente: a conclusão deve se basear nas métricas obtidas e nas condições em que os modelos foram avaliados.

## Tecnologias utilizadas

- Python
- TensorFlow / Keras
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- Pillow (PIL)
- KaggleHub
- SHAP, para explorar explicações das previsões

## Como executar

1. Abra o notebook desejado no **Google Colab** ou em um ambiente Jupyter com suporte ao TensorFlow.
2. Instale as dependências necessárias, caso ainda não estejam disponíveis no ambiente.
3. Execute as células do notebook na ordem apresentada.
4. Aguarde o download do dataset pelo `kagglehub`.
5. Execute o treinamento e as etapas de avaliação.
6. Analise os gráficos e as métricas geradas e compare os resultados dos dois modelos.

O tempo de execução pode variar de acordo com o hardware e os recursos disponíveis. O uso de GPU, quando disponível, pode ajudar a acelerar o treinamento.

## Informações acadêmicas

- **Disciplina:** Redes Neurais Artificiais
- **Avaliação:** Unidade 2
- **Professora:** Rosana Cibely
- **Tema:** comparação de arquiteturas de redes neurais convolucionais para classificação de imagens de satélite

## Contribuição

Contribuições são bem-vindas! Se você quiser contribuir para este projeto, abra uma *issue* para discutir as mudanças propostas ou envie um *pull request*.

## Equipe

<table align="center">
  <tr>
    <td align="center">
      <a href="https://github.com/franciscalorraynes">
        <img src="https://avatars.githubusercontent.com/u/104534319?v=4" width="120px;" alt="Foto de Francisca Lorrayne no GitHub"/><br>
        <sub><b>Francisca Lorrayne</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/samirafq">
        <img src="https://avatars.githubusercontent.com/u/111064435?v=4" width="120px;" alt="Foto de Samira França no GitHub"/><br>
        <sub><b>Samira França</b></sub>
      </a>
    </td>
  </tr>
</table>

<p align="center">
Cada contribuidora desempenhou um papel essencial no desenvolvimento e aprimoramento deste projeto.
</p>

---

Desenvolvido para fins acadêmicos e de estudo em aprendizado profundo.

## Licença

Este projeto está licenciado sob a licença MIT. Consulte o arquivo [LICENSE](LICENSE) para obter mais informações.
