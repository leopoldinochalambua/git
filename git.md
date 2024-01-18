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


