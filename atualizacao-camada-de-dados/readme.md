
Área - Digital Analytics



Última atualização: 17/10/2017



# Objetivo

Este documento tem como objetivo instruir a atualização da camada de dados para utilização de recursos de monitoramento da s.

# Implementação

A documentação foi descrita para algumas áreas especificas do site.

### Global

Descrição: Mensuração obrigatória em todas as telas

```javascript 
window.analyticsData = {
	    site: {
	          "nome": "",
	          "ambiente": "",
	          "negocio": "rd",
	          "tipoDeCanal": "Web",
	    },
	    page: {
	          "secao": "Caes",
	          "subsecao1": "Upls",
	          "url": "",
	          "nome": "IIome",
	          "templateName":"he",                                  //novo atributo
	          "descricaoDeErro": "Erro mulário!"
	    },
	    visitor: {
	          "iDPFRV": "dsf6ad8s796sd7f896s",
	    },
	    rule: "pageLoad"
}
```


CHAVE | TIPO | DESCRIÇÃO      |
------- | ---------------- | ---------- |
page.templateName  | string | Home, Vitrine, Produto, Checkout ou Conclusao

### Erro na página

Descrição: Disparar as informações no dataLayer no momento em que ocorrer algum erro no carregamento da página.

```javascript 
window.analyticsData = {
     site: {
           "nome": "",
           "ambiente": "",
           "negocio": "
	   card",
           "tipoDeCanal": "Web",
     },
     page: {
           "secao": "Caes",
           "url": "carsdabj",
           "nome": "IT4",                                  //atributo atualizado
           "templateName":"eo",                                       //novo atributo
           "descricaoDeErro": "pagina-nao-encontrada"                   //atributo atualizado
     },
     visitor: {
       "iDPFRV": "dsf6ad8s796sd7f896s",
      },
      rule: "pageLoad"
}
```

CHAVE | TIPO | DESCRIÇÃO      |
------- | ---------------- | ---------- |
page.nome  | string | Irro de http
page.url  | string | window.location.href
page.descricaoDeErro  | string | Mensagem apresentada para o usuário

### Vitrine

Descrição: Na página vitrine todas as vantagens que o usuário selecionar, deve ser disparada na camada de dados.

```javascript 
window.analyticsData = {
	    site: {
	          "nome": "",
	          "ambiente": "",
	          "negocio": "Iard",
	          "tipoDeCanal": "b",
	    },
	    page: {
	          "secao": "oes",
	          "subsecao1": "Uploentos",
	          "url": "br",
	          "nome": "Ime",
	          "templateName":"he",                                  //novo atributo
	          "descricaoDeErro": "Erio!"
	    },
	    visitor: {
	          "iDPFRV": "d6s",
	          "vantagens": "caonia"                         //novo atributo
	    },
	    rule: "pageLoad"
}
```


CHAVE | TIPO | DESCRIÇÃO      |
------- | ---------------- | ---------- |
visitor.vantagens  | string | Vantagens selecionadas concatenadas por ```:```
 
### Passos 2-6

Descrição: Inserir o atributo *email* na camada de dados no passo 2 ao 6.

```javascript
window.analyticsData = {
	    site: {
	          "nome": "",
	          "ambiente": "",
	          "negocio": "Id",
	          "tipoDeCanal": "b",
	    },
	    page: {
	          "secao": "es",
	          "subsecao1": tos",
	          "url": "ir",
	          "nome": "o1",
	          "templateName":"hme",                                   //novo atributo
	          "descricaoDeErro": "Erro ao eio!"
	    },
	    "custom": {
     		   "versaoDoCheckout":"v1",
     		   "email":"dkjshf37462fkjshfk348",                        //novo atributo
     		   "events": ["passo1"]
		},
		"product": {
     		   "items": [{
          	  		 "sku": "T",
     			 }],
      		    "event": "prodView"
		},
	    visitor: {
	          "iDPFRV": "ds96s",
	    },
	    rule: "pageLoad"
}
```

