# Bibliotecas Python para Processamento de Imagens

Na aplicação do [pré-processamento de imagens](https://didatica.tech/visao-computacional-e-processamento-de-imagens/) as bibliotecas são fundamentais, **simplificando tarefas complexas, tornando o desenvolvimento mais ágil e os códigos mais rápidos em suas execuções.**

![OpenCV, Pillow e scikit-image](https://didatica.tech/wp-content/uploads/2020/10/image-5-1024x430.png)

### **Finalidade**

As bibliotecas de processamento de imagens surgiram com o mesmo objetivo das outras bibliotecas utilizadas para [machine learning](https://didatica.tech/o-que-e-machine-learning-aprendizado-de-maquina/). Para quem já trabalhou com [linguagem Python](https://didatica.tech/a-linguagem-python/), imagine quando se usa, por exemplo, um modelo de [regressão linear](https://didatica.tech/regressao-linear-com-linguagem-r/) – um dos primeiros [modelos](https://didatica.tech/o-que-e-um-modelo-de-machine-learning/) estudados no ramo: não é necessário [programar](https://didatica.tech/programacao-para-quem-nao-e-programador-como-aprender-com-facilidade/) do zero todo o [algoritmo](https://didatica.tech/algoritmos-de-machine-learning/) usando Python, mesmo que seja possível. A razão de não ser necessário fazer isso é porque **alguém já havia desenvolvido esse algoritmo**; ele já estava pronto porque alguém já sabia que o algoritmo de regressão linear seria usado muitas vezes. O que acontece é que se constrói uma vez esse algoritmo, se disponibiliza isso publicamente em forma de código aberto e, assim, as pessoas podem usá-lo.

Esse é o conceito, e isso é o que acontece aqui, também, no ramo do processamento de imagens: da mesma forma que existem bibliotecas específicas da linguagem Python, onde são utilizadas para algoritmos de machine learning, por exemplo, agora veremos bibliotecas que servem, basicamente, para usar funções prontas para fazermos **manipulações de imagens**.

Afinal, transformar uma imagem que está colorida (sendo que há três canais de cores RGB) para uma escala de cinza é uma coisa que será feita muitas vezes, então, por isso, alguém criou uma fórmula, um algoritmo que já está pronto para fazer isso para nós. Há várias funções prontas que podemos utilizar, apenas chamando-as e passando os parâmetros, e elas farão as mais diversas manipulações.

![Imagem Colorida e Imagem em Escala de Cinza](https://didatica.tech/wp-content/uploads/2020/10/Escala_de_cinza-1024x287.jpg)

### **OpenCV**

Em nosso curso [Redes Neurais, Deep Learning e Visão Computacional](https://didatica.tech/curso-redes-neurais-deep-learning-e-visao-computacional/) focamos na biblioteca do [OpenCV](https://opencv.org/), que é uma das mais completas de todas. Há várias bibliotecas que fazem manipulações de imagens, como **Scikit-image**, o **Pillow**, o **SimpleCV**, e muitas delas são complementares pois fazem funções que outras não fazem. **A OpenCV é uma das mais populares e mais completas, por isso dedicamos a maior parte do curso nela**.

Ao final também mostraremos, um pouco, como se usa o Pillow, que é até um pouco mais simples que o OpenCV, apesar de ser um pouco mais limitado; depois, em alguns momentos, quando falamos de um ou outro algoritmo, acabaremos usando alguma outra biblioteca como Scikit-image, mas focamos mais atentamente no OpenCV. Até porque não adianta ficar mergulhando com todos os detalhes de cada uma das bibliotecas, **sendo que muitas funções que uma usa a outra também faz de forma um pouco diferente**, com um código um pouco diferente, mas que acaba tendo o mesmo resultado.

### **Evolução das bibliotecas**

![Cores em movimento](https://didatica.tech/wp-content/uploads/2020/10/Movimento.jpg)

É importante destacar que, apesar de estarmos dando esse destaque para o OpenCV, **se, no futuro, em alguma aplicação específica, você precisar de alguma manipulação que o OpenCV não faz, poderá ser que uma das outras bibliotecas o façam**.

As **bibliotecas estão sempre em evolução**, e outra coisa importante de entender também é que hoje, quando começamos a usar as bibliotecas, elas possuem alguns recursos, mas amanhã elas já podem possuir outras funções extras ou reformulações das funções antigas, porque todas as bibliotecas estão em constante desenvolvimento.

O conceito de código aberto, de contribuição, é interessante por causa disso: qualquer pessoa pode contribuir, adicionar um pacote, disponibilizar para os demais desenvolvedores. Então, as bibliotecas vão ficando mais complexas, mais robustas e, por isso, **algumas soluções que não existiam hoje ou ontem, podem existir amanhã**. Isso vale não só para o OpenCV, mas, também, para outras bibliotecas.

![Gato ohando atentamente para uma borboleta](https://didatica.tech/wp-content/uploads/2020/10/Gato_atento.jpg)

### **Processamento de imagens na prática**

Conforme mencionamos, em [nossos cursos](https://didatica.tech/cursos-machine-learning-diferenciados-pela-didatica-aprendizado/) mostramos na prática, **de forma detalhada**, como utilizar as bibliotecas para processamento de imagens, assim como **toda a teoria e prática** das demais áreas da [inteligência artificial](https://didatica.tech/o-que-e-inteligencia-artificial/).

Não deixe de conferir, temos[ opções gratuitas e completas](https://didatica.tech/o-que-e-inteligencia-artificial/), **do básico ao avançado, com muita didática**, tanto em assuntos teóricos quanto nas aplicações práticas.