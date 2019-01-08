Olá Rafael, boa noite. Tudo bem?

Desculpe a demora, conforme o William disse estava de férias.

Mas legal, analisei a implementação do ```GTM``` e ```data attributes```, aparentemente está correta! Não encontrei a msg de erro no console. Podemos marcar uma videoconferência para sanar todas as dúvidas?

Também reparei um código dando push na camada de dados com um debugger, podemos conversar para eu conseguir entender o propósito da implementação?

Segue o código:

``` javascript
	window.dataLayer = window.dataLayer || [];
	var listProducts = GetProductsSku();
	debugger;
	window.dataLayer.push({
		'products': [listProducts]
	}); 
	
	function GetProductsSku(){
	
		var list = document.querySelectorAll('.gtm-link-event');
		var listToArray = Array.prototype.slice.call(list);
		var data = [];
		var product = '';
		debugger;
		for(var i = 0; i < listToArray.length; i++)
		{
			product = listToArray[i].dataset;
			data.push({'category': product.gtmEventCategory, 'product': product.gtmEventAction, 'plu': product.gtmEventLabel });
		}
		
		return data;
	}
  ```
  
  Qualquer dúvida estou à disposição.
  Abraços
