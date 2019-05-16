# Chrome DevTools

## Aba Elements > Styles:

- É possível selecionar a cor clicando no quadradinho da cor.
- É possível adicionar e remover classes clicando em .cls (cls = classe)

## Aba Console

```
console.log() // mostra mensagens
console.error() // mostra uma mensagem com formatação de erro
console.warn() // mostra uma mensagem com formatação de aviso
console.assert(condition, msg) // mostra uma msg de erro, caso a condição não seja atendida
```

```
console.group()
console.groupEnd() // serve para agrupar erros
console.table(matrix) // mostra uma tabela no console
```

- É possível preservar as msgs de erro ao clicar na engrenagem e depois em ```Preserve Log```
- Na aba elements, ao apertar ```esc```, o console abre em uma janela abaixo.
- Pode-se acessar os elementos do DOM ao clicar em cima de um elemento e escrever o ```$0```

Vai de ```$0``` até ```$4```, mostrando assim os últimos 5 elementos navegados na árvore DOM pelo devtools

## Aba Source:

- Visualizar os arquivos utilizados na aplicação (html, css, js, imagens, etc.)

- serve para debugar a aplicação:

Basta escolher linhas de parada no código, voltar a aplicação e executa-la

- É possível linkar a pasta do projeto com o devtools para que alterações feitas no devtools
sejam feitas automaticamente no código fonte.
