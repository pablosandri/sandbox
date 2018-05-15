Serasa Empreendedor - Digital Analytics

Última atualização: 14/05/2018

# Objetivo

Este documento tem como objetivo realizar um diagnostico da implementação do Adobe Analytics no ambiente [Serasa Empreendedor](https://www.serasaempreendedor.com.br/).

# Diagnostico

## Configuração e Implementação

Conforme o [**Guia de implementação do Adobe Analytics**](https://helpx.adobe.com/analytics/kb/analytics-standard-implementation-guide.html), na etapa de pré-implementação, é crucial documentar as soluções desenvolvida para o ambiente. Sem um, as organizações têm dificuldade em gerir uma governancia de dados e atender as necessidades de relatórios e tendem a perder a coleta de dados importantes.

Documentos obrigatorios para governancia:

### Solution Desing: 
Documento de design de solução, é basicamente o modelo de sua implementação de análise. Ele define os requisitos de negócios identificados pelas partes interessadas em toda a organização e os converte em variáveis no Adobe Analytics, delegando padrões de dados, nomenclatura etc.

**Obs:** Documento que auxilia os novos integrantes do time a identificar o que temos disponivel no Adobe Analytics, padrões de dados, alocações de variaveis e etc.

### TechSpec: 
O Tech Spec é uma documentação detalhada sobre como implementar cada componente das soluções, camada de dados disparos e como validá-los.

## Padrões

Notamos que a arquitetura de mensuração da Adobe está diferente entre os ambientes [Serasa Experian](https://www.serasaexperian.com.br/) e [Serasa Empreendedor](https://www.serasaempreendedor.com.br/). Podendo podendo gerar problemas posteriores de governancia de dados.

## KPIs

Análise sobre nossos indicadores chaves de desempenho do Serasa Empreendedor.

**Contratação de Crédito:** Todos os steps da contratação são mensurados por customLink e para calcular o total de Leads foi preciso criar uma métrica calculada para conseguir a quantidade de customlink por VisitorID. Qual mótivo dessa arquitetura?

**Cadastros:** Precisamos criar uma métrica calculada para conseguir a quantidade de customlink por VisitorID.
Obs:


**Acompanhamento de produtos:** Não estamos mensurando nossos produtos como recomenda a [Adobe](https://marketing.adobe.com/resources/help/pt_BR/sc/implement/products.html), sendo assim não conseguimos explorando todos os recursos e ficando limitados a análises superficiais.


### Server Calls







