
Integrantes:
- Giovanna Batista – RA:  
- Marcelo Amorim – RA:  
- Anali Rodrigues – RA:  

# Sistema de Campeonato de Tênis

Nosso sistema tem como objetivo simular um campeonato de Tênis, permitindo o cadastro de times e jogadores, a realização dos confrontos com pontuação, e por fim, determinar o time vencedor com base nos resultados obtidos durante o torneio.

Para a estruturação do código foram utilizados:
Listas, tuplas e dicionários para organizar os dados dos times, jogadores e pontuação. 
Também utiliza laços de repetição (while e for implícito), condicionais (if, elif, else), funções, e até recursão para repetir confrontos empatados.
Basicamente ele segue essa linha de comandos:

Cadastro do times e Jogadores, permitindo cadastrar 4 times, e 4 jogadores por time, e validando se o jogador já não há cadastro dentro do time, e também há a opção de finalizar os cadastros do times com apenas 2 cadastrados.
Seleção dos times por ordem de cadastro para o confronto, validação das pontuações para saber qual time pontuou mais e segue no confrontos para final, caso de empate um novo confronto e realizado
E por fim o sistema calcula qual time pontuou mais e recebe o titulo como vencedor!



Cadastro dos Times e Jogadores

O código começa com duas mensagens introdutórias utilizando a função print() para informar ao usuário que o campeonato vai começar e que o primeiro passo será cadastrar os times:

print('Vamos começar o Campeonato de Tênis!')
print('Primeiro vamos começar pelo Cadastro dos times e Jogadores!')

A seguir, temos a função cadastrar_times() junto de uma lista vazia:

def cadastrar_times():
    times = []

A lista times é criada para armazenar os times que serão cadastrados. 
NEssa função utilizamos um laço while que controla o número de times cadastrados "len(times) <4" (máximo de 4 times):

while len(times) < 4:
    nome_time = input(f"Digite o nome do Time(ou 'fim' para encerrar): ")
    if nome_time.lower() == "fim":
        break

O input() permite ao usuário digitar o nome do time. Caso o usuário digite “fim”, o break encerra o loop, possibilitando cadastrar menos de 4 times(utilizamos o lower para a verificação acontecer caso o usuario utilize outra formatação do fim, como FIm Fim FIM, etc).
Desde que o número mínimo para o campeonato (2 times) seja respeitado.

Depois, criamos duas listas dentro do loop:

Jogadores, que armazena os dados dos jogadores do time. 
Nomes_jogadores, que serve para garantir que não haja nomes repetidos dentro do mesmo time.

jogadores = []
nomes_jogadores = []

while len(jogadores) < 4:
    nome_jogador = input(f"Digite o nome do jogador {len(jogadores) + 1}: ")
    if nome_jogador in nomes_jogadores:
        print("Jogador já cadastrado neste time. Tente outro nome.")
        continue

O if nome_jogador in nomes_jogadores valida se um mesmo nome seja já foi utilizado na lista jogadores e impede que ele seja cadastrado duas vezes no mesmo time. 
Se isso acontecer, é exibida uma mensagem de erro e o continue reinicia o laço.

posicao = input(f"Digite a posição do jogador {len(jogadores) + 1}: ")
jogador = (nome_jogador, posicao)
jogadores.append(jogador)
nomes_jogadores.append(nome_jogador)

Cada jogador é salvo como uma tupla, que junta o nome e a posição do atleta (composta pela lista nome_jogador e a variavel posição, utilizamos a tupla pois permite a variedade de composição de seus itens). 
Essas tuplas são adicionadas à lista jogadores.


Ao final, os dados do time são armazenados em um dicionário, com as chaves nome, jogadores e pontuacao.
 Esse dicionário é adicionado à lista times.

time = {
    'nome': nome_time,
    'jogadores': jogadores,
    'pontuacao': 0
}
times.append(time)

Quando todos os times forem cadastrados ou o usuário digitar "fim", a função retorna a lista times contendo os dados dos times criados.

Função realizar_confronto

Essa função é responsável por simular um confronto entre dois times:

def realizar_confronto(time1, time2):
    print(f"\nConfronto entre {time1['nome']} vs {time2['nome']}")

Ela recebe dois dicionários (os times) e exibe qual confronto será realizado.
 Em seguida, na variavel p1 e p2, o input(definido como int) recebe a pontuação da primeira rodada de jogos o usuário digita a pontuação de cada time:
(p1, recebe a pontuação do primeiro time e p2 recebe a pontuação do segundo time)

p1 = int(input(f"Digite a pontuação de {time1['nome']}: "))
p2 = int(input(f"Digite a pontuação de {time2['nome']}: "))

As pontuações são convertidas para inteiros e adicionadas ao valor já existente na chave 'pontuacao' que antes estavam vazias de cada time:

time1['pontuacao'] += p1
time2['pontuacao'] += p2

O time com maior pontuação vence o confronto e é retornado pela função:
o if foi utilizado para validar se o primeira pontuação(p1) é maior que o segunda(p2), caso seja ele retornara o primeiro time como vencerdor,
o elif foi utilizado para validar caso a segunda pontuação(p2) for maior que a primeira(p2), ela ser retornada
e por fim o else para se caso os valores forem iguais.

if p1 > p2:
    return time1
elif p2 > p1:
    return time2
else:
    print("Empate! O confronto será repetido.")
    return realizar_confronto(time1, time2)

Se houver empate, o confronto será repetido até que haja um vencedor. 
Isso é feito com uma chamada recursiva da função (a função chama a si mesma).

Função campeonato

Essa função organiza o campeonato em várias rodadas, até que reste apenas um time, que será o campeão.
a variavel rodada = 1, serve pra indicar em qual rodada o programa está rodando, a cada loop ele recebe mais 1.
o while nesse caso le quantos times foram declarados e verifica se possui mais de 1
Será declarada na lista vencedores quem obteve a maior pontuação na rodada.

def campeonato(times):
    rodada = 1
    while len(times) > 1:
        print(f"\n Iniciando a Rodada {rodada}")
        vencedores = []


Em cada rodada, os times são emparelhados de dois em dois para realizar confrontos. 

Um índice i é usado para navegar pela lista de times:
Esse while interno pega dois times por vez (ex: 0 e 1, depois 2 e 3, etc.)
Para cada par, chama a função realizar_confronto e armazena o vencedor na lista vencedores

i = 0
while i < len(times) - 1:
    time1 = times[i]
    time2 = times[i + 1]
    vencedor = realizar_confronto(time1, time2)
    vencedores.append(vencedor)
    i += 2

Usamos o if para se acaso  o número de times for ímpar, ele e adicionado na lista vendedores e avança automaticamente para a próxima rodada:

if len(times) % 2 != 0:
    print(f"{times[-1]['nome']} avançou automaticamente!")
    vencedores.append(times[-1])

A lista times é atualizada com os vencedores da rodada, e o processo se repete:

times = vencedores
rodada += 1

Criamos uma variavel que recebera a lista times ja atualizada, na qual a posição 0 indicaria quem será o vencedor

Quando sobra apenas um time, ele é declarado campeão:

campeao = times[0]
print(f"\nO campeão do torneio é {campeao['nome']} com {campeao['pontuacao']} pontos!")

Execução Final

Ao final do código, chamamos a função de cadastro e verificamos se há pelo menos dois times para iniciar o campeonato:

times_cadastrados = cadastrar_times()
if len(times_cadastrados) < 2:
    print("É necessário pelo menos 2 times para iniciar o campeonato.")
else:
    campeonato(times_cadastrados)

Considerações Finais

Esse sistema usa estruturas como listas, tuplas e dicionários para organizar os dados dos times, jogadores e pontuação.
 Também utiliza laços de repetição (while e for implícito), condicionais (if, elif, else), funções, e até recursão para repetir confrontos empatados.

O fluxo do sistema é interativo, claro e organizado para simular de forma realista um torneio, controlando todas as etapas de forma lógica e coerente.
