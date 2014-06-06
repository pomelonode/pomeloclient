pomeloclient
============

pomelo client for sioconnector

These two clients are both for pomelo sioconnector, one is use pomelo-protocol, the other is not. The pomeloclient.js can not be used in IE 6,7,8, for there is some data structures is not available in low version of IE. So we introduce pomeloclient_ie.js, and it support all kinds of browers, including all versions of IE.

##Usage

### pomeloclient.js

Use pomeloclient.js in web-server.

### pomeloclient_ie.js

Use pomeloclient_ie.js in web-server, and configure connector in game-server/app.js.

```

var encode = function(reqId, route, msg) {
	if (!!reqId) {
		return{
			id: reqId,
			body: msg
		};
	} else {
		var m = {
			route: route,
			body: msg
		};
		return JSON.stringify(m);
	}
};

var decode = function(data) {
	data = JSON.parse(data);
	return {
		id: data.id,
		route: data.route,
		body: data.msg
	};
};

app.configure('production|development', 'connector|gate', function() {
		app.set('connectorConfig', {
		connector: pomelo.connectors.sioconnector,
		encode: encode,
		decode: decode
	});
});

```