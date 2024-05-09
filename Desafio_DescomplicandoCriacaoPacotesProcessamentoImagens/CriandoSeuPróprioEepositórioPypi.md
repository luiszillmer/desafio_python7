# Criando seu próprio repositório do Pypi

Posted by [Cleber J Santos](https://www.simplesconsultoria.com.br/author/cleber) at 01/12/2009 12:25 | [Permalink](https://www.simplesconsultoria.com.br/blog/criando-seu-proprio-repositorio-do-pypi-1)

Filed under: [Python](https://www.simplesconsultoria.com.br/search?Subject=Python), [Produto](https://www.simplesconsultoria.com.br/search?Subject=Produto), [Desenvolvimento](https://www.simplesconsultoria.com.br/search?Subject=Desenvolvimento), [Plone Symposium](https://www.simplesconsultoria.com.br/search?Subject=Plone+Symposium), [ZOPE](https://www.simplesconsultoria.com.br/search?Subject=ZOPE), [Sprint](https://www.simplesconsultoria.com.br/search?Subject=Sprint), [Plone](https://www.simplesconsultoria.com.br/search?Subject=Plone)

<iframe id="twitter-widget-0" scrolling="no" frameborder="0" allowtransparency="true" allowfullscreen="true" class="twitter-share-button twitter-share-button-rendered twitter-tweet-button" title="Twitter Tweet Button" src="https://platform.twitter.com/widgets/tweet_button.21f942bb866c2823339b839747a0c50c.pt.html#dnt=false&amp;id=twitter-widget-0&amp;lang=pt&amp;original_referer=https%3A%2F%2Fwww.simplesconsultoria.com.br%2Fblog%2Fcriando-seu-proprio-repositorio-do-pypi-1&amp;size=m&amp;text=Criando%20seu%20pr%C3%B3prio%20reposit%C3%B3rio%20do%20Pypi&amp;time=1639171057659&amp;type=share&amp;url=https%3A%2F%2Fwww.simplesconsultoria.com.br%2Fblog%2Fcriando-seu-proprio-repositorio-do-pypi-1&amp;via=simplesconsult" style="position: absolute; visibility: hidden; width: 0px; height: 0px;"></iframe>

[Tweet](https://twitter.com/share) 

<iframe ng-non-bindable="" frameborder="0" hspace="0" marginheight="0" marginwidth="0" scrolling="no" tabindex="0" vspace="0" width="100%" id="I0_1639171032477" name="I0_1639171032477" src="https://apis.google.com/u/0/se/0/_/+1/fastbutton?usegapi=1&amp;size=medium&amp;origin=https%3A%2F%2Fwww.simplesconsultoria.com.br&amp;url=https%3A%2F%2Fwww.simplesconsultoria.com.br%2Fblog%2Fcriando-seu-proprio-repositorio-do-pypi-1&amp;gsrc=3p&amp;ic=1&amp;jsh=m%3B%2F_%2Fscs%2Fapps-static%2F_%2Fjs%2Fk%3Doz.gapi.pt_PT.sKW0KjkqEMc.O%2Fam%3DAQ%2Fd%3D1%2Frs%3DAGLTcCNKWoBYBzZxOr1oPygQJcgjo3xOuw%2Fm%3D__features__#_methods=onPlusOne%2C_ready%2C_close%2C_open%2C_resizeMe%2C_renderstart%2Concircled%2Cdrefresh%2Cerefresh&amp;id=I0_1639171032477&amp;_gfid=I0_1639171032477&amp;parent=https%3A%2F%2Fwww.simplesconsultoria.com.br&amp;pfname=&amp;rpctoken=32115691" data-gapiattached="true" style="position: absolute; top: -10000px; width: 450px; margin: 0px; border-style: none;"></iframe>





— filed under: [Python](https://www.simplesconsultoria.com.br/search?Subject%3Alist=Python), [Produto](https://www.simplesconsultoria.com.br/search?Subject%3Alist=Produto), [Desenvolvimento](https://www.simplesconsultoria.com.br/search?Subject%3Alist=Desenvolvimento), [Plone Symposium](https://www.simplesconsultoria.com.br/search?Subject%3Alist=Plone Symposium), [ZOPE](https://www.simplesconsultoria.com.br/search?Subject%3Alist=ZOPE), [Sprint](https://www.simplesconsultoria.com.br/search?Subject%3Alist=Sprint), [Plone](https://www.simplesconsultoria.com.br/search?Subject%3Alist=Plone)

É incrível como ainda me impressiona o fato de eventos como o Plone Symposium South America, realizado em São Paulo, pode nos render ainda mais aprendizado, fora as amizades e trocas de experiências é claro ;)

[![Criando seu próprio repositório do Pypi](https://www.simplesconsultoria.com.br/blog/criando-seu-proprio-repositorio-do-pypi-1/image_preview)](https://www.simplesconsultoria.com.br/blog/criando-seu-proprio-repositorio-do-pypi-1/image/image_view_fullscreen)



Em uma rápida conversa com os amigos [Daniel (@dvainsencher)](https://twitter.com/dvainsencher), [Leonardo (@macagua)](https://www.twitter.com/macagua) e [Pacheco (@lucmult)](https://www.twitter.com/lucmult), surgiu a necessidade de implementar um espelho (mirror) do Pypi internamente aqui na Simples já que iria-mos realizar o sprint.

Para essa brincadeira usei o pacote [**z3c.pypimirror**](https://pypi.python.org/pypi/z3c.pypimirror), que é um módulo para a construção de um espelho do PyPI, sua instalação é bem simples, estou partindo do princípio de que já temos uma versão de [Python 2.4](https://www.python.org/) ou superior + [setuptools](http://peak.telecommunity.com/dist/ez_setup.py), também será necessário que tenhamos pelo **5GB de espaço livre** para os pacotes, então façamos assim:



```
easy_install z3c.pypimirror
```


Depois disso temos que configurar nosso Pypi, para isso eu criei um usuário no sistema chamado pypimirror mas fica a critério, na home do usuário pypimirror é onde pretendo centralizar os pacotes logs e etc... Crie uma pasta de nome pacotes com o comando:



```
mkdir -p /home/pypimirror/pacotes
```


Esse será o diretório onde iremos manter nossos pacotes vindos do Pypi, os logs podemos manter ou em tmp ou ainda em **/home/pypimirror** eu os mantive em pypimirror mesmo, agora temos que criar o arquivo de configuração, eu o chamei de ***pypimirror.cfg***, ele terá o seguinte conteúdo.



```
[DEFAULT]
# the root folder of all mirrored packages.
# if necessary it will be created for you
mirror_file_path = /home/pypimirror/pacotes


# where's your mirror on the net?
base_url = http://pypi.seudominio.com.br


# lock file to avoid duplicate runs of the mirror script
lock_file_name = /home/pypimirror/pypi-poll-access.lock


# Pattern for package files, only those matching will be mirrored
filename_matches =
    *.zip
    *.tgz
    *.egg
    *.tar.gz
    *.tar.bz2


# Pattern for package names; only packages having matching names will
# be mirrored
package_matches =
   zope.*
   plone.*
   Products.*
   collective.*


# remove packages not on pypi (or externals) anymore
cleanup = True


# create index.html files
create_indexes = True


# be more verbose
verbose = True


# resolve download_url links on pypi which point to files and download
# the files from there (if they match filename_matches).
# The filename and filesize (from the download header) are used
# to find out if the file is already on the mirror. Not all servers
# support the content-length header, so be prepared to download
# a lot of data on each mirror update.
# This is highly experimental and shouldn't be used right now.
#
# NOTE: This option should only be set to True if package_matches is not
# set to '*' - otherwise you will mirror a huge amount of data. BE CAREFUL
# using this option!!!
external_links = False


# similar to 'external_links' but also follows an index page if no
# download links are available on the referenced download_url page
# of a given package.
#
# NOTE: This option should only be set to True if package_matches is not
# set to '*' - otherwise you will mirror a huge amount of data. BE CAREFUL
# using this option!!!
follow_external_index_pages = False


# logfile
log_filename = /home/pypimirror/pypimirror.log
```


Essa configuração é uma cópia do arquivo **pypimirror.cfg.sample** localizado em **$PYTHON/site-packages/z3c.pypimirror-1.0.14-py2.4.egg/z3c/pypimirror**, um detalhe importante durante a configuração é que em ***package_matches\***, estamos dizendo para baixar apenas pacotes zope, plone, Products e collective, sendo assim o próprio pacote z3c.pypimirror por exemplo ficaria fora, então para pegar todo e qualquer pacote do Pypi você pode comentar as linhas e deixar como abaixo:



```
package_matches =
#   zope.*
#   plone.*
#   Products.*
#   collective.*
   *.*
```


Agora que já temos nosso Pypi devidamente configurado, podemos automatizar o sync dos pacotes adicionando a seguinte linha no crontab



```
*/6 * * * * pypimirror /usr/bin/pypimirror /home/pypimirror/pypimirror.cfg --update-fetch
```


Chegamos ao final, agora você pode configurar seu Apache por exemplo apontando o ***DocumentRoot\*** para este diretório, não é necessário se preocupar em criar páginas como o index.html pois no arquivo de configuração acima estamos dizendo para que este seja criado automaticamente **(create_indexes = True)**, depois de tudo feito, você só necessita dizer no seu buildout que este é o servidor onde ele deverá buscar os pacotes:



```
[buildout]
index =  http://pypi.seudominio.com.br
...
```


Ou com o SetupTools você pode especificar o servidor de onde você deseja baixar o pacote, com o comando:

```
easy_install -i http://pypi.seudominio.com.br meupacote
```



