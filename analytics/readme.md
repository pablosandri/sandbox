Olá Rafael, boa noite. Tudo bem?

Desculpa a demora, como o William disse estava de ferias.

Mas legal análisei a implementação do ```GTM``` e ```data attributes``` e aparentemente está correta! Não encontrei a msg de erro no console. Podemos marcar uma video conferencia para sanar todas as dúvidas?

Também reparei um codigo dando push na camada de dados com um ```debugger```, podemos conversar para eu coseguir entender o proposito da implementação?

Segue o codigo:
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
