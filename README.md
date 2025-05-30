
Integrantes:  
Giovanna Batista – RA:  
Marcelo Amorim – RA:  
Anali Rodrigues – RA:  

Sistema de Campeonato

Nosso sistema tem como objetivo simular um Campeonato de Tênis, onde são realizados os cadastros dos times e jogadores, os confrontos entre os times, a pontuação das partidas e, por fim, a definição do time campeão com base nas pontuações acumuladas.

Cadastro dos Times e Jogadores

O código começa com a função responsável por cadastrar os times. O sistema permite o cadastro de até 4 times para participarem do campeonato. Para isso, é criada uma lista vazia chamada `times`, que armazenará os dicionários com os dados de cada time.

Para limitar a quantidade de times cadastrados, é utilizado um laço `while` que depende da condição `len(times) < 4`, ou seja, o loop continuará até que 4 times tenham sido cadastrados. A cada iteração do loop, o sistema solicita que o usuário digite o nome do time.

Há também uma verificação que permite sair do cadastro antes de atingir os 4 times: caso o usuário digite “fim”, o comando `break` interrompe o laço, permitindo seguir adiante. Isso é útil caso o usuário queira realizar o campeonato com menos de 4 times, mas o sistema exige pelo menos 2 times para que o campeonato aconteça.

Durante o cadastro de um time, são criadas duas listas: `jogadores` e `nomes_jogadores`. A lista `jogadores` armazenará as tuplas contendo o nome e a posição de cada jogador. Já `nomes_jogadores` serve como controle para evitar que o mesmo nome de jogador seja inserido mais de uma vez no mesmo time.

É iniciado um segundo laço, agora para o cadastro dos jogadores. O sistema exige 4 jogadores por time. Em cada repetição, o usuário deve informar o nome do jogador. Caso o nome já exista na lista `nomes_jogadores`, é exibida uma mensagem de erro e o `continue` faz o código voltar para o início do laço, solicitando outro nome. Isso garante que não haja duplicidade de nomes dentro de um mesmo time.

Após validar o nome, o sistema solicita a posição do jogador. O nome e a posição são então armazenados em uma tupla `(nome_jogador, posicao)` e adicionados à lista `jogadores`. O nome também é adicionado à lista `nomes_jogadores` para continuar o controle.

Quando os 4 jogadores são cadastrados, o time é salvo como um dicionário contendo o nome do time, a lista de jogadores e a pontuação inicial, que começa em zero. Esse dicionário é então adicionado à lista `times`.

Esse processo se repete até que o número máximo de times seja atingido ou o usuário encerre o cadastro com “fim”.

Funções utilizadas no Cadastro

Durante essa fase, o sistema utiliza o `input()` para coletar dados do usuário e `print()` para exibir mensagens orientando o uso. O laço `while` controla o número de times e o `for` (ou um novo `while`) controla o número de jogadores por time. A estrutura condicional `if` garante que não haja jogadores com nomes repetidos. As listas armazenam e organizam os dados, e as tuplas agrupam informações do jogador. O `break` é usado como saída antecipada do cadastro e o `continue` para repetir a solicitação de entrada em caso de erro.

Realização dos Confrontos

Após os cadastros, o sistema avança para a fase dos confrontos. Essa etapa é realizada pela função `realizar_confronto`, que simula uma partida entre dois times. A função recebe dois times como parâmetro, exibe os nomes dos adversários e solicita que o usuário informe a pontuação de cada um deles.

Essas pontuações são então somadas ao total já existente de cada time (armazenado na chave `'pontuacao'` de cada dicionário). Isso permite acompanhar o desempenho acumulado dos times ao longo do campeonato.

O sistema então compara as pontuações: o time com maior pontuação vence o confronto e é retornado pela função para continuar no campeonato. Caso ocorra um empate, o sistema informa que a partida será repetida e a função se chama novamente, utilizando recursão, até que um vencedor seja definido. Essa lógica garante que cada fase do campeonato tenha um vencedor claro, sem empates.

Organização do Campeonato

A função `campeonato` é responsável por organizar o andamento do torneio, dividindo-o em rodadas e conduzindo os confrontos até que reste apenas um time vencedor.

Ela começa iniciando uma variável `rodada`, que é usada apenas para informar o número da rodada atual. Enquanto houver mais de um time na lista, o campeonato continua.

Para cada rodada, o sistema percorre os times cadastrados em pares (dois em dois), e realiza os confrontos utilizando a função `realizar_confronto`. Os times vencedores de cada confronto são armazenados em uma nova lista chamada `vencedores`, que substituirá a lista original na rodada seguinte.

Se o número de times for ímpar, o último time da lista automaticamente avança para a próxima fase sem disputar, recebendo uma mensagem indicando isso.

Essa lógica de confrontos se repete até que reste apenas um time na lista. Quando isso ocorre, o campeonato chega ao fim, e o sistema declara o time campeão, informando também sua pontuação total acumulada ao longo do torneio.

Conclusão

O código apresenta uma estrutura lógica bem organizada para simular um campeonato esportivo. Utiliza listas, tuplas, dicionários, laços `while`, `for`, condições `if` e chamadas recursivas. As estruturas de dados permitem armazenar informações de maneira eficiente e segura, com verificações que garantem a integridade dos dados (como nomes únicos de jogadores por time). A recursividade e os laços garantem a repetição controlada das rodadas e dos confrontos, tornando o sistema robusto para diversas combinações e cenários.

O resultado é um sistema interativo, simples e funcional para simular uma competição esportiva do tipo mata-mata, com todas as etapas bem definidas: cadastro, confrontos, pontuação e definição do vencedor.
