# Setting up environment for studying for OCEJWCD exam

This describes my setup for studying for OCEJWCD exam

1. Download and install newest Eclipse (Mars)
1. Create separate directory for workspace (eg. ~/Documents/java/ocejwcd)
1. Download and install newest Tomcat (8.0)
1. Add Tomcat directory in Servers setup for Eclipse
1. Use maven-archetype-webapp to create framework to try examples
1. To pom.xml you should add servlet api dependency
  ```xml
  <dependency>
		<groupId>javax.servlet</groupId>
		<artifactId>servlet-api</artifactId>
		<version>2.5</version>
		<scope>provided</scope>
  </dependency>
  ```
1. Now you can create Servlet class that extends javax.servlet.http.HttpServlet and overrides method doGet. For instance:
  ```java
  package hr.analemma;

  import java.io.IOException;
  import javax.servlet.ServletException;
  import javax.servlet.http.HttpServlet;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;

  /**
   * Servlet implementation class Chapter05Servlet
   */
  public final class Chapter05Servlet extends HttpServlet {
  	private static final long serialVersionUID = 1L;

      /**
       * Default constructor.
       */
      public Chapter05Servlet() {
          // TODO Auto-generated constructor stub
      }

  	/**
  	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
  	 */
  	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  		// TODO Auto-generated method stub
  		response.getWriter().append("Served at: ").append(request.getContextPath());
  	}

  }
  ```
1. And you should add servlet mappings to web.xml in src/webapp/WEB-INF.
  ```xml
  <!DOCTYPE web-app PUBLIC
   "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
   "http://java.sun.com/dtd/web-app_2_3.dtd" >

  <web-app>
    <display-name>Archetype Created Web Application</display-name>
    <servlet>
    	<servlet-name>Chapter05Servlet</servlet-name>
    	<display-name>Chapter 05 Servlet</display-name>
    	<description>Servlet for learning request and response object</description>
    	<servlet-class>hr.analemma.Chapter05Servlet</servlet-class>
    	<init-param>
    		<param-name>purpose</param-name>
    		<param-value>learning</param-value>
    		<description>Test Servlet Prameter</description>
    	</init-param>
    </servlet>
    <servlet-mapping>
    	<servlet-name>Chapter05Servlet</servlet-name>
    	<url-pattern>/Chapter05Servlet</url-pattern>
    </servlet-mapping>
  </web-app>
  ```
1. Servlet and servlet mapping can be done automatically if you use Eclipse Java EE perspective and click right click on Deployment Descriptor->Servlets in Project Explorer view and select New->Servlet and fill in data in wizard that will open.
1. Then you can deploy servlet to tomcat by right clicking on Tomcat server in Servers View and selecting Add and Remove and add your project to server.
1. You should start Tomcat in debug mode and you can put brake point in your code in appropriate place.
1. You can simulate GET request from terminal with command `curl -i -X GET http://localhost:8080/chapter05/Chapter05Servlet`
1. If you want to add headers to GET request you can do it like this `curl -i -X GET http://localhost:8080/chapter05/Chapter05Servlet`
