# jQuery cheatsheet

## jQuery e $
$ é uma referência de objeto que aponta para uma função. A variável jQuery faz o mesmo para a mesma função.
$ retorna um array-like object (jquery collection) com métodos adicionais.
Posso passar argumentos como ```$(string)```, ```$(function)``` ou ```$(DOM elemento)```. Também posso chamar métodos diretamente do $, como $.ajax().

## Selecionar elementos do DOM:
Posso selecionar elementos DOM a partir do $:
$(‘tag’), $(‘.class’) ou $(‘#id’).

## Seleção Transversal:
$(‘#Cameron’)
	.parent() – 1 level acima
	.parents() – vários leveis acima
	.children() – 1 level abaixo
	.find() – vários leveis abaixo
	.siblings() – outros elementos no mesmo nível

## Inserção de Elementos:
Para inserir elementos usa-se o .append(), .prepend(), .insertAfter() e .insertBefore()

## looping com .each()
http://api.jquery.com/each/

## Executar comandos quando o DOM é carregado
https://api.jquery.com/ready/

```$( function )``` ou ```$( document ).ready( function )``` ou...

## Lidando com eventos
```$( target ).on( event, callback)```
O callback pode usar como argumento o objeto event (do jQuery) que é fornecido quando um evento é ouvido.

https://api.jquery.com/category/events/event-object/

https://api.jquery.com/event.target/

```
$( target ).on( event, function (event) {
    console.log(event);
})
```
Para usar o evento original do browser: ```event.originalEvent```
* qualquer palavra pode ser utilizada para armazenar o evento. ex: evt, e, event.

## Delegação de eventos
```$( '.container' ).on( 'click', 'article', function() { … });```
O código ouvi eventos click no elemento de classe .container e verifica se o event.target é o 'article' mencionado.
