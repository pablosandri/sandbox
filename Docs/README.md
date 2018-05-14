Serasa Empreendedor - Digital Analytics

Última atualização: 14/05/2018

# Objetivo

Este documento tem como objetivo realizar um diagnostico da implementação do Adobe Analytics no ambiente [Serasa Empreendedor](https://www.serasaempreendedor.com.br/).

# Diagnostico

## Configuração e Implementação

Conforme o [**Guia de implementação do Adobe Analytics**](https://helpx.adobe.com/analytics/kb/analytics-standard-implementation-guide.html), na etapa de pré-implementação, é crucial documentar as Soluções abordadas.

### Solution Desing: 
Documento de design de solução, é basicamente o modelo de sua implementação de análise. Ele define os requisitos de negócios identificados pelas partes interessadas em toda a organização e os converte em variáveis no Adobe Analytics. Sem um, as organizações têm dificuldade em coordenar as necessidades de relatórios e tendem a perder a coleta de dados importantes.

**Obs:** É documento que auxilia os novos integrantes do time a identificar o que temos disponivel no Adobe e padrões de dados, alocações de variaveis e etc.

### TechSpec: 
O Tech Spec é uma documentação detalhada sobre como implementar cada componente das soluções, camada de dados disparos e como validá-las.

## Padrões

Notamos que o padrão adotado no ambiente [Serasa Experian](https://www.serasaexperian.com.br/) e [Serasa Empreendedor](https://www.serasaempreendedor.com.br/), não batem. Ex: Pagename, products e etc.

## KPIs
Análise sobre nossos indicadores chaves de desempenho.

**Contratação de Crédito:** Métrica de sucesso: Precisamos criar uma métrica calculada para conseguir a quantidade de customlink por VisitorID.

**Cadastros:** Métrica de sucesso: Precisamos criar uma métrica calculada para conseguir a quantidade de customlink por VisitorID.


**Acompanhamento de produtos:** Não estamos mensurando nossos produtos como recomenda a [Adobe](https://marketing.adobe.com/resources/help/pt_BR/sc/implement/products.html), sendo assim não estamos explorando todos os recursos e ficando limitados a poucas análises.











