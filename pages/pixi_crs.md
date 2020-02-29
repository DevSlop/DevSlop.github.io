## Pixi-CRS Module

The Pixi-CRS Continuous Integration pipeline provides automated end-to-end testing of the intentionally-vulnerable Pixi application with a Web Application Firewall (WAF) in front of the application, and an automated security vulnerability scanner and web proxy ("ZAP", OWASP Zed Attack Proxy) pointed at the application and WAF.


In an ideal world, we wouldn't need to use a WAF, because the application wouldn't have any bugs. However, we all know that we can‘t be sure that an application or the libraries used are 100% bug-free and perfectly secure.  
We add a WAF as an additional layer of defense against common web application attacks, such as many of those described by the OWASP Top Ten.
    
By adding and testing the WAF in the Continuous Integration (CI) stage, we provide the application developer early feedback about how their application will react when behind a WAF. We assure that Pixi's legitimate traffic is not blocked by the WAF, and that illegitimate traffic is.
   
We use the WAF ModSecurity with the [OWASP ModSecurity Core Rule Set](https://coreruleset.org) as the WAF and signature set in this proof of concept pipeline. 

To start the Core Rule Set in front of Pixi we use [OWASP's modsecurity-crs Docker Image](https://hub.docker.com/r/owasp/modsecurity-crs/)
     
The application tests are written in Testcafe. They are executed once against Pixi directly and then again through the Core Rule Set.  
The Continuous Integration is implemented in CircleCI.  
As a result, we see which CRS rules were hit by the tests.

This module is lead by [Franziska Bühler](team.md).

Code to be found [here](https://github.com/DevSlop/pixi-crs)  
Video explanation [here](https://vimeo.com/271451246)  
Blog explanation [here](https://dev.to/devslop/devslop-s-pixi-crs-pipeline-4bie)  

