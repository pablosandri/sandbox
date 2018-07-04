![CI&T](https://pablosandri.github.io/sandbox/ciandt.png)

# Serasa Empreendedor - Activity Map

Última atualização: 04/07/2018

Em caso de dúvidas, entrar em contato com: [pablo.sandri@experian.com](mailto:pablo.sandri@experian.com)

# Objetivo

Veja onde os visitantes estão interagindo com o seu site!

Existe um plugin da Adobe chamado `Activity Map`, com ele conseguimos identificar onde os usuários estão interagindo no site.

# Tutorial de como usar.

## Instalação do plugin Activity Map

Entre no Adobe Analytics > Tools > Activity Map e instale a extensão.

## Aplicando

Entre na página que gostaria de ver as interações clique no Plugin e faça o login.

Ex:

![](https://pablosandri.github.io/sandbox/ciandt.png)

## Envio das váriaveis 

Declare sua string da products no `s.products` conforme ilustrado abaixo:

>	Obs: Caso queira enviar outras informações como event, prop e evar consulte essa [documentação]()

```javascript
s.products = 'Category;ABC123;,;ABC456;2;19.98;event1=1.99|event2=100;evar1=Ground Shipping,;;;;event3=2.9;evar3=20% off'

s.tl()    // Compila todas as variáveis definidas e envia para adobe
```
Pronto, o disparo foi enviado para adobe.

## Homologação

Por fim se você estiver com o *adobe debugger* no favorito é só executar, ou execute o seguinte codigo no console.

```javascript
javascript:void(window.open("","dp_debugger","width=600,height=600,location=0,menubar=0,status=1,toolbar=0,resizable=1,scrollbars=1").document.write("<script language='JavaScript' id=dbg src='https://www.adobetag.com/d1/digitalpulsedebugger/live/DPD.js'></"+"script>"));
```

Verifique se os valores foram atribuidos nos seus respectivos lugares, conforme print.

