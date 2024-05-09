# Processamento de imagens sem OpenCV | Python

[Leave a Comment](https://acervolima.com/processamento-de-imagens-sem-opencv-python/#respond) / [Python](https://acervolima.com/category/python/) / By [Acervo Lima](https://acervolima.com/author/jack_sparrow/)

Sabemos que o OpenCV é amplamente utilizado para operar em imagens e possui um amplo espectro de funções para isso. Mas e se quisermos processar os arquivos de imagem sem usar nenhuma biblioteca externa como o OpenCV. Vamos ver como podemos fazer isso.

### Escala da imagem (usando a interpolação do vizinho mais próximo):

A interpolação do vizinho mais próximo é a forma mais simples de interpolação. Este método simplesmente determina o pixel vizinho “mais próximo” e assume o valor de intensidade dele.

Considere uma imagem pequena que tem ‘w’ pixels de largura por ‘h’ pixels de altura, que queremos redimensionar para ‘p’ pixels de largura por ‘q’ pixels de altura, assumindo que p> meq> n. Agora, precisamos de duas constantes de escala:

```
scale_x = p / w
scale_y = q / h
```

Agora, simplesmente percorremos todos os pixels na imagem de saída, endereçando os pixels de origem dos quais copiar, dimensionando nossas variáveis de controle em *scale_x* e *scale_y* , e arredondando os valores de índice dimensionados resultantes.

**Representação pictórica:**
Imagem de 3X3 pixels (total de 9 pixels), agora se quisermos aumentar o tamanho da imagem até 6X6 então, de acordo com o algoritmo vizinho mais próximo 6/3 (ou seja, 2) pixels devem ter o mesmo valor RGB que o de o pixel na imagem original.





![img](https://media.geeksforgeeks.org/wp-content/uploads/20190326204952/scaling3.png)

**Programa para dimensionar uma imagem:**

```
import matplotlib.image as img 
import numpy as npy 
m = img.imread("taj.png"); 
w, h = m.shape[:2]; 
after scaling 
xNew = int(w * 1 / 2); 
yNew = int(h * 1 / 2); 
xScale = xNew/(w-1); 
yScale = yNew/(h-1); 
  
newImage = npy.zeros([xNew, yNew, 4]); 
  
for i in range(xNew-1): 
   for j in range(yNew-1): 
       newImage[i + 1, j + 1]= m[1 + int(i / xScale), 
                                 1 + int(j / yScale)] 
img.imsave('scaled.png', newImage); 
```

**Resultado:**
![img](https://media.geeksforgeeks.org/wp-content/uploads/20190326193121/faterscaling1-300x241.png)
![img](https://media.geeksforgeeks.org/wp-content/uploads/20190326193245/faterscaling2.png)

### Dimensionamento de cinza de uma imagem:

Usando o método de valor médio, esse método destaca a intensidade do pixel em vez de mostrar em quais valores RGB ele consiste. Quando calculamos o valor médio do RGB e atribuímos ao valor RGB do pixel, já que o valor RGB do pixel é o mesmo, ele não será capaz de criar qualquer cor, pois todas as cores são formadas devido à proporção diferente do valor RGB desde em esta proporção de caso será 1: 1: 1. Portanto, a imagem então formada parecerá uma imagem cinza.

**Representação pictórica :**
![img](https://media.geeksforgeeks.org/wp-content/uploads/20190322212518/gray1.png)

**Programa para escala de cinza em uma imagem:**

```
import numpy as npy 
import matplotlib.image as img 
from statistics import mean  
  
m = img.imread("taj.png") 
w, h = m.shape[:2] 
newImage = npy.zeros([w, h, 4]) 
print( w ) 
print( h ) 
  
for i in range(w): 
   for j in range(h): 
      
      lst = [float(m[i][j][0]), float(m[i][j][1]), float(m[i][j][2])] 
      avg = float(mean(lst)) 
      newImage[i][j][0] = avg 
      newImage[i][j][1] = avg 
      newImage[i][j][2] = avg 
      newImage[i][j][3] = 1
  
img.imsave('grayedImage.png', newImage) 
```

**Resultado:**
![img](https://media.geeksforgeeks.org/wp-content/uploads/20190326193707/aftergray1.png)
![img](https://media.geeksforgeeks.org/wp-content/uploads/20190326193821/aftergray2.png)

### Corte de uma imagem:

Cortar é basicamente remover o pixel indesejado. Isso pode ser feito pegando o pixel necessário em uma grade de imagem diferente, cujo tamanho é o necessário após o corte.

Considere uma imagem de tamanho 10 X 10 pixels e se precisarmos cortar apenas o centro da imagem com 4 X 4 pixels, então precisamos coletar os valores de pixel de (10-4) / 2 começando de (3, 3) até 4 pixels na *direção xe* 4 pixels na *direção y* .

**Representação pictórica :**
![img](https://media.geeksforgeeks.org/wp-content/uploads/20190325110407/cropping.png)

```
import matplotlib.image as img 
import numpy as npy 
m = img.imread("taj.png") 
w, h = m.shape[:2] 
xNew = int(w * 1 / 4) 
yNew = int(h * 1 / 4) 
newImage = npy.zeros([xNew, yNew, 4]) 
print(w) 
print(h) 
  
for i in range(1, xNew): 
    for j in range(1, yNew): 
     newImage[i, j]= m[100 + i, 100 + j] 
img.imsave('cropped.png', newImage) 
```

**Resultado:**
![img](https://media.geeksforgeeks.org/wp-content/uploads/20190326193121/faterscaling1.png)
![img](https://media.geeksforgeeks.org/wp-content/uploads/20190326194755/aftercrop.png)
 

Artigo escrito por [rakesh797](https://auth.geeksforgeeks.org/user/rakesh797/articles) e traduzido por Acervo Lima de [Image Processing without OpenCV | Python](https://www.geeksforgeeks.org/image-processing-without-opencv-python/).

### Postagens Relacionadas:

1. [Python | Operações morfológicas no processamento de imagens (abertura) | Set-1](https://acervolima.com/python-operacoes-morfologicas-no-processamento-de-imagens-abertura-set-1/)
2. [Detecção de borda em tempo real usando OpenCV em Python | Método de detecção de borda Canny](https://acervolima.com/deteccao-de-borda-em-tempo-real-usando-opencv-em-python-metodo-de-deteccao-de-borda-canny/)
3. [Python OpenCV | método cv2.blur()](https://acervolima.com/python-opencv-metodo-cv2-blur/)
4. [Operações aritméticas em imagens usando OpenCV | Conjunto-1 (adição e subtração)](https://acervolima.com/operacoes-aritmeticas-em-imagens-usando-opencv-conjunto-1-adicao-e-subtracao/)