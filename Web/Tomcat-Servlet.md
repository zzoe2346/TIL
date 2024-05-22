# Tomcat, Servlet
## Servlet
- 서블릿을 한마디로 정의하면 '웹 서버에서 동적 웹 콘텐츠를 생성하는 자바 프로그램'
- 클라이언트 요청에 따라 동적으로 HTML 페이지를 생성.
## Tomcat

톰캣은 web server이자 servlet container다. 내가 찾은 자료들에서는 WAS(web application server)보다 web server에 가깝다고 함.

톰캣 이전, 직접 서블릿api 사용해서모든 것을 구현해야했음. 이건 서블릿 개발을 간편하기 위해 탄생. 개발자는 톰캣을 사용하면 서블릿 개발에 필요한 기본적인 기능을 쉽게 활용할 수 있으며, 직접 서블릿 구현에 대한 부담을 줄일 수 있다.

- 서블릿 라이프 사이클 관리
- 서블릿 매핑
- url 처리 
- JSP 컴파일 및 실행
- 보안
- 클러스터링 
- JSP: HTML 코드 안에 Java 코드를 삽입하여 동적으로 HTML 페이지를 생성하는 기술

서블릿 컨테이너는 웹 서버와 함께 사용된다. 웹 서버는 정적 파일(HTML, CSS, JavaScript 등)을 처리하고, 서블릿 컨테이너는 동적 웹 페이지(서블릿, JSP)를 처리함.

대표적인 서블릿 컨테이너: Apache Tomcat, Jetty, JBoss 등

https://docs.oracle.com/javaee/7/tutorial/servlets001.htm#BNAFE
[https://www.geeksforgeeks.org/introduction-java-servlets/?ref=lbp](https://www.geeksforgeeks.org/introduction-java-servlets/?ref=lbp)
[https://www.geeksforgeeks.org/introduction-to-jsp/?ref=lbp](https://www.geeksforgeeks.org/introduction-to-jsp/?ref=lbp)