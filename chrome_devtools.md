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

Visualizar os arquivos utilizados na aplicação (html, css, js, imagens, etc.)

É possível linkar a pasta do projeto com o devtools para que alterações feitas no devtools
sejam feitas automaticamente no código fonte. (mas a explicação do professor não funciona mais
na versão do chrome que uso )

**Obs: Nesta aba, na parte de baixo, o ```{}``` serve para dar um pretty print no código. É util para códigos minified por exemplo.**
### Debug:
Basta escolher linhas de parada no código, voltar a aplicação e executa-la
- Debug JS (só escolher uma linha de parada do arquivo js)
- Debug DOM (inserção de sub-elementos, remoção de elementos, alteração de atributos)
- Debug EventListeners: aba Source > Event Listeners Break points

Só escolher quais eventos irão disparar o debug

## Aba Network

### WaterFall TimeLine
https://developers.google.com/web/tools/chrome-devtools/network-performance/reference#timing-explanation
**Queueing:** quanto tempo ficou na fila.
**Stalled:** quanto tempo atrasou.
**DNS Lookup:** procurar qual ip pertence aquela URL requisitada.
**Initial Connection:** quanto tempo durou a tentativa de conexão com o servidor.
**SSL**: faz parte da conexão especial, checa o certificado para saber se a conexão é realmente segura.

**Request sent:** duração do pedido.
**Waiting(TTFB):** duração da espera após o pedido.
**Content Download:** duração do download da resposta
