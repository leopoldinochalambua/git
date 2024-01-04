O que são ocntrole de versão
----------------------------
Controle de Versão

O que é "controle de versão", e porque eu deveria me importar?

Controle de versão é um sistema que registra alterações em um arquivo ou conjunto de arquivos ao longo do tempo para, que você possa lembrar versões específicas mais tarde. Para os exemplos neste livro você irá utilizar o código-fonte de software com arquivos que possuam controle de versão, embora na realidade você possa fazer isso com quase qualquer tipo de arquivo em um computador.

Se você é um designer gráfico ou web designer e quer manter todas as versões de uma imagem ou layout (o que você certamente deveria querer), um sistema de controle de versão (VCS) é a coisa correta a ser usada. Ele permite que você reverta para estado anterior determinados arquivos ou um projeto inteiro, compare as mudanças ao longo do tempo, veja quem modificou pela última vez algo que pode estar causando um problema, quem introduziu um problema, quando, e muito mais. Usar um VCS também significa que se você estragar tudo ou perder arquivos, você pode facilmente recuperar. Além disso, você tem tudo isso com muito pouco trabalho.

Uma Breve História do Git

Como muitas coisas na vida, o Git começou com um pouco de destruição criativa e uma ardente controvérsia.

O núcleo (kernel) do Linux é um projeto de código aberto com um escopo bastante grande. A maior parte da vida da manutenção do núcleo o Linux (1991-2002), as mudanças no código eram compartilhadas como correções e arquivos. Em 2002, o projeto do núcleo do Linux começou usar uma DVCS proprietária chamada BitKeeper.

Em 2005, a relação entre a comunidade que desenvolveu o núcleo do Linux e a empresa que desenvolveu BitKeeper quebrou em pedaços, e a ferramenta passou a ser paga. Isto alertou a comunidade que desenvolvia o Linux (e especialmente Linus Torvalds, o criador do Linux) a desenvolver a sua própria ferramenta baseada em lições aprendidas ao usar o BitKeeper. Algumas metas do novo sistema era os seguintes:

    Velocidade
    Projeto simples
    Forte suporte para desenvolvimento não-linear (milhares de ramos paralelos)
    Completamente distribuído
    Capaz de lidar com projetos grandes como o núcleo o Linux com eficiência (velocidade e tamanho dos dados)

Desde seu nascimento em 2005, Git evoluiu e amadureceu para ser fácil de usar e ainda reter essas qualidades iniciais. Ele é incrivelmente rápido, é muito eficiente com projetos grandes, e ele tem um incrível sistema de ramos para desenvolvimento não linear.

O Básico do Git
Então, em poucas palavras, o que é o Git ? Esta é uma parte que é importante aprender, porque se você entender o que o Git é e os fundamentos de como ele funciona, em seguida, provavelmente usar efetivamente o Git será muito mais fácil para você. Enquanto você estiver aprendendo sobre o Git, tente esquecer das coisas que você pode saber sobre outros VCSs, como Subversion e Perforce; isso vai ajudá-lo a evitar a confusão sutil ao usar a ferramenta. O Git armazena e vê informações de forma muito diferente do que esses outros sistemas, mesmo que a interface do usuário seja bem semelhante, e entender essas diferenças o ajudará a não ficar confuso. 

O diretório Git é onde o Git armazena os metadados e o banco de dados de objetos de seu projeto. Esta é a parte mais importante do Git, e é o que é copiado quando você clona um repositório de outro computador.

O diretório de trabalho é uma simples cópia de uma versão do projeto. Esses arquivos são pegos do banco de dados compactado no diretório Git e colocados no disco para você usar ou modificar.

A área de preparo é um arquivo, geralmente contido em seu diretório Git, que armazena informações sobre o que vai entrar em seu próximo commit. É por vezes referido como o “índice”, mas também é comum referir-se a ele como área de preparo (staging area).

O fluxo de trabalho básico Git é algo assim:

    Você modifica arquivos no seu diretório de trabalho.
    Você prepara os arquivos, adicionando imagens deles à sua área de preparo.
    Você faz commit, o que leva os arquivos como eles estão na área de preparo e armazena essa imagens de forma permanente para o diretório do Git.

Se uma versão específica de um arquivo está no diretório Git, é considerado commited. Se for modificado, mas foi adicionado à área de preparo, é considerado preparado. E se ele for alterado depois de ter sido carregado, mas não foi preparado, ele é considerado modificado. Em [ch02-git-basics], você vai aprender mais sobre esses estados e como você pode tirar proveito deles ou pular a parte de preparação inteiramente.

Configuração Inicial do Git

Agora que você tem o Git em seu sistema, você deve fazer algumas coisas para personalizar o ambiente Git. Você fará isso apenas uma vez por computador e o efeito se manterá após atualizações. Você também pode mudá-las em qualquer momento rodando esses comandos novamente.

O Git vem com uma ferramenta chamada git config que permite ver e atribuir variáveis de configuração que controlam todos os aspectos de como o Git aparece e opera. Estas variáveis podem ser armazenadas em três lugares diferentes:

    /etc/gitconfig: válido para todos os usuários no sistema e todos os seus repositórios. Se você passar a opção --system para git config, ele lê e escreve neste arquivo.

    ~/.gitconfig ou ~/.config/git/config: Somente para o seu usuário. Você pode fazer o Git ler e escrever neste arquivo passando a opção --global.

    config no diretório Git (ou seja, .git/config) de qualquer repositório que você esteja usando: específico para este repositório.

Cada nível sobrescreve os valores no nível anterior, ou seja, valores em .git/config prevalecem sobre /etc/gitconfig.

No Windows, Git procura pelo arquivo .gitconfig no diretório $HOME (C:\Users\$USER para a maioria). Ele também procura por /etc/gitconfig, mesmo sendo relativo à raiz do sistema, que é onde quer que você tenha instalado Git no seu sistema.
Sua Identidade

A primeira coisa que você deve fazer ao instalar Git é configurar seu nome de usuário e endereço de e-mail. Isto é importante porque cada commit usa esta informação, e ela é carimbada de forma imutável nos commits que você começa a criar:

$ git config --global user.name "Fulano de Tal"
$ git config --global user.email fulanodetal@exemplo.br

Reiterando, você precisará fazer isso somente uma vez se tiver usado a opção --global, porque então o Git usará esta informação para qualquer coisa que você fizer naquele sistema. Se você quiser substituir essa informação com nome diferente para um projeto específico, você pode rodar o comando sem a opção --global dentro daquele projeto.

Muitas ferramentas GUI o ajudarão com isso quando forem usadas pela primeira vez.
Seu Editor

Agora que a sua identidade está configurada, você pode escolher o editor de texto padrão que será chamado quando Git precisar que você entre uma mensagem. Se não for configurado, o Git usará o editor padrão, que normalmente é o Vim. Se você quiser usar um editor de texto diferente, como o Emacs, você pode fazer o seguinte:

$ git config --global core.editor emacs

Warning
Vim e Emacs são editores de texto populares comumente usados por desenvolvedores em sistemas baseados em Unix como Linux e Max. Se você não for acostumado com estes editores ou estiver em um sistema Windows, você precisará procurar por instruções de como configurar o seu editor preferido com Git. Se você não configurar o seu editor preferido e não sabe usar o Vim ou Emacs, é provável que você fique bastante confuso ao entrar neles.

Configurar Git com Visual Studio Code
-------------------------------------
Com o path do Code instalado, podemos iniciar a configuração do Git.
Agora, para definir o Visual Studio Code como seu editor padrão, digite esta linha de código na linha de comando:
git config --global core.editor 'code --wait'

Para finalizar, verificamos que tudo funciona corretamente, abrindo o arquivo de configuração do git digitando no terminal:
git config --global -e

    InícioBack-end

3 anos atrás
Visual Studio Code como editor de texto padrão do Git
visual studio code logo

Por que utilizar o Visual Studio Code como padrão do Git? Afinal de contas, o Git já utiliza o VIM como editor de texto no console.

Justamente por essa opção não permitir uma experiência otimizada para configuração e utilização do Git, simples assim.

Então veremos uma opção simples, mas que muitos desconhecem, que se refere a utilizar a interface gráfica do Visual Studio Code como editor default para a ferramenta de versionamento.
Conteúdo ocultar
1 O que é o Visual Studio Code?
2 O que é o Git?
3 Como configurar o VS Code como editor default do Git
3.1 Como corrigir os erros, caso ocorram?
3.2 Configurar Git com Visual Studio Code
4 Como definir o Visual Studio Code como seu difftool
O que é o Visual Studio Code?

Em 2015 foi lançado pela Microsoft um editor de código destinado ao desenvolvimento de aplicações web chamado de Visual Studio Code, ou VSCode.

Ele é um editor de código prático e dinâmico utilizado por desenvolvedores de todo o mundo para operações de desenvolvimento como depuração, execução de tarefas e controle de versão.

Ele é multiplataforma, funciona em Windows, macOS e Linux e com suporte para JavaScript, TypeScript e Node.js e muitas extensões para outras linguagens, como: C++, C#, Java, Python, PHP, Go entre outras.

O VSCode é como um canivete suíço, ele fornece as principais ferramentas e extensões para o dia a dia no trabalho como programador.

    Quer saber mais? Confira também quais as melhores extensões para o Visual Studio Code. 

O que é o Git?

O Git é o sistema de controle de versão mais usado no mundo atualmente.

É um projeto de código aberto maduro e com manutenção ativa desenvolvido em 2005 por Linus Torvalds, sim, o mesmo cara do Linux.
oqueégit

O Git nos ajuda a controlar o fluxo de novas funcionalidades entre vários programadores no mesmo projeto com ferramentas para análise e correção de problemas quando o mesmo arquivo é editado por mais de um desenvolvedor.

Um número expressivo de projetos de software em todo o mundo dependem do Git para controle de versão, incluindo projetos comerciais e opensource.

Os conceitos originais do Git eram fazer um sistema de controle de revisão distribuído mais rápido que desafiasse abertamente as convenções e práticas usadas no CVS.

É desenvolvido principalmente para Linux, claro, e tem como característica ser muito rápido, peer-to-peer, seguro, flexível e com uma árvore de histórico completo disponível off-line.

    Git, SVN e CVS — comparação das principais ferramentas de controle de versão de software.

Como configurar o VS Code como editor default do Git

Inicialmente, antes de configurarmos o git para utilizar o VSCode, devemos verificar se o Path do Code está corretamente instalado para o terminal.

Podemos fazer isso executando o comando code –help no terminal e se tudo funcionar corretamente, você poderá ver a lista de comandos que o Code tem disponível.
VS code com Git
Como corrigir os erros, caso ocorram?

Caso retorne a mensagem de comando não encontrado: erro de código. Deveremos proceder com a instalação do Path da seguinte maneira.

    Abra o Visual Studio Code.
    Abra a paleta de comandos, você pode fazer isso tocando na engrenagem no canto inferior esquerdo e selecione a opção da paleta de comandos ou com o atalho de teclado cmd + shift + p no MAC ou control + shift + p no Windows.

vscode-com-git-no-shell

    Na guia que foi aberta, digite o seguinte código> Shell Command: Install ‘code’ command in PATH.
    Pressione Enter e aguarde a instalação.

instalar-vscode-com-git

Tente novamente o comando code –help no terminal para verificar se tudo foi instalado corretamente.

Configurar Git com Visual Studio Code
Com o path do Code instalado, podemos iniciar a configuração do Git.

Agora, para definir o Visual Studio Code como seu editor padrão, digite esta linha de código na linha de comando:
git config --global core.editor 'code --wait'

Para finalizar, verificamos que tudo funciona corretamente, abrindo o arquivo de configuração do git digitando no terminal:
git config --global -e

visual-studio-code-com-git-conferir-se-funciona
E está lá!

Depois de definir o Visual Studio Code como seu editor padrão, com o comando git config –global -e, vai abrir o arquivo .gitconfig global no Visual Studio Code.

A propósito, o comando –wait mantém o shell até que o Visual Studio Code seja fechado.
O comportamento comum é retornar o acesso ao shell assim que o Código do Visual Studio for carregado.

O Git aguarda o sinal do shell para confirmar as alterações do arquivo temporário para o arquivo principal.

Testando Suas Configurações
Se você quiser testar as suas configurações, você pode usar o comando git config --list para listar todas as configurações que o Git conseguir encontrar naquele momento:

$ git config --list
user.name=Fulano de Tal
user.email=fulanodetal@exemplo.br
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...

Pode ser que algumas palavras chave apareçam mais de uma vez, porque Git lê as mesmas chaves de arquivos diferentes (/etc/gitconfig e ~/.gitconfig, por exemplo). Neste caso, Git usa o último valor para cada chave única que ele vê.

Você pode também testar o que Git tem em uma chave específica digitando git config <key>:

$ git config user.name
Fulano de Tal

Pedindo Ajuda
Se você precisar de ajuda para usar o Git, há três formas de acessar a página do manual de ajuda (manpage) para qualquer um dos comandos Git:

$ git help <verb>
$ git <verb> --help
$ man git-<verb>

Por exemplo, você pode ver a manpage do commando config rodando

$ git help config

Estes comandos podem ser acessados de qualquer lugar, mesmo desconectado. Se as manpages e este livro não forem suficientes e você precisar de ajuda personalizada, você pode tentar os canais #git ou #github no servidor IRC Freenode (irc.freenode.net). Estes canais estão sempre cheios com centenas de pessoas que são bem versadas com o Git e dispostas a ajudar.

Controle e monitoramento de estados
Diretório de trabalho corrente (WORKING DIRECTORY)
	* - Arquivos alterados e salvos localmennte
Alterações elencadas para commit (STAGED snapshot)
	* - Arquivos alterados que não estão elecados (controlados) para o commit
Historico de alterações publicadas (commit history)
	* - Alterações em códigos-fote que já foram publicadas no repositório
	* - É possível trabalhar tanto no repositório local, como nos remotos

Principais comandos git
---------------------------------------------------------------------------------------------
config ---> Altera as configurações do git na maquina local
clone ----> Clonar um repositório em um novo diretório
add ------> Rastreia e adiciona arquivos e mudanças
init -----> Crie um repositório Git vazio ou reinicialize um existente
branch ---> Listar, criar ou excluir filiais
commit ---> Registrar alterações no repositório
status --->
merge ----> Unir dois ou mais históricos de desenvolvimento
rebase ---> Reapply confirma em cima de outra dica base
reset ----> Redefinir o HEAD atual para o estado especificado
switch ---> Mudar ramos
tag ------> Criar, listar, excluir ou verificar um objeto de tag assinado com GPG
fetch ----> Download objects and refs from another repository
pull -----> Fetch from and integrate with another repository or a local branch
push -----> Update remote refs along with associated objects
diff ----->
log ------>
stash ---->


Os passos são:
git add .
git status
git commit -m "Mensagem"

username: -->
token: ----->

html5$ git push origin main --> Sobe u, repositório para remoto
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

html5$ git pull origin main --> Atualiza o local com o remoto
From https://github.com/leopoldinochalambua/html5
 * branch            main       -> FETCH_HEAD
Already up to date.





buscar objetos de download e referências de outro repositório
   extraia o Fetch e integre-o a outro repositório ou branch local
   push Atualizar referências remotas junto com objetos associados

############
Breansh --> são versões do sistema. O padrão tem o nome de master.
commit ---> É o método usado para que uma alteração seja preparada  ara ser enviada da origem git. O commmit deve ser acompanhado com uma comentário a dizer que alterações foram feitas junto com o commit.

#################
Adições e comites

git add -A ----------------> Prepara todos os arquivos para o comite
git commit -m "mensagem" --> Manda todos os arquivos para o git
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


