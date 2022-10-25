# Como Contribuir Para O Sherlock
Primeiramente, muto obrigado por ajudar!

Existem diversas maneiras de se contribuir. Aqui está um agrupamento de alto nível

## Adicionando Novos Sites

Por favor, veja a página da nossa Wiki 
[adding new sites](https://github.com/sherlock-project/sherlock/wiki/Adding-Sites-To-Sherlock) 
para entender os problemas.

Qualquer novos sites a serem adicionados precisam de um nome de usuário já existente e o nome de um
usuário não existente, sendo documentado nos dados do mesmo site. Isso permite que Testes de Regressão garantam que tudo está funcionando como esperado.

It is required that a contributor test any new sites by either running the full tests, or running
a site-specific query against the claimed and unclaimed usernames.

It is not required that a contributor run the 
[site_list.py](https://github.com/sherlock-project/sherlock/blob/master/site_list.py)
script.

If there are performance problems with a site (e.g. slow to respond, unreliable uptime, ...), then
the site may be removed from the list.  The 
[removed_sites.md](https://github.com/sherlock-project/sherlock/blob/master/removed_sites.md)
file contains sites that were included at one time in Sherlock, but had to be removed for
one reason or another.

## Adicionando Novas Funcionalidades

Por favor, garanta que o conteúdo da sua branch passe em todos os testes antes de submeter sua 
pull request.
