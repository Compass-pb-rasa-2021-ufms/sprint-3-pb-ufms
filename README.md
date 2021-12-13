# 🟢 Avaliação Sprint 3 - Programa de Bolsas Compass.uol e UFMS 🟢
# Acesso ao Projeto
- Para executar o notebook é necessário acessar o link [clicando aqui](https://jupyter-tensorflow-notebook-viniciusmarchi.cloud.okteto.net/notebooks/cifar10-model.ipynb). A senha de acesso é "okteto", caso exigida. 
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

Vale ressaltar que a pasta denominada "Dataset", contida neste repositório, não representa o dataset CIFAR10, pois esse é baixado e armazenado em memória apenas durante as fases de treinamento, validação e teste do modelo. A pasta "Dataset" armazena as imagens obtidas da internet pelo grupo para realizar inferências.

# Desenvolvimento
## Bibliotecas utilizadas
* [numpy](https://numpy.org/)
* [tensorflow](https://www.tensorflow.org/)
* [matplotlib](https://matplotlib.org/)
* [pymongo](https://pymongo.readthedocs.io/en/stable/)
* [gridfs](https://pymongo.readthedocs.io/en/stable/examples/gridfs.html)
* [bson](https://docs.mongodb.com/manual/reference/bson-types/)
* [Ipython](https://ipython.org/)

## Deploy no okteto
Para realizar o deploy no okteto utilizamos o catálogo disponibilizado dentro da própria plataforma, como mostra a imagem abaixo, o qual se encarrega de construir imagens pré-definidas e disponibilizar os pods já funcionando.

![okteto catalogo](Assets/okteto_catalog.png)

Deste catálogo além dos pods para o Jupyter Notebook, criamos também para o banco de dadoso Mongo. Dessa forma, ficou simples estabelecer uma entre o Jupyter e o banco de dados. 
# Problemas encontrados

## Arquivos sumindo do Okteto
O primeiro problema enfrentado por nós foi o desaparecimento dos arquivos contidos no okteto. De maneira inexplicável, de um dia para o outro, todos os arquivos contidos na pasta do okteto sumiram. Incluindo o jupyter notebook, contendo o código.
Esse comportamento se mostrou recorrente em outros deploys.

## Versão desatualizada do Tensorflow
Ao realizar o deploy do jupyter notebook diretamente do catálogo disponibilizado no okteto, como comentado, percebemos um problema. O oketo apresentou um comportamento inconsistente em relação ao versionamento do tensorflow. Em instâncias diferentes de deploy, criadas em momentos diferentes, mas no mesmo dia, o okteto apresentou versões diferentes do tensorflow. Na primeira instância obtivemos a versão 1.12.0 (versão oficial disponibilizada pelo okteto), enquanto que na segunda obtivemos a versão 1.14.0.

Além disso, consideramos que a versão 1.12.0, se encontra desatualizada, visto que o tensorflow se encontra, atualmente, na versão 2.7. Entretanto não conseguimos atualizar o tensorflow pois todas as outras libs, até mesmo o próprio python, se encontravam em versões incompatíveis com o tensorflow mais atualizado. A atualização de todo o ambiente não foi possível, sempre que tentávamos o okteto reinicializava o notebook, apenas conseguiamos atualizar libs específicas, então optamos por continuar com o tensorflow na versão 1.12. Entretanto, isso gerou dificuldades para encontrar documentos, tutoriais e libs que funcionassem sem erros com essa versão, porém isso foi contornado e não influenciou no desenvolvimento.

O problema mais grave encontrado foi um comportamento inesperado de *não* convergência do modelo. Utilizamos como base a documentação do tensorflow para construir o modelo capaz de resolver o problema de classificação apresentado pelo dataset CIFAR10, entretanto obtemos um erro, uma função, descrita pela documentação, ainda não existia, devido a versão desatualizada, como mostra a figura abaixo:

Como mostra a figura: 

![erro de loss](Assets/tf_version_loss_error.png)

Então, buscando por versões anteriores da documentação, encontramos a maneira correta para a versão 1.12, como mostra a figura abaixo:

![loss na versão 1.12](Assets/tf_loss_1-12_version.png)

Nesse momento, o comportamento inesperado de não convergência aconteceu. O modelo deixou de convergir. Inexplicavelmente, permanecendo durante 10 épocas de treinamento com o *exato* mesmo valor de loss e accuracy, como se não estivesse sendo otimizado de fato. Esse comportamento inesperado não lançou nenhum erro por parte do tensorflow, o que dificultou a compreensão da situação, então, simplesmente realizando outro deploy de jupyter notebook, o erro foi corrigido, entretanto ele foi observado em outros momentos.

Não sabemos o que causou esse comportamento, mas conseguimos resolvê-lo apenas recriando a instância do jupyter notebook, assim conseguindo treinar o modelo normalmente.

## Erro ao utilizar Pickle
Na versão 1.12 não foi possivel utilizar a lib Pickle para serializariar o arquivo que representa o modelo gerado pelo tensorflow, a fim de tornar possível sua inserção no banco de dados.

![erro ao utilizar pickle](Assets/error_numpy.png)

Esse erro foi encontrado em issues no repositório do Tensorflow, por isso optamos por utilizar outra lib para realizar esse processo, o GridFS.

## Erro de conexão e reinicialização do notebook
Por fim, um erro não relacionado ao código, mas a plataforma em si, que causou empecilhos, foi o erro de conexão do okteto. Esporadicamente (até mesmo no meio do treinamento do modelo) o oketo enviava uma mensagem de erro informando que aconteceram problemas no kernel, como mostra a figura abaixo:

![notebook error](Assets/notebook_error.png)

Esse erro precedia a desconexão completa do jupyter notebook, o qual ficava inoperante, como mostra a figura abaixo. 

![jupyter desconectado](Assets/notebook_not_connected.png)

Essa desconexão causava a perda de todas as variáveis instanciadas e seus valores armazenados em memória, o que exigia a completa reexecução do notebook. Em outras palavras, precisamos executar novamente todas as células, inclusive a que treinava o modelo, caso esse erro tivesse acontecido durante seu treinamento, antes que o mesmo finalizasse para que pudéssemos salvar o modelo em disco.

Além disso, a construção de código de modo colaborativo
de maneira simultânea era impossibilitado, pois quando um integrante do grupo alterava o jupyter notebook, os demais recebiam o aviso exibido pela figura abaixo. O qual, caso acontecesse muitas vezes, também gerava uma reinicialização do notebook. Esse problema em questão não afetou o desenvolvimento pois é facilmente contornado, mas é uma questão interessante, por isso foi descrita nesse documento.

![notebook alterado](Assets/notebook_changed.png)

## Desenvolvido por 
- 👩‍💻 Anália Beatriz
- 👨‍💻 Leonardo Oliveira
- 👨‍💻 Vinicius Marchi 

---
