## boas práticas git
boas práticas git para pessoas e times.

### Básico

#### 1. Configure corretamente nome e e-mail
Para que seus commits não sejam gravados com autor “root” e-mail “root@root” configure esses valores iniciais assim que instalar seu GIT.

```shell
$ git config --global user.name "Nome Sobrenome"
$ git config --global user.email "email@domain.ext"
```

Pode acontecer de ter que mudar de e-mail dependendo do projeto, nesse caso rode isso dentro do diretório do seu projeto para sobrescrever as configurações globais

```shell
$ cd meu_projeto/
$ git config user.name "Nome Sobrenome"
$ git config user.email "email@domain.ext"
```

#### 2. Configure seu editor favorito globalmente
Eu gosto de usar o VIM e Code

```shell
 $ git config --global core.editor vim
 $ git config --global core.editor 'code --wait'
```

#### 3. Ative o autocorrect
O autocorrect vai te ajudar nos erros mais comuns, afinal quem nunca digitou git stats o branch né?

```shell
$ git config --global help.autocorrect 10
```
olhe um exemplo quando digitamos BRAMCH ao invés de BRANCH

```shell
$ git bramch
WARNING: You called a Git command named 'bramch', which does not exist.
Continuing in 1.0 seconds, assuming that you meant 'branch'.
dev
prod
* main
```

olhe um exemplo quando digitamo STATS ao invés de STATUS

 ```shell
 $ git stats
WARNING: You called a Git command named 'stats', which does not exist.
Continuing in 1.0 seconds, assuming that you meant 'status'.
On branch gh-pages
nothing to commit, working tree clean
```

O valor 10 declara 10x10 décimos de segundo, o mesmo que 1 segundo e por aí vai. Caso queira que corrija automaticamente sem aguardar, use o valor 1.

```shell
$ git config --global help.autocorrect 1
```

#### como desligar o autocorrect?

```shell
$ git config --global --unset help.autocorrect
```

#### Crie aliases para agilizar seu trabalho

Atalhos para mais produtividade, o Git oferece aliases para que possamos economizar alguns caracteres, veja como usar:

```shell
$ git config --global alias.co checkout
$ git co production
Switched to branch 'production'
```

outro exemplo

```shell
$ git config --global alias.st status
$ git st
On branch gh-pages
nothing to commit, working tree clean
```

Uma outra forma de criar aliases é editar seu gitconfig e setar manualmente

```shell
$ vim ~/.gitconfig
```

Adicione uma sessão com essa

```shell
[alias]
    co = checkout
    st = status
```

