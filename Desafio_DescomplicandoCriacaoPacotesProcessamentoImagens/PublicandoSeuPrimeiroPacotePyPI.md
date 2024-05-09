# Publicando seu primeiro pacote PyPI

## Aprenda a disponibilizar seu código no maior repositório Python

[![Caio Carneloz](https://miro.medium.com/fit/c/96/96/1*lQkn8F82g9bZmEF7I1Yb-g.jpeg)](https://medium.com/@caiocarneloz?source=post_page-----de7eb75db452-----------------------------------) -  [Caio Carneloz](https://medium.com/@caiocarneloz?source=post_page-----de7eb75db452-----------------------------------) - [Feb 23, 2020](https://medium.com/data-hackers/pypi-publicando-seu-primeiro-pacote-de7eb75db452?source=post_page-----de7eb75db452-----------------------------------) · 6 min read



![img](https://miro.medium.com/max/1400/0*OF_A_rgPerdFrQy3.png)

**Python Package Index** ou **PyPI** é um repositório de pacotes para a linguagem de programação Python. Por meio do PyPI, é possível encontrar e instalar programas desenvolvidos pela comunidade Python. Além disso, também é possível submeter o seu próprio pacote, que fica disponível para qualquer usuário no mundo que tenha o PyPI instalado.

O processo de adquirir um novo pacote é muito simples. Na linguagem popular, é “só dar um pip”. Um exemplo pode ser dado ao adquirir uma das bibliotecas mais populares de *machine learning*, o *scikit-learn*. Com o PyPI instalado, basta executar o seguinte comando no terminal:

```
pip install sklearn
```

Ao fim, você tem em mãos centenas de ferramentas e modelos de *machine learning* prontos para serem usados, sem a necessidade de nenhum outro *download* ou configuração.

Neste tutorial, será demonstrada uma maneira fácil de subir os seus pacotes para o repositório do PyPI. Vamos criar um projeto do zero, realizar a submissão e, ao fim, baixar o projeto e testá-lo dentro do Python.

# 1. Primeiros passos

Inicialmente, **é necessário criar uma conta** nos sites [**PyPI**](https://pypi.org/) e [**Test PyPI**](https://test.pypi.org/).
O site [Test PyPI](https://test.pypi.org/) é disponibilizado justamente para que possamos testar as submissões que desejamos fazer futuramente. Lembre-se bem do seu login e senha, eles serão necessários quando formos submeter o pacote.

Também será necessário obter alguns pacotes que são disponibilizados no PyPI. São eles: *setuptools, wheel e twine*. Tendo o PyPI, basta executar:

```
pip install setuptools wheel twine
```

# 2. Estrutura de arquivos

Para darmos continuidade, será necessário criar algumas pastas e arquivos. O mesmo padrão pode ser seguido para submeter qualquer outro pacote.

O nome do pacote usado neste exemplo será **pacotepypi**. Este nome é único, portanto é necessário que você **escolha um nome que ainda não foi usado**. Você pode pesquisar os que já existem tanto no site do [PyPI](https://pypi.org/) (para o release oficial) quanto do [Test PyPI](https://test.pypi.org/) (para testes). O nome que eu estou utilizando já foi submetido por mim, então sugiro que você o substitua.

```
/exemplo
  └LICENSE
  └README.md
  └setup.py
  └/pacotepypi
     └modulo.py
```

- **/exemplo
  **- diretório raiz, onde ficarão todos os arquivos
- **setup.py**
  \- código python que contém informações sobre o pacote
- **LICENSE
  **- arquivo que contém a licença do pacote
- **/pacotepypi**
  \- diretório onde ficarão os códigos do pacote
- **modulo.py
  **- código python que contém as funções do nosso pacote

# 3. Conteúdo dos arquivos

## LICENSE

Este arquivo conterá todos os detalhes sobre a licença do seu pacote. Existem vários exemplos de licenças para softwares na internet. Você pode escolher uma licença no site https://choosealicense.com/, que é exatamente o que faremos aqui. Eu optei pela *MIT License*, que é bem simples e clara.

```
MIT License

Copyright (c) 2020 pacotepypi

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## README

Como o nome já indica, este arquivo existe para que o usuário leia algumas informações sobre o pacote. Proposta, dependências, funcionalidades e formas de usar o pacote são algumas das informações que podem estar aqui. Este arquivo não é obrigatório para que possamos subir o nosso pacote, mas é interessante tê-lo. Você pode aprender como formatar este arquivo neste [link](https://guides.github.com/features/mastering-markdown/).

````
# pacotepypi
Example of PyPI package.## Getting Started
#### Dependencies
You need Python 3.7 or later to use **pacotepypi**. You can find it at [python.org](https://www.python.org/).You also need setuptools, wheel and twine packages, which is available from [PyPI](https://pypi.org). If you have pip, just run:
```
pip install setuptools
pip install wheel
pip install twine
```
#### Installation
Clone this repo to your local machine using:
```
git clone https://github.com/caiocarneloz/pacotepypi.git
```## Features
- File structure for PyPI packages
- Setup with package informations
- License example
````

O README é exibido na página inicial do seu pacote no PyPI. Como o pacote utilizado de exemplo neste tutorial já foi submetido, você pode conferir como ficou a página inicial por este [link](https://pypi.org/project/pacotepypi/).

## setup.py

O arquivo de setup será utilizado pelo *setuptools* para construção do seu pacote. Ele irá conter diversas informações como nome, versão, descrição e afins. Como possuímos um arquivo README, também será necessário incluí-lo nas informações. Você pode substituir os campos da forma que desejar.

A maior parte dos atributos é bem intuitiva. O atributo “ install_requires” contém uma lista de dependências do seu pacote. Neste exemplo, nosso pacote precisará do numpy para funcionar, então devemos colocá-lo. Tudo que está presente na lista de dependências será instalado junto ao seu pacote.

## modulo.py

Por fim, o arquivo modulo.py irá conter o código fonte do nosso pacote. Sendo assim, as funções que você deseja disponibilizar devem estar codificadas aqui.

Neste exemplo teremos uma função que imprime números de 0 a 9 e exibe uma mensagem indicando que está tudo ok. Poderíamos ter mais módulos além desse, basta criar novos arquivos. A forma de acessá-los por meio do pacote será abordada mais a frente.

# 4. Criação do pacote

Para criar o pacote que será enviado ao PyPI, será necessário executar o arquivo setup.py passando como parâmetro “sdist”. Pelo terminal, navegue até a pasta onde se encontra o arquivo setup.py e use o seguinte comando:

```
python setup.py sdist
```

Será criada a pasta chamada “dist”, que contém o pacote a ser submetido.

# 5. Upload do pacote

## Repositório de teste

Por fim, basta fazer o upload do pacote gerado na pasta “dist”. No entanto, é interessante primeiramente fazer o upload no site de teste do repositório PyPI. Desta forma, você não atrapalha o versionamento do repositório oficial e pode conferir se está tudo funcionando conforme desejado. Para isto, execute o comando de upload do twine informando a URL da API do [Test PyPI](https://test.pypi.org/):

```
twine upload --repository-url https://test.pypi.org/legacy/ dist/*
```

Nesta etapa, serão requisitados login e senha da sua conta no [Test PyPI](https://test.pypi.org/). Lembre-se que sua conta no PyPI não é compartilhada com o Test PyPI, portanto é necessário fazer o cadastro em ambas.

## Repositório oficial

Para subir seu pacote no repositório oficial, basta executar o mesmo comando utilizado acima, mas sem informar nenhuma URL como parâmetro. Aqui será requisitado seu login e senha do repositório oficial.

```
twine upload dist/*
```

# 6. Instalação do pacote

Se tudo funcionou corretamente nas etapas anteriores, você conseguirá visualizar informações sobre o seu pacote fazendo login no Test PyPI ou PyPI.

Agora iremos instalar e utilizar o nosso pacote. Para instalar o pacote que está no repositório oficial basta usar o pip de maneira convencional. O nome do pacote criado aqui é “pacotepypi”, para instalá-lo basta executar:

```
pip install pacotepypi
```

Para instalar o pacote disponível no Test PyPI, inclua a URL da API:

```
pip install -i https://test.pypi.org/simple/ pacotepypi
```

# 7. Utilização do pacote

Agora que o seu pacote PyPI está instalado, você pode utilizá-lo normalmente. O código abaixo realiza o import do “**pacotepypi”** e utiliza a função **“teste”** do módulo **“modulo”**. Com tudo funcionando, não apenas você mas qualquer pessoa no mundo com acesso ao pip poderá usufruir do seu pacote/biblioteca.

<iframe src="https://medium.com/media/60310da5fe52b9560b06754cd890d515" allowfullscreen="" frameborder="0" height="106" width="680" title="" class="t u v tr aj" scrolling="auto" style="box-sizing: inherit; position: absolute; top: 0px; left: 0px; width: 680px; height: 105.99px;"></iframe>

O exemplo utilizado neste tutorial, com todos os arquivos estruturados e a estrutura de pastas, está disponível no Github pelo seguinte link:

[caiocarneloz/pacotepypiExample of PyPI package. Dependencies You need Python 3.6 or later to use pacotepypi. You can find it at python.org…github.com](https://github.com/caiocarneloz/pacotepypi.git)

# 8. Referências

[Packaging Python Projects - Python Packaging User GuideThis tutorial walks you through how to package a simple Python project. It will show you how to add the necessary files…packaging.python.org](https://packaging.python.org/tutorials/packaging-projects/)

[Using TestPyPI - Python Packaging User GuideTestPyPI is a separate instance of the Python Package Index (PyPI) that allows you to try out the distribution tools…packaging.python.org](https://packaging.python.org/guides/using-testpypi/)

[How to upload your python package to PyPiThe PyPi package index is one of the properties that makes python so powerfull: With just a simple command, you get…medium.com](https://medium.com/@joel.barmettler/how-to-upload-your-python-package-to-pypi-65edc5fe9c56)

[Data Hackers](https://medium.com/data-hackers?source=post_sidebar--------------------------post_sidebar--------------)