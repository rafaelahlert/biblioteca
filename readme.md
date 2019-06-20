# Biblioteca com funções matemáticas para o dia-a-dia

     Tem o intuito de facilitar a vida dos usuários, automatizando tarefas e cálculos necessários na
     rotina de cada um.

## Transforma Quilômetros em metros e metros em centímetros
    Muitas pessoas tem dificuldade em trasformação de grandezas, essa função automatiza isto.
    Basta a pessoa entrar com o parâmetro que irá informar os quilômetros e a função faz o resto.

````js
function km(a) {
        var metros = a*1000
        var cm = metros*100

        console.log("Em metros: " + metros + " m" + ". Em centímetros: " + cm + " cm.")
}

km(20)

````

## Transforma polegadas em centímetros
    
### Uma breve introdução do que são polegadas:
    São apenas unidades de comprimentos utilizadas no sistema imperial, muito presentes no cotidiano, como referencial da tela de televisões e monitores. Uma polegada refere-se a 2,54 centímetros.

    Então o usuário basta entre com o parâmentro informando quantas polegdas são que a função tratará de calcular o resultado. 

```` js
function polegadas(a) {
    var b = a* 2.54
    console.log(b + "cm")  
}
polegadas(5)

 ````
