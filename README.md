# Criação de Uma Base de Dados e Treinamento da Rede YOLO

Este repositório descreve o processo de criação de uma base de dados e treinamento de uma rede YOLO (You Only Look Once) para detecção de objetos em imagens. A YOLO é uma rede neural convolucional (CNN) de última geração, capaz de realizar detecção de objetos em tempo real.

## Objetivo

O objetivo deste projeto é criar uma base de dados personalizada e treinar a rede YOLO para detectar e classificar objetos nas imagens. A YOLO realiza a detecção de múltiplos objetos em uma imagem ao mesmo tempo, fornecendo resultados rápidos e precisos.

## Requisitos

Antes de começar, você precisa ter os seguintes pré-requisitos:

- Python 3.x
- Biblioteca OpenCV
- TensorFlow ou PyTorch (dependendo da implementação YOLO utilizada)
- Biblioteca de manipulação de arquivos (ex: os, shutil)
- Ferramenta para anotação de imagens (ex: LabelImg)
- Modelos YOLO pré-treinados ou configuração personalizada para treinamento

## Passos para a Criação da Base de Dados e Treinamento da Rede YOLO

### 1. Criação e Anotação da Base de Dados

Primeiro, você precisa coletar um conjunto de imagens que contenham os objetos que você deseja detectar. Essas imagens podem ser coletadas manualmente ou obtidas de fontes públicas.

#### 1.1. Ferramentas para Anotação

Use ferramentas como **LabelImg** para criar as **bounding boxes** (caixas delimitadoras) ao redor dos objetos nas imagens. Cada objeto será rotulado com uma classe específica. Exemplo de classes: `carro`, `pessoa`, `cachorro`.

- Instale o LabelImg:
  ```bash
  pip install labelImg

1.2. Salvamento das Anotações

Cada anotação gerada será salva como um arquivo XML (formato Pascal VOC) ou como um arquivo TXT (formato YOLO), dependendo da configuração escolhida. Cada linha nos arquivos de anotações deve ter o seguinte formato:

<class_id> <x_center> <y_center> <width> <height>

Onde:

    <class_id> é o índice da classe do objeto (começando de 0).
    <x_center> e <y_center> são as coordenadas do centro da caixa normalizadas entre 0 e 1.
    <width> e <height> são a largura e altura da caixa normalizadas entre 0 e 1.

1.3. Organizando as Imagens e Anotações

Organize as imagens e anotações da seguinte maneira:

dataset/
  ├── images/
  │   ├── image1.jpg
  │   ├── image2.jpg
  │   └── ...
  ├── labels/
  │   ├── image1.txt
  │   ├── image2.txt
  │   └── ...

2. Preparação do Ambiente de Treinamento
2.1. Instalação das Dependências

Instale as bibliotecas necessárias para treinar o modelo YOLO. Dependendo da implementação do YOLO, as dependências podem variar. Exemplo com Darknet (uma implementação popular do YOLO):

git clone https://github.com/AlexeyAB/darknet
cd darknet
make

2.2. Arquivos de Configuração

    Configuração do modelo YOLO: Você precisará configurar o arquivo .cfg com os parâmetros apropriados para o seu conjunto de dados.

    Arquivos de nomes das classes: Crie um arquivo obj.names que contenha os nomes das classes em cada linha. Exemplo:

    carro
    pessoa
    cachorro

    Arquivos de treino e validação: Crie arquivos .txt com os caminhos das imagens de treino e validação. Por exemplo, train.txt e valid.txt devem listar os caminhos absolutos para as imagens.

2.3. Modificando o Arquivo de Configuração

Edite o arquivo .cfg para refletir o número de classes e os parâmetros de treinamento (taxa de aprendizado, número de épocas, etc.). As principais mudanças são:

    classes=NUM_CLASSES
    filters= (num_classes + 5) * 3
    max_batches = (num_classes + 5) * 2000

3. Treinamento do Modelo

Com tudo configurado, inicie o treinamento do modelo utilizando a ferramenta escolhida. Para o Darknet, por exemplo, use:

./darknet detector train data/obj.data cfg/yolov4.cfg yolov4.weights

Durante o treinamento, o modelo ajusta seus pesos para detectar objetos nas imagens com base nas anotações.
4. Avaliação e Testes

Após o treinamento, você pode testar o modelo em novas imagens para verificar o desempenho. Use os seguintes comandos:

./darknet detector test data/obj.data cfg/yolov4.cfg backup/yolov4_final.weights data/test_image.jpg

5. Resultados e Ajustes Finais

Após o treinamento, analise as imagens de saída para verificar se os objetos estão sendo detectados corretamente. Caso necessário, ajuste os hiperparâmetros e continue o treinamento.
Conclusão

Neste projeto, você aprendeu como criar uma base de dados personalizada e treinar a rede YOLO para realizar a detecção de objetos. A implementação da YOLO pode ser adaptada para diferentes tipos de objetos e aplicações, desde a segurança até a análise médica. Ajustes nos parâmetros do modelo e nos dados de treinamento podem melhorar a precisão e a performance da rede.
