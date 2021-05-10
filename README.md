# Angular Tomcat No Hash Router

## How to setup Angular application without ```useHash: true``` router configuration when deployed in Tomcat

It is assumed that frontend Angular application and backend API are deployed on same tomcat server.
The following configuration redirects all not found server requests to Angular's ```index.html```.

1.  Add ```WEB-INF``` folder with ```web.xml``` file that redirects 404 Not found and 410 Gone to ```index.jsp```

### web.xml
```HTML
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
      http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" id="bg.borica.remoteid.webidv.cli" version="3.0">
	<display-name>Remote Web Identification Cli</display-name>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
	</welcome-file-list>
	<error-page>
		<error-code>404</error-code>
		<location>/index.jsp</location>
	</error-page>
	<error-page>
		<error-code>410</error-code>
		<location>/index.jsp</location>
	</error-page>
</web-app>
```

2.  Add ```index.jsp``` file in ```src``` folder, which is next to Angular ```index.html``` file
  
### index.jsp

```HTML
<%
response.setStatus(response.SC_OK);
%>
<%@ include file="index.html" %>
````