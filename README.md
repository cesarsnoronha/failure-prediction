# César Noronha - Desafio indicium lighthouse

## Outros arquivos:

- Arquivo requirements com todos os pacotes utilizados
    arquivo environment.yml
    esse arquivo pode criar um environment atraves dos comandos: 
    conda env create environment.yml
    conda activate .grupo-01-venv

- Relatório de EDA em PDF, Jupyter Notebook ou semelhante conforme passo 1
    O relatório está em 3 arquivos, esse arquivo aqui contando todo o passo-a-passo do que foi feito, o arquivo main/datasets/dataproc.ipynb contando a analise exploratória e a transformação dos dados, e o arquivo main/model/model.ipynb contendo o treinamento do modelo e a criação dos resultados

- Códigos de modelagem utilizados no passo 2.
    Esses estão no arquivo model/model.ipynb 

- Arquivo final predicted.csv conforme passo 3 acima.
    O arquivo está em main/predicted.csv

- 1 Descreva graficamente os dados disponíveis, apresentando as principais estatísticas descritivas. Comente o porquê da escolha dessas estatísticas.

    A Descrição dos dados espiníveis estão no notebook datasets/data_proc.ipynb. Inicialmente observei a distribuição das variáveis através de histogramas com o objetivo de entender se havia outliers e se os dados aparentavam ter comportamento normal. Em seguida plotei os dados em uma matriz de correlação. o objetivo ai foi observar quais variáveis estavam muito relacionadas, e assim talvez fazer alguma alteração ou excluir essa variável do estudo. Após observarmos que as variáveis de temeratura estavam correlacionadas e tinha valores de media, max e min com uma diferença bem baixa, decidi criar a variável temperature_diff. Investiguei também atraves de boxplots o comportamento de cada variável para cada tipo de falha, assim caso alguma variável tivesse algum comportamente bom distinto para algum tipo de falha eu poderia considerar essa variável essencial. Foi o que aconteceu para a variável torque e velocidade, assim mesmo elas tendo uma correlação negativa alta, decidi não excluir uma das duas. Também observei a distribuição de falhas para os extremos de algumas variáveis, sendo que para torque e velocidade foi observado um aument relativo de falhas quando estamos em Z > 3;

    Também observei através dos boxplots que a os dados com o erro random failure tem uma distribuição parecida com os No failure, e somado a descrição do escudo, decidi transformar os dados random failure em No failure, pois apenas iriam confundir o classificador sem acrescentar informação.

- 2 Explique como você faria a previsão do tipo de falha a partir dos dados. Quais variáveis e/ou suas transformações você utilizou e por quê? Qual tipo de problema estamos resolvendo (regressão, classificação)? Qual modelo melhor se aproxima dos dados e quais seus prós e contras? Qual medida de performance do modelo foi escolhida e por quê?

    Algumas das variáveis e transformações que utilizei estão na resposta para a questão acima. Também tratei valores nulos e duplicados (o que não haviam). Também normalizei os dados e e converti os tipos de variáveis. Por fim dividi os dados em treino e teste. Eu queria ter usado o método Kfold, mas não consegui separar tempo o suficiente (explicarei melhor abaixo).

    Estamos lidando com um problema de classificação.

    Os possíveis classificadores que decidi testar são: Logistic Regression, Decision Trees, Random Forest, Support Vector Machines e Neural Networks. O plano foi avaliar a performance de cada modelo através das métricas definidas na resposta da próxima questão e em seguida realizar um hyperparameter tunning para explorar todo o potencial do classificador que obtesse o melhor resultado na primeira fase de testes. Porém como apenas puder realizar o desafio no penúltimo dia para a entrega do resultado pois mudei de cidade e comecei um emprego novo no processo, tive que converter o desafio para um problema de classificação de 0 ou 1, pois não teria tempo de finalizar tudo caso tentasse o desafio por inteiro. Abaixo o passo-a-passo do que consegui fazer:

        Treinei um modelo de classificação para identificar tipos de falhas. Primeiro, separei a coluna de falhas das variáveis e criei dois dataframes (features e target). Utilizei o Label Encoder para transformar as categorias de falhas em valores numéricos. Também apliquei o SimpleImputer para preencher valores ausentes em algumas variáveis e o OrdinalEncoder para a variável 'type'. Em seguida, criei um pipeline de transformação que incluía normalização dos dados, redução de dimensionalidade (PCA) e entrada para o classificador.

        Usei a técnica de KFold para avaliar diferentes distribuições de treino e teste. Treinei vários modelos (DecisionTreeClassifier, LogisticRegression e KNeighborsClassifier) e identifiquei que o modelo 2 (que foi baseado em parâmetros de um projeto anterior) teve a melhor performance. A próxima etapa seria o tuning dos hiperparâmetros para ainda mais melhorar o desempenho do modelo.

    Eu escolhi accuracy F1-score e ROC AUC para esse extudo, pois são as que prefiro usar quando trabalho com classes desbalanceadas, mas na prátiva só utilizei a accuracy devido a falta de tempo citado no paragrafo acima.
# Predicao_de_falha
# Predicao_de_falha
# failure-prediction
