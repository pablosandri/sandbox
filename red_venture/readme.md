Área - Digital Analytics

# Red Venture - cartoes.itau.com.br

Última atualização: 26/10/2017

Em caso de dúvidas, entrar em contato com: [psandri@ciandt.com](mailto:psandri@ciandt.com)

# Objetivo

Este documento tem como objetivo instruir a atualização da camada de dados para utilização de recursos de monitoramento da Adobe Analytics.

# Implementação

A documentação foi descrita para algumas áreas especificas do site.

## Passos do Funil

### Merchandising

Descrição: Atualizar o ```product```, com detalhes do produto.

```javascript 
window.analyticsData = {
	 product: {
	       items: [{
	       		 "merchandising":{
	       		 	"cdc:bandeira": "Mastercard",
	       		 	"cdc:portfolio": "Walmart",
	       		 	"cdc:rendaminima": "R$1.000",
	       		 	"cdc:variante": "Internacional"
	       		 },	
	             "nome": "Walmart Itaucard 2.0 Internacional MasterCard",
	             "sku": "9004"
	       }],
	       "event": "prodView"
	 }
}
```


CHAVE | TIPO | DESCRIÇÃO      |
------- | ---------------- | ---------- |
merchandising  | objeto | Objeto para armazenar detalhes do produto.
cdc:bandeira  | string | Bandeira do cartão
cdc:portfolio  | string | Cliente vinculado ao cartão. Exemplo: Extra, Netshoes, Classicos e etc.
cdc:rendaminima  | string | Renda mínima vinculada ao cartão.
cdc:variante	| string | Variante do produto. Exemplo: Internacional, Nacional, Platinum e etc.

### PageName

Descrição: Alterar os valor da chave ```pageName``` dos formularios.

De:
 IT:NL:NCC-RV:Cartoes:Formulario-Passo1, Passo2..., Passo6, Conclusão.

Para:
 IT:NL:NCC-RV:Cartoes:Formulario-Dados-passo1, Dados-passo2..., Personalizacao, Conclusao.

### PropostaRV

Descrição: Com o intuito de serializar os eventos dos Steps, precisamos da propostaRV em todos os Steps.

```javasctipt
window.analyticsData = {
	 custom: {
	       "versaoDoCheckout":"v1",
	       "email":"dkjshf37462fkjshfk348",
	       "events": ["passo6"],
	       "iDPropostaRedVentures":"HUDHUH47"
	 }
}
```
