<p align=center>
  <br>
  <a href="https://sherlock-project.github.io/" target="_blank"><img src="https://user-images.githubusercontent.com/27065646/53551960-ae4dff80-3b3a-11e9-9075-cef786c69364.png"/></a>
  <br>
  <span>Cace contas em redes sociais através de nomes de usuário em <a href="https://github.com/sherlock-project/sherlock/blob/master/sites.md">Redes Sociais</a></span>
  <br>
  <a target="_blank" href="https://www.python.org/downloads/" title="Python version"><img src="https://img.shields.io/badge/python-%3E=_3.6-green.svg"></a>
  <a target="_blank" href="LICENSE" title="License: MIT"><img src="https://img.shields.io/badge/License-MIT-blue.svg"></a>
  <a target="_blank" href="https://github.com/sherlock-project/sherlock/actions" title="Test Status"><img src="https://github.com/sherlock-project/sherlock/workflows/Tests/badge.svg?branch=master"></a>
  <a target="_blank" href="https://github.com/sherlock-project/sherlock/actions" title="Nightly Tests"><img src="https://github.com/sherlock-project/sherlock/workflows/Nightly/badge.svg?branch=master"></a>
  <a target="_blank" href="https://twitter.com/intent/tweet?text=%F0%9F%94%8E%20Find%20usernames%20across%20social%20networks%20&url=https://github.com/sherlock-project/sherlock&hashtags=hacking,%20osint,%20bugbounty,%20reconnaissance" title="Share on Twitter"><img src="https://img.shields.io/twitter/url/http/shields.io.svg?style=social"></a>
  <a target="_blank" href="http://sherlock-project.github.io/"><img alt="Website" src="https://img.shields.io/website-up-down-green-red/http/sherlock-project.github.io/..svg"></a>
  <a target="_blank" href="https://hub.docker.com/r/theyahya/sherlock"><img alt="docker image" src="https://img.shields.io/docker/v/theyahya/sherlock"></a>
</p>

<p align="center">
  <a href="#installation">Instalação</a>
  &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#usage">Usabilidade</a>
  &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#docker-notes">Sobre o Docker</a>
  &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#contributing">Contribuições</a>
</p>

<p align="center">
<a href="https://asciinema.org/a/223115">
<img src="./images/sherlock_demo.gif"/>
</a>
</p>


## Instalação

```console
# clone o repositório
$ git clone https://github.com/sherlock-project/sherlock.git

# mude para o diretório do sherlock
$ cd sherlock

# instale os pacotes requeridos pelo projeto
$ python3 -m pip install -r requirements.txt
```

## Usabilidade

```console
$ python3 sherlock --help
usage: sherlock [-h] [--version] [--verbose] [--folderoutput FOLDEROUTPUT]
                [--output OUTPUT] [--tor] [--unique-tor] [--csv]
                [--site SITE_NAME] [--proxy PROXY_URL] [--json JSON_FILE]
                [--timeout TIMEOUT] [--print-all] [--print-found] [--no-color]
                [--browse] [--local]
                USERNAMES [USERNAMES ...]

Sherlock: Find Usernames Across Social Networks (Version 0.14.2)

positional arguments:
  USERNAMES             One or more usernames to check with social networks.
                        Check similar usernames using {%} (replace to '_', '-', '.').

optional arguments:
  -h, --help            show this help message and exit
  --version             Display version information and dependencies.
  --verbose, -v, -d, --debug
                        Display extra debugging information and metrics.
  --folderoutput FOLDEROUTPUT, -fo FOLDEROUTPUT
                        If using multiple usernames, the output of the results will be
                        saved to this folder.
  --output OUTPUT, -o OUTPUT
                        If using single username, the output of the result will be saved
                        to this file.
  --tor, -t             Make requests over Tor; increases runtime; requires Tor to be
                        installed and in system path.
  --unique-tor, -u      Make requests over Tor with new Tor circuit after each request;
                        increases runtime; requires Tor to be installed and in system
                        path.
  --csv                 Create Comma-Separated Values (CSV) File.
  --xlsx                Create the standard file for the modern Microsoft Excel
                        spreadsheet (xslx).
  --site SITE_NAME      Limit analysis to just the listed sites. Add multiple options to
                        specify more than one site.
  --proxy PROXY_URL, -p PROXY_URL
                        Make requests over a proxy. e.g. socks5://127.0.0.1:1080
  --json JSON_FILE, -j JSON_FILE
                        Load data from a JSON file or an online, valid, JSON file.
  --timeout TIMEOUT     Time (in seconds) to wait for response to requests (Default: 60)
  --print-all           Output sites where the username was not found.
  --print-found         Output sites where the username was found.
  --no-color            Don't color terminal output
  --browse, -b          Browse to all results on default browser.
  --local, -l           Force the use of the local data.json file.
```

Para procurar por um usuário apenas:
```
python3 sherlock user123
```

Para procurar por mais de um usuário:
```
python3 sherlock user1 user2 user3
```

Contas encontradas serão guardadas em um arquivo de texto separado com o nome de usuário correspondente (ex: ```user123.txt```).

## Sobre o Anaconda (Windows)

Se você está usando o Anaconda no Windows, rodar com 'python3' pode não funcionar. Use 'python' no
lugar.

## Sobre o Docker

Caso o docker esteja instalado, você pode realizar a build de uma imagem e rodá-la em um container.

```
docker build -t minha-imagem-sherlock .
```

Uma vez que a imagem está pronta, o sherlock pode ser invocado da seguinte forma:

```
docker run --rm -t minha-imagem-sherlock user123
```

A flag opcional ```--rm```  remove o container do seu sistema por completo, para prevenir de imagens antigas e obsoletas. Veja: https://docs.docker.com/engine/reference/run/#clean-up---rm

A flag opcional ```-t``` aloca um pseudo-TTY, o que permite ter cores no output do terminal. Veja: https://docs.docker.com/engine/reference/run/#foreground

Use o comando a seguir para acessar os resultados salvos:

```
docker run --rm -t -v "$PWD/results:/opt/sherlock/results" minha-imagem-sherlock -o /opt/sherlock/results/text.txt user123
```

A opção dada por ```-v "$PWD/results:/opt/sherlock/results"``` diz para o docker criar (ou usar) a pasta `results` no presente diretório e para montá-lo em `/opt/sherlock/results` dentro do container docker.
A opção `-o /opt/sherlock/results/text.txt` diz para o `sherlock` imprimir os resultados no arquivo de texto.

Ou você pode usar o "Docker Hub" para rodar o `sherlock`:

```
docker run theyahya/sherlock user123
```

### Usando `docker-compose`

Você pode utilizar o arquivo `docker-compose.yml` do próprio repositório e rodar este comando:

```
docker-compose run sherlock -o /opt/sherlock/results/text.txt user123
```

## Contribuindo
Nós amaríamos em ter sua contribuição no desenvolvimento para o Sherlock. Toda e cada contribuição é super valorizada!

Aqui estão algumas coisas que apreciaríamos em ter sua ajuda com:
- Adição do suporte a novos sites ¹
- Trazer de volta o suporte a [sites que foram removidos](removed_sites.md) no passado, devido a falsos positivos

[1] Por favor dê uma olhada na página da nossa Wiki sobre [adicionar novos sites](https://github.com/sherlock-project/sherlock/wiki/Adding-Sites-To-Sherlock)
para entender os problemas.

## Testes

Obrigado por contribuir com o projeto Sherlock!

Antes de criar uma Pull Request com o seu código a ser contribuído, por favor rode os testes 
localmente para garantir que tudo está funcionando corretamente. Além disso, seria uma ótima ideia 
rodar os testes também antes de começar o seu desenvolvimento, para distinguir os problemas 
pré-existentes do Sherlock, dos seus problemas.

Segue o exemplo a seguir de como rodar todos os testes do Sherlock localmente. Essa invocação esconde 
o texto de progresso que normalmente é printado no terminal pelo Sherlock e, ao invés, o output dos 
testes é printado de forma verbosa.

```
$ cd sherlock/sherlock
$ python3 -m unittest tests.all --verbose
```

Nota-se que temos atualmente uma cobertura de 100% dos testes existentes. Infelizmente, alguns dos
sites que o Sherlock checa, nem sempre estão disponíveis, então é comum ter problemas de resposta. 
Qualquer problema de conexão aparecerá como warnings no output dos testes, ao invés de erros reais.

Se alguns sites estiverem falhando por conta de problemas de conexão (o site caiu ou não existe mais, 
está em manutenção, etc), você pode excluí-los dos testes criando um arquivo `tests/.excluded_sites` 
com a lista dos sites a serem ignorados (um site por linha).

## Stargazers pelo tempo

[![Stargazers over time](https://starchart.cc/sherlock-project/sherlock.svg)](https://starchart.cc/sherlock-project/sherlock)

## Licença

MIT © Sherlock Project<br/>
Criador Original - [Siddharth Dushantha](https://github.com/sdushantha)
