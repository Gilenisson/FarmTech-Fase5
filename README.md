# FarmTech Solutions – Fase 5

## Machine Learning e Computação em Nuvem

Projeto desenvolvido para a **Fase 5 do curso de Inteligência Artificial da FIAP**, utilizando técnicas de Machine Learning aplicadas à análise de dados agrícolas e estudo de infraestrutura em nuvem.

## Integrantes

- **Gilenisson Lucas Bezerra dos Santos** – RM573716
- **Gabriela Brito Rocha Menezes** – RM574145

---

## 1. Machine Learning

Nesta etapa foi realizada uma análise de dados agrícolas com o objetivo de identificar padrões e desenvolver modelos capazes de prever o rendimento (`Yield`) de diferentes culturas.

### Dataset

O conjunto de dados utilizado contém **156 registros** e informações sobre quatro culturas:

- Cocoa, beans
- Oil palm fruit
- Rice, paddy
- Rubber, natural

As principais variáveis analisadas foram:

- Precipitação
- Umidade específica
- Umidade relativa
- Temperatura
- Cultura (`Crop`)
- Rendimento agrícola (`Yield`)

O arquivo utilizado está disponível na pasta `data` deste repositório:

`data/crop_yield.csv`

---

## 2. Análise Exploratória dos Dados

Durante a análise exploratória foram verificadas:

- dimensões e estrutura do dataset;
- tipos das variáveis;
- valores ausentes;
- registros duplicados;
- estatísticas descritivas;
- distribuição das culturas;
- correlação entre variáveis numéricas;
- distribuição do rendimento agrícola por cultura.

O dataset não apresentou valores ausentes ou registros duplicados.

Foram observadas diferenças significativas de rendimento entre as culturas, principalmente para **Oil palm fruit**, que apresentou rendimento médio superior às demais culturas analisadas.

---

## 3. Aprendizado Não Supervisionado – K-Means

Foi utilizado o algoritmo **K-Means** para identificar agrupamentos naturais presentes nos dados agrícolas.

Foram testadas diferentes quantidades de clusters (`k = 2` até `k = 6`) e utilizado o **Silhouette Score** como métrica de avaliação.

O melhor resultado foi obtido com:

- **k = 5**
- **Silhouette Score ≈ 0,3741**

A análise dos clusters mostrou que um dos grupos foi composto exclusivamente por registros de **Oil palm fruit**, cultura que também apresentou os maiores valores de rendimento.

---

## 4. Análise de Outliers

Para identificar possíveis valores discrepantes na variável `Yield`, foi utilizado o método do **Intervalo Interquartil (IQR)**.

A análise foi realizada separadamente para cada cultura devido às diferenças naturais de rendimento existentes entre elas.

Com o critério de 1,5 vezes o intervalo interquartil, **não foram identificados outliers de Yield dentro das culturas analisadas**.

---

## 5. Aprendizado Supervisionado

O objetivo da etapa supervisionada foi prever o rendimento agrícola (`Yield`) utilizando as características climáticas e o tipo de cultura.

Os dados foram divididos em:

- **80% para treinamento**
- **20% para teste**

A variável categórica `Crop` foi tratada utilizando **One-Hot Encoding**.

Foram avaliados cinco algoritmos de regressão:

1. Regressão Linear
2. Random Forest Regressor
3. Decision Tree Regressor
4. Gradient Boosting Regressor
5. KNN Regressor

As métricas utilizadas para avaliação foram:

- **MAE** – Mean Absolute Error
- **MSE** – Mean Squared Error
- **R²** – Coeficiente de Determinação

### Resultados

| Modelo | MAE | MSE | R² |
|---|---:|---:|---:|
| Regressão Linear | 3132,80 | 19.308.693,24 | 0,9950 |
| Random Forest | 2705,92 | 21.793.824,05 | 0,9944 |
| Decision Tree | 3404,44 | 31.495.583,69 | 0,9919 |
| Gradient Boosting | 3080,05 | 36.887.957,64 | 0,9905 |
| KNN | 61324,36 | 5.316.164.952,44 | -0,3705 |

Considerando conjuntamente as métricas avaliadas, a **Regressão Linear apresentou o melhor desempenho geral**, com o maior R² e o menor MSE entre os modelos testados.

O Random Forest também apresentou excelente desempenho e obteve o menor MAE.

O KNN apresentou desempenho significativamente inferior aos demais modelos na configuração utilizada.

---

## 6. Pontos Fortes e Limitações

O projeto combinou técnicas de aprendizado supervisionado e não supervisionado, permitindo analisar os dados agrícolas sob diferentes perspectivas.

Entretanto, o dataset possui apenas **156 registros**, o que representa uma quantidade relativamente pequena de observações para treinamento e avaliação de modelos de Machine Learning.

Além disso, existem diferenças expressivas de rendimento entre as culturas, fazendo com que a variável `Crop` tenha grande importância para a previsão de `Yield`.

Os resultados correspondem ao conjunto de treino e teste utilizado neste estudo e não garantem o mesmo desempenho quando os modelos forem aplicados a novos dados agrícolas.

---

## 7. Notebook

O desenvolvimento completo da análise, incluindo códigos, gráficos, modelos e resultados, encontra-se no notebook:

`GilenissonLucasBezerradosSantos_rm573716_pbl_fase4.ipynb`

---

## 8. Computação em Nuvem – AWS

> **Seção reservada para a análise de infraestrutura e custos em nuvem.**

Nesta etapa será apresentada a comparação de custos para hospedar a API e o banco de dados da FarmTech Solutions na AWS, considerando as regiões:

- São Paulo (sa-east-1)
- Virgínia do Norte (us-east-1)

A análise deverá considerar uma máquina Linux com configuração equivalente a:

- 2 CPUs
- 1 GiB de memória
- até 5 Gigabit de rede
- 50 GB de armazenamento

Também será apresentada a justificativa da região escolhida considerando aspectos financeiros e requisitos legais relacionados ao armazenamento dos dados.

---

## Tecnologias Utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook
- Visual Studio Code
- Git
- GitHub
- AWS

---

## Estrutura do Repositório

    FarmTech-Fase5/
    ├── data/
    │   └── crop_yield.csv
    ├── GilenissonLucasBezerradosSantos_rm573716_pbl_fase4.ipynb
    └── README.md

---

## FIAP

Projeto acadêmico desenvolvido para a **Fase 5 – FarmTech Solutions**.
