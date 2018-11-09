```javascript
=========================AAM DIL CODE=====================================



/* 
  AudienceManager Settings DIL CODE
*/



//Visitor ID service instantiation
/* var visitor = Visitor.getInstance("4435697753736FB20A490D45@AdobeOrg", {
    loadTimeout: 10000
});

var userId1 = s.eVar22; // Hash CPF
if(userId1!=undefined) {
  visitor.setCustomerIDs({
    "HashPFId":{
      "id": userId1,
    }
  });
}     */
var userId1 = s.eVar22;
if(userId1!=undefined) {
  var pabloDil = DIL.create({
    partner : "pablo",
    containerNSID : 0,
    uuidCookie:{
      name:'aam_uuid',
      days:30
    },
    visitorService: {
      namespace: '4435697753736FB20A490D45@AdobeOrg'
    },
    declaredId : {
      dpid : "61376" ,
      dpuuid : userId1
      }

  });
}
else {
  var pabloDil = DIL.create({
    partner : "pablo",
    containerNSID : 0,
    uuidCookie:{
      name:'aam_uuid',
      days:30
    },
    visitorService: {
      namespace: '4435697753736FB20A490D45@AdobeOrg'
    }
  });
}

var _scDilObj;
if(typeof s != 'undefined' && s === Object(s) && typeof s.account != 'undefined' && s.account){
  _scDilObj = s_gi(s.account);
} 
else {
  _scDilObj = s_gi(s_account);
}

DIL.modules.siteCatalyst.init(_scDilObj, pabloDil, {
  names: ['pageName', 'channel', 'campaign', 'products', 'events', 'pe', 'referrer', 'server', 'purchaseID', 'zip', 'state'],
  iteratedNames: [{
    name: 'eVar',
    maxIndex: 100
  }, {
    name: 'prop',
    maxIndex: 75
  }, {
    name: 'pev',
    maxIndex: 3
  }, {
    name: 'hier',
    maxIndex: 4
  }, {
      name: "list",
      maxIndex: 3
    }]
});

function objIsEmpty(obj) { 
    for(var prop in obj) { 
        if(obj.hasOwnProperty(prop) && prop !== "") 
            return false; 
    }; 
        return true; 
};

var uriData = DIL.tools.decomposeURI(document.URL);
delete uriData.search;
delete uriData.href;
if(! objIsEmpty(uriData.uriParams)){ 
  pabloDil.api.signals(uriData.uriParams, 'c_');
};
if(objIsEmpty(uriData.pathname)){ 
  delete uriData.pathname;
};
delete uriData.uriParams;
pabloDil.api.signals(uriData, 'c_').submit();


if (pabloDil)
{
  //pabloDil.api.traits([7277123]);
  pabloDil.api.signals({ d_referer : document.referrer });
}

//document.URL value
if (pabloDil)
{
  pabloDil.api.signals({ d_URL : document.URL });
}

====================FIM===================================================
```
