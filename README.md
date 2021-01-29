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

* **Genoma**: é a forma como o indivíduo é representado para o algoritmo, é o mesmo que **genótipo**, no caso das rainhas, é o vetor com os valores inteiros que indicam a posição de cada rainha.

* **Gene**: é cada posição individual dentro do genoma, no caso, seria cada poisção do vetor e os valores internos que cada gene pode assumir, isto é, o conjunto finito de valores que cada posição pode assumir é chamado de **alelo**.

* **Fenótipo**: são as caracteristicas do genes quando são expressos, em resumo, é a forma como outros indivíduos enxergam aquele indivíduo, no problema das rainhas, é o tabuleiro com as rainhas posicionadas.

* **Máxima Global**: também é chamado como **ótimo global**, é quando o algoritmo chega ao seu fim e consegue encontrar a melhor solução para o problema, em alguns casos, somente os indivíduos dentro de uma máximo local são aceitos como solução para o problema e tem casos em que mesmo que não se chegue a esse patamar, o individuo encontrado ainda é uma solução, só não será a melhor de todas.

* **Máxima Local**: também conhecido como **ótimo local**, é quando se chega ao final do algoritmo e não encontrou o melhor resultado, isso geralmente acontece quando se ocorre uma perda na variação genética da população e assim, os indivíduos são muito parecidos e não se é possível mais recuperar os genes perdidos de indivíduos que já foram eliminados, ainda é possível que esse indíviduo seja usado como solução, mas a eficiência do algoritmo será menor que o comum, no caso das N-rainhas, se chegar a uma máximo local, ele não poderá ser utilizado como solução, pois ainda se terão rainhas se atacando.

* **Convêrgencia Prematura**: acontece quando se perde variação genética na população e nem mesmo o processo de mutação consegue recuperar, assim o código converge para uma solução que não é ótima caindo uma máxima local.

Após essa explicação dos termos, é necessário entender quais são as partes de um algoritmo genético:

1. **Representação dos indivíduos**: é uma parte extremamente importante, pois a representação errada dos indivíduo pode trazer resultados indesejados ou dificuldade nas outras partes, em algoritmos genéticos se usa strings ou vetores com um conjunto de valores finitos para representar os indivíduo, no problema das rainhas tem varias formas de representar, mas a que eu escolhi foi usar um vetor com n-1 posições, onde cada posição representa do vetor representa uma coluna do tabuleiro e o conjunto de valores vai de 0 até n-1 e não podem se repetir, sendo uma permuta de 0 até n-1, esse valores representarão as linhas do tabuleiro em que cada rainha está, isso remove a possibilidade de se ter mais de uma rainha em cada linha e coluna, então a única preocupação será verificar se elas se atacam nas diagonais.

2. **Criação da primeira população**: a primeiro população de um algoritmo genético é criado de forma totalmente aleatória e vai depender de como é a representação do seu indivíduo, no problema das N-rainhas, a primeira população é criada por meio de um algoritmo que cria M vetores com permutações de 0 até N-1, sendo M o tamanho da população.

3. **Seleção dos pais**: é o processo de seleção dos pais daquela geração, isto é, a seleção de indíviduos que irão perpetuar o seu material genéticos para os novos indivíduos que serão gerados, conhecido como filhos, e essa seleção pode acontecer de diversas formas, como, por exemplo, por meio de seleção aleatória de indivíduos dentro da população ou por seleção por torneio, em que dois são selecionados e aquele que tem a melhor aptidão ganha e isso se repete até que se tenha o número de pais necessarios, falando em número de pais, a quantidade de pais é definido pelo programador e varia de caso para caso, podendo até ter caso em que todos são selecionados, pois o número de filhos gerados será o mesmo que o tamanho da população e todos os indivíduos serão substituidos por novos. Na minha implementação, a quantidade de pais selecionados é equivalente a 30% do tamanho da população e serão sempre gerados 2 filhos e partir de 2 pais, então no final, 30% da população será modificada a cada geração.

4. **Processo de recombinação(crossing over)**: é o momento em que o material genético dos pais são combinados para a geração dos filhos que entrarão para a população, essa recombinação pode acontecer de formas diferentes, exemplos são a escolha arbitrária, em que ao se olhar uma posição do vetor se escolhe de forma aleatória se aquele gene vai para o primeiro ou segundo filho ou pela escolha de corte de um ou mais pontos, nesse caso, se escolhe um ponto de corte no genoma dos pais e a parte anterior ao corte vai para um filho e a posterior ao corte vai para outro e o contrário acontece no outro pai, assim, os filhos possuem uma parte do material de ambos os pais.

5. **Processo de mutação**: como na realidade é possível acontecer mutações que podem ou não melhorar o indivíduo e torna-lo mais ou menos apto para um ambiente, o mesmo é replicado num algoritmo genético, é uma função em que se calcula a probabilidade de um filho sofrer mutação e se a decisão tomada for que irá sofrer mutação, então um ou mais genes são selecionados para sofrer mutação, assim alterando o valor atual para outro valor dentro do conjunto finitos de valores que cada gene pode assumir. No problema das N-rainhas, como escolhi seguir o padrão de permutações, para não quebrar isso, o que fiz foi inverter dois genes de lugar, assim o novo indivíduo gerado continua sendo uma permutação e há também a possibilidade de acontecer dupla mutação, isto é, o processo de mutação se repete em outras duas posições.

6. **Função de aptidão**: é quando se mede o quão apto um indivíduo está para aquele ambiente, se usa uma formula matemática para isso e geralmente visa a maximização da aptidão, mas não é errado se usar uma função de minimização para a função de aptidão, não quebrará a lógica do algoritmo, mas a função em si varia de acordo com o problema em questão. Para o meu algoritmo, a função é determinar por Aptidão = 1/numAttacks, isto é, a aptidão do individuo é determinado pela quantidade de ataques que está acontecendo no tabuleiro, em suma, quantas rainhas estão atacando outras rainhas.

7. **Seleção de sobreviventes**: depois que os filhos já tem a sua aptidão medida, é hora de selecionar quais indivíduos da população irão sobreviver para a proxima geração e quais serão eliminados para a entrada dos novos filhos gerados, esse seleção pode acontecer de algumas formas, como a eliminação dos indivíduo com a pior aptidão ou por meio de eliminação dos mais velhos, pois como são mais velhos, o que se espera é que já tenha perpeturado seu material genético. No meu algoritmo, eu optei por eliminar os com a pior aptidão, mas tem que se tomar cuidado ao fazer isso, pois um indivíduo muito novo pode ser eliminado sem passar parte do seu material genético e isso causar perca de variação genética na população.

8. **Critério de parada**: é o ultimo, mas não menos importante ponto a se considerar sobre o algoritmo, pois sem a determinação do critério de parada, o algoritmo irá rodar de forma infinita, então em algoritmos genéticos geralmente se tem alguns critérios mais comuns, o principal é quando se chega a um ótimo global, isto é, quando se acha a melhor solução para o problema, no caso das N-rainhas é simples determinar isso, a solução é quando se chega a um tabuleiro sem rainhas se atacando, porém nem sempre é fácil assim determinar isso, tem casos em que não é possivel determinar se o indivíduo é um ótimo global ou local, pois não se tem conhecimento de qual seria uma solução ótima, para isso, outros critérios devem ser considerados, como atingir um limite máximo de gerações ou de processos de recombinação, quando a média da melhora de aptidão de cada geração já não é significante nas ultimas M gerações, entre outros. Os critérios escolhidos ficam a do programador, no meu caso, eu escolhi quando achar a melhor solução ou atingir um máximo de gerações, o que vier primeiro.

Se o algoritmo possuir todas essas partes, se tem um algoritmo genético funcional e que irá resolver o problema para o qual foi projetado.


## Diferença entre as versões do Algoritmo Genético

A principal diferença está na parte de seleção de pais e recombinação. Na **versão 1**, a seleção de pais é a escolha aleatória entre individuos da população e sempre escolhendo o melhor daquela geração, já na **versão 2** a escolhe é por meio de torneio. A mudança na recombinação é a seguinte, na **versão 1** eu escolhi a recombinação com um ponto de corte enquanto que na **versão 2** é feito por meio de 2 pontos de corte.

Essa mudanças foram feitas pois ao rodar testes com um N acima de 30, na versão 1 acontecia muita convergência prematura e para diminuir isso alterações foram feitas para diminuir a quantidade de vezes em que aconteceu convergência prematura e isso realmente aconteceu, quanto mais N aumenta, menos são os casos de ótimos locais, porém isso teve um custo, a **versão 2** do algoritmo é mais lento que a **versão 1**, pelo fato de ter que fazer mais verificações e escolhas durante a sua execução a cada geração.
