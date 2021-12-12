# 🟢 Avaliação Sprint 3 - Programa de Bolsas Compass.uol e UFMS 🟢
## Avaliação da terceira sprint do programa de bolsas Compass.uol para formação em chatbot Rasa.
---
# Acesso ao Projeto
- Para executar o notebook é necessário acessar o link [clicando aqui](https://jupyter-tf-test-tensorflow-notebook-viniciusmarchi.cloud.okteto.net/tree?)
Você encontrará uma pasta chamada "Dataset" onde está armazenado todas as imagens que usamos e junto com ela o arquivo .ipynb, sendo ele nosso notebook contendo todo o projeto da rede convulacional.
---
## DataSet
 O dataset escolhido foi o [CIFAR10](https://www.tensorflow.org/tutorials/images/cnn) que consiste em uma rede convulacional que reconhece padrões diversos em imagens, baseado nas seguintes classes: 
  * Avião (airplane)
  * Automovel (automobile)
  * Cachorro (dog)
  * Caminhão (truck) 
  * Cavalo (horse)
  * Cervo (deer)
  * Gato (cat)
  * Navio (ship)
  * Passáro (bird)
  * Sapo (frog)

---

# Desenvolvimento


# Problemas encontrados


## Bug do okteto, arquivos sumindo
O primeiro problema enfretado por nós foi o desaparecimento dos arquivos do okteto. De um dia para o outro todos os arquivos contidos na pasta sumirám, includindo o jupyter notebook.
Onde tudo funcionava com corretude. Haviam outros jupyter notebooks implantados no okteto, todos sumiram.

## Versão do tensorflow disponível
O oketo apresentou um comportamento inconsistente em relação ao versionamento do tensorflow. Em instâncias diferentes de deploy, criadas em um intervalo de tempo de 10 minutos, o okteto apresentou versões diferentes do tensorflow. Na primeira instância obtivemos a versão 1.12.0, enquanto que na segunda obtivemos a versão 1.14.0.

A versão 1.12.0 apresentou problemas de convergencia. Utilizamos como base a documentação do tensorflow para construir o modelo capaz de resolver o problema de classificação apresentado pelo dataset CIFAR10.

Como mostra a figura ![erro de loss](Assets/tf_version_loss_error.png)

A documentação do tensorflow se encontra na versão 2.x e os documentos e tutorais apresentados seguem essa versão. Então, tivemos que buscar alterativas para conseguir rodar esse modelo.

Realizando no histórico de documentação, encontramos no github a maneira como a loss era definida no modelo na versão 1.12, e realizamos essa alteração, como mostra a figura abaixo

![loss na versão 1.12](Assets/tf_loss_1-12_version.png)


Nesse momento


## Desenvolvido por 
- 👩‍💻 Anália Beatriz
- 👨‍💻 Leonardo Oliveira
- 👨‍💻 Vinicius Marchi 

---
