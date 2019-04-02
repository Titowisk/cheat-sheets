# Curso HTML e CSS II da Alura

## Position: absolute

O elemento é posicionado absolutamente com relação ao primeiro bloco pai que possua um position: relative,absolute, fixed... 
(tudo menos static)
Caso não haja, ele irá se posicionar baseado na tela do navegador.

## CSS3 e navegadores:

Os principais browsers usam estes prefixos para suas funcionalidades BETA:
-webkit- (Chrome, Safari, newer versions of Opera, almost all iOS browsers (including Firefox for iOS); 
basically, any WebKit based browser)
-moz- (Firefox)
-o- (Old, pre-WebKit, versions of Opera)
-ms- (Internet Explorer and Microsoft Edge)

Com isso, podemos colocar todos os prefixos no código para testar em todos os navegadores. Mas ainda não é o suficiente, pois no **futuro** as funcionalidades não estarão mais em teste e o site precisa continuar funcionando, então também se **faz necessária a linha sem os prefixos**:
```
-webkit-border-radius: 10px;
-moz-border-radius: 10px;
-ms-border-radius: 10px;
-o-border-radius: 10px;
border-radius: 10px;
```
Desse modo, seu site funciona no presente e fica Future Proof, para quando as funcionalidades não mais estiverem em BETA.
