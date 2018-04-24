# Quick knowledge JS

Ramda é uma biblioteca funcional de uso prático para programadores Javascript.

## Overview funcional

Alguns conceitos de liguagem funcional antes:

### Funções puras
Caracteristicas de uma função pura
- O valor de retorno das funções puras depende de seus argumentos, portanto, se você chamar as funções puras com o mesmo conjunto de argumentos, sempre obterá os mesmos valores de retorno;
- Elas não têm efeitos colaterais como chamadas de rede ou banco de dados;
- Elas não modificam os argumentos que são passados para eles.

### Funções impuras
Caracteristicas de uma função impura
- O valor de retorno das funções impuras não depende apenas de seus argumentos, portanto, se você chamar as funções impuras com o mesmo conjunto de argumentos, poderá obter os diferentes valores de retorno
- Elas podem ter efeitos colaterais como chamadas de rede ou banco de dados
- Elas podem modificar os argumentos que são passados para eles






## Programação Funcional com Javascript

* Apatridia
* Evitando efeitos colaterais

### Apatridia
Linguagens de programação têm a noção de "estado". Este é um instantâneo do ambiente atual de um programa: todas as variáveis que foram declaradas, funções criadas e o que está sendo executado no momento.

Uma expressão em uma linguagem de programação pode ser "stateful" ou "stateless". Uma expressão com estado é aquela que altera o ambiente atual de um programa. Um exemplo muito simples em Javascript seria incrementar uma variável por 1:
```js
var number = 1;
var increment = function () {
    return number + = 1;
};
increment();
```
Uma expressão sem estado, por outro lado, é aquela que não modifica o ambiente de um programa:
```js
var number = 1;
var increment = function (n) {
    return n + 1;
};
increment(number);
```
Ao contrário do exemplo anterior, quando chamamos de incremento aqui, não alteramos o valor do número, apenas retornamos um novo valor.

A programação orientada a objetos funciona alterando o estado do programa para produzir respostas. Por outro lado, a programação funcional produz respostas através de operações sem estado. O contraste mais claro pode ser visto em como as duas metodologias lidam com o loop. Uma abordagem orientada a objetos seria usar um loop for:
```js
var loop = function () {
    para (var x = 0; x <10; x + = 1) {
        console.log(x);
    }
};
loop();
```
O loop produz seus resultados alterando constantemente o valor de x. Uma abordagem funcional envolveria recursão (abordada com mais detalhes posteriormente):
```js
var loop = function (n) {
    if (n> 9) {
        console.log(n);
        Retorna;
    } outro {
        console.log (n);
        loop(n + 1);
    }
};
loop(0);
```
Nesse caso, obtemos nossos resultados chamando a função loop a cada vez com um novo valor, em vez de modificar o estado do programa.

Portanto, a programação funcional exige que escrevamos expressões sem estado e mantenham nossos dados imutáveis.

### Evitando efeitos colaterais
Quando uma função é executada, ela pode alterar o estado de um programa além de retornar um valor:
```js
var number = 2;
var sideEffect = function (n) {
    number = n * 3;
    número de retorno * n;
};
sideEffect (3);
```
O efeito colateral dessa função é que ela altera o valor do número toda vez que é executada. A programação funcional promove o uso de “funções puras”: funções que não têm efeitos colaterais. No exemplo acima, alterar o valor do número não seria permitido sob este paradigma. Se sempre podemos escrever funções que não têm efeitos colaterais, nosso programa se torna “referencialmente transparente”. Isso significa que, se inserirmos o mesmo valor em um programa, sempre obteremos o mesmo resultado.

O exemplo acima não é referencialmente transparente, porque se nós sempre chamarmos sideEffect com 3, obteríamos um resultado diferente a cada vez.

#### Programação funcional pura em Javascript
Se quiséssemos programar de forma funcional e pura em Javascript, poderíamos definir as seguintes regras:

Nenhuma atribuição, ou seja, alterar o valor de algo já criado com = (instruções var com = estão bem)
Não para ou loops while (use recursão em vez disso)
Congelar todos os objetos e matrizes (já que modificar um objeto ou array existente seria uma expressão de estado)
Proibir Data (uma vez que sempre produz um novo valor, independentemente das entradas)
Não permitir Math.random (mesmo motivo que Data)
Por que programar funcionalmente?
Depois de analisar os temas da programação funcional e as regras que precisamos definir para garantir que podemos escrever programas puros, pode parecer que precisamos passar por muitos obstáculos apenas para fazer qualquer coisa. De fato, a programação funcional parece inferior quando confrontada com ambientes que estão constantemente em fluxo. Isto é particularmente verdade no DOM (uma das principais interações do Javascript) que pode mudar constantemente através de inserções, exclusões, animações, etc. Na verdade, os criadores da linguagem de programação Haskell desenvolveram o Monads como uma forma de gerenciar estados em mudança, mas mantendo a pureza funcional (Douglas Crockford também deu uma palestra sobre a implementação do Monad's em Javascript).

A grande vantagem que a programação funcional nos oferece é que podemos raciocinar e testar nossos programas com muito mais facilidade. Isso pode nos ajudar a ser mais produtivos, reduzir erros e escrever softwares melhores. Nem sempre é possível escrever tudo de uma forma puramente forma funcional, mas é algo pelo que lutar. John Carmack, da Id Software, escreveu um bom artigo discutindo as considerações práticas da programação funcional.Conceitos em programação funcionalPrimeira classe e funções de ordem superiorNós já discutimos funções de primeira classe e como elas podem ser armazenadas e passadas como valores. Claro que estas são expressões muito simples em Javascript: var funcAsValue = function (y) {return y * 4;}; var returnFunc = function (z) {função return (a) {return a * z; };} var funcAsArgument = function (a, func) {return func (a);}; As duas últimas expressões são exemplos de funções de “ordem superior”. Estas são funções que retornam funções como resultado ou tomam outras funções como argumentos.ClosesAs funções Javascript podem acessar variáveis ​​em seu escopo externo: var func = function () {var a = 3; função de retorno (b) {return b * a; };}} var closure = func (); closure (4) // 12Neste exemplo, a função retornada pelo encerramento ainda pode acessar a, já que está em seu escopo externo. Quando as funções retornam, elas “tiram uma foto” de seu ambiente atual. que eles podem ler os últimos valores de. Assim, em essência, encerramentos são funções que, além de ter um corpo de expressão e receber argumentos, também registram um escopo ou ambiente externo. É importante ressaltar que os closures sempre têm acesso ao último valor de uma variável. Se reescrevermos o exemplo acima para sempre incrementar a, podemos ver como é esse o caso (embora isso quebre nossos princípios funcionais): var func = function () {var a = 3; função de retorno (b) {a = ++ a; devolve b * a; };}} var closure = func (); encerramento (4) // 16closure (5) // 25RecursionA função recursiva é uma função que simplesmente se chama: var recursive = function (n) {if (n <1) { return n; } else {return recursivo (n - 1); }}; recursivo (1); // 0A programação funcional favorece a recursão para looping, em vez dos loops while ou for tradicionais, já que podemos manter a apatridia e evitar efeitos colaterais. Por exemplo, para calcular o fatorial do valor n com estados, poderíamos fazer: var fatorial = function (n) {var result = 1; para (var x = 1; x <= n; x + = 1) {resultado = x * resultado; } return result;}; fatorial (5) // 120A abordagem sem estado seria: var recursiveFactorial = function (n) {if (n <2) {return n; } else {return n * recursiveFactorial (n - 1); }}; recursiveFactorial (5) // 120Tail call optimisationA maioria das linguagens de programação funcional implementam “otimização de chamada final” para funções recursivas. Para entender isso, seria melhor começar observando o que acontece quando a recursão não é otimizada dessa maneira. Cada vez que uma função é chamada, um espaço adicional é ocupado na pilha de chamadas. Se você estiver usando um ambiente Javascript que suporte o log de console.trace, poderá ver a pilha de chamadas da função recursiveFactorial acima: var recursiveFactorial = function (n) {if (n <2) {console.trace (); return n; } else {console.trace (); return n * recursivoFatorial (n - 1); }}; recursiveFactorial (5); Esta pilha é construída de forma que quando um valor é retornado o programa sabe para onde voltar. Uma “chamada final” é uma chamada para uma função que ocorre como a última ação de outra função. Nossas chamadas recursivas acima não são chamadas finais, já que a ação final da função é multiplicar o que é retornado por recursiveFactorial por n. Vamos mudar isso para que eles sejam: var recursiveFactorial = function (n) {var recur = função (x, y) {if (y === n) {console.trace () return x * y; } else {console.trace () retorna recur (x * y, y + 1); }} return recur (1, 1);}; recursiveFactorial (5); Como o JavaScript não implementa a otimização de chamada de cauda, ​​podemos ver no console que construímos a pilha toda vez que a recorrência é chamada. Em linguagens de programação que suportam a cauda otimização de chamadas uma grande pilha de chamadas como esta não seria construída. A linguagem pode determinar que, se uma chamada estiver em posição final, não será necessário criar espaço adicional para ela na pilha toda vez que ela for chamada. Um exemplo da Wikipedia ilustra muito bem o procedimento. Infelizmente, uma vez que o Javascript não implementa a recursão da otimização da chamada final, é muito mais lento do que os loops tradicionais para ou while. No entanto, as chamadas finais do ECMAScript 6 serão otimizadas. Estilo de passagem de passagem Por enquanto ainda podemos escrever loops de maneira recursiva, sem ocupar mais espaço na pilha de chamadas. Isso pode ser feito com o continuation passing style (CPS). No CPS, usamos “continuações” (funções) para representar o próximo estágio de uma computação. Uma continuação é passada como um argumento para uma função de ordem superior que é então chamada por aquela função quando uma operação anterior é completada. Esse padrão é muito comum em Javascript. Pedidos AJAX e Node.js usam CPS para que a computação possa ser executada de forma assíncrona. Por exemplo: $. Get ('url', function (data) {console.log (dados);}); Neste exemplo, passamos uma continuação para o nosso método get quando os dados foram recuperados. Um exemplo mais complexo é fatorial. no CPS:

Com nosso exemplo fatorial recursivo original, uma vez que chegamos ao final do “loop”, cada resultado teve que ser retornado ao seu chamador original, significando que o programa tinha que percorrer todo o caminho de volta através da pilha para obter o resultado final.Por outro lado , com o CPS uma vez que o "loop" está no fim, a função retorna o resultado da aplicação da continuação com 1. Isso, por sua vez, aplica o resultado dessa função a outra continuação e assim por diante até chegarmos ao resultado final. Portanto, em vez de recuar até a pilha de chamadas, a função CPSFactorial cria novas funções, cada uma representando o próximo estágio da computação.Thunks e trampolinsCom o CPS, ainda há alguma recursão: o CPSFactorial chama-se várias vezes durante a computação. Podemos evitar a recursão completamente com “thunks” e “trampolins”. Uma conversão é muito parecida com uma continuação, exceto que ela é armazenada como uma estrutura de dados para uso posterior. Um trampolim gerencia os valores de execução e retorno de thunks (assim chamado porque ele rebate thunks ao redor). Em Javascript, podemos representar uma conversão da seguinte maneira: var thunk = function (f, lst) {return {tag: "thunk", func: f, args: lst};} var thunkValue = function (x) {return {tag : "valor", val: x};}; Nesse caso, nosso thunk armazena uma função e uma lista de argumentos a serem executados posteriormente. Graças aos encerramentos, os thunks têm um registro de seu ambiente quando são armazenados. A função thunkValue simplesmente retorna o valor final de nosso cálculo. Podemos manipular todos os thunks que criamos com um trampolim: var trampoline = function (thk) {while (verdadeiro) {if (thk.tag === "value") {return thk.val; } if (thk.tag === "thunk") {thk = thk.func.apply (nulo, thk.args)); }}}; Aqui, o trampolim faz uma conversão e chama sua função com seus argumentos, se tiver a tag correta, caso contrário, retorna um valor. Este exemplo quebra nossa regra de apatridia (já que reatribuímos a um novo valor a cada vez) para que pudéssemos escrever da seguinte forma: var trampoline = function (thk) {if (thk.tag === "valor") {return thk .val; } if (thk.tag === "thunk") {retorno do trampolim (thk.func.apply (null, thk.args)); }}; No entanto, voltamos a usar recursão novamente. Podemos usar thunks e um trampolim para calcular o fatorial: var thunk = function (f, lst) {return {tag: "thunk", func: f, args: lst };}} var thunkValue = function (x) {return {tag: "valor", val: x};} var thunkFactorial = função (n, cont) {if (n <2) {retorno thunk (cont, [ n]); } else {var new_cont = função (v) {var resultado = v * n; return thunk (cont, [resultado]); }; retornar thunk (thunkFactorial, [n - 1, new_cont]); }}; var trampoline = function (thk) {while (verdadeiro) {if (thk.tag === "valor") {retorno thk.val; } if (thk.tag === "thunk") {thk = thk.func.apply (nulo, thk.args); }}}; trampoline (thunkFactorial (5, thunkValue)); Neste exemplo, evitamos a recursão completamente, já que estamos sempre criando novos thunks para serem executados, em vez de funções invocando a si mesmos. Uma implementação divertida (mas sem sentido) disso é um jQuery Plugin que pode atuar como um substituto para cada método do jQuery.Optimizações na programação funcionalPropriedade do aplicativo (currying) Como o Javascript tem funções de ordem superior, podemos chamar funções com alguns de seus argumentos pré-preenchidos. Isso é conhecido como aplicação parcial ou currying. O exemplo mais simples disso é o método de vinculação do Javascript. bind simplesmente retorna uma nova função com um contexto customizado e argumentos pré-preenchidos: var bindExample = function (a, b) {retornar a / b;}; var test = bindExample.bind (null, 3); teste (4); // 0.75 Aqui o teste cria uma nova função que quando invocada já tem o argumento a cheio como 3.bind é um método ECMAScript 5 então não está disponível em todos os ambientes Javascript. Podemos escrever uma ligação customizada da seguinte forma: var bind = function (a, func) {return function () {return func.apply (null, [a] .concat (Array.prototype.slice.call (arguments))); };} var bindExample = função (a, b) {retorno a / b;}; teste var = bind (3, bindExample); teste (4); // 0.75 Exatamente como o método ES5, a função bind neste caso retorna uma nova função que quando chamada aplica a função que passamos para ela com um argumento pré-preenchido. MemoryFunctions que são caras de rodar podem ser otimizadas com memoisation. Isso envolve o uso de um fechamento para armazenar em cache os resultados das chamadas anteriores para a função. Um exemplo muito simples seria: var memoise = function (func) {var cache = {}; função de retorno (arg) {if (arg no cache) {console.log (arg + 'no cache'); return cache [arg]; } else {console.log (arg + 'não no cache'); cache de retorno [arg] = func (arg); }}; var memo = memoise (função (n) {return n * 2;}); memo (1) // 2 (1 não em cache) memo (1) // 2 (1 em cache) Aqui nós passar uma função para memoise cujos resultados desejamos armazenar em cache. Quando chamamos memo, ele recupera o valor do cache ou ele chamará a função memoised e armazenará seu valor no cache. Vale a pena notar que, para podermos memorizar uma função, ela deve ser referencialmente transparente, caso contrário, nenhum resultado será armazenado em cache.É claro que esse exemplo viola nossa regra de evitar efeitos colaterais. Infelizmente, é bastante problemático usar o memoisation sem mudar de estado, já que temos que continuar atualizando nosso cache. É mais fácil em uma linguagem como Haskell, que pode usar a avaliação preguiçosa para memoise. A mensuração é mais útil onde uma função provavelmente calcula muitos dos mesmos resultados, como a seqüência de fibonacci.
