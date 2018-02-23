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

Por fim podemos iniciar os testes, declare sua string no `s.products` conforme ilustrado abaixo:
>	Obs:Caso queira enviar outras informações como event, prop e evar consulte essa [documentação]()

```javascript
s.products = 'Category;ABC123;,;ABC456;2;19.98;event1=1.99|event2=100;evar1=Ground Shipping,;;;;event3=2.9;evar3=20% off'
```

Caso queira definir mais alguma informação para testar, como Prop, eVar e eventos, consulte está [documentação]().

Agora podemos escolher como vamos enviar esse disparo para adobe.


