# CRIANDO SEU PRÓPRIO REPOSITÓRIO DO PYPI

É incrível como ainda me impressiona o fato de eventos como o Plone Symposium South America, realizado em São Paulo, pode nos render ainda mais aprendizado, fora as amizades e trocas de experiências é claro! ;)

Em uma rápida conversa com os amigos Daniel (@dvainsencher), Leonardo (@macagua) e Pacheco (@lucmult), surgiu a necessidade de implementar um espelho (mirror) do *Pypi* internamente na empresa que trabalho (Simples consultoria), já que iriamos realizar o sprint.

Para essa brincadeira usei o pacote *z3c.pypimirror*, que é um módulo para a construção de um espelho do PyPI. Sua instalação é bem simples, estou partindo do princípio de que já temos uma versão de Python 2.4 ou superior + setuptools. Também será necessário que tenhamos pelo 5GB de espaço livre para os pacotes. Então façamos assim:

**# easy_install z3c.pypimirror**

Depois disso temos que configurar nosso Pypi, para isso eu criei um usuário no sistema chamado *pypimirror*, mas fica a critério, na home do usuário pypimirror é onde pretendo centralizar os pacotes logs etc. Crie uma pasta de nome pacotes com o comando:

**# mkdir -p /home/pypimirror/pacotes**

Esse será o diretório onde iremos manter nossos pacotes vindos do Pypi, os logs podemos manter ou em tmp ou ainda em /home/pypimirror eu os mantive em pypimirror mesmo, agora temos que criar o arquivo de configuração, eu o chamei de pypimirror.cfg, ele terá o seguinte conteúdo.



[DEFAULT]
\# the root folder of all mirrored packages.
\# if necessary it will be created for you
mirror_file_path = /home/pypimirror/pacotes

\# where's your mirror on the net?
base_url = http://pypi.seudominio.com.br

\# lock file to avoid duplicate runs of the mirror script
lock_file_name = /home/pypimirror/pypi-poll-access.lock

\# Pattern for package files, only those matching will be mirrored
filename_matches =
  *.zip
  *.tgz
  *.egg
  *.tar.gz
  *.tar.bz2

\# Pattern for package names; only packages having matching names will
\# be mirrored
package_matches =
  zope.*
  plone.*
  Products.*
  collective.*

\# remove packages not on pypi (or externals) anymore
cleanup = True

\# create index.html files
create_indexes = True

\# be more verbose
verbose = True

\# resolve download_url links on pypi which point to files and download
\# the files from there (if they match filename_matches).
\# The filename and filesize (from the download header) are used
\# to find out if the file is already on the mirror. Not all servers
\# support the content-length header, so be prepared to download
\# a lot of data on each mirror update.
\# This is highly experimental and shouldn't be used right now.
\#
\# NOTE: This option should only be set to True if package_matches is not
\# set to '*' - otherwise you will mirror a huge amount of data. BE CAREFUL
\# using this option!!!
external_links = False

\# similar to 'external_links' but also follows an index page if no
\# download links are available on the referenced download_url page
\# of a given package.
\#
\# NOTE: This option should only be set to True if package_matches is not
\# set to '*' - otherwise you will mirror a huge amount of data. BE CAREFUL
\# using this option!!!
follow_external_index_pages = False

\# logfile
log_filename = /home/pypimirror/pypimirror.log


Essa configuração é uma cópia do arquivo pypimirror.cfg.sample, localizado em $PYTHON/site-packages/z3c.pypimirror-1.0.14-py2.4.egg/z3c/pypimirror. Um detalhe importante durante a configuração é que em package_matches, estamos dizendo para baixar apenas pacotes zope, plone, Products e collective, sendo assim o próprio pacote z3c.pypimirror por exemplo ficaria fora, então para pegar todo e qualquer pacote do Pypi você pode comentar as linhas e deixar como abaixo:



package_matches =
\#  zope.*
\#  plone.*
\#  Products.*
\#  collective.*
  *.*


Agora que já temos nosso Pypi devidamente configurado, podemos automatizar o sync dos pacotes adicionando a seguinte linha no crontab:



*/6 * * * * pypimirror /usr/bin/pypimirror /home/pypimirror/pypimirror.cfg --update-fetch


Chegamos ao final, agora você pode configurar seu Apache por exemplo apontando o DocumentRoot para este diretório, não é necessário se preocupar em criar páginas como o index.html, pois no arquivo de configuração acima estamos dizendo para que este seja criado automaticamente (create_indexes = True). Depois de tudo feito, você só necessita dizer no seu buildout que este é o servidor onde ele deverá buscar os pacotes:



[buildout]
index = http://pypi.seudominio.com.br
...


Ou com o SetupTools você pode especificar o servidor de onde você deseja baixar o pacote, com o comando:

**# easy_install -i http://pypi.seudominio.com.br meupacote**

Até a próxima!

Referência: http://www.cleberjsantos.com.br/pzp/criando-seu-proprio-repositorio-do-pypi
Publicado originalmente em: [http://www.simplesconsultoria.com.br](http://www.simplesconsultoria.com.br/)