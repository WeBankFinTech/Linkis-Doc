Q1、linkis启动报错：NoSuchMethodErrorgetSessionManager()Lorg/eclipse/jetty/server/SessionManager：

具体堆栈：
Failed startup of context o.s.b.w.e.j.JettyEmbeddedWebAppContext@6c6919ff{application,/,[file:///tmp/jetty-docbase.9102.6375358926927953589/],UNAVAILABLE} java.lang.NoSuchMethodError: org.eclipse.jetty.server.session.SessionHandler.getSessionManager()Lorg/eclipse/jetty/server/SessionManager;
 at org.eclipse.jetty.servlet.ServletContextHandler$Context.getSessionCookieConfig(ServletContextHandler.java:1415) ~[jetty-servlet-9.3.20.v20170531.jar:9.3.20.v20170531]
 
 A1、jetty-servlet 和 jetty-security版本需要从9.3.20升级为9.4.20；
