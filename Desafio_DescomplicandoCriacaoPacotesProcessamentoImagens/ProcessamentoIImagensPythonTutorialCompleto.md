# Processamento de Imagens com Python - Tutorial Completo

![Felipe Santana](https://www.gravatar.com/avatar/e28b55ddd7b7768feeaebbed71ce7490?d=mm&s=128)

Escrito por [**Felipe Santana**](https://minerandodados.com.br/author/felipesf05/)em janeiro 30, 2020

![Processamento de Imagens com Python - Tutorial Completo](https://minerandodados.com.br/wp-content/uploads/2020/01/image.jpg)

##### JUNTE-SE A MAIS DE 30.000 PESSOAS.

### Entre para nossa lista e receba conteúdos exclusivos e com prioridade

Quero me Inscrever na Lista VIP

Processar uma imagem significa modificar ou extrair suas informações.

E é uma tarefa amplamente utilizada quando estamos trabalhando com projetos de visão computacional como por exemplo: reconhecimento facial e detecção de objetos.

```python
# Instalando a biblioteca Pillow:
!pip install pillow
import PIL
```

**Observação:** Instalamos o pillow mas importamos o PIL, isso ocorre porque o desenvolvimento do pillow foi interrompido e as atualizações passaram a ser feitas no PIL(Python Image Library).

Essa biblioteca nos permite fazer a manipulação de imagens a partir de um script Python.

### Trabalhando com o PIL

```python
# Classe para fazer a manipulação de imagens:
from PIL import Image

# Carregar um imagem a partir do disco:
image = Image.open("imagens/new-york.jpg")
```

Vamos trabalhar com essa imagem durante todo o tutorial.

```python
# Visualizando a imagem:
image
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-151.png)

### Exibindo as propriedades da imagem

```python
# Formato da imagem:
print(image.format)

JPEG
# Canal do formato de pixels:
print(image.mode)

RGB
```

O propósito principal do sistema RGB é a reprodução de cores em dispositivos eletrônicos.

```python
# Dimensões da imagem em pixels:
print(image.size)

(639, 358)
```

### Pixel e Estrutura de Dados de Imagens

**Pixel** é a menor unidade de informação que compõe uma imagem digital.

Em uma imagem RGB o pixel é representado por três números de **8 bits** associados com as cores **R,G e B** que correspondem as cores **Red (Vermelho)**, **Green (Verde)** e **Blue (Azul)** respectivamente.

Como são números de 8 bits a faixa de valores é de **0 até 255**.

```python
Image.open("imagens/pixel-rgb.png")
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-152.png)

A cor do Pixel será gerada a partir da combinação de cada um dos canais.

Se a combinação de valores for 255 a cor do pixel será **branco**, se a combinação for 0, a cor do Pixel será **preto**.

### Convertendo Imagens para arrays Numpy

As imagens digitais nada mais são do que matrizes com números e para trabalhar com dados desse tipo nos temos a biblioteca Numpy do Python.

```python
# Importando as bibliotecas para visualização das imagens:
from matplotlib import image
from matplotlib import pyplot
# Carregando imagem como um array NumPy:
data = image.imread("imagens/new-york.jpg")
# Imprimindo o conteúdo do array NumPy:
print(data)

[[[148 188 188]
  [148 188 188]
  [148 188 188]
  ...
  [119 145 146]
  [119 145 146]
  [119 145 144]]

 [[149 189 189]
  [149 189 189]
  [149 189 189]
  ...
  [119 145 146]
  [119 145 146]
  [118 144 145]]

 [[150 190 190]
  [150 190 190]
  [150 190 190]
  ...
  [118 144 145]
  [118 144 145]
  [118 144 145]]

 ...

 [[132 137 105]
  [128 135 102]
  [124 131  98]
  ...
  [ 16  22  44]
  [ 15  27  49]
  [ 22  39  59]]

 [[129 134 102]
  [127 134 101]
  [123 130  99]
  ...
  [ 66  64  85]
  [ 51  53  76]
  [ 38  46  67]]

 [[124 129  97]
  [124 131  98]
  [125 132 101]
  ...
  [ 39  30  49]
  [ 46  41  64]
  [ 52  52  76]]]
```

Observe que para cada linha nos temos 3 valores que correspondem as tonalidades das cores RGB e cada uma dessas linhas corresponde a 1 pixel.

```python
# Imprimindo as propriedades do array de pixels:

print(data.dtype)
uint8

print(data.shape)
(358, 639, 3)

print(data.max())
255

print(data.min())
0
# Exibindo o array de pixels como uma imagem:
pyplot.imshow(data)
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-153.png)

**Convertendo o array de pixels em um objeto Image Pillow**

```python
image2 = Image.fromarray(data)

# Verificando o tipo do objeto:
type(image2)

PIL.Image.Image
```

**Convertendo um objeto do tipo imagem para um array numpy**

```python
from numpy import asarray
image = Image.open("imagens/new-york.jpg")

# Método asarray para realizar a conversão:
data = asarray(image)
# Imprimindo os atributos do array:
print(data.dtype)
print(data.shape)

uint8
(358, 639, 3)
```

### Salvando imagens em disco

```python
# Salvando a imagem no formato PNG:
image.save("imagens/new-york.png",format="PNG")
# Salvando a imagem no formato GIF:
image.save("imagens/new-york.gif",format="GIF")
# Carregando novamente a imagem e verificando o formato:
image3 = Image.open("imagens/new-york.gif")
print(image3.format)

GIF
```

### Convertendo imagens

```python
# Convertendo a imagem em escala de cinza:
image_cinza = image.convert(mode="L")
image_cinza
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-154.png)

```python
# Salvando a imagem em disco:
image_cinza.save("imagens/new-york-cinza.jpg")
```

Na conversão da imagem para escala de cinza temos uma perda de dados, pois deixamos de ter as informações das cores , teremos somente intensidades de preto e branco.

Mais essa conversão é importante porque alguns métodos e algoritmos exigem que a imagem esteja nesta escala.

### Resize Imagens

Nesse processo geramos imagens com dimensões menores. Você pode definir valores para deixar a sua imagem ou imagens em um determinado padrão.

```python
# Verificando o tamanho da imagem com o atributo size:
print(image.size)

(639, 358)
# Gerando thumbnail de tamanho 100x100:
image.thumbnail((100,100))
image
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-155.png)

```python
# Verificando as novas dimensões:
print(image.size)

(100, 56)
```

Parece que algo deu errado, apesar de ter especificado no parâmetro thumbnail() que a imagem deveria ter a dimensão de (100,100) ele me retornou uma imagem com a dimensão (100,56).

Por padrão o thumbnail() mantém o aspect ratio, ou seja, ele mantém a porcentagem de dimensão para que a imagem não seja distorcida.

```python
# Carregando novamente a imagem:
image = Image.open("imagens/new-york.jpg")

# Resize a imagem ignorando o aspect ratio:
image_resize = image.resize((200,200))
```

O método resize() é o responsável por ignorar o aspect ratio e gerar uma imagem com as dimensões especificadas no parâmetro. Nesse caso queremos uma imagem de dimensão (200,200).

```python
# Verificando as novas dimensões:
print(image_resize.size)

(200, 200)

pyplot.imshow(image_resize)
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-156.png)

### Invertendo Imagens (Flip)

É muito utilizado quando estamos trabalhando com machine learning e deep learning para gerar dados diferentes para o nosso conjunto de treinamento afim de diminuir o overfitting e com isso obter melhores resultados.

```python
# Inversão horizontal:
horizontal_image = image.transpose(Image.FLIP_LEFT_RIGHT)

# Visualizando a imagem:
pyplot.imshow(horizontal_image)
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-157.png)

```python
# Inversão vertical:
vertical_image = image.transpose(Image.FLIP_TOP_BOTTOM)

# Visualizando a imagem:
pyplot.imshow(vertical_image)
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-158.png)

### Girar Imagens (Rotate)

```python
# Carregando novamente a imagem:
image = Image.open("imagens/new-york.jpg")

# Rotacionando a imagem em 45 graus:
pyplot.imshow(image.rotate(45))
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-159.png)

```python
# Rotacionando a imagem em 90 graus:
pyplot.imshow(image.rotate(90))
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-160.png)

Note que carregamos a imagem várias vezes para garantir que as transformações sejam feitas a partir da imagem original.

### Cortar Imagens (Crop)

Permite cortar as imagens a partir de coordenadas especificas.

```python
# Exibindo a imagem original:
pyplot.imshow(image)
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-161.png)

```python
# Exibindo o corte a partir das coordenadas especificadas - left, upper, right, and lower:
pyplot.imshow(image.crop((100,100,200,200)))
```

![img](https://minerandodados.com.br/wp-content/uploads/2020/01/image-162.png)

É um processo comum em tarefas de reconhecimento facial, como a nossa área de interesse na imagem é somente a parte em que temos um face , podemos usar esse método para cortar uma determinada coordenada que foi utilizada para detectar uma face no nosso conjunto de imagens.

### Técnicas de pré-processamento aplicado a imagens

Os algoritmos de machine learning esperam que as imagens estejam em uma determinada escala ou distribuição.

```python
# Normalizando valores de pixels:
image = Image.open("imagens/new-york.jpg")
# Convertendo a imagem em um array:
pixels = asarray(image)
# Verificando a faixa de valores entre 0 e 255:
print('Data Type: %s' % pixels.dtype)
print('Min: %.3f, Max: %.3f' % (pixels.min(), pixels.max()))

Data Type: uint8
Min: 0.000, Max: 255.000
# Converte os valores inteiros em float para realizar a operação:
pixels = pixels.astype('float32')
# Normaliza a faixa de valores:
pixels /= pixels.max()
# Verificando a faixa de valores normalizada:
print('Data Type: %s' % pixels.dtype)
print('Min: %.3f, Max: %.3f' % (pixels.min(), pixels.max()))

Data Type: float32
Min: 0.000, Max: 1.000
```

### Tutorial em formato de vídeo:

<iframe title="Processamento de Imagens com Python (Passo a Passo + Script para download)" width="500" height="281" src="https://www.youtube.com/embed/Zkv_Gmj7Ml4?feature=oembed&amp;enablejsapi=1&amp;origin=https://minerandodados.com.br" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; font: inherit; vertical-align: baseline; outline: 0px; text-decoration: none; position: absolute; left: 0px; top: 0px; width: 945px; height: 531.562px;"></iframe>

### Conclusão:

Como vimos podemos extrair dados referentes à dimensão, escala e número de objetos em uma cena.

Em conjunto com a técnica de visão computacional o processamento de imagens permite adquirir “insights” de dados a partir de imagens ou vídeos.

Há inúmeras aplicações que podem ser desenvolvidas com visão computacional e elas abrangem em sua maioria diversos setores de tecnologia da informação.

Graças ao reconhecimento facial hoje já existe a possibilidade de fazer o bloqueio e desbloqueio do seu smartphone apenas aproximando seu rosto do aparelho, e a base para toda essa tecnologia vem do processamento de imagens.

Curti? então que tal deixa seu cometário na seção abaixo.