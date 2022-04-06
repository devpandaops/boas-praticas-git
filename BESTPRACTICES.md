### Boas práticas com branchs

#### Use e abuse de branchs
O recurso de branch é fantástico, você pode criar a partir de qualquer uma.

**Dicas principais:**

- Evite gravar diretamente na main.

- Sempre trabalhe em uma branch separada

- Integre sua branch quando finalizar seu trabalho

- Apague sua branch depois que tiver terminado

**Exemplo**

```shell
$ git branch -u main correcao_criacao_vpc
$ git checkout correcao_criacao_vpc
```

Quando terminar seu ticket, apague a branch

```shell
$ git branch -D correcao_criacao_vpc
```

#### Use branchs de integração

Quando estamos trabalhando com integração contínua o uso de **branchs de integração** é fundamental, precisamos integrar nosso código com o código de nossos colegas e rodar os testes na pipeline.

Geralmente temos uma branch de integração para **desenvolvimento** e depois vamos promovendo esse código para outras branchs que vão nos ajudar a **fechar a release e publicar**, tudo depende do **git-flow** que seu time acordou e está seguindo.

#### Não escreva direto na branch MAIN

Evitamos escrever direto na branch main pois geralmente é a última versão estável devidamente testada e validada por todos, é de fato a fonte da verdade, portanto, para colocar código lá devemos sempre passar por diversos testes em sua pipeline e revisões de seus colegas.

#### Mantenha sua feature-branch atualizada

Faça rebases regulares para garantir isso!

Exemplo de atualização da branch main localmente e depois rebase

```shell
$ git checkout main
$ git pull
$ git checkout feature-xyz  
$ git rebase main 
```

Exemplo de merge do código com a main

 ```shell
$ git checkout main
$ git pull
$ git merge feature-xyz
```

#### De vez em quando recrie suas branchs de integração

Isso é legal de fazer para dar uma limpada na coisa toda e começar novamente.

```shell
$ git checkout main
$ git branch -D devel
$ git branch -u main devel
```

#### Limpe periodicamente branchs de feature

O ideal é sempre apagar suas branchs de feature ou de teste após finalizar um ticket.

Apesar de ser o ideal, nem sempre lembramos, então de vez em quando é bom olhar e apagar branchs que não estão sendo usadas.

Pode-se até definir um tempo de vida para branchs que não são fixas, e definindo isso podemos até criar uma automação para limpar o repo.

### Boas práticas com commit

#### Corrija as mensagens do seu commit se errar

Caso perceba algum typo na sua mensagem de commit, use o amend para corrigir

```shell
$ git commit -v --amend
```

#### Faça commits pontuais e objetivos

Evite fazer um commit com dezenas de arquivos, em especial se esses arquivos trazem mais de uma mudança ou correção. Devemos evitar isso pois fica difícil rastrear, entender e revisar o que foi feito no commit.

Prefira fazer commits pequenos e pontuais de algo que está terminado, algo que funciona e que não traga muitas alterações de uma vez só.

#### Faça commits atômicos quando possível

Já sabemos que commitar poucas alterações é o melhor caminho, mas dá para ser ainda menor.

Os commits atômicos são aqueles que gravam apenas uma única mudança – ainda que envolva vários arquivos – em um único commit.

É claro que nem sempre dá para fazer, mas é uma prática excelente se conseguir fazer.

A ideia do commit atômico é gravar a menor e mais importante melhoria que voce fez no código, sendo grande suficiente para adicionar algum valor, contudo, pequena o suficiente para ser gerenciada com flexibilidade.

Se quiser trabalhar dessa forma tenha em mente duas coisas:

- Trabalhe em uma coisa por vez

- Faça alterações pequenas e pontuais

#### Faça commits regulares e frequentes

Não espere demais!

Algumas pessoas esperam demais até gravar alguma alteração, às vezes ficam ali melhorando algo que já está funcionando, buscando algum tipo de perfeição antes de gravar.

Deixa eu te dizer uma coisa, o git funciona melhor e te ajuda mais quando você grava com frequência ao invés de esperar muitoooo tempo para gravar sua mudança.

Ao gravar com frequência você vai rastrear inclusive como você foi melhorando aquele código ao longo do seu processo e histórico de desenvolvimento.

E lembre-se, o GIT só cuida do seu código depois que você grava, se você fechar o editor por acidente ou se o editor travar, seu código já era, contudo, se estiver commitando com frequência você evita isso.

#### Quebre seu commit em commits menores

As vezes a gente vai trabalhando e se empolga demais, e com isso acaba fazendo mais de uma alteração em um mesmo arquivo, e neste caso, tais alteraçoes que poderiam ser commitadas de forma separada. Se for esse o caso, o commando abaixo te permite escolher quais mudanças você deseja commitar em um determinado arquivo.

```shell
git add -p <nome_do_arquivo>
```

Assim vamos conseguir commitar pequenas porções do arquivo por vez.

#### Não faça commit de algo que você não finalizou

Nunca, eu repito, nunca grave algo que não está funcionando ou que não está completo.

#### Teste seu código antes de gravar

Essa é uma das coisas mais básicas que vou falar hoje, mas tem que falar e tem que fazer.

Caso não saiba, gravar código quebrado é algo bastante incômodo, poderá irritar seus colegas, podendo em alguns casos chegar a ser considerado uma falta de respeito e falta de profissionalismo.

Verifique a sintaxe do seu código, rode um linter e execute o código para ver se o que fez está funcionando, seja uma feature, seja um bugfix, seja um hotfix, afinal, se o código estiver funcionando e se sua solução resolver o ticket, isso será o melhor dos mundos.

O git inclusive oferece um sistema de HOOKS que permite por exemplo, executar comandos de checagem antes de de gravar seu código, nesse caso estou falando do hook “pre-commit”, veja o link abaixo e leia sobre esse e outros hooks, é um recurso muito útil, acredite.

- https://git-scm.com/docs/githooks

#### Escreva mensagens de commit claras

As mensagens precisam fazer sentido e ser úteis para todos do time.

#### Commitando em uma linha

A mensagem tem que fazer sentido, ser fácil de ler e ser suficiente para entender o que foi feito.

**Exemplos**
Podemos usar convenções para mostrar que fizemos uma correção

```shell
fix: corrige bug quando modulo vai crair a 2o VPC na AWS
```

ou uma refatoração

```shell
refact: refatora código que configura IAM para EKS na AWS
```

ou uma documentação

```shell
doc: adiciona docs para uso do modulo IAM/EKS
```

ou que inserimos testes

```shell
test: adiciona testes unitários no módulo
```

ou que criamos uma nova feature

```shell
feat: adiciona recurso para lidar com ALB no EC2/AWS
```

#### Entendendo a estrutura

É simples

```shell
feat: adiciona fature para recursos ALB no EC2/AWS #220412
^--^  ^-----------------------------------------^
|     |
|     +-> Sumário da sua mudança
|
+-------> Tipo: docs, feat, fix, refact, ou test.
```

Se você estiver usando um sistema de tickets junto, adicione o número do ticket na mensagem, sistemas como GitLab e GitHub já farão a associação para você entre a issue e o commit.

Evite colocar ponto final na mensagem, afinal é um título.

Vale lembrar que você deve evitar escrever mais de 50 caracteres ou vai quebrar a saída do “git log”.

#### De que modo escrever a mensagem?

Em alguns blogs vocês verão pessoas que defendam usar verbos no imperativo ou presente do indicativo, e faz sentido. Em ambos os casos a ideia é que o commit responda essa pergunta:

```shell
  "Em caso de aplicar esse commit ele..."
```

**Resposta**

```shell
...altera código X
...corrige módulo Y
...refatora manifesto Z
...cria feature W para módulo X
```

Eu já gosto de usar particípio do passado, pois foi algo que já foi realizado e nem precisa fazer a perguntinha para ver como tem que escrever, neste caso você pode afirmar ao invés de perguntar, dessa forma:

```shell
"Nesse commit foi..."
```

**Resposta**

```shell
...alterado código X
...corrigido módulo Y
...refatorado manifesto Z
...criada a feature W para módulo X
```

Enfim, existem longas threads sobre isso na internet, quase uma guerra santa, contudo, IMHO isso vai depender de cada um, ou da forma como cada time decidiu trabalhar.

No final o importante é você versionar seu código e conseguir entender o que fez ali lendo a mensagem de commit :)

#### Usando o editor para algo mais detalhado

As vezes precisamos escrever um pouco mais, indo além do “one line commit”, especialmente se foi uma correção complexa, se tem alguma pegadinha, ou se for preciso explicar porque você fez aquilo daquela forma. No caso do trabalho e o dia-a-dia dos Cloud Engineers nem sempre é necessário, mas se for, veja como fazer.

Nesse caso, como é uma mensagem longa, não podemos fazer “one line commit”, temos que ir para o editor.

```shell
$ git commit
```

**E escrever a mensagem**

```shell
Assunto da mensagem com no máximo 50 caracteres, sem ponto final

Descrição em múltiplas linhas
sobre seu commit. Use até 72 caracteres

Outros parágrafos podem vir após inserir 
uma linha em branco
Aqui nao tem mais limite de caracteres

Podemos usar bullets também, ajuda a organizar a informação

- Enumerando
- Alterações
- Realizadas
- Por
- Este
- Commit

Se existe um ticket coloque 
o número dele na mensagem e os tickets relacionados

Esse commit resolve o problema do ticket #2222
E está relacionado com o ticket #3333 e #4444
```

