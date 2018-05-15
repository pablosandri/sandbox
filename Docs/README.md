![Serasa Empreendedor](https://pablosandri.github.io/sandbox/empreendedor.jpg)

# Serasa Empreendedor - Digital Analytics

Última atualização: 14/05/2018

# Objetivo

Este documento tem como objetivo realizar o diagnóstico da implementação do Adobe Analytics no ambiente [Serasa Empreendedor](https://www.serasaempreendedor.com.br/).

# Diagnóstico 

## Configuração e Implementação

Conforme o [**Guia de implementação do Adobe Analytics**](https://helpx.adobe.com/analytics/kb/analytics-standard-implementation-guide.html), na etapa de pré-implementação é crucial documentar as soluções desenvolvidas para o ambiente. Sem isso as organizações terão dificuldade em gerir uma governança de dados e atender as necessidades de relatórios e tendem a perder coletas de dados importantes.

Documentos obrigatórios para implementação e controle (quais foram solicitados a empresa Lima, porém eles não possuem):

### Solution Design: 
Documento de design de solução, é basicamente o modelo de sua implementação de análise. Ele define os requisitos de negócios identificados pelas partes interessadas em toda a organização e os converte em variáveis no Adobe Analytics, delegando padrões de dados, nomenclatura etc.

**Obs:** Documento que auxilia os novos integrantes do time a identificar o que temos disponível no Adobe Analytics, padrões de dados, alocações de variáveis etc.

### TechSpec: 
O Tech Spec é uma documentação detalhada sobre como implementar cada componente das soluções, camada de dados, disparos e como validá-los.

## Padrões

Notamos que a arquitetura de mensuração e dados da Adobe está diferente entre os ambientes [Serasa Experian](https://www.serasaexperian.com.br/) e [Serasa Empreendedor](https://www.serasaempreendedor.com.br/), podendo gerar problemas posteriores de governança de dados e conflitos.

Exemplo:

X       | Serasa Experian | Serasa Empreendedor  |
------- | ---------------- | ---------- | 
Page Name  | ::home-serasa-experian  | home não logada


Sugestão:

X       | Serasa Experian | Serasa Empreendedor  | Construção do Page Name
------- | ---------------- | ---------- |  --------------
Page Name  | SE:EXPERIAN:NL:HOME  | SE:EMPREENDEDOR:NL:HOME  |  [site]:[Ambiente]:[Logado ou deslogado]:[Página]

## KPIs

Análise sobre nossos indicadores chaves de desempenho do Serasa Empreendedor.

KPI | Variável Adobe | Observação |
------- | ---------------- | ---------- | 
Cadastro  | Métricas calculadas | Não é recomendado popular leads com métricas calculadas.
Lead Crédito  | Métricas calculadas | Não é recomendado popular leads com métricas calculadas.
Acompanhamento de produto | eVars | Para acompanhamento de produto a adobe recomenda [Merchandising Variable](https://marketing.adobe.com/resources/help/en_US/sc/implement/var_merchandising_impl.html)

### Contratação de Crédito:

Solução Presente: Todos os steps da contratação são mensurados por customLink e para calcular o total dos Leads foi preciso criar uma ```métrica calculada``` para conseguir a quantidade de customlink por VisitorID.

Obs: Existe eventos de sucesso, mas não estão serializados.

### Cadastros:

Solução Presente: Todos os steps dos cadastros são mensurados por customLink e para calcular o total dos Leads foi preciso criar uma ```métrica calculada``` para conseguir a quantidade de customlink por VisitorID.

Obs: Existe eventos de sucesso, mas não estão serializados.
### Acompanhamento de produtos:

Solução Presente: Atualmente não estamos mensurando nossos produtos como recomenda a [Adobe](https://marketing.adobe.com/resources/help/pt_BR/sc/implement/products.html), sendo assim não conseguimos explorar todos os recursos como montante monetário, prodImpressions, prodView e etc. Ficando limitados às análises superficiais.

## Server Calls

Server Calls são os hits com informções enviadas a Adobe para processamento, esses hits são custiados individualmente, portanto devem ser usados com cuidado.
No Serasa Empreendedor existem muitos disparos redundantes que poderiam enviar todas informações na mesma solicitação, qual gostariamos de entender o motivo. Segue exemplo:

Fluxo de cadastro de usuarios(simples):

Solução presente: 

Passos | Server Calls | Observação      |
------- | ---------------- | ---------- | 
Formulário  | 1 hit | CustomLink: EventCadastra-se
Formulário  | 2 hit | CustomLink: CadastroInicio, e101(Cadastro Inicio)
Formulário  | 3 hit | Pageview: Validar Token
Token  | 4 hit | CustomLink: EventValidarToken
Token  | 5 hit | CustomLink: CadastroValidarToken, e103(Cadastro Validação Token)
Senha  | 6 hit | CustomLink: CustomLink: EventSenhaDadosIniciais
Senha  | 7 hit | CustomLink: CustomLink: Cadastro | Definicao Senha, e104(Cadastro Definicao senha)
Senha  | 8 hit | Pageview: home

Sugestão:

Passos | Server Calls | Observação      |
------- | ---------------- | ---------- | 
Formulário  | 1 hit | Pageview: Validar Token, e101(Cadastro Inicio), propX: IniciouCadastro
Token  | 2 hit | CustomLink: CadastroValidarToken, e103(Cadastro Validação Token) propX: TokenCadastro
Senha  | 3 hit | Pageview: home, e104(Cadastro Definicao senha), propX: RealizouCadastro
