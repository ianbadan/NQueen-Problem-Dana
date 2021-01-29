# Problema das N-Rainhas

Este repositório contendo algoritmos que resolvem o problema das N-Rainhas, um algoritmo é uma implementação utilizando backtracking e o outro é uma implementação utilizando algoritmo genético para resolver o problems, ambos os algoritmos foram implementados utilizando a linguagem de programação DANA (http://www.projectdana.com).

## O que é Dana?

O DANA é a linguagem de programação adaptativa mais avançada do mundo, é capaz de trocar componentes do sistemas em microsegundos sem problema algum e de forma que o sistema continue funcionando enquanto os componentes são alterados. Isso é possivel através da utilização rigorosa de encapsulamento de interfaces que descreve o que cada componente fornece como serviço e o que requer de outros componentes como dependência.

Apesar de todo esse podem de adaptação, esses algoritmos apresentados seguem uma ideia mais linear, próximo ao utilizado no C, pois utilizar de componentes só dificultaria o processo de desenvolvimento do algoritmo.

## O problema das N-rainhas (N-queens problem)

O problema da N-Queens consiste em colocar N rainhas em um tabuleiro de N x N de forma que as rainhas não se ataquem, para isso, deve se olhar todas as formas de ataque de uma rainha. As rainhas podem atacar na mesma linha, na mesma coluna e nas duas diagonais. então para que esse problema seja resolvido, todas as rainhas devem estar em posições que não ocorra conflito com nenhuma outra rainha.

Para N = 1, é trivial e só possui uma solução, já para N = 2 não existe solução alguma, uma rainha em qualquer posição automáticamente bloqueia toda as outras posições do tabuleiro, mas para qualquer N > 2 existe pelo menos uma solução possivel.

Este é um problema clássico da computação e existem várias formas de resolve-lo, mas duas formas específicas foram escolhidas, a primeira foi utilizando um algoritmo com backtracking para entender melhor o problema em questão e o segundo foi utilizando algoritmo genético para praticas e obter resultados melhores quando o N possui um valor muito alto.

## Solução utilizando Backtracking

Um dos jeitos é com Backtracking Linear que é um método que vai testando todas as possibilidades de configuração até chegar na primeira configuração de tabuleiro que seja uma solução para o problema ou pode mostrar todas as configurações possíveis se projetado para isso.

Esse algoritmo funciona de forma muito específica, irá posicionando as rainhas da esquerda para a direita no tabuleiro, sempre na primeira posição disponível para isso, então será assim, a primeira rainha será posicionada na primeira coluna e então irá para a segunda e posicionará ela na primeira posição que está livre e isso se repetirá até chegar a um tabuleiro que seja resposta ou chegar em uma coluna em que não é possível posicionar a rainha em nenhuma linha, quando isso acontecer o algoritmo irá voltar pra coluna anterior e mudará a posição da rainha até que a próxima tenha uma posição valida, caso isso não aconteça, voltará mais uma coluna e mudará a rainha dessa coluna de posição e vai verificar as rainhas a direita, esse método de avançar e retornar quando se chegar em um caminho sem saída é como o algoritmo funciona.

É um excelente algoritmo para valores pequenos de N, mas quando o valor de N aumenta, vemos que é um algoritmo não muito efetivo, pois o tempo necessário para se obter o resultado cresce exponencialmente, porque as possibilidades de posições totais aumenta dessa forma, sempre seguindo a ideia de N!, se o algoritmo for pensado com a ideia de permutações e caso não pense assim, se torna N^n, o que piora de forma ainda mais drástica o seu custo computacional e tempo de computação.

O algoritmo implementado na pasta BacktrackingLinear funciona seguindo a ideia de permutações e para ao encontrar o primeiro resultado que é uma solução para o problema.

## Solução com Algoritmo Genético (AG)
A aplicação com algoritmo genético é um pouco mais complicado, mas soluciona o problema de custo computacional, principalmente de tempo de computação, pois esse algoritmo é capaz de dar saltos dentro do espaço de busca, assim não tendo a necessidade de olhar todas as possibilidades de combinação para esse problema.

Isso é possível porque o algoritmo genético é pensando para quando se tem problemas de otimização e adaptação, pois como utiliza as ideias de evolução, seleção natural e genética, é possivel criar indivíduos iniciais e através deles ir melhorando a aptidão das população por meio da criação de novos indivíduos pela recombinação de material genético dos pais até chegar em um indivíduo que tenha uma aptidão alta a ponto de resolver o problema.

Antes de explicar as partes de um algoritmo genético, alguns termos devem ser explicados, são eles:

* **Indivíduo**: é uma possível solução para o problema, tem o seu próprio gene e caracteristicas únicas.

* **População**: um conjunto de indivíduos, em algoritmos genéticos o tamanho da população é fixo, então para novos indivíduos entrarem na população, outros devem ser eliminados.

* **Gene**: é a forma como o indivíduo é representado para o algoritmo, é o mesmo que **genótipo**, no caso das rainhas, é o vetor com os valores inteiros que indicam a posição de cada rainha.

* **Fenótipo**: são as caracteristicas do genes quando são expressos, em resumo, é a forma como outros indivíduos enxergam aquele indivíduo, no problema das rainhas, é o tabuleiro com as rainhas posicionadas.

* **Máxima Global**: também é chamado como **ótimo global**, é quando o algoritmo chega ao seu fim e consegue encontrar a melhor solução para o problema, em alguns casos, somente os indivíduos dentro de uma máximo local são aceitos como solução para o problema e tem casos em que mesmo que não se chegue a esse patamar, o individuo encontrado ainda é uma solução, só não será a melhor de todas.

* **Máxima Local**: também conhecido como **ótimo local**, é quando se chega ao final do algoritmo e não encontrou o melhor resultado, isso geralmente acontece quando se ocorre uma perda na variação genética da população e assim, os indivíduos são muito parecidos e não se é possível mais recuperar os genes perdidos de indivíduos que já foram eliminados, ainda é possível que esse indíviduo seja usado como solução, mas a eficiência do algoritmo será menor que o comum, no caso das N-rainhas, se chegar a uma máximo local, ele não poderá ser utilizado como solução, pois ainda se terão rainhas se atacando.

* **Convêrgencia Prematura**: acontece quando se perde variação genética na população e nem mesmo o processo de mutação consegue recuperar, assim o código converge para uma solução que não é ótima caindo uma máxima local.

Após essa explicação dos termos, é necessário entender quais são as partes de um algoritmo genético:

1. **Representação dos indivíduos**: é uma parte extremamente importante, pois a representação errada dos indivíduo pode trazer resultados indesejados ou dificuldade nas outras partes, em algoritmos genéticos se usa strings ou vetores com um conjunto de valores finitos para representar os indivíduo, no problema das rainhas tem varias formas de representar, mas a que eu escolhi foi usar um vetor com n-1 posições, onde cada posição representa do vetor representa uma coluna do tabuleiro e o conjunto de valores vai de 0 até n-1 e não podem se repetir, sendo uma permuta de 0 até n-1, esse valores representarão as linhas do tabuleiro em que cada rainha está, isso remove a possibilidade de se ter mais de uma rainha em cada linha e coluna, então a única preocupação será verificar se elas se atacam nas diagonais.

2. **Criação da primeira população**: a primeiro população de um algoritmo genético é criado de forma totalmente aleatória e vai depender de como é a representação do seu indivíduo, no problema das N-rainhas, a primeira população é criada por meio de um algoritmo que cria M vetores com permutações de 0 até N-1, sendo M o tamanho da população.

3. **Seleção dos pais**: 

4. **Processo de recombinação(crossing over)**:

5. **Processo de mutação**:

6. **Função de aptidão**:

7. **Seleção de sobreviventes**:

8. **Critério de parada**:


## Diferença entre as versões do Algoritmo Genético
