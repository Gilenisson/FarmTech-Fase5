# FarmTech Solutions – Fase 5

## Machine Learning e Computação em Nuvem

Projeto desenvolvido para a **Fase 5 do curso de Inteligência Artificial da FIAP**, utilizando técnicas de Machine Learning aplicadas à análise de dados agrícolas e estudo de infraestrutura em nuvem.

## Integrantes

- **Gilenisson Lucas Bezerra dos Santos** – RM573716
- **Gabriele Brito Rocha Menezes** – RM574145

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

# Estimativa de Custos AWS — São Paulo vs. N. Virginia

Para hospedar a API que recebe os dados dos sensores da FarmTech e executa o modelo 
de Machine Learning, utilizamos a Calculadora de Preços da AWS para simular uma 
instância EC2 com a seguinte configuração, conforme especificado no projeto:

- **2 vCPUs**
- **1 GiB de memória RAM**
- **Até 5 Gbps de rede**
- **50 GB de armazenamento (EBS)**
- **Sistema operacional Linux**
- **Modelo de precificação: On-Demand (100% de utilização mensal)**
- **Tipo de instância: t4g.micro** (família Graviton, ARM, custo-benefício superior 
  às instâncias x86 equivalentes para cargas leves como uma API de inferência)
  
### Evidência das estimativas (Calculadora AWS)

**São Paulo (sa-east-1):**
<img width="592" height="672" alt="image" src="https://github.com/user-attachments/assets/8eec3d40-e811-481a-945b-87171a1994e0" />


**N. Virginia (us-east-1):**
img width="548" height="696" alt="image" src="https://github.com/user-attachments/assets/7bc0e85c-15e5-4327-ae3a-689b5ecf1fe0" />

### Resultado comparativo

| Região                  | Custo mensal | Custo em 12 meses |
|-------------------------|:------------:|:------------------:|
| São Paulo (BR)          | US$ 17,38    | US$ 208,56          |
| N. Virginia (EUA)       | US$ 10,13    | US$ 121,56          |
| **Diferença**           | US$ 7,25/mês | **US$ 87,00/ano**   |

A região de N. Virginia apresenta um custo **~42% menor** que São Paulo para a 
mesma configuração exata de hardware. Essa diferença é esperada e documentada pela 
própria AWS: a região us-east-1 foi a primeira infraestrutura da AWS, possui a 
maior densidade de datacenters do mundo e o maior volume de clientes, o que gera 
economia de escala repassada ao preço final. Já a região sa-east-1 (São Paulo) tem 
custos operacionais mais altos (energia, importação de hardware, impostos locais) 
e menor escala, refletindo diretamente no preço da hora de instância.

Do ponto de vista puramente financeiro, portanto, N. Virginia seria a opção mais 
barata. Entretanto, como veremos a seguir, o critério de custo não é o único, nem 
o mais importante para esta decisão.


## Justificativa Técnica: Escolha da Região

Apesar do menor custo em N. Virginia, **a região escolhida para hospedar a solução 
é São Paulo (sa-east-1)**. Essa escolha é sustentada por três fatores técnicos:

### 1. Restrição legal — LGPD (Lei nº 13.709/2018)

Os dados coletados pelos sensores (umidade, temperatura, precipitação) estão 
associados a uma propriedade rural identificável e podem ser combinados com dados 
cadastrais do produtor (nome, CPF/CNPJ, localização geográfica da fazenda), 
caracterizando **dado pessoal** nos termos do Art. 5º, I da LGPD. A lei estabelece, 
no Capítulo V (Arts. 33 a 36), que a transferência internacional de dados pessoais 
só é permitida em hipóteses específicas: países com nível de proteção adequado 
reconhecido pela ANPD, uso de cláusulas contratuais padrão, selos/certificados 
específicos, ou consentimento explícito do titular para aquela finalidade.

Manter os dados na região us-east-1 (EUA) configuraria uma transferência 
internacional de dados que exigiria salvaguardas contratuais adicionais (ex.: 
Standard Contractual Clauses da própria AWS) e aumentaria a exposição da FarmTech 
a risco regulatório — incluindo multas de até 2% do faturamento (limitadas a 
R$ 50 milhões por infração, Art. 52). Hospedar em sa-east-1 elimina esse risco por 
completo, mantendo os dados sob jurisdição nacional.

### 2. Latência e acesso rápido aos dados dos sensores

A fazenda e os sensores estão fisicamente localizados no Brasil. O trajeto de rede 
entre um dispositivo IoT em território nacional e um datacenter na costa leste dos 
EUA envolve múltiplos saltos internacionais (backbone submarino), adicionando entre 
120–180 ms de latência round-trip adicional em relação a um datacenter local em 
São Paulo (tipicamente 5–20 ms). Para uma aplicação que recebe leituras de sensores 
e precisa retornar inferências de Machine Learning em tempo próximo ao real (ex.: 
alertas de rendimento de safra), essa diferença é significativa e pode comprometer 
a experiência de monitoramento contínuo, especialmente em cenários de conectividade 
rural já instável.

### 3. Análise de custo-benefício

A diferença de custo entre as duas regiões é de US$ 87,00 por ano (aproximadamente 
R$ 480, cotação de referência). Esse valor é **irrisório** frente ao risco de 
não conformidade legal (multas na casa de milhões de reais) e frente ao ganho de 
performance obtido com a menor latência. Em outras palavras: economizar US$ 7,25 
por mês não justifica o risco jurídico nem o impacto operacional de uma latência 
maior, a relação custo-risco é claramente desfavorável para a opção mais barata.

### Conclusão

Considerando os três critérios acima — conformidade legal, desempenho de acesso e viabilidade econômica —, a região **São Paulo (sa-east-1)** é a escolha tecnicamente mais adequada para a FarmTech Solutions, mesmo representando um custo ~42% maior que a alternativa em N. Virginia. Este é um exemplo prático de que a decisão de arquitetura em nuvem não deve ser guiada apenas pelo menor preço, mas por uma análise multicritério que inclua compliance regulatório e requisitos não funcionais do sistema.


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
