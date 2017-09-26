![Zoly](http://lucida-brasil.github.io/public/Images/zoly-logo.png)

Área - Digital Analytics

# Sadia - Kits Natalinos

Última atualização: 12/09/2017

Em caso de dúvidas, entrar em contato com: [brf@zoly.com.br](mailto:brf@zoly.com.br)

## Índice
- [Objetivo](#objetivo)
- [Overview e Descrições Técnicas](#overview-e-descrições-técnicas)
    - [Google Tag Manager](#google-tag-manager)
    - [Camada de dados](#camada-de-dados-datalayer)
    - [Atributos HTML](#atributos-html-data-attributes)
    - [Eventos](#eventos)
- [Implementação](#implementação)
    - [Seções](#seções)
      - [User](#user)
        - [Login](#login)
        - [Logout](#logout)
        - [Cadastro](#cadastro)
      - [Enhanced-ecommerce](#enhanced-ecommerce)
        - [Product detail](#product-detail)
        - [Add to Cart](#add-to-cart)
        - [Checkout](#checkout)
          - [Step 1](#step-1---click-para-finalizar)
          - [Step 2](#step-2---selecionou-entrega)
          - [Step 3](#step-3---selecionou-entrega-ou-retirada)
          - [Step 4](#step-4---abriu-o-form-de-identificação)
          - [Step 5](#step-5---abrir-o-form-de-pagamento)
          - [Step 6](#step-6---sucesso-ao-preencher-o-form-de-pagamento)
      - [Outros](#outros)
        - [Botão Assistente de compra](#click-no-botão-assistente-de-compra)
        - [Botão Mostre os Melhores Presentes](#clique-no-botão-mostre-os-melhores-presentes)
        - [Enviar e-mail](#click-enviar-o-e-mail)

# Objetivo
Este documento tem como objetivo instruir a implementação do Google Tag Manager e a camada de dados para utilização de recursos de monitoramento do Google Analytics, referentes ao [Wireframe](https://app.zeplin.io/projects)

# Overview e Descrições Técnicas

## Google Tag Manager

É uma ferramenta da Google onde são inseridas pequenas instruções javascript com a finalidade de estruturar a coleta dados e unificar diversos fornecedores de tags terceiros sem a necessidade de várias implementações complexas de hardcode do projeto. 

- Instalação

  Para instalar o  Google Tag Manager é preciso que o desenvolvedor inclua os códigos abaixo no HTML do site, em todas as páginas do site proposto. Caso o site possua algum template comum que é inserido em todas as páginas, também pode ser utilizado.

Cole o código abaixo após a tag `<head>` do site:

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start': new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0], j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src='https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);})(window,document,'script','dataLayer','GTM-P8JD8JT');</script>
<!-- End Google Tag Manager -->
```

Cole o código abaixo, após a tag `<body>` do site:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-P8JD8JT" height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```

## Camada de dados (DataLayer)

É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação. 

- Instalação

Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'atributo1': 'valor1',
    'atributo2': 'valor2'
  });
</script>
```

## Atributos HTML (Data Attributes)

São atributos customizados inseridos nos elementos HTML da página que permite a inclusão de dados adicionais.

- Instalação

1. Elementos de link: ```<a href="..." class="minha_classe">Link</a>```

Elementos do tipo link que foram mapeados, precisam receber a classe **gtm-link-event** e os data attributes em sua estrutura.

```html
<a href="http://www.meudominio.com.br/page2"
  class="minha_classe gtm-link-event"
  data-gtm-event-category="exemplo valor categoria"
  data-gtm-event-action="exemplo valor acao"
  data-gtm-event-label="exemplo valor rotulo">Texto do link</a>
```

2. Elementos comuns: ```<div class="minha_classe">Elemento</div>```

Todos os elementos comuns do html que não são links e que foram mapeados, precisam receber a classe **gtm-element-event** em sua estrutura.
    
```html
<div class="minha_classe gtm-element-event" 
  data-gtm-event-category="exemplo valor categoria"
  data-gtm-event-action="exemplo valor acao"
  data-gtm-event-label="exemplo valor rotulo">Texto do elemento</div>
```

## Eventos

São estruturas de dados que muitas vezes são consideradas como conversões ou micro conversões e servem para identificar as interações do usuário que foram mapeadas para coleta. Esses eventos podem ser implementados através de Data Atributos ou Camada de Dados conforme descrito acima.

- Conversões (KPI’s) 

São os principais indicadores (métricas) do site e são utilizadas para acompanhar os resultados, por exemplo: cadastro de lead’s, transações.
As conversões geralmente serão implementadas através de Camada de Dados para garantir uma maior qualidade dos dados coletados.

- Micro-conversões (Interações)
São métricas secundárias utilizadas para entender as interações dos usuários até chegarem às conversões principais.
As micro-conversões geralmente serão implementadas através de Data Atributos.

---

# Implementação

A documentação foi descrita para algumas áreas especificas do site.

> Os valores entre colchetes `[]` são variáveis, devem ser preenchidas conforme a tabela de `chave e descrição`.

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais.

> *Obs:* Caso não houver algum valor preencher com `undefined`.

## Seções

### User

#### Login

Descrição: Disparar as informações no dataLayer no callback da função de login.

```javascript
  window.dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'login', // fixo
    'userId': '[[D14555]]',
    'eventCategory': 'autenticacao', // fixo
    'eventAction:': 'login', //fixo
    'eventLabel': '[tentativa | sucesso ]'
  });
```

| CHAVE | TIPO | DESCRIÇÃO |
| :---- | :--: | :-------- |
| userId | string | Identificador único do usuário |
| eventLabel | string | Sucesso ou tentativa do login |


#### Logout
Descrição: Disparar as informações no dataLayer no callback da função de logout em caso de sucesso.

```javascript
  window.dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'logout', // fixo
  });
```

#### Cadastro

Descrição: Disparar as informações no dataLayer no callback da função de cadastro.

```javascript
  window.dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'event', // fixo
    'eventCategory': 'autenticacao', //fixo
    'eventAction': 'cadastro', //fixo
    'eventLabel': '[tentativa | sucesso]'
  });
```

| CHAVE | TIPO | DESCRIÇÃO |
| :---- | :--: | :-------- |
| eventLabel |  string | Sucesso ou tentativa do cadastro |

### Enhanced-ecommerce

#### Product detail

Descrição: Disparar as informações no dataLayer nas páginas de detalhes do produto.

```javascript
  dataLayer.push({
  'event': 'product-detail',
  'eventCategory': 'pagina-de-produto', //fixo
  'eventAction': 'abriu', //fixo
  'eventLabel': 'abriu', //fixo
    'ecommerce': {
      'detail': {
        'products': [{
    'name': '[kit-conquista]',     
    'id': '[12345]',
    'price': '[100,50]',
    'brand': '[sadia]',
    'category': '[linha-classica]',
         }]
       }
     }
  });
```

| CHAVE | TIPO | DESCRIÇÃO |
| :---- | :--: | :-------- |
| name | string | Nome do Kit |
| id | string | Identificador único do Kit |
| price | number | Preço do Kit |
| brand | string | Marca do Kit. Exemplo: 'sadia' 'perdigao' |
| category | string | Categoria do Produto. Exemplo: 'linha classica' ''linha premium' |

#### Add to Cart

Descrição: Disparar as informações no dataLayer quando ocorrer a adição de algum produto ao carrinho.

```javascript
dataLayer.push({
  'event': 'addToCart',
  'eventCategory': 'funil-de-transacao', //fixo
  'eventAction': 'adicionar-ao-carrinho', //fixo
  'eventLabel': ['kit_gloria'], 
  'ecommerce': {
    'currencyCode': 'BRL',
    'add': {                               
      'products': [{                       
        'name': '[kit_gloria]',
        'id': '[k12345]',
        'price': '[100.25]',
        'brand': '[sadia]',
        'category': '[linha_premium]',
        'quantity': 3
       }]
    }
  }
});
```

| CHAVE | TIPO | DESCRIÇÃO |
| :---- | :--: | :-------- |
| name | string | Nome do Kit |
| id | string | Identificador único do Kit |
| price | number | Preço do Kit |
| brand | string | Marca do Kit. Exemplo: 'sadia' 'perdigao' |
| category | string | Categoria do Produto. Exemplo: 'linha classica' ''linha premium' |
| quantity | number | Quantidade adicionada |

#### Checkout

##### Step 1 - Click para finalizar

Descrição: Disparar as informações no dataLayer no momento do clique para *Finalizar compra* dentro do Carrinho.

```javascript
 dataLayer.push({
    'event': 'checkout',
    'eventCategory': 'funil-de-transacao', //fixo
    'eventAction': 'checkout', //fixo
    'eventLabel': 'ir-para-checkout', //fixo 
    'ecommerce': {
      'checkout': {
        'actionField': {'step': 1},
        'products': [{                           
        'name': '[kit sucesso]',   
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       },
       {
        'name': '[kit conquista]', 
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       }]
     }
   }
   });
```

> Obs: Essa tabela de `Chave` e `Descrição` pertence a todos os Steps do Checkout.  

| CHAVE | TIPO | DESCRIÇÃO |
| :---- | :--: | :-------- |
| products | objeto | Array de objetos |
| products.name | string | O nome do Kit  |
| products.id | string | O ID do Kit. Esse ID é o que vincula os itens às transações a que pertencem   |
| products.price | number | O preço individual unitário de cada item  |
| products.brand | string | sadia  |
| products.quantity | number | A quantidade de itens com mesmo ID |
| products.category | string | A categoria a que o item pertence  |

##### Step 2 - Selecionou entrega

Descrição: Disparar as informações no dataLayer no momento da seleção se será realizada entrega ou retirada.

```javascript
 dataLayer.push({
    'event': 'checkout',
    'eventCategory': 'funil-de-transacao', //fixo
    'eventAction': 'checkout', //fixo
    'eventLabel': 'ir-para-checkout', //fixo 
    'ecommerce': {
      'checkout': {
        'actionField': {'step': 2}, //fixo
        'products': [{                           
        'name': '[kit sucesso]',   
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       },
       {
        'name': '[kit conquista]', 
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       }]
     }
   }
   });
```

##### Step 3 - Selecionou entrega ou retirada

Descrição: Disparar as informações no dataLayer no momento do preenchimento do form para Retirada ou Recebimento.

```javascript
 dataLayer.push({
    'event': 'checkout',
    'eventCategory': 'funil-de-transacao', //fixo
    'eventAction': 'checkout', //fixo
    'eventLabel': 'ir-para-checkout', //fixo 
    'ecommerce': {
      'checkout': {
        'actionField': {'step': 3}, //fixo
        'products': [{                           
        'name': '[kit sucesso]',   
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       },
       {
        'name': '[kit conquista]', 
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       }]
     }
   }
   });
```

##### Step 4 - Abriu o form de identificação

Descrição: Disparar as informações no dataLayer no momento em que abir o form de identificação.

```javascript
 dataLayer.push({
    'event': 'checkout',
    'eventCategory': 'funil-de-transacao', //fixo
    'eventAction': 'checkout', //fixo
    'eventLabel': 'ir-para-checkout', //fixo 
    'ecommerce': {
      'checkout': {
        'actionField': {'step': 4},
        'products': [{                           
        'name': '[kit sucesso]',   
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       },
       {
        'name': '[kit conquista]', 
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       }]
     }
   }
   });
```

##### Step 5 - Abrir o form de pagamento

Descrição: Disparar as informações no dataLayer no momento em do click do botão *Ir para pagamento*.

```javascript
 dataLayer.push({
    'event': 'checkout',
    'eventCategory': 'funil-de-transacao', //fixo
    'eventAction': 'checkout', //fixo
    'eventLabel': 'ir-para-checkout', //fixo 
    'ecommerce': {
      'checkout': {
        'actionField': {'step': 5},
        'products': [{                           
        'name': '[kit sucesso]',   
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       },
       {
        'name': '[kit conquista]', 
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       }]
     }
   }
   });
```

##### Step 6 - Sucesso ao preencher o form de pagamento

Descrição: Disparar as informações no dataLayer no callback de validação do form de pagamento.

```javascript
 dataLayer.push({
    'event': 'checkout',
    'eventCategory': 'funil-de-transacao', //fixo
    'eventAction': 'checkout', //fixo
    'eventLabel': 'ir-para-checkout', //fixo 
    'ecommerce': {
      'checkout': {
        'actionField': {'step': 6}, //fixo
        'products': [{                           
        'name': '[kit sucesso]',   
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       },
       {
        'name': '[kit conquista]', 
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       }]
     }
   }
   });
```

#### Purchase

Descrição: Disparar as informações no dataLayer no momento em que a página de transação for carregada.

> Obs: É importante que ocorra na pagina de conclusão da compra e que ocorra apenas 1 vez, mesmo que a página seja atualizada, ou vamos ter problemas com transações duplicadas.

```javascript
dataLayer.push({
  'event': 'purchase',
  'eventCategory': 'funil-de-transacao', //fixo
  'eventAction': 'checkout', //fixo
  'eventLabel': 'sucesso', //fixo 
  'dimension2': '[pj]',
  'dimension3': '[retirada]',
  'dimension4': '[loja_ibirapuera]',
  'dimension5': '[nao-optou-por-entrega]',
  'dimension6': '[sim]',
  'ecommerce': {
    'purchase': {
      'actionField': {
        'id': '[T12345]',                         
        'affiliation': '[sadia]',
        'revenue': '[3000.43]',                    
        'shipping': '[5000.99]',
      },
      'products': [{                            
        'name': '[kit sucesso]',    
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       },
       {
        'name': '[kit conquista]',    
        'id': '[12345]',
        'price': '[150.25]',
        'brand': '[sadia]',
        'category': '[linha-classic]',
        'quantity': 10,
       }]
    }
  }
});
```

| CHAVE | TIPO | DESCRIÇÃO |
| :---- | :--: | :-------- |
| event | string | purchase |
| actionField.id | string | O ID da transação   |
| actionField.affiliation | string | A loja ou afiliação a partir da qual ocorreu essa transação   |
| actionField.revenue | number | Especifica a receita total ou o total geral associado à transação  |
| actionField.shipping | number | Especifica o custo total de envio da transação  |
| products | objeto | Array de objetos |
| products.name | string | O nome do Kit  |
| products.id | string | O ID do Kit. Esse ID é o que vincula os itens às transações a que pertencem   |
| products.price | number | O preço individual unitário de cada item  |
| products.brand | string | sadia  |
| products.quantity | number | A quantidade de itens com mesmo ID |
| products.category | string | A categoria a que o item pertence  |
| dimension2 | string | Se o usuário selecionou pessoa juridica ou pessoa física. Valores esperados: *pj* ou *pf*.  |
| dimension3 | string | Se o usuário selecionou entrega ou retirada. Valores esperados: *entrega* ou *retirada*.  |
| dimension4 | string | Local de retirada selecionado pelo cliente. Valor esperado: 'nome-da-loja' ou 'nao-optou-por-retirada'  |
| dimension5 | string | Data de Entrega selecionado pelo cliente. Valor esperado: DD-MM-AAAA ou 'nao-optou-por-entrega' |
| dimension6 | string | Se o usuário em questão já realizou compra naquele device. Valores esperados: *sim* ou *não*. |

> *Obs:* Caso não houver algum valor preencher com `undefined`.



### Outros

#### Click no botão *Assistente de compra*

O botão deve ter em sua estrutura `html` a classe `gtm-link-event` se for um link `<a>` ou `gtm-element-event` se o elemento não for um link `<a>`, conforme já detalhado acima e os data-attributes `data-gtm-event-category`, `data-gtm-event-action` e `data-gtm-event-label`. 

```html
<!-- Use se o elemento for um link -->
<a href="#"
  class="gtm-link-event" 
  data-gtm-event-category="assistente-de-compras"
  data-gtm-event-action="abriu"
  data-gtm-event-label="abriu"
>Link</a>

<!-- Use se o elemento não for um link -->
<i class="gtm-element-event" 
  data-gtm-event-category="assistente-de-compras"
  data-gtm-event-action="abriu"
  data-gtm-event-label="abriu"
>Botão</i>
```

#### Clique no botão *Mostre os Melhores Presentes*

Descrição: Disparar as informações no dataLayer no click do botão.

```javascript
  window.dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'event', // fixo
    'eventCategory': 'assistente-de-compras', //fixo
    'eventAction': 'mostrar-produtos', //fixo
    'eventLabel': '[itens-do-presente:todos-entrada:bolsas-termicas:viagem:quantidade-kits:pessoas-10-verba-por-kit-100]' 
  });
```

| CHAVE | TIPO | DESCRIÇÃO |
| :---- | :--: | :-------- |
| eventLabel |  string | Concatenar os checkbox selecionados e os valores |


#### Click enviar o e-mail

O botão deve ter em sua estrutura `html` a classe `gtm-link-event` se for um link `<a>` ou `gtm-element-event` se o elemento não for um link `<a>`, conforme já detalhado acima e os data-attributes `data-gtm-event-category`, `data-gtm-event-action` e `data-gtm-event-label`. 

```javascript
  window.dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'event', // fixo
    'eventCategory': 'e-mail', // fixo
    'eventAction:': 'enviou-email', //fixo
    'eventLabel': '[tentativa | sucesso ]'
  });
```

| CHAVE | TIPO | DESCRIÇÃO |
| :---- | :--: | :-------- |
| eventLabel | string | Sucesso ou tentativa do envio |

<br />
