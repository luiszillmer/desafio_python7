# Processamento de imagem, em Python?

Recentemente, deparei com um problema que requer pelo menos um nível básico de processamento de imagem. Posso fazer isso em Python? Em caso afirmativo, com o que?

**[python](https://www.ti-enxame.com/pt/python/)****[image](https://www.ti-enxame.com/pt/image/)****[image-processing](https://www.ti-enxame.com/pt/image-processing/)****[image-manipulation](https://www.ti-enxame.com/pt/image-manipulation/)**

18 de set. de 2008[akdom](https://stackoverflow.com/users/145/akdom)

A biblioteca mais conhecida é [PIL](http://effbot.org/zone/pil-index.htm) . No entanto, se você está simplesmente fazendo manipulação básica, provavelmente está melhor com as ligações Python para [ImageMagick](https://wiki.python.org/moin/ImageMagick) , que serão muito mais eficientes do que escrever as transformações em Python.

Dependendo do que você quer dizer com "processamento de imagem", uma melhor opção pode estar nas bibliotecas baseadas em números: [mahotas](http://luispedro.org/software/mahotas) , [scikits.image](http://scikit-image.org/) ou [scipy.ndimage](https://www.scipy.org/SciPyPackages/Ndimage) . Tudo isso funciona com matrizes numpy, para que você possa misturar e combinar funções de uma biblioteca e de outra.

Comecei o site [http://pythonvision.org](http://pythonvision.org/) que tem mais informações sobre eles.

Você também tem uma abordagem para o processamento de imagens com base em módulos científicos "padrão": **O SciPy** possui um pacote inteiro dedicado ao processamento de imagens: [scipy. ndimage](https://docs.scipy.org/doc/scipy/reference/tutorial/ndimage.html) . Scipy é de fato o pacote padrão de cálculos numéricos gerais; é baseado no módulo de manipulação de matriz padrão de fato [NumPy](https://www.numpy.org/) : as imagens também podem ser manipuladas como matriz de números. Quanto à exibição de imagens, [Matplotlib](http://matplotlib.sourceforge.net/gallery.html) (também parte da "trilogia científica") torna a exibição de imagens [bastante simples](http://matplotlib.sourceforge.net/examples/pylab_examples/image_demo3.html) .

O SciPy ainda é mantido ativamente, por isso é um bom investimento para o futuro. Além disso, atualmente o SciPy é executado com Python 3, enquanto a Biblioteca de Criação de Imagens (PIL) Python não.

Para concluir a lista: opencv http://opencv.willowgarage.com/documentation/python/index.html

