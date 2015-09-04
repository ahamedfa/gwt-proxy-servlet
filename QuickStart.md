# Quick Start #

The only class you need to instanciate is ProxyServlet.

I order to translate input queries to the right server, you need to provide the target server URL.

You also need to configure the max number of connection allowed.

The simplest way is to subclass ProxyServlet as following :

```
public class MyProxyServlet extends ProxyServlet {

	@Override
	public void init() throws ServletException {
		try {
		init("http://my-services.org", 200);
		} catch (IOException e) {
			throw new ServletException(e);
		} catch (ConfigurationException e) {
			throw new ServletException(e);
		}
	}	
}
```

Then, you must configure the proxy in your web.xml file :

```
 <servlet>
  <servlet-name>ProxyServlet</servlet-name>
  <servlet-class>org.example.MyProxyServlet</servlet-class>
 </servlet>

 <servlet-mapping>
  <servlet-name>ProxyServlet</servlet-name>
  <url-pattern>/proxy/*</url-pattern>
 </servlet-mapping>
```

It says that every request to http://my-webapp-url/proxy/ will be redirected to http://my-services.org.

For example, http://my-webapp-url/proxy/my-rest-service will be translated in http://my-services.org/my-rest-service.