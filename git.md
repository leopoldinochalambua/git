# - LINKS
https://www.codigofonte.com.br/artigos/top-25-comandos-do-git
https://www.hostinger.com.br/tutoriais/comandos-basicos-de-git

Controle de versão
----------------------------
* - Introdução
* - Exemplo de plataformas
* - Plataformas de Hospedagens
 
O que é "controle de versão
---------------------------
Controle de versão é um sistema que registra alterações em um arquivo ou conjunto de arquivos ao longo do tempo para, que você possa lembrar versões específicas mais tarde. Para os exemplos neste livro você irá utilizar o código-fonte de software com arquivos que possuam controle de versão, embora na realidade você possa fazer isso com quase qualquer tipo de arquivo em um computador.

Porque eu deveria me importar?
------------------------------
Se você é um designer gráfico ou web designer e quer manter todas as versões de uma imagem ou layout (o que você certamente deveria querer), um sistema de controle de versão (VCS) é a coisa correta a ser usada. Ele permite que você reverta para estado anterior determinados arquivos ou um projeto inteiro, compare as mudanças ao longo do tempo, veja quem modificou pela última vez algo que pode estar causando um problema, quem introduziu um problema, quando, e muito mais. Usar um VCS também significa que se você estragar tudo ou perder arquivos, você pode facilmente recuperar. Além disso, você tem tudo isso com muito pouco trabalho.

Plataformas
* - Subversion
* - git (A mais popular)

Plataformas de hospedagem
* - Bibuucket
* - SourceForge
* - GitLab
* - GitHub
	* - Gratuito
	* - Famoso por projetos Open Source

Uma Breve História do Git
-------------------------
Como muitas coisas na vida, o Git começou com um pouco de destruição criativa e uma ardente controvérsia.

O núcleo (kernel) do Linux é um projeto de código aberto com um escopo bastante grande. A maior parte da vida da manutenção do núcleo o Linux (1991-2002), as mudanças no código eram compartilhadas como correções e arquivos. Em 2002, o projeto do núcleo do Linux começou usar uma DVCS proprietária chamada BitKeeper.

Em 2005, a relação entre a comunidade que desenvolveu o núcleo do Linux e a empresa que desenvolveu BitKeeper quebrou em pedaços, e a ferramenta passou a ser paga. Isto alertou a comunidade que desenvolvia o Linux (e especialmente Linus Torvalds, o criador do Linux) a desenvolver a sua própria ferramenta baseada em lições aprendidas ao usar o BitKeeper. Algumas metas do novo sistema era os seguintes:

* - Velocidade
* - Projeto simples
* - Forte suporte para desenvolvimento não-linear (milhares de ramos paralelos)
* - Completamente distribuído
* - Capaz de lidar com projetos grandes como o núcleo o Linux com eficiência (velocidade e tamanho dos dados)

Desde seu nascimento em 2005, Git evoluiu e amadureceu para ser fácil de usar e ainda reter essas qualidades iniciais. Ele é incrivelmente rápido, é muito eficiente com projetos grandes, e ele tem um incrível sistema de ramos para desenvolvimento não linear.

O Básico do Git
---------------
Então, em poucas palavras, o que é o Git ? Esta é uma parte que é importante aprender, porque se você entender o que o Git é e os fundamentos de como ele funciona, em seguida, provavelmente usar efetivamente o Git será muito mais fácil para você. Enquanto você estiver aprendendo sobre o Git, tente esquecer das coisas que você pode saber sobre outros VCSs, como Subversion e Perforce; isso vai ajudá-lo a evitar a confusão sutil ao usar a ferramenta. O Git armazena e vê informações de forma muito diferente do que esses outros sistemas, mesmo que a interface do usuário seja bem semelhante, e entender essas diferenças o ajudará a não ficar confuso. 

Os Três Estados do git
----------------------
Agora, preste atenção. Esta é a principal coisa a lembrar sobre Git se você quiser que o resto do seu processo de aprendizagem ocorra sem problemas. O Git tem três estados principais que seus arquivos podem estar: committed, modificado (modified) e preparado (staged). Committed significa que os dados estão armazenados de forma segura em seu banco de dados local. Modificado significa que você alterou o arquivo, mas ainda não fez o commit no seu banco de dados. Preparado significa que você marcou a versão atual de um arquivo modificado para fazer parte de seu próximo commit.

Isso nos leva a três seções principais de um projeto Git: o diretório Git, o diretório de trabalho e área de preparo.

* - O diretório Git é onde o Git armazena os metadados e o banco de dados de objetos de seu projeto. Esta é a parte mais importante do Git, e é o que é copiado quando você clona um repositório de outro computador.

paulo@lpc:git$ cd .git/
paulo@lpc:.git$ ls 
branches  description  HEAD   index  logs     ORIG_HEAD    refs
config    FETCH_HEAD   hooks  info   objects  packed-refs
paulo@lpc:.git$ 

* - O diretório de trabalho é uma simples cópia de uma versão do projeto. Esses arquivos são pegos do banco de dados compactado no diretório Git e colocados no disco para você usar ou modificar.

* - A área de preparo é um arquivo, geralmente contido em seu diretório Git, que armazena informações sobre o que vai entrar em seu próximo commit. É por vezes referido como o “índice”, mas também é comum referir-se a ele como área de preparo (staging area).

O fluxo de trabalho básico Git é algo assim:
--------------------------------------------
* - Você modifica arquivos no seu diretório de trabalho.
* - Você prepara os arquivos, adicionando imagens deles à sua área de preparo.
* - Você faz commit, o que leva os arquivos como eles estão na área de preparo e armazena essa imagens de forma permanente para o diretório do Git.

Se uma versão específica de um arquivo está no diretório Git, é considerado commited. Se for modificado, mas foi adicionado à área de preparo, é considerado preparado. E se ele for alterado depois de ter sido carregado, mas não foi preparado, ele é considerado modificado. Em [ch02-git-basics], você vai aprender mais sobre esses estados e como você pode tirar proveito deles ou pular a parte de preparação inteiramente.

A Linha de Comando
Existem várias formas diferentes de usar o Git. Existem as ferramentas originais de linha de comando, e existem várias de interfaces gráficas de usuário (GUI - Graphical User Interface) com opções variadas. Para este material, nós usaremos o Git na linha de comando. 

A linha de comando é o único lugar onde você pode rodar todos os comandos do Git - a maioria das GUI implementa somente um subconjunto das funcionalidades do Git. Se você sabe como usar o Git na linha de comando, você provavelmente descobrirá como rodar versões GUI, enquanto o oposto não é necessariamente verdade. Além disso, enquanto a sua escolha da interface gráfica é uma questão de gosto pessoal, todos os usuário terão as ferramentas de linha de comando instaladas e disponíveis.

Então, nós esperamos que você saiba como abrir um Terminal no Mac, ou Linha de Comando ou Powershell no Windows. 

Instalando o Git
----------------
Antes de começar a usar o Git, você tem que torná-lo disponível em seu computador. Mesmo se ele já tiver sido instalado, é provavelmente uma boa idéia atualizar para a versão mais recente. Você pode instalá-lo como um pacote ou através de outro instalador, ou baixar o código fonte e compilá-lo.

:~# apt install git
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
git is already the newest version (1:2.39.2-1.1).
0 upgraded, 0 newly installed, 0 to remove and 3 not upgraded.

Configuração Inicial do Git
---------------------------
Agora que você tem o Git em seu sistema, você deve fazer algumas coisas para personalizar o ambiente Git. Você fará isso apenas uma vez por computador e o efeito se manterá após atualizações. Você também pode mudá-las em qualquer momento rodando esses comandos novamente.

O Git vem com uma ferramenta chamada [git config] que permite ver e atribuir variáveis de configuração que controlam todos os aspectos de como o Git aparece e opera. Estas variáveis podem ser armazenadas em três lugares diferentes:

* - /etc/gitconfig: válido para todos os usuários no sistema e todos os seus repositórios. Se você passar a opção --system para git config, ele lê e escreve neste arquivo.
* - ~/.gitconfig ou ~/.config/git/config: Somente para o seu usuário. Você pode fazer o Git ler e escrever neste arquivo passando a opção --global.
* - config no diretório Git (ou seja, .git/config) de qualquer repositório que você esteja usando: específico para este repositório.

Cada nível sobrescreve os valores no nível anterior, ou seja, valores em .git/config prevalecem sobre /etc/gitconfig.

No Windows, Git procura pelo arquivo .gitconfig no diretório $HOME (C:\Users\$USER para a maioria). Ele também procura por /etc/gitconfig, mesmo sendo relativo à raiz do sistema, que é onde quer que você tenha instalado Git no seu sistema.

Sua Identidade
--------------
A primeira coisa que você deve fazer ao instalar Git é configurar seu nome de usuário e endereço de e-mail. Isto é importante porque cada commit usa esta informação, e ela é carimbada de forma imutável nos commits que você começa a criar:

$ git config --global user.name "Fulano_de_Tal"
$ git config --global user.email fulanodetal@exemplo.com

Reiterando, você precisará fazer isso somente uma vez se tiver usado a opção [--global], porque então o Git usará esta informação para qualquer coisa que você fizer naquele sistema. Se você quiser substituir essa informação com nome diferente para um projeto específico, você pode rodar o comando sem a opção [--global] dentro daquele projeto.

Muitas ferramentas GUI o ajudarão com isso quando forem usadas pela primeira vez.

Seu Editor
-----------
Agora que a sua identidade está configurada, você pode escolher o editor de texto padrão que será chamado quando Git precisar que você entre uma mensagem. Se não for configurado, o Git usará o editor padrão, que normalmente é o Vim. Se você quiser usar um editor de texto diferente, como o Emacs, você pode fazer o seguinte:

$ git config --global core.editor emacs

Warning
Vim e Emacs são editores de texto populares comumente usados por desenvolvedores em sistemas baseados em Unix como Linux e Max. Se você não for acostumado com estes editores ou estiver em um sistema Windows, você precisará procurar por instruções de como configurar o seu editor preferido com Git. Se você não configurar o seu editor preferido e não sabe usar o Vim ou Emacs, é provável que você fique bastante confuso ao entrar neles.

Testando Suas Configurações
---------------------------
Se você quiser testar as suas configurações, você pode usar o comando git config --list para listar todas as configurações que o Git conseguir encontrar naquele momento:

:~$ git config --list 
user.name=leopoldinopaulo
user.email=leopaulo227@hotmail.com
core.editor=geany

Pedindo Ajuda
-------------
Se você precisar de ajuda para usar o Git, há três formas de acessar a página do manual de ajuda (manpage) para qualquer um dos comandos Git:

$ git help <verb>
$ git <verb> --help
$ man git-<verb>

Por exemplo, você pode ver a manpage do commando config rodando

$ git help config

Estes comandos podem ser acessados de qualquer lugar, mesmo desconectado. Se as manpages e este livro não forem suficientes e você precisar de ajuda personalizada, você pode tentar os canais #git ou #github no servidor IRC Freenode (irc.freenode.net). Estes canais estão sempre cheios com centenas de pessoas que são bem versadas com o Git e dispostas a ajudar.

Termos importantes e Monitoramento
----------------------------------
Diretório de trabalho corrente (WORKING DIRECTORY)
	* - Arquivos alterados e salvos localmennte
Alterações elencadas para commit (STAGED snapshot)
	* - Arquivos alterados que não estão elecados (controlados) para o commit
Historico de alterações publicadas (commit history)
	* - Alterações em códigos-fote que já foram publicadas no repositório
	* - É possível trabalhar tanto no repositório local, como nos repositórios remotos

Principais comandos básicos do git
----------------------------------
config --> Altera as configurações do git na maquina local. Esse comando é fundamental para configurar sua identidade de usuário, inserindo informações como nome e email que serão empregadas em cada commit.
* - $ git config –global user.name “Seu nome”
* - $ git config –global user.email “Seu email”

init ----> Esse é o comando que você irá utilizar para criar um novo projeto de git. O comando irá criar um repositório novo em branco e, a partir daí, será possível armazenar seu código fonte, alterar, salvaguardar alterações etc.

clone ---> Cria uma cópia exata de um repositório existente em um novo diretório

add -----> Rastreia e adiciona arquivos e mudanças, sejam arquivos novos ou arquivos anteriores que foram alterados. Oferece diferentes possibilidades de sintaxe.
* - $ git add seu_arquivo (esse comando irá adicionar um arquivo em específico ao repositório)
* - $ git add * (esse comando irá adicionar todos os arquivos novos e/ou modificados ao repositório)

commit --> É fundamental se estabelecer uma diferença entre git add e git 
* - git add adiciona seus arquivos modificados à fila para serem submetidos a um commit posteriormente. Os arquivos não passaram por um commit.
* - O git commit executa o commit dos arquivos que foram adicionados e cria uma nova revisão com um log. Por outro lado, se você não adicionar nenhum arquivo, o git não fará o commit de nada.
É possível combinar as duas ações em um único comando: $ git commit -a.

Também é possível adicionar uma mensagem para a execução de um commit. Exemplo:
$ git commit -m “seu comentário”

status --> Mostra se o ficheiro esta sob o controle do git ou não
branch --> A grosso modo, um branch é um caminho independente de desenvolvimento, uma alternativa. A princípio pode parecer fácil se perder em diversos caminhos, mas o comando git branch facilita o gerenciamento de tudo isso. Com diferentes parâmetros, é possível listar, criar ou apagar os branches.

Exemplos:
$ git branch (lista todas as ramificações)
$ git branch <nome_do_branch> (cria um branch com o nome especificado)
$ git branch -d <nome_do_branch> (deleta o branch com o nome especificado)

git checkout
Ainda sobre branches, esse comando Git pode ser utilizado para trocar de uma ramificação para outra.

Exemplo:
$ git checkout <nome_do_branch>

Também é possível combinar operações, criando e fazendo o checkout de um novo branch com um único comando:
$ git checkout -b <nome_do_branch_novo>

Comandos intermediários do git
------------------------------
git remote
O comando Git remote estabelece uma conexão entre seu repositório local e um repositório remoto.

Exemplo:
$ git remote add <nomecurto> <url>

push ----> Esse comando serve para subir suas modificações para um repositório remoto conectado anteriormente com git remote.
Exemplo:
* - $ git push -u <nome_curto> <nome_do_branch>

fetch ---> Baixar as mudanças criadas por outros membros do seu projeto colaborativo.
Exemplo:
* - $ git fetch

pull ----> baixa o conteúdo (não os metadados) do que foi alterado no repositório remoto para o seu repositório local e imediatamente atualiza seu contreúdo para a última versão.
Exemplo:
* - $ git pull <URL>

stash ---> armazena temporariamente seus arquivos modificados em uma área chamada stash (“esconderijo”), sem interagir com os outros arquivos até ser necessário.
Exemplo:
$ git stash

Para listar todos os seus “esconderijos”, usamos:
$ git stash list

Quando for o momento de aplicar o conteúdo do stash a um branch, usamos o parâmetro “apply”:
$ git stash apply

show ----> detalhes específicos sobre um commit que o log não mostra.
Exemplo:
git show <hash_do_commit>

rm ------> Remove arquivos do seu diretório
Exemplo:
git rm <nome_do_arquivo>

help ----> Felizmente, o próprio Git tem o comando help para trazer ajuda diretamente no terminal.
Exemplo:
$ git help <nome_comando>

merge ---> integra as mudanças de dois branches diferentes em um único branch. Ele precisa ser iniciado a partir de um branch já selecionado, que será mesclado com outro, com o nome passado por parâmetro.
Exemplo:
$ git merge <nome_do_branch>

Comandos avançados do git
-------------------------
rebase ----> ele integra dois branches em um branch único. Porém, esse comando refaz o histórico de commits, tornando-o linear. É o mais indicado para consolidar
Exemplo:
$ git rebase <base>

pull –rebase ----> Essa é uma variação do comando pull mostrado anteriormente. A partir dessa instrução, o Git irá fazer um rebase (não um merge) depois de se utilizar um comando pull.
Exemplo:
$ git pull –rebase

cherry-pick -----> Esse é um comando poderoso que permite selecionar qualquer commit específico de um brach e aplicá-lo a outro branch, sem precisar de uma mescla completa. A operação fica adicionada no histórico.
Exemplo:
$ git cherry-pick <commit-hash>

archive ----> Esse comando Git combina múltiplos arquivos em um único arquivo, como se fosse um arquivo zipado. Esse pacote pode ser aberto depois e os arquivos contidos podem ser extraídos individualmente.
Exemplo:
$ git archive –format zip HEAD > archive-HEAD.zip

blame ----> O comando “dedo-duro”, blame ajuda a determinar qual usuário realizou qual mudança em um determinado arquivo.
Exemplo:
$ git blame <nome_do_arquivo>

tag ----> Tags são uma boa opção para marcar uma branch e evitar alteração, principalmente em releases públicos. Cria, lista, exclui ou verificar um objeto de tag assinado com GPG
Exemplo:
$ git tag -a v1.0.0

diff ----> comparar dois arquivos gits ou dois branches antes de passarem por um commit ou um push, é importante executar esse comando Git.

Exemplos:
comparando o repositório ativo com o repositório local: 
$ git diff HEAD <nome_do_arquivo>
comparando duas ramificações: 
$ git diff <branch de origem> <branch de destino>

git citool
Esse comando Git oferece uma alternativa gráfica ao commit.
Exemplo:
$ git citool

git whatchanged
Esse comando oferece informações de log, mas em formato raw.
Exemplo:
$ git whatchanged

reset ---> Redefinir o HEAD atual para o estado especificado
switch --> Mudar ramos
tag -----> Criar, listar, excluir ou verificar um objeto de tag assinado com GPG

Ao longo do material vamos ver em detalhes cada comando.


### Teoria do commit
--------------------
Adiciona apenas as mudanças "certas"
* Evita fazer um único commit de todo o código escrito
* Busca sempre commitar o que está relacionado a um pequeno módulo
* Muitos commits atrapalha equioe de produção

#### Controle de commits
git diff
git status
git add

Título: Mais conciso possível
* Se está com dificuldade de escrever é porque etsá grande
Corpo: Explicação mais detalhada
* Diferença entre antes e agora.
* Razão pela qual foi feita a mudança
* Informações, extras, cuidados alertas etc.

Não commita tudo
.gitignore: Muitos arquivos e artefatos do código não podem ser commited
.env: Bibliotecas/modulos que auxilia a esconder informações importantes

## Fluxo do comando commit
código
	|->git add
		    |->git commit	
				    |->git push
					       |->pull request
					
### Iniciando o um repositório
```
git$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
_Initialized empty Git repository in /home/xala/git/.git/_
```
## Oque são branches
Branches, ou ramos em português, é uma cópia das linhas de códigos de um softeware gerenciado por um sistema de controle de versão. A ramificação serve para ajudar as equipes de desenvolvimento a consertar bugs e inserir funções, separando o trabalho em andamento do código de teste e estável.

## Tipos de branches
Branch Main/Master
Principal branch, contém associadas a ela as versões de publicação para facilitar o acesso e a busca por versões mais antigas. Também entendemos que é o espelho do programa que está no ar, já que o último código dessa branch deve sempre estar em produção. Além do mais, a única maneira de interagir com essa branch é através de uma Hotfix ou de uma nova Release.

Branch Feature
Uma das branches temporárias e auxiliares do nosso fluxo, sendo a branch que contém uma nova funcionalidade específica para a nossa aplicação. Nela temos a convenção do nome feature/nome_do_recurso que será utilizada no nosso fluxo de trabalho. Não podemos esquecer que toda nova Feature começa e termina obrigatoriamente a partir da develop.

Branch Develop
É uma das principais branches e serve como uma linha com os últimos desenvolvimentos. Como visto na imagem, é uma cópia da branch principal contendo algumas funcionalidades que ainda não foram publicadas. Sendo assim, é a base para o desenvolvimento de novas features.

* Não se faz commits diretamente

Branch Release
Por fim, a branch de lançamento do nosso programa. Nela unimos o que está pronto em nossa branch de desenvolvimento e “jogamos” para a branch principal. No mais, é criado uma nova versão etiquetada no nosso projeto para que possamos ter um histórico completo do desenvolvimento.

Branch Hotfix
Também é uma branch auxiliar e temporária, utilizada quando ocorre algum problema no ambiente de produção no qual a correção deve ser feita imediatamente. Conseguimos com isso solucionar o erro e fazer a mesclagem da solução para as branches main/master e develop para que não ocorra a perda do nosso código.

###Diferença entre branch local e branch remoto

O branch local, como o próprio nome sugere, consiste em ramificações do código que apenas um desenvolvedor tem acesso, ficando disponível localmente em seu computador. Essa estratégia costuma ser adotada em projetos individuais.

O branch remoto, por outro lado, coloca as ramificações em um local que pode ser acessado remotamente por outros desenvolvedores. Dessa forma, é possível trabalhar em conjunto no mesmo projeto para agilizar a criação de novos recursos e melhorar a resolução de problemas.

## Prinicpais acções de git-branch:
-a, --all ----->  list both remote-tracking and local branches
-d, --delete -->  delete fully merged branch
-D ------------>  delete branch (even if not merged)
-m, --move ---->  move/rename a branch and its reflog
-M ------------>  move/rename a branch, even if target exists
-c, --copy ---->  copy a branch and its reflog
-C ------------>  copy a branch, even if target exists
-l, --list ---->  lista nomes de branch

## Git push
```
git$ git log --pretty=oneline
git$ git checkout -b "feature"
Switched to a new branch 'feature'
paulo@lpc:git$ git log --pretty=oneline
97dd777fda1534e6e03305bdb790ac84da7fefd8 (HEAD -> feature, origin/main, origin/HEAD, main) Update git.md
fed1b277d7a1f63b6d10eca440ea9e95fcbab657 Subindo o git.md
7adeff8bd56bfe3d901a20423b94d75e9d2c8472 Initial commit
```

git$ git commit -m "3º Trabalhando o sistema git na feature"
[feature 9c3b7a8] 3º Trabalhando o sistema git na feature
 2 files changed, 512 insertions(+), 67 deletions(-)
 mode change 100644 => 100755 git.md
 create mode 100644 git.old
paulo@lpc:git$ git status
On branch feature
nothing to commit, working tree clean

`git$ git push --set-upstream origin feature`
Esta linha sobe o código da maquina local para o github


Quando não há informações pessoais no git, qualquer acção pode geream erro como o descrito abaixo:

```
git$ git commit -m "3º Trabalhando o sistema git na feature"
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'paulo@lpc.(none)')
```





`Passos para monitorar o código no git:`
Criar o conteúdo
git add .
git status
git commit -m "Mensagem"

username: -->
token: ----->

`html5$ git push origin main --> Sobe o repositório de local para remoto`
Username for 'https://github.com': leopoldinopaulo
Password for 'https://leopoldinopaulo@github.com': 
Enumerating objects: 95, done.
Counting objects: 100% (95/95), done.
Delta compression using up to 2 threads
Compressing objects: 100% (91/91), done.
Writing objects: 100% (93/93), 5.51 MiB | 1.49 MiB/s, done.
Total 93 (delta 5), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (5/5), done.
To https://github.com/leopoldinochalambua/html5
   54d567a..face8f3  main -> main

`html5$ git pull origin main --> Atualiza o local com o remoto`
From https://github.com/leopoldinochalambua/html5
 * branch            main       -> FETCH_HEAD
Already up to date.

buscar objetos de download e referências de outro repositório
extraia o Fetch e integre-o a outro repositório ou branch local
cle	push Atualizar referências remotas junto com objetos associados

#########################
Adições e comites

git add -A ----------------> Prepara todos os arquivos para o comite
git commit -m "mensagem" --> É o método usado para que uma alteração seja preparada para ser enviada da origem git. O commmit deve ser acompanhado com uma comentário a dizer que alterações foram feitas junto com o commit.
git log -------------------> Mostra todos os comites feitos
Na informação do comando "git log", nos é informado um número de hashdo commite feito onde apenas os 7 primeiros digitos nos intereçam.

#####################
Modificações

Para revertermos um arquivo para um ponto anterior podemos usar o comando "git reset" com uma das três opções abaixo:
	* - "git reset --soft" -----> volta para o primeiro estado antes do comite e toda suas alterções.
	* - "git reset --mixed" ----> volta para o estado anterior, porem não estara preparado para o comite
	* - "git reset --hard" -----> Volta todos os arquivos  para o ponto zero. *Não recomendado para trabalhar emm equipe*

Para fazer um reset em um comite, deve ser informado o número de hash do comite que se pretende desfazer. Por exemplo "git rese --opção <hash>"

#######
Branchs --> Permite manter diferentes versões do sistema dentro de um projeto.

git brench -----------------> lista todos os banchs dentro de um projeto. O que estiver com um "*" este é o breach corrente.

git branch <novo_branch> ---> Esse comando cria um branch novo. Para trocar de branch usamos o comando abaixo:

git checkout <branch> ------> Caso haja mais de uma branch devemos usar "git branch" seguido do nome da branch que queremos mudar.

################
Commits e Locais

É possivel ver quais diferenças foram feitas num arquivo com o comando "git status", o comando "git dif" permite ver o que fpi alterado nos arquivos antes de fazer comite.


