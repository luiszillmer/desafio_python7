# Empacotamento e publicação de código Python

[Leave a Comment](https://acervolima.com/empacotamento-e-publicacao-de-codigo-python/#respond) / [Python](https://acervolima.com/category/python/) / By [Acervo Lima](https://acervolima.com/author/jack_sparrow/)

Se você tem codificado em python, mesmo por um tempo, você deve estar familiarizado com o conceito de ‘pip’ agora. É um sistema de gerenciamento de pacotes usado para instalar e gerenciar pacotes / bibliotecas de software escritos em Python.
Então, alguém pode perguntar onde todos esses pacotes / bibliotecas estão armazenados? É óbvio que deve haver um grande “repositório on-line” que armazena todo esse código. E a resposta a essa pergunta é [Python Package Index](https://pypi.python.org/pypi) (PyPI).

PyPI é o repositório oficial de software de terceiros para Python. No momento em que este artigo foi escrito, o PyPI já hospedava 95971 pacotes!
pip usa PyPI como fonte padrão para pacotes e suas dependências. Então, sempre que você digitar:

```
 pip install package_name
```

pip procurará esse pacote no PyPI e, se encontrado, fará o download e instalará o pacote em seu sistema local.

Neste artigo, demonstrarei como você pode publicar seu próprio pacote Python no PyPI para que seja instalável em uma linha e facilmente disponível para todos os outros usuários de Python online! Vou pegar o exemplo de um pacote de amostra e mostrar o processo completo. O pacote de exemplo está hospedado no [Github](https://github.com/nikhilkumarsingh/mygmap) .

**Etapa 1: prepare os scripts Python**





O primeiro passo é, obviamente, preparar seu programa Python (que você deseja publicar no PyPI)!

Pode ser qualquer script Python. Aqui, estou usando meu próprio script python, que **chamei de** ‘ **locator.py** ‘ (estou usando esse nome apenas para fins de referência. Sinta-se à vontade para salvar seus scripts Python com qualquer nome). Este arquivo está disponível [aqui](https://github.com/nikhilkumarsingh/mygmap/blob/master/geo/locator.py) .

**Etapa 2: Preparando a estrutura do diretório do pacote**

Este e o passo mais importante. Agora, temos que seguir alguma estrutura pré-definida para o diretório do nosso pacote.
Como referência, sinta-se à vontade para verificar o repositório Github do projeto de amostra que é usado neste tutorial. Você pode clonar este repositório e fazer algumas modificações para criar seu próprio pacote.

A estrutura do diretório deve ser assim:
![Preparando a estrutura do diretório do pacote](https://media.geeksforgeeks.org/wp-content/uploads/PackagingPython.png)

Ok, vamos discutir o que todos esses arquivos irão conter.

- setup.py:

   

  é o arquivo mais importante. É o arquivo onde vários aspectos do seu projeto são configurados. O principal recurso do setup.py é que ele contém uma função setup() global. Os argumentos de palavra-chave para esta função são como os detalhes específicos do seu projeto são definidos.

  Você precisará instalar estas

   

  ferramentas de configuração

   

  biblioteca usando pip:

  

  ```
  pip install setuptools
  ```

  É assim que meu **setup.py se** parece:

  

  

  

  *filter_none*

  

  *editar*
  *fechar*

  *play_arrow*

  *link*
  *brilho_4*
  *código*

  `from` `setuptools ``import` `setup` `with ``open``(``'DESCRIPTION.txt'``) as ``file``:`  `long_description ``=` `file``.read()`  `REQUIREMENTS ``=` `[``'requests'``]` `CLASSIFIERS ``=` `[`  `'Development Status :: 4 - Beta'``,`  `'Intended Audience :: Developers'``,`  `'Topic :: Internet'``,`  `'License :: OSI Approved :: MIT License'``,`  `'Programming Language :: Python'``,`  `'Programming Language :: Python :: 2'``,`  `'Programming Language :: Python :: 2.6'``,`  `'Programming Language :: Python :: 2.7'``,`  `'Programming Language :: Python :: 3'``,`  `'Programming Language :: Python :: 3.3'``,`  `'Programming Language :: Python :: 3.4'``,`  `'Programming Language :: Python :: 3.5'``,`  `]` `setup(name``=``'mygmap'``,`   `version``=``'1.0.0'``,`   `description``=``'A small wrapper around google maps api'``,`   `long_description``=``long_description,`   `url``=``'https://github.com/nikhilkumarsingh/mygmap'``,`   `author``=``'Nikhil Kumar Singh'``,`   `author_email``=``'nikhilksingh97@gmail.com'``,`   `license``=``'MIT'``,`   `packages``=``[``'geo'``],`   `classifiers``=``CLASSIFIERS,`   `install_requires``=``REQUIREMENTS,`   `keywords``=``'maps location address'`   `)`

  *chevron_right*

  

  ```
  
  ```

  *filter_none*

  

  ```
  
  ```

  Vamos ver o que os diferentes argumentos da função de configuração fazem:

  1. **nome** : É o nome do seu projeto. Seu pacote será listado com este nome no PyPI.
  2. **version** : É uma string na qual você pode especificar a versão atual do seu projeto.
     É totalmente sua escolha como você deseja definir o esquema da série de versões (Você pode usar ‘1.0’ ou ‘0.1’ ou mesmo ‘0.0.1’).
     Esta versão é exibida no PyPI para cada lançamento, se você publicar seu projeto. Cada vez que você faz upload de uma nova versão, você também terá que alterar este argumento.
  3. **descrição:** uma breve descrição do pacote. Você pode usar o argumento long_description para escrever descrições longas.
  4. **long_description:** Podemos usar rich text para melhor descrição de nossos arquivos. O formato de arquivo padrão é [reStructuredText](https://en.wikipedia.org/wiki/ReStructuredText) . Você pode dar uma olhada em [DESCRIPTION.txt](https://github.com/nikhilkumarsingh/mygmap/blob/master/DESCRIPTION.txt) para ter uma ideia da sintaxe.
  5. **url: o** URL da página inicial do seu projeto. Isso torna mais fácil para as pessoas acompanharem ou contribuírem com seu projeto.
  6. **autor, autor_email:** Detalhes sobre o autor
  7. **licença:** especifique o tipo de licença que você está usando.
  8. **classificadores:** é uma lista de strings na qual podemos especificar mais detalhes sobre nosso projeto, como seu status de desenvolvimento, tópico, licença e versões de Python com suporte para seu projeto. Você pode ver mais classificadores [aqui](https://pypi.python.org/pypi?%3Aaction=list_classifiers) .
  9. **install_requires:** pode ser usado para especificar quais bibliotecas de terceiros seu pacote precisa para rodar. Essas dependências serão instaladas pelo pip quando alguém instalar seu pacote.
  10. **palavras-chave:** Liste palavras-chave para descrever seu projeto.

- **DESCRIPTION.txt** : Este arquivo contém a longa descrição sobre nosso pacote para mostrar na página PyPI. Usamos o formato de arquivo reStructuredText aqui. Verifique o arquivo usado em nosso pacote [aqui](https://github.com/nikhilkumarsingh/mygmap/blob/master/DESCRIPTION.txt) .

- **LICENSE.txt** : É uma boa prática definir uma licença para o uso de seu projeto. Você pode usar qualquer um dos modelos disponíveis gratuitamente. Mais comumente usada é a licença do **MIT** .
  A licença que estou usando para este projeto está disponível [aqui](https://github.com/nikhilkumarsingh/mygmap/blob/master/LICENSE.txt) . (Você pode substituir o nome do autor para usar esta licença em seus projetos)

- **README.md** : Este arquivo não tem nada a ver com nosso pacote PyPI. Ele contém uma descrição a ser mostrada na página do Github. Você pode usá-lo para a página PyPI também, mas precisará de mais algumas modificações em nosso código. Por enquanto, vamos manter as coisas simples.

- **__init__.py** : O uso principal de __init__.py é inicializar um pacote Python.
  A inclusão deste arquivo em um diretório indica ao interpretador Python que o diretório deve ser tratado como um pacote Python.
  Você pode deixar este arquivo vazio.

**Etapa 3: Crie suas contas
**Agora, é hora de criar uma conta no [PyPI](https://pypi.python.org/pypi?%3Aaction=register_form) e [testar o PyPI](https://testpypi.python.org/pypi?%3Aaction=register_form) . Test PyPI é apenas um site de teste onde faremos o upload de nosso código primeiro para ver se tudo funciona corretamente ou não.

Depois de fazer as contas, crie este arquivo **.pypirc** no diretório inicial do seu sistema e insira os detalhes da conta.



```
[distutils]
index-servers =
  pypi
  mais pypitest
[pypi]
repository = https: //pypi.python.org/pypi
username = your_username
senha = sua_senha
[pypitest]
repository = https: //testpypi.python.org/pypi
username = your_username
senha = sua_senha
```



Nota *: Se você estiver em um sistema Windows, basta digitar **echo% USERPROFILE%** no prompt de comando para saber o diretório inicial do seu PC. Coloque o arquivo **.pypirc** lá.*

**Etapa 4: faça** **upload do pacote**

Finalmente, estamos prontos para carregar nosso pacote no PyPI!

- Em primeiro lugar, verificaremos se nosso pacote é instalado corretamente no Test PyPI.

  Abra o prompt de comando / terminal no diretório raiz do seu pacote.

  Execute isto no terminal:

  

  ```
  python setup.py register -r pypitest
  ```

  Isso tentará registrar seu pacote no servidor de teste do PyPI, apenas para certificar-se de que configurou tudo corretamente.

  Agora, execute isto:

  ```
  python setup.py sdist upload -r pypitest
  ```

  Você não deve obter nenhum erro e também deve ser capaz de ver sua biblioteca no [repositório PyPI de teste](https://testpypi.python.org/pypi) .

- Depois de fazer o upload com sucesso para o teste PyPI, execute as mesmas etapas, mas aponte para o servidor PyPI ativo.

  Para se registrar no PyPI, execute:

  

  

  

  ```
  python setup.py register -r pypi
  ```

  Então corra:

  ```
  python setup.py sdist upload -r pypi
  ```

E está tudo pronto! Seu pacote agora está publicamente disponível no PyPI e pode ser facilmente instalado por um simples comando pip!
O pacote que criamos usando este tutorial está disponível [aqui](https://pypi.python.org/pypi/mygmap/1.0.3) .

Basta digitar no terminal,

```
 pip install your_package_name
```

para verificar se o processo de instalação está sendo concluído com sucesso.
**
Referências:**

- http://peterdowns.com/posts/first-time-with-pypi.html
- https://packaging.python.org/distributing/