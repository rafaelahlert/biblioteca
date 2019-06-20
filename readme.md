# Ponteiros em C
A utilização de ponteiros em linguagem C é uma das características que tornam a linguagem tão flexível e poderosa.

Ponteiros ou apontadores, são variáveis que armazenam o endereço de memória de outras variáveis.

Dizemos que um ponteiro “aponta” para uma varíável quando contém o endereço da mesma.

Os ponteiros podem apontar para qualquer tipo de variável. Portanto temos ponteiros para int, float, double, etc.

```` C
#include <stdio.h>
void main()
{
  int a;
  int b;
  int c;
  int *ptr;  // declara um ponteiro para um inteiro
             // um ponteiro para uma variável do tipo inteiro
  a = 90;
  b = 2;
  c = 3;
  ptr = &a;
  printf("Valor de ptr: %p, Conteúdo de ptr: %d\n", ptr, *ptr);
  printf("B: %d, C: %d"), b, c);
} 

````

## Por que usar ponteiros?

Ponteiros são muito úteis quando uma variável tem que ser acessada em diferentes partes de um programa.

Neste caso, o código pode ter vários ponteiros espalhados por diversas partes do programa, “apontando” para a variável que contém o dado desejado.

Caso este dado seja alterado, não há problema algum, pois todas as partes do programa tem um ponteiro que aponta para o endereço onde reside o dado atualizado.

Existem várias situações onde ponteiros são úteis, por exemplo:

- Alocação dinâmica de memória

- Manipulação de arrays.

- Para retornar mais de um valor em uma função.

- Referência para listas, pilhas, árvores e grafos

## Impressão de Ponteiros

Em C, pode-se imprimir o valor armazenado no ponteiro (um endereço), usando-se a função printf com o formatador %p na string de formato. Por exemplo:

````C
#include <stdio.h>
void main()
{
  int x;
  int *ptr;
  ptr = &x;
  printf("O endereço de X é: %p\n", ptr);
}
````
## Acessando o Conteúdo de uma Posição de Memória através de um Ponteiro

Para acessar o conteúdo de uma posição de memória, cujo endereço está armazenado em um ponteiro, usa-se o operador de derreferência (*). Por exemplo:

````C
#include <stdio.h>
void main()
{
  int x;
  int *ptr;
  x = 5;
  ptr = &x;
  printf("O valor da variável X é: %d\n", *ptr);  // derreferenciando um ponteiro
  *ptr = 10;  // usando derreferencia no "lado esquerdo" de uma atribuição
  printf("Agora, X vale: %d\n", *ptr);
}

````
## Alocação Dinâmica de Memória

Durante a execução de um programa, pode-se alocar dinamicamente memória para usar como variáveis do programa. Em C, a alocação é feita com a função malloc (e, para liberar memória, usa-se a função free). 
````C

#include <stdlib.h>
#include <stdio.h>

void main()
{
 int *ptr_a;

 ptr_a = malloc(sizeof(int));
 // cria a área necessária para 01 inteiro e
 // coloca em 'ptr_a' o endereço desta área.

  if (ptr_a == NULL)
  {
    printf("Memória insuficiente!\n");
    exit(1);
  }

  printf("Endereço de ptr_a: %p\n",  ptr_a);
  *ptr_a = 90;
  printf("Conteúdo de ptr_a: %d\n", *ptr_a);  // imprime 90
  free(ptr_a);  // Libera a área alocada
} 

````
## Alocação de Vetores

Nos exemplos anteriores, foi alocado um espaço para armazenar apenas um dado do tipo int. Entretanto, é mais comum utilizar ponteiros para alocação de vetores. Para tanto, basta especificar o tamanho desse vetor no momento da alocação. Nos exemplos abaixo, apresenta-se a alocação de vetores com malloc e new. Após a alocação de uma área com vários elementos, ela pode ser acessada exatamente como se fosse um vetor.

````C

#include <stdlib.h>
void main()
{
  int i;
  int *v;
  v = (int*)malloc(sizeof(int)*10);  // 'v' é um ponteiro para uma área que
                                     // tem 10 inteiros.
                                     // 'v' funciona exatamente como um vetor
  v[0] = 10;
  v[1] = 11;
  v[2] = 12;
  // continua...
  v[9] = 19;

  for(i = 0; i < 10; i++)
    printf("v[%d]: %d\n", i, v[i]);

  printf("Endereço de 'v': %p", v);  // imprime o endereço da área alocada para 'v'
  free(v);
} 
````
## Aritmética de Ponteiros

Além de acessar os dados de uma área alocada dinâmicamente como se fosse um vetor, é possível acessá-los através do próprio ponteiro, utilizando a técnica chamada aritmética de ponteiros. 

````C
#include <stdlib.h>
void main()
{
  int *vet;
  int *ptr;

  vet = (int*)malloc(sizeof(int)*10);
  vet[4] = 44;  // 'vet' funciona como um vetor, depois de malloc

  ptr = vet;  // 'ptr'  aponta para o início da
              // área alocada por 'vet

  *ptr = 11;  // vet[0] = 11
              // coloca 11 na primeira posição da área alocada

  ptr++;      // avança o apontador
  *ptr = 12;  // vet[1] = 12

  printf("%p\n",  ptr);
  printf("%d\n", *ptr);
  
  // free(ptr);  // Liberar 'ptr' direto causa NULL POINTER ASSIGNMENT
  // Corrigindo, a forma correta é:
  ptr--;
  free(ptr);
}
````

## Realocação de Memória

Se for preciso aumentar o tamanho do vetor, use:

````C
realloc(ptr, novo_tam);
````

Exemplo:

````C
// código (...)
cadastro = (TPESSOA*)realloc(cadastro, 20);
ptr = cadastro;
// a área de memória é realocada, e todos os dados são copiados da área antiga para a área nova.
````
 
## Testes de Alocação

Para verificar se foi possível alcar a memória solicitada, pode-se testar o valor do ponteito usado para armazenar a área alocada. Se o valor deste ponteiro for NULL, não foi possível alocar a memória.

````C
int *ptr;
ptr = (int*)malloc(sizeof(int)*10);
if (ptr == NULL)
{
  printf("Não foi possível alocar memória!\n");
  exit(1);
}

````

# Referências PHP

## O que as referências fazem 

Há três operações básicas ao se utilizar referências: atribuição por referência, passagem por referência, e retorno por referência. Esta seção fará uma introdução dessas operações, com links para leituras posteriores.

## Atribuição por referência 

Referências no PHP permitem criar duas variáveis que se referem ao mesmo conteúdo. Ou seja, quando você faz:
 
 ```` PHP
<?php
$a =& $b;
?>

````
então aqui $a e $b apontam para o mesmo conteúdo.

>$a e $b são completamente iguais aqui, mas não porque $a está apontando para $b ou vice versa, mas sim que $a e $b apontam para o mesmo lugar.

>Se você atribuir, passar ou retornar uma variável indefinida por referência, ela irá ser criada.

## Usando referência com variáveis indefinidas

````php
<?php
function foo(&$var) { }

foo($a); // $a é "criada" e setada par null

$b = array();
foo($b['b']);
var_dump(array_key_exists('b', $b)); // bool(true)

$c = new StdClass;
foo($c->d);
var_dump(property_exists($c, 'd')); // bool(true)
?>

````
A mesma sintaxe pode ser utilizada com funções, que retornem referências, e com o operador new (a partir do PHP 4.0.4 e antes do PHP 5.0.0):

````PHP
<?php
$foo =& find_var($bar);
?>
````

>Se você atribuir uma referência para uma variável declarada global dentro da função, a referência irá ser visível somente dentro da função. Você pode evitar isto usando o array ``$GLOBALS.``

## Referenciando variáveis globais de dentro de funções

````PHP
<?php
$var1 = "Example variable";
$var2 = "";

function global_references($use_globals)
{
    global $var1, $var2;
    if (!$use_globals) {
        $var2 =& $var1; // visível somente dentro da função
    } else {
        $GLOBALS["var2"] =& $var1; // visível também no contexto global
    }
}

global_references(false);
echo "var2 is set to '$var2'\n"; // var2 is set to ''
global_references(true);
echo "var2 is set to '$var2'\n"; // var2 is set to 'Example variable'
?>
````

>Se você atribuir um valor para uma variável com referência numa instrução foreach a referência também é modificada.

 ## Referências e o comando foreach
````PHP
<?php
$ref = 0;
$row =& $ref;
foreach (array(1, 2, 3) as $row) {
    // faz alguma coisa
}
echo $ref; // 3 - último elemento do array iterado
?>
````

Ainda que não seja uma atribuição por referência explícita, expressões criadas com o constructo array() também podem se comportar como tais com o prefixo & no elemento de array a ser acrescentado. Exemplo:
````PHP
<?php
$a = 1;
$b = array(2, 3);
$arr = array(&$a, &$b[0], &$b[1]);
$arr[0]++; $arr[1]++; $arr[2]++;
/* $a == 2, $b == array(3, 4); */
?>
````

Note que referências dentro de arrays são potencialmente perigosas. Fazer uma atribuição normal (sem referência) com uma referência à direita não transforma a expressão a esquerda numa referência, mas referências dentro de arrays são preservadas nessas atribuições normais. Isso também se aplica a chamadas de função onde arrays são passados por valor. Exemplo:

````PHP
<?php
/* Atribuição de variáveis escalares */
$a = 1;
$b =& $a;
$c = $b;
$c = 7; //$c não é referência; não modifica $a ou $b

/* Atribuição de variaveis do array */
$arr = array(1);
$a =& $arr[0]; //$a e $arr[0] estão no mesmo conjunto de referências
$arr2 = $arr; //não atribui por referência!
$arr2[0]++;
/* $a == 2, $arr == array(2) */
/* O conteúd de $arr foi modificado mesmo que ele não seja uma referência! */
?>
````

Em outras palavras, o comportamento de referências em arrays é definido elemento por elemento. O comportamento de referências dos elementos individualmente são dissociados da referência do container array.
Passagem por referência ¶
A segunda coisa que referências fazem é passar variáveis por referência. Isso é feito com a criação de uma variável local em uma função e uma variável no escopo chamador que referênciem o mesmo conteúdo. Assim:
````PHP
<?php
function foo(&$var)
{
    $var++;
}

$a=5;
foo($a);
?>
````

A variável $a será 6 no final. Isto ocorre porque na função foo a variável $var se referem ao mesmo conteúdo de $a. Para mais informações disso veja a seção de passagem por referência


# Funções: parâmetro, retorno e recursividade 

Funções são blocos de construção fundamentais em JavaScript. Uma função é um procedimento de JavaScript - um conjunto de instruções que executa uma tarefa ou calcula um valor. Para usar uma função, você deve defini-la em algum lugar no escopo do qual você quiser chamá-la.

A definição da função (também chamada de declaração de função) consiste no uso da palavra chave function, seguida por:

- Nome da Função.
- Lista de argumentos para a função, entre parênteses e separados por vírgulas.
- Declarações JavaScript que definem a função, entre chaves { }.

Por exemplo, o código a seguir define uma função simples chamada square:

````js
function square(numero) { 
  return numero * numero; 
}
````
Toda função em JavaScript é um objeto ``Function``. Veja ``Function`` para informação das propriedades e métodos dos objetos ``Function``.

Funções não são como procedimentos (procedure). Uma função sempre retorna um valor, mas um procedimento pode ou não retornar um valor.

Para retornar um valor diferente do padrão, uma função deve ter uma instrução ``return`` que específica o valor a ser retornado. Uma função sem um`` return`` retornará um valor padrão. No caso de um ``método construtor`` chamado com a palavra reservada ``new``, o valor padrão é o valor do parâmetro this. Para todas as outras funções, o valor padrão de retorno é ``undefined``.

Os parâmetros de uma função são chamados de argumentos da função. Argumentos são passados para a função por valor. Se uma função muda o valor de um argumento, esta mudança não é refletida globalmente ou na chamada da função. Contudo, referência de objetos são valores também, e eles são especiais: se a função muda as propriedades do objeto referenciado, estas mudanças são visíveis fora da função, como é mostrado no exemplo a seguir:

```` js
/* Declare a função 'minhaFunção' */
function minhaFuncao(objeto) {
   objeto.marca = "Toyota";
 }
 
 /*
  * Declare a variável 'meucarro';
  * crie e inicialize um novo Objeto;
  * atribua referência para 'meucarro'
  */
 var meucarro = {
   marca: "Honda",
   modelo: "Accord",
   ano: 1998
 };

 /* Exibe 'Honda' */
 console.log(meucarro.marca);

 /* Passe a referência do objeto para a função */
 minhaFuncao(meucarro);

 /*
  * Exibe 'Toyota' como valor para a propriedade 'marca'
  * do objeto, mudado pela função.
  */
 console.log(meucarro.marca);
 ````

A palavra reservada ``this`` não se refere a função sendo executada no momento, então você deve referenciar um objeto ``Function`` pelo nome, mesmo dentro do corpo da função.

## Parâmetros de funçãoSeção
Começando com ECMAScript 6, há dois tipos novos de parâmetros: parâmetros padrão e parâmetros rest.

## Parâmetros padrão 
Em JavaScript, parâmetros padrões de funções são undefined. No entanto, em algumas situações pode ser útil definir um valor padrão diferente. Isto é onde os parâmetros padrão podem ajudar.

No passado, a estratégia geral para definir padrões era testar os valores de parâmetro no corpo da função e atribuir um valor se eles fossem undefined. Se, no exemplo a seguir, nenhum valor é fornecido para b na chamada, seu valor seria undefined ao avaliar a*b e a chamada para multiplicar retornaria NaN. No entanto, isso é pego com a segunda linha neste exemplo:

````js
function multiplicar(a, b) {
  b = typeof b !== 'undefined' ?  b : 1;

  return a*b;
}

multiplicar(5); // 5
````

Com parâmetros padrão, a verificação no corpo da função não é mais necessária. Agora você pode simplesmente colocar 1 como valor padrão para b no campo de declaração de parâmetros:

````js
function multiplicar(a, b = 1) {
  return a*b;
}

multiplicar(5); // 5
````
## Parâmetros rest
A sintaxe de parâmetro rest permite representar um número indefinido de argumentos como um array. No exemplo, usamos parâmetros rest para coletar argumentos do segundo argumento ao último. Então os multiplicamos pelo primeiro argumento. Neste exemplo é usado uma função seta, que será introduzida na próxima seção.

````js
function multiplicar(multiplicador, ...args) {
  return args.map(x => multiplicador * x);
}

var arr = multiplicar(2, 1, 2, 3);
console.log(arr); // [2, 4, 6]
````

## Retorno

Define o valor retornado por uma função. Quando não há um valor especificado, undefined será retornado.
Interrompe a execução da função atual.
Retorno com valor

````js
function retornaValor() {
    return 1;
}
console.log(retornaValor());
````

O código acima imprime 1 no console.

## Retorno sem valor

````js
function retornoVazio() {
    return;
}
console.log(retornoVazio());
````

O código acima imprime undefined no console.

## Retorno fora de função (global)

Por outro lado, se você tentar usar o return fora de uma função, num código executado num navegador, receberá um erro. Por exemplo, no Chrome, obtive:

````js
Uncaught SyntaxError: Illegal return statement
````

## Retorno de bloco {}

Mesmo se usado dentro de um bloco de código, o return irá finalizar a função atual ou causar o erro como já descrito. Não existe o conceito de retorno de um bloco. Exemplo

````js
function f(val) {
    if (val) {
        return 1;
    } else {
        return 2
    }
}
````

O código acima irá retornar 1 ou 2 para a função, independendo das chaves.

## Quanto e como usar o return

Algumas pessoas acreditam que cada método/função deve ter um ponto de saída único. Considere o seguinte exemplo:
````js
function f(a, cond) {
    if (cond) {
        return -2;
    } else {
        for (var i = 0; i < a.length; i++) {
            if (a[i] == 1) return i;
        }
    }
    return -1;
}
````

Esta função é pequena, mas logo podem surgir dezenas condições e returns, tornando o código difícil de entender.

Uma alternativa seria a seguinte:

````js
function f(a, cond) {
    val retorno = cond ? -2 : -1;
    if (!cond) {
        for (var i = 0; i < a.length; i++) {
            if (a[i] == 1) {
                retorno = i;
                break;
            }
        }
    }
    return retorno;
}
````

## Recursividade


Quando você precisa executar a mesma tarefa repetidas vezes, pode ser um caso onde a recursão vai ser útil.

Vamos a um exemplo bastante útil: você vai mostrar uma mensagem a cada vez que um grilo chiar. Você passa como parâmetro da função, quantas vezes você quer que aconteça o chiado, e a função retorna com a palavra chirp a cada vez.

Sem usar recursão, nossa implementação se pareceria com isso:

````JS
function chirp(n) {
  var ch = 'chirp';
  if( n < 1 || isNaN(n) ) return;
  for( var i = n - 1; i--; ) {
    ch += '-chirp';
  }
  return ch;
}
````

Invocando a função, temos como resultado:

````JS
chirp( 3 ); // => "chirp-chirp-chirp"
````

Agora, usando o formato recursivo:

````JS
function chirp( n ) {
  if( n < 1 || isNaN( n ) ) return;
  return n < 2 ? 'chirp' : chirp( n - 1 ) + '-chirp';
}
````

E a invocação traz o mesmo resultado:

````JS
chirp( 3 ) // => "chirp-chirp-chirp"

````

# Biblioteca jQuery 

Por conta das dificuldades enfrentadas pelos programadores JavaScript para páginas Web, foi criada uma biblioteca que traz diversas funcionalidades voltadas à solução dos problemas mais difíceis de serem contornados com o uso do JavaScript puro.
Uma biblioteca é um arquivo de JavaScript que contém um monte de funções, e essas funções realizam alguma tarefa útil para sua página web.

A principal vantagem na adoção de uma biblioteca de JavaScript é permitir uma maior compatibilidade de um mesmo código com diversos navegadores. Uma maneira de se atingir esse objetivo é criando funções que verificam quaisquer características necessárias e permitam que o programador escreva um código único para todos os navegadores.

Além dessa vantagem, o jQuery, que é hoje a biblioteca padrão na programação front-end para Web, traz uma sintaxe mais "fluida" nas tarefas mais comuns ao programador que são: selecionar um elemento do documento e alterar suas características.

O jQuery é um Framework do JavaScript, um Framework é constituído de métodos prontos e compilados em um arquivo só, desenvolvido para facilita a programação.
O jQuery foi criado sob a ideia de “Write less, do more” (Escreva menos, faça mais) e é exatamente por causa disso que ele é tão surpreendente.
Quando você aprender como usar jQuery, você será capaz de executar todas os tipos de ações com facilidade.
Com jQuery é possível fazer diversos efeitos com poucas linhas e, que custariam dezenas de linhas em JavaScript puro.

## Alguns recursos oferecidos pelo jQuery

- Seleção e manipulação de elementos HTML

- Manipulação de CSS

- Efeitos e animações

- Navegação pelo DOM

- Ajax

- Eventos

O Jquery destina-se a adicionar interatividade e dinamismo às páginas web, proporcionando ao desenvolvedor funcionalidades necessárias à criação de scripts que visem a incrementar, de forma progressiva e não obstrutiva, a usabilidade, a acessibilidade e o design, enriquecendo  a experiência do usuário.

## Como usar

Necessário incluir a biblioteca jQuery. Podendo baixar, ou usar de uma CDN.
``` javascript

<script src="jquery.min.js"></script>
```

## jQuery - A função $

O jQuery é uma grande biblioteca que contém diversas funções que facilitam a vida do programador. A mais importante delas, que inicia a maioria dos códigos, é a função $.

Com ela é possível selecionar elementos com maior facilidade, maior compatibilidade, e com menos código. Por exemplo:

``` javascript
// JavaScript "puro"
var cabecalho = document.querySelector("#cabecalho");

if (cabecalho.attachEvent) {
  cabecalho.attachEvent("onclick", function (event) {
    alert("Você clicou no cabeçalho, usuário do IE!");
  });
} else if (cabecalho.addEventListener) {
  cabecalho.addEventListener("click", function (event) {
    alert("Você clicou no cabeçalho!")
  }, false);
}

// jQuery
$("#cabecalho").click(function (event) {
  alert("Você clicou no cabeçalho!");
});
```
Com a utilização do JQuery o codigo passa a ser:

``` javascript

// jQuery
$("#cabecalho").click(function (event) {
  alert("Você clicou no cabeçalho!");
});
```
Note que a sintaxe do JQuery é bem menor.

## Exemplos de jQuery

Você pode criar efeitos de slide com apenas algumas linha de código.
Você pode usar os comandos SlideDown(), SlideUp() e SlideToogle().
```` javascript
$("#flip").click(function(){
 $("#panel").slideDown();
});
````

Com jQuery, você também pode esconder os elementos em HTML com os comandos Hide() e Show(). Veja:

```` javascript
$("#hide").click(function(){
 $("p").hide();
});
$("#show").click(function(){
 $("p").show();
});
````
E aqui está um exemplo de animação:
```` javascript
$("button").click(function(){
 $("div").animate({
     left: '250px',
     height: '+=150px',
     width: '+=150px'
 });
});
````

E aqui você vê o fragmento de um código para entender como manipular o CSS.

```` javascript
$("button").click(function(){
 $("h1, h2, p").toggleClass("blue");
});
````