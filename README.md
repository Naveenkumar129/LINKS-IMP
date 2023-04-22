apiVersion: networking.istio.io/v1alpha3
[https://github.com/boredabdel/istio-workshop-gcp]
https://github.com/Naveenkumar129/istio-workshop-gcp?organization=Naveenkumar129&organization=Naveenkumar129

https://github.com/Naveenkumar129/istio-project-k8/blob/master/ts-service-part2-1.yml

https://github.com/yzgqy/train-ticket-master/tree/284b0cee2d2dff3d2786cf9c6323626997543ee7








//Properties:  
var vHost = "https://MGMT:5554/mgmt/status/default/MemoryStatus";  
var vLogCategory = {'category':'GetStatCategory'};  
var sm = require('service-metadata');  
var hm = require('header-metadata');  
var urlopen = require('urlopen');  
var ct = hm.current.get('Content-Type');  
var ctx = session.name('getstat') || session.createContext('getstat');  
var vAppliance = ctx.getVar('devicename').replace('<?xml version="1.0" encoding="UTF-8"?>','') || 0;  
var vDomainName = sm.getVar("var://service/domain-name");  
var vXMLContentType = "application/json";  
            // define the urlopen options  
            var options = {  
            target : vHost,  
            method : 'GET',  
            contentType : vXMLContentType,  
            timeout : 2  
};  

// open connection to target and send data over  
urlopen.open(options, function (error, response) {  
            if (error) {  
                        // an error occurred during request sending or response header parsing  
                        console.log('urlopen error: ' + error);  
                        session.output.write("urlopen connect error: " + error);  
            } else {  
                        // read response data  
                        // get the response status code  
                        var responseStatusCode = response.statusCode;  
                        if (responseStatusCode == 200) {  
                                    response.readAsJSON(function(err, readAsJSONResponse) {  
                                                if (err) {  
                                                            session.reject("readAsJSON error: " + JSON.stringify(err));  
                                                } else {  
                                                            session.output.write(" Success ");  
                                                            console.options(vLogCategory).log("Appliance: " + vAppliance + ", MemoryUsage: " + JSON.stringify(readAsJSONResponse.MemoryStatus.Usage));  
                                                }  
                                    });  
                                    };  
                        }  
            });



apim.readInputAsBuffer(function (error, buffer) { if (error) { apim.setvariable('message.status.code', 500); } else { var response = { "active": true };

	//simulate OAuth provider that returns scopes as part of the introspection lookup
	if (apim.getvariable('demo.introspect.response.scope') !== '' &&
		apim.getvariable('demo.introspect.response.scope') !== undefined) {
		response['scope'] = apim.getvariable('demo.introspect.response.scope');
	}

	//TESTING ONLY: include the basic-auth header in the request back in the response
	response['basic-authorization'] = apim.getContext('request.authorization');
	//TESTING ONLY: include the input body from the request back in the response
	response['input_body'] = buffer.toString();
	//set the response context
	apim.output('application/json');
	apim.setvariable('message.status.code', 200);
	console.error ('>> oauth introspection - returning response %s', JSON.stringify(response));
	session.output.write(JSON.stringify(response));
}
