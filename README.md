#  :red_circle: Acesso ao app
- https://jupyter-tensorflow-notebook-danielyudicarvalho.cloud.okteto.net/notebooks/notebook.ipynb

#  :floppy_disk: Dataset: IMDB
- https://ai.stanford.edu/~amaas/data/sentiment/aclImdb_v1.tar.gz
# :page_with_curl: Justificativa pro dataset
  O grupo definiu que seria feito um classificador de texto, ao invés de imagem, para treinar e se aprofundar em processamento de linguagens naturais.
  Para isso, foi escolhido o dataset da IMBD de reviews para filmes, que já vem com labels. A versão em inglês foi utilizada, visto que em português não conseguimos achar um dataset compativel com nossas necessidades.
# :desktop_computer: Modelo de treinamneto
  Nosso treinamento foi baseado no classificador basico disponivel na documentação do tensorflow [text_classification](https://www.tensorflow.org/tutorials/keras/text_classification)
# :warning: Dificuldades

  A principal dificuldade encontrada pela equipe foi a utilização do notebook no okteto. Isso ocorreu pelo fato do okteto ter disponivel apenas a versão 0.1.3 do tensorflow. Isso significa que, ao tentar rodar as células do notebook, algumas funções não funcionam, como por exemplo : "text_dataset_from_directory". Essa função em especifico é essencial para nossa aplicação e ela só está disponivel em versões mais recentes do tensorflow.
  Para contornar esse problema, foi utilizado o google colab para rodar e testar nossa aplicação, os resultados podem ser encontrados no [colab](https://colab.research.google.com/drive/1huB00Utn_S0ET7Dzhi4tyswl0PfTWUkN?usp=sharing)

# :busts_in_silhouette: Integrantes do grupo
- Daniel Yudi Carvalho
- Filipe Camuso Fernandez
- João Paulo de Souza Wakugawa

# :chart_with_upwards_trend: Desenvolvimento da aplicação
Foi desenvolvida uma rede neural capaz de aprender a classificar o sentimento descrito num texto como bom, regular ou ruim, a partir do dataset IMDB, no qual possui 50,000 reviews de filmes, onde metade foram utilizadas para teste e a outra metade para treinar o modelo.

<img title="Modelo PLN 1" alt="Alt text" src="/images/modeloPLN.png">
<img title="Modelo PLN 2" alt="Alt text" src="/images/modeloPLN2.png">


## :pushpin: Links
- https://trello.com/b/ylcfHqPg/pb-rasa-2021-sprint-3

# :books: Tecnologias e dependências
- <a href="https://docs.python.org/3/">Python</a>
- <a href="https://docs.mongodb.com/">MongoDB</a>
- <a href="https://okteto.com/docs/reference/manifest/">Okteto</a>
- <a href="https://www.tensorflow.org/">Tensorflow</a>
- <a href="https://keras.io/">Keras</a>
- <a href="https://pymongo.readthedocs.io/en/stable/index.html">Pymongo</a>
- <a href="https://jupyter.org/">Jupyter Notebook</a>
- <a href="https://www.docker.com/">Docker</a>
- <a href="https://colab.research.google.com/notebooks/welcome.ipynb?hl=pt_BR">Google Colab</a>
