![CI&T](https://pablosandri.github.io/sandbox/ciandt.png)

# CI&T - Syntax of the Products Variable 

Última atualização: 19/02/2018

Em caso de dúvidas, entrar em contato com: [psandri@ciandt.com](mailto:psandri@ciandt.com)

# Objetivo

Diante da dúvidas de muitos se a Syntax da Products Merchandising está correta, eu fiz um tutorial para ajudar na homologação.

# Overview e Descrições Técnicas

## Instalação do Adobe Debugger(Não obrigatório)

Complete as etapas adequadas para o navegador desejado:
	
>	[Mozilla Firefox](https://marketing.adobe.com/resources/help/pt_BR/sc/implement/debugger_firefox.html)
>	[Google Chrome](https://marketing.adobe.com/resources/help/pt_BR/sc/implement/debugger_chrome.html)

# Implementação

## Preparando o ambiente

Primeiro vamos abrir uma página que contenha o ``dtm``, para certificar que ele exista na página, vamos abrir a ferramenta do desenvolvedor(f12), vamos procurar a lib do dtm na aba console:

Digite no console:
```javascript
s = new AppMeasurement                      //Declarando a lib AppMeasurement no escobo global

var s_account="itau.d2.sc.omtrdc.net"       //Declarando o Tracking Server
var s=s_gi('teste')			    //Declarando o Report Suite
```

## Envio das váriaveis 

Declare sua string da products no `s.products` conforme ilustrado abaixo:

>	Obs: Caso queira enviar outras informações como event, prop e evar consulte essa [documentação]()

```javascript
s.products = 'Category;ABC123;,;ABC456;2;19.98;event1=1.99|event2=100;evar1=Ground Shipping,;;;;event3=2.9;evar3=20% off'

s.tl()    // Compila todas as variáveis definidas e envia para adobe
```
Pronto, o disparo foi enviado para adobe.

## Homologação

Por fim se você estiver com o *adobe debugger* no favorito é só executar, ou execute o seguinte codigo no console.

```javascript
javascript:void(window.open("","dp_debugger","width=600,height=600,location=0,menubar=0,status=1,toolbar=0,resizable=1,scrollbars=1").document.write("<script language='JavaScript' id=dbg src='https://www.adobetag.com/d1/digitalpulsedebugger/live/DPD.js'></"+"script>"));
```

Verifique se os valores foram atribuidos nos seus respectivos lugares, conforme print.

