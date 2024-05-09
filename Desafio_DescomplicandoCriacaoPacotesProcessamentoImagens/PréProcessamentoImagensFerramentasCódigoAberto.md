# Pré-processamento de imagens com ferramentas de código aberto



***Uma breve análise do pré-processamento de imagens para fazer IA em visão computacional\***

**Andi Sama** - *CIO, Sinergi Wahana Gemilang com* ***Andrew Widjaja\*** *e* ***Cahyati S. Sangaji\***

\#SinergiWahanaGemilang #ArtificialIntelligence #ComputerVision #IBMVisualInsights #GoogleAutoML #ImagePreprocessing #PythonImageLibrary #Matplotlib #Keras #OpenCV

Os arquivos de suporte (arquivo Python Notebook + Imagens) para este artigo podem ser encontrados no github .

Quando estamos construindo um modelo de aprendizado de máquina (ou aprendizado profundo) em visão computacional com Python, geralmente usamos conjuntos de dados na forma de imagens ou vídeos. Fazendo isso manualmente, sem nenhuma ferramenta automatizada, como IBM Visual Insights ou Google AutoML, por exemplo, na maioria das vezes precisamos pré-processar os dados antes que eles possam ser consumidos por nosso algoritmo de aprendizado de máquina.

Este artigo se concentra na introdução de abordagens para fazer o pré-processamento na imagem de origem, transformando a imagem em um array numpy e vice-versa (formato JPEG, PNG). Ele é implementado na linguagem de programação Python usando bibliotecas de código aberto comuns, como Python Image Library (PIL), Matplotlib, Keras e OpenCV.

O seguinte mostra o exemplo de uma imagem de origem (reside em 'data / smurf.jpg') que usamos neste artigo (Avforums, 2017). O arquivo de imagem de origem é codificado na sequência RGB - Vermelho, Verde, Azul. Esta sequência é importante porque no OpenCV, por exemplo, a sequência codificada é BGR (azul, verde, vermelho) em vez de RGB.

![img](https://ichi.pro/assets/images/max/724/1*zAsw8sT6cK1UPNnMbUVqPQ.png)Bunch of Smurfs, a imagem fonte base para trabalharmos.

Normalmente, essas abordagens (implementadas com várias bibliotecas disponíveis como código aberto) também se aplicam a arquivos de vídeo ou fluxo de vídeo da câmera (bem como a imagem estática da câmera), pois o fluxo de vídeo provavelmente será convertido em série de imagens primeiro, o que significa que iremos processar uma imagem de cada vez de qualquer maneira.

# Preparando o Meio Ambiente

O seguinte mostra o ambiente que estamos usando no sistema operacional Windows 10. Os artigos anteriores foram implementados principalmente na distribuição Linux Ubuntu ou RHEL - instalados localmente (no local) ou na nuvem: IBM IaaS Cloud, GCP (Google Cloud Platform IaaS) ou AWS EC2 (Amazon Web Services, Elastic Compute Cloud). Estamos fazendo algo diferente agora, está totalmente em execução no Windows 10.



```
import os, platform
print('OS name:', os.name, ', system:', platform.system(), ', release:', platform.release())
import sys
print("Anaconda version:")
!conda list anaconda
print("Python version: ", sys.version)
print("Python version info: ", sys.version_info)
import PIL
print("PIL version: ", PIL.__version__)
import matplotlib
print("Matplotlib version: ", matplotlib.__version__)
import tensorflow as tf
print("Keras version:", tf.keras.__version__)
import cv2
print("OpenCV version: ", cv2.__version__)
```





```
OS name: nt , system: Windows , release: 10
Anaconda version:
# packages in environment at C:\Users\andis\anaconda3:
#
Python version:  3.7.6 (default, Jan  8 2020, 20:23:39) [MSC v.1916 64 bit (AMD64)]
Python version info:  sys.version_info(major=3, minor=7, micro=6, releaselevel='final', serial=0)
PIL version:  7.0.0
Matplotlib version:  3.1.3
Keras version: 2.2.4-tf
OpenCV version:  4.2.0
# Name                    Version                   Build  Channel
_anaconda_depends         2019.03                  py37_0
anaconda                  custom                   py37_1
anaconda-client           1.7.2                    py37_0
anaconda-navigator        1.9.12                   py37_0
anaconda-project          0.8.4                      py_0
```



Primeiro de tudo, instale o Anaconda para Windows 10 (Anaconda, 2020) seguido por OpenCV (Pranav Sreedhar, 2019). Por padrão, Python, Matplotlib e Jupyter Notebook (Interactive Integrated Development Environment) serão instalados com o Anaconda.

A primeira coisa a fazer é criar um ambiente virtual antes de fazer qualquer coisa, desde a instalação do Anaconda. No Prompt do Anaconda, use o comando 'conda create'



```
(base) C:\Users\andis>conda create -n myenv
```





```
Collecting package metadata (current_repodata.json): done
Solving environment: done
## Package Plan ##
environment location: C:\Users\andis\anaconda3\envs\myenv
Proceed ([y]/n)? y
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate myenv
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```





```
(base) C:\Users\andis>conda activate myenv
```





```
(myenv) C:\Users\andis>conda install pip
```





```
(myenv) C:\Users\andis>pip install package_name
```



![img](https://ichi.pro/assets/images/max/724/1*3K6ass0vPm0sv1etDPwm1w.png)

Em geral, especialmente em Python - precisamos converter uma imagem em um formato interno no qual possamos trabalhar e, normalmente, isso será convertido em um array numpy (Justin Johnson, Spring 2020).

Uma imagem RGB contém dados em 3 dimensões (altura, largura, canal) como (768, 1024, 3) com 2.359.296 pixels no total (768 * 1024 * 3). Cada um desse pixel por canal tem um valor de 8 bits (1 Byte) variando de 0–255. Significa que para cada pixel RGB, possui 3 bytes (24 bits) de dados (1 Byte para cada canal: R, G e B).

Quando esses dados de pixels são convertidos em uma matriz numpy, eles são mais fáceis de manipular. Este é o propósito de algumas das ferramentas que estamos discutindo aqui: PIL, Matplotlib, Keras e OpenCV.

# **Pré-processamento de imagens com PIL - Biblioteca de imagens Python**

O seguinte mostra como abrir e exibir uma imagem com Python Image Library (PIL). A imagem é exibida em uma janela separada após a execução da função 'img.show ()'. Observe que também visualizamos algumas informações básicas sobre a origem da imagem: seu formato: JPEG e modo: RGB, embora pareça internamente PIL está convertendo a imagem para PNG, para exibição na tela.



```
# A. IMAGE MANIPULATION with PIL - Python Image Library
# First of all, VIEWing an IMAGE
# - first import necessary libraries
import numpy as np
from PIL import Image
# - set a few generic variables
FilePath = 'data/'
FileName = 'smurf'
FileExt = '.jpg'
ImageFile = FilePath + FileName + FileExt
# - open the imagefile
img = Image.open(ImageFile)
# - inspect necessary information
print('Image format: ', img.format)
print('Image mode: ', img.mode)
# - display
img.show()
```





```
Image format:  JPEG
Image mode:  RGB

      
```



Convertemos a imagem carregada em nparray usando a função asarray de numpy. A imagem convertida (dados) agora está no formato nparray com tipo de dados: <class 'numpy.ndarray'> e formato de dados (altura: 393, largura: 700, canal: 3).



```
# A.1. CONVERT an IMAGE to NP ARRAY
# - first import necessary libraries
from numpy import asarray
# - convert image format to numpy array
data = asarray(img)
# - inspect necessary information
print('data type: ', type(data))
print('data shape: ', data.shape)
```





```
data type:  <class 'numpy.ndarray'>
data shape:  (393, 700, 3)
```





```
print(data)
```





```
[[[ 82  99 143]
[ 93 107 156]
[ 99 105 165]
...
[215 234 248]
[215 234 248]
[215 234 248]]
...
[[116 160 223]
[ 98 142 205]
[103 147 208]
...
[ 69  54 139]
[ 72  54 140]
[ 74  54 139]]]
```



Quando terminarmos de trabalhar com os dados (fazendo limpeza e transformação de dados, por exemplo), podemos converter os dados (no formato nparray) de volta para o formato de imagem. O fromarray da Numpy é uma função que usamos exatamente para este propósito.



```
# A.2. CONVERT NP ARRAY back to IMAGE format
# - convert numpy array to image format
img_fromnparray = Image.fromarray(data)
img_fromnparray.show()
# - inspect necessary information
print('Image size: ', img_fromnparray.size)
print('Image format: ', img_fromnparray.format)
print('Image mode: ', img_fromnparray.mode)
```





```
Image size:  (700, 393)
Image format:  None
Image mode:  RGB
```





```
# A.3. SAVE the IMAGE to ANOTHER FORMAT, e.g. PNG (source was JPG before)
#  - 1st reopen image, and save is as PNG
data = asarray(Image.open(ImageFile))
print("Saving as PNG (RGB)...", FilePath + FileName)
print(type(data), data.shape)
img_png = Image.fromarray(data).save(FilePath + FileName + '_pil-rgb' + '.png')
#  - 2nd reopen image and convert it to grey, and save is as PNG
data = asarray(Image.open(ImageFile).convert('L'))
print("Saving as PNG (Grey)...", FilePath + FileName)
print(type(data), data.shape)
img_png = Image.fromarray(data).save(FilePath + FileName + '_pil-grey' + '.png')
```





```
Saving as PNG (RGB)... data/smurf
<class 'numpy.ndarray'> (393, 700, 3)
Saving as PNG (Grey)... data/smurf
<class 'numpy.ndarray'> (393, 700)
```



![img](https://ichi.pro/assets/images/max/724/1*ubah--CJAjGGn27CITdYTw.png)Arquivos de imagem gerados (smurf_pil-grey.png e smurf_pil-rgb.png) no diretório 'data /'.

# **Pré-processamento de imagem com Matplotlib**

Uma das maneiras mais rápidas de exibir uma imagem embutida no Jupyter Notebook é usar a função imshow () do matplotlib. Apenas use 'image.imread' para ler a imagem, então use 'pyplot.imshow ()' para mostrar a imagem carregada. Uma imagem embutida é a imagem exibida no Jupyter Notebook como resultado da execução de 'pyplot.imshow ()'.



```
# B. IMAGE MANIPULATION with Matplotlib
# - first import necessary libraries
from matplotlib import image, pyplot
img = image.imread(ImageFile)
# - inspect necessary information
print('Image dtype: ', img.dtype)
print('Image shape: ', img.shape)
# - then show the image
pyplot.imshow(img)
# pyplot.show()
```



![img](https://ichi.pro/assets/images/max/724/1*1jYVvRJorov8l21T77a7bg.png)Uma imagem embutida é exibida no Jupyter Notebook como resultado da execução da função pyplot.imshow () de matplotlib.

# **Pré-processamento de imagem com PIL (continuação)**

Ainda há muito mais coisas que podemos fazer com o PIL *(Fredrik Lundh, 1995–2011 e Alex Clark e Contribuidores, 2010–2020).* Entre outros estão a Transformação da imagem conforme mostrado abaixo (rotação, corte).



```
# A.4 Continuing IMAGE MANIPULATION with PIL
#     Rotate, Crop, Contrast & Brightness
#  - Image rotation with PIL
Rotation_Degree = 30
im = Image.open(ImageFile)
im.rotate(Rotation_Degree).show()
#  - Image crop with PIL
#    Looking at the pixel locations in above image, we can define the coordinate (box) to crop
box = (350, 100, 500, 200) #left, upper, right, lower
im.crop(box).show()
```



![img](https://ichi.pro/assets/images/max/724/1*-HLkZQ_9RqhYpY2WOweSbA.png)Rotação de imagem (30 graus) e corte de imagem usando PIL (com base na área definida em uma caixa). Ambas as operações são baseadas na imagem original.

Em seguida, Transformação da imagem (contraste, brilho) conforme mostrado abaixo. Os aprimoramentos de nitidez e cor, bem como a filtragem de imagem (por exemplo, desfoque, relevo, nitidez, suavização, aprimoramento de borda) são funções adicionais, por exemplo, que podemos usar com PIL.



```
#  - Image Enhancements with PIL: Contrast
from PIL import ImageEnhance
enh = ImageEnhance.Contrast(im)
enh.enhance(1.75).show("75% more contrast")
#  - Image Enhancements with PIL: Brightness
enh = ImageEnhance.Brightness(im)
enh.enhance(1.5).show("50% more brightness")
```



![img](https://ichi.pro/assets/images/max/724/1*A2U3AwHdphgesnftITh-wA.png)Aprimoramentos de imagem (contraste e brilho). O contraste e o brilho são definidos em valores bastante significativos para que possamos ver claramente o efeito dos aprimoramentos de imagem. Ambas as operações são baseadas na imagem original.

# **Pré-processamento de imagens com Keras**

Keras é a estrutura de alto nível para trabalhar com aprendizagem profunda. Ele é desenvolvido com base no Tensorflow, uma das bibliotecas mais conhecidas para fazer aprendizado profundo. A outra biblioteca é a Pytorch.

O comando a seguir instala o Keras no ambiente conda. Tensorflow, a biblioteca de suporte também deve ser instalada automaticamente.



```
# C. IMAGE MANIPULATION with Keras (built on top of Tensorflow)
# - first import necessary libraries
from keras.preprocessing.image import load_img
import warnings
# - load and view the image
img = load_img(ImageFile)
print('Image type:', type(img), ', image format:', img.format, ', image mode:', img.mode, ', image size:', img.size)
img.show()
```





```
Using TensorFlow backend.
Image type: <class 'PIL.JpegImagePlugin.JpegImageFile'> , image format: JPEG , image mode: RGB , image size: (700, 393)
```





```
from keras.preprocessing.image import img_to_array, array_to_img
print('Original type of image:', type(img))
# - convert the image to numpy array
img_nparray = img_to_array(img)
print('Numpy array info:', type(img_nparray))
print('type:', type(img_nparray.dtype))
print('shape:', type(img_nparray.shape))
```





```
Original type of image: <class 'PIL.JpegImagePlugin.JpegImageFile'>
Numpy array info: <class 'numpy.ndarray'>
type: <class 'numpy.dtype'>
shape: <class 'tuple’>
```





```
print(img_nparray)
```





```
[[[ 82.  99. 143.]
[ 93. 107. 156.]
[ 99. 105. 165.]
...
[215. 234. 248.]
[215. 234. 248.]
[215. 234. 248.]]
...
[[116. 160. 223.]
[ 98. 142. 205.]
[103. 147. 208.]
...
[ 69.  54. 139.]
[ 72.  54. 140.]
[ 74.  54. 139.]]]
```



Keras é a estrutura de alto nível para trabalhar com aprendizagem profunda. Ele é desenvolvido com base no Tensorflow, uma das bibliotecas mais conhecidas para fazer aprendizado profundo. A outra biblioteca é a Pytorch.

O comando a seguir instala o Keras no ambiente conda. Tensorflow, a biblioteca de suporte também deve ser instalada automaticamente.



```
(myenv) C:\Users\andis>conda install –c anaconda keras
```





```
img_pil = array_to_img(img_nparray)
print("Converted (back) type of the image:", type(img_pil))
# - saving an image with keras
from keras.preprocessing.image import load_img, save_img
ImageFile = FilePath + FileName + '_keras' + '.png'
print("Saving Image File with Keras...", FilePath + FileName)
save_img(ImageFile, img_nparray)
# - loading an image with keras
print("Loading Image File with Keras...", FilePath + FileName)
img = load_img(ImageFile)
print('Image type:', type(img), ', image format:', img.format, ', image mode:', img.mode, ', image size:', img.size)
img.show()
```





```
Converted (back) type of the image: <class 'PIL.Image.Image’>
Saving Image File with Keras... data/smurf
Loading Image File with Keras... data/smurf
Image type: <class 'PIL.PngImagePlugin.PngImageFile'> , image format: PNG , image mode: RGB , image size: (700, 393)
```



![img](https://ichi.pro/assets/images/max/724/1*NahSuLkMSaUaYRacORGb3w.png)Um arquivo PNG gerado por Keras, convertido da imagem de origem.

Keras, como uma das principais estruturas de aprendizado profundo em visão computacional, pode realizar muito mais variações de pré-processamento de imagens. Vamos dar uma olhada em alguns exemplos usando a classe ImageDataGenerator que pode gerar lotes de dados de imagem de tensor com aumento de dados em tempo real.

Aumento de dados é o recurso muito importante ao preparar imagens para treinamento antes de fazer o treinamento para gerar um modelo treinado em aprendizado profundo. Rotação, inversão horizontal / vertical, ajuste de brilho, redimensionamento, zoom são algumas das operações que podemos fazer com ImageDataGenerator.

Inicialmente, inicializamos a classe ImageDataGenerator com 'Datagen = ImageDataGenerator ()' e, em seguida, usamos a função apply_transform () para executar vários pré-processamento de imagem.

A função apply_transform () leva 2 argumentos (Chollet, Francois e outros, 2015–2020). Primeiro é x, a imagem de entrada (deve estar na forma de dados de tensor 3D). O segundo argumento é transform_parameters, que pode ser 'theta': ângulo de rotação em graus, 'tx': deslocamento na direção x, 'ty': deslocamento na direção y, 'cisalhamento': ângulo de corte em graus, 'zx': Zoom na direção x, 'zy': Zoom na direção y, 'flip_horizontal': inversão horizontal, 'flip_vertical': inversão vertical, 'channel_shift_intencity': intensidade de mudança de canal e 'brilho': intensidade de mudança de brilho.



```
# - do image flip (horizontal)
from keras.preprocessing.image import ImageDataGenerator
img = load_img(ImageFile)
img_nparray = img_to_array(img)
Datagen = ImageDataGenerator()
flip_horizontal = Datagen.apply_transform(x=img_nparray, transform_parameters={'flip_horizontal':True})
array_to_img(flip_horizontal).show()
# - do image flip (vertical)
flip_vertical = Datagen.apply_transform(x=img_nparray, transform_parameters={'flip_vertical':True})
array_to_img(flip_vertical).show()
```



![img](https://ichi.pro/assets/images/max/724/1*uIb2XDQWurFlWh0s42jsjw.png)Fazendo a inversão horizontal da imagem e inversão vertical com a função ImageDataGenerator apply_transform () no Keras.

Enquanto o seguinte mostra como executar a rotação da imagem, zoom-out e zoom-in. Novamente, todas as operações de pré-processamento são aplicadas a partir da imagem de origem original.



```
# - do image rotation
rotate = Datagen.apply_transform(x=img_nparray, transform_parameters={'theta':-25})
array_to_img(rotate).show()
# - zoom-out in x and y direction
zoom_out = Datagen.apply_transform(x=img_nparray, transform_parameters={'zx':2, 'zy':2})
array_to_img(zoom_out).show()
# - zoom-iin in x and y direction
zoom_in = Datagen.apply_transform(x=img_nparray, transform_parameters={'zx':.5, 'zy':.5})
array_to_img(zoom_in).show()
```



![img](https://ichi.pro/assets/images/max/724/1*3vBaDBY1TgADjfXeJrnAAw.png)Fazendo rotação, redução e ampliação da imagem com a função ImageDataGenerator apply_transform () no Keras.

# **Pré-processamento de imagem com OpenCV**

No final, discutimos o pré-processamento de imagens com OpenCV - The Open Source Computer Vision and Machine Learning Library. O OpenCV fornece uma infraestrutura comum para aplicativos de visão computacional, bem como para acelerar o uso da percepção da máquina em produtos comerciais (OpenCV Team, 2020).

Em Inteligência Artificial, especialmente em aprendizagem profunda - o OpenCV tem apoiado extensivamente a implementação de muitos aplicativos reais relacionados à visão computacional, tanto Tensorflow quanto baseados em Pytorch, entre outros. O reconhecimento facial é um de seus casos de uso comum.

Em Python, usamos OpenCV importando cv2. Manipulações básicas de imagens com OpenCV são mostradas abaixo. Começamos lendo o arquivo de imagem de origem formatado em RGB e salvando-o em um arquivo de formato PNG. Depois disso, converta o espaço de cores da imagem para CINZA e HSV usando a função cvtColor (). O espaço de cores HSV é comumente usado na detecção de objetos e no rastreamento de objetos, como implementado no Auto-Driving-Car.



```
# *********************************
# D. IMAGE MANIPULATION with OpenCV
# *********************************
# - first import necessary libraries
# import cv2
# - set ImageFile to our original image, then read the image
ImageFile = FilePath + FileName + FileExt
im = cv2.imread(ImageFile)
#cv2.imshow("my image", im)
# - save the file as PNG before conversion (internally it's in BGR order)
cv2.imwrite(FilePath + FileName + '_opencvRGB' + '.png', im)
print(type(img))
# - convert to GRAY color space
img = cv2.cvtColor(im, cv2.COLOR_BGR2GRAY)
# - save the file as PNG after conversion
cv2.imwrite(FilePath + FileName + '_opencvGREY' + '.png', img)
# - convert to HSV color space (typical for object tracking)
img = cv2.cvtColor(im, cv2.COLOR_BGR2HSV)
# - save the file as PNG after conversion
cv2.imwrite(FilePath + FileName + '_opencvHSV' + '.png', img)
```





```
<class 'numpy.ndarray'>

      
       Using cvtColor() function in OpenCV to do basic color space manipulations.
      
```





```
# - apply 50% blur
#   alternatively we can use cv2.imshow() to display the image instead of writing it to a file
#   e.g.:
#     cv2.imshow("OpenCV: apply 50% blur", img)
#     cv2.waitKey(0)
img = cv2.medianBlur(im, 5)
cv2.imwrite(FilePath + FileName + '_opencvBLUR' + '.png', img)
# - apply Edge Detection
img = cv2.Canny(im, 100, 200)
cv2.imwrite(FilePath + FileName + '_opencvEdgeDetect' + '.png', img)
```



![img](https://ichi.pro/assets/images/max/724/1*wv6DgOtfS74Ayx5-Hfebqg.png)Mais manipulações de imagem com OpenCV - realizando Blur e detecção de bordas na imagem de origem.

O seguinte mostra uma visão ampliada do arquivo na detecção de bordas.

![img](https://ichi.pro/assets/images/max/724/1*6eIyRf8me866_nHTEthvwA.png)Uma visão ampliada da detecção de bordas com OpenCV.

Observe que continuamos usando a função cv2.imwrite () a cada vez para gravar o resultado em um arquivo de imagem externo. Alternativamente, podemos usar cv2.imshow () seguido pela função cv2.waitKey () para exibir a imagem em vez de gravá-la em um arquivo.

# **O que vem a seguir então?**

Abordamos rapidamente a Python Image Library (PIL), Matplotlib, Keras e OpenCV com a linguagem de programação Python para ilustrar suas funcionalidades básicas no pré-processamento de imagens. As ferramentas têm muito mais a oferecer do que o discutido neste artigo, apenas esperando que exploremos.

Ser um cientista de dados (ou apenas um aspirante a cientista de dados) exige um aprendizado contínuo e de longa duração na exploração e experimentação de conjuntos de dados, além de ter muita curiosidade para nos manter atualizados sobre vários tipos de algoritmos e ferramentas para uso em vários setores -cases implementações.

Como qualquer outro cientista em outras disciplinas, muitas vezes dedica sua vida em perseguir coisas em sua área de foco de pesquisa, a fim de se manter atualizado e se esforçar para ser melhor do que o estado da arte. Pode parecer quase impossível atingir os objetivos definidos no início da jornada - porém, com muita persistência e muita paciência, no final do caminho, embora nem sempre verdadeiro, todos os esforços que temos feito, vai valer a pena J.

Ser prático e ter conhecimento e experiência atualizados com ferramentas práticas em conjuntos de dados de pré-processamento (neste caso, trabalhar e manipular imagem ou fluxo de vídeo) antes de fazer qualquer análise ou modelagem de aprendizado de máquina / profundo seria uma habilidade inestimável para um cientista de dados.

Bem, vamos começar fazendo algo. E a hora certa, é agora !.

# *Referências*

Anaconda, 2020, “ *Anaconda Individual Edition: Anaconda 2020.02 para Windows Installer, Python 3.7 versão* ”.

Andi Sama et.al., 2020, *“* *Um breve olhar para Data Wrangling: An Essential Supporting Skill for doing Analytics in Data Science* *”* .

Andi Sama et al., 2019, *“* *Think like a Data Scientist* *”* .

Avforums, 2017, “ *Smurfs The Lost Village 4K Ultra HD Blu-ray Disc Review* ”.

Francois Chollet e outros, 2015–2020, “ ImageDataGenerator methods: apply_transform ”, Keras Documentation.

*Fredrik Lundh, 1995–2011 e Alex Clark and Contributors, 2010–2020, “* *Pillow Tutorial: Using the Image class* *”* .

Gaurav Singhal, 2020, “ *Importing Image Data into NumPy Arrays* ”.

Justin Johnson, Spring 2020, “ *CS231n Convolutional Neural Networks for Visual Recognition: Python Numpy Tutorial* ”, Stanford University.

Mokhtar Ali Ebrahim, 2019, “ *Python Image Processing Tutorial (Using OpenCV)* ”.

Pranav Sreedhar, 2019, “ *Instalando OpenCV para Python no Windows usando Anaconda ou WinPython* ”.

Equipe OpenCV, 2020, “ *Open Source Computer Vision Library* ”, OpenCV.org.

Sinergi Wahana Gemilang, 2017–2020, *“* *Artigos múltiplos sobre Internet das Coisas (IoT), Inteligência Artificial (IA) e Computação Quântica* *”* , SWG Insight trimestral - edições múltiplas.

**YOU MAY LIKE**

[![Adskeeper](https://cdn.adskeeper.co.uk/images/adskeeper_svg.svg)](https://widgets.adskeeper.com/?utm_source=widget_adskeeper&utm_medium=text&utm_campaign=add&utm_content=1127595)