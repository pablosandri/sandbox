
Área - Digital Analytics

# Red Venture - cartoes.itau.com.br

Última atualização: 17/10/2017



# Objetivo

Este documento tem como objetivo instruir a atualização da camada de dados para utilização de recursos de monitoramento da Adobe Analytics.

# Implementação

A documentação foi descrita para algumas áreas especificas do site.

### Global

Descrição: Mensuração obrigatória em todas as telas

```javascript 
window.analyticsData = {
	    site: {
	          "nome": "IT",
	          "ambiente": "NL",
	          "negocio": "Itaucard",
	          "tipoDeCanal": "Web",
	    },
	    page: {
	          "secao": "Cartoes",
	          "subsecao1": "UploadDeDocumentos",
	          "url": "itau.com.br",
	          "nome": "IIT:NL:NCC-RV:Cartoes:Home",
	          "templateName":"home",                                  //novo atributo
	          "descricaoDeErro": "Erro ao enviar o formulário!"
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
           "nome": "IT",
           "ambiente": "NL",
           "negocio": "Itaucard",
           "tipoDeCanal": "Web",
     },
     page: {
           "secao": "Cartoes",
           "url": "cartoes.itau.com.br/sdabj",
           "nome": "IT:NL:NCC-RV:404",                                  //atributo atualizado
           "templateName":"erro",                                       //novo atributo
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
page.nome  | string | IT:NL:NCC-RV: + erro de http
page.url  | string | window.location.href
page.descricaoDeErro  | string | Mensagem apresentada para o usuário

### Vitrine

Descrição: Na página vitrine todas as vantagens que o usuário selecionar, deve ser disparada na camada de dados.

```javascript 
window.analyticsData = {
	    site: {
	          "nome": "IT",
	          "ambiente": "NL",
	          "negocio": "Itaucard",
	          "tipoDeCanal": "Web",
	    },
	    page: {
	          "secao": "Cartoes",
	          "subsecao1": "UploadDeDocumentos",
	          "url": "itau.com.br",
	          "nome": "IIT:NL:NCC-RV:Cartoes:Home",
	          "templateName":"home",                                  //novo atributo
	          "descricaoDeErro": "Erro ao enviar o formulário!"
	    },
	    visitor: {
	          "iDPFRV": "dsf6ad8s796sd7f896s",
	          "vantagens": "carros:telefonia"                         //novo atributo
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
	          "nome": "IT",
	          "ambiente": "NL",
	          "negocio": "Itaucard",
	          "tipoDeCanal": "Web",
	    },
	    page: {
	          "secao": "Cartoes",
	          "subsecao1": "UploadDeDocumentos",
	          "url": "itau.com.br",
	          "nome": "IT:NL:NCC-RV:Cartoes:Formulario-Passo1",
	          "templateName":"home",                                   //novo atributo
	          "descricaoDeErro": "Erro ao enviar o formulário!"
	    },
	    "custom": {
     		   "versaoDoCheckout":"v1",
     		   "email":"dkjshf37462fkjshfk348",                        //novo atributo
     		   "events": ["passo1"]
		},
		"product": {
     		   "items": [{
          	  		 "sku": "TudoAzul Itaucard 2.0 Internacional MC",
     			 }],
      		    "event": "prodView"
		},
	    visitor: {
	          "iDPFRV": "dsf6ad8s796sd7f896s",
	    },
	    rule: "pageLoad"
}
```

