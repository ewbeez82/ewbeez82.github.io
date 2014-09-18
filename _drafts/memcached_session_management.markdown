---
layout: post
title:  "Memcached Session Management"
date:   2014-09-18 09:10:00
categories: java memcached
---

On a number of projects, I've been using [spring boot][springboot] with an embedded tomcat container.  One of the issues I've had is with maintaining the session.  Sometimes it's not that important.  For example if you have a single application running on a single server.  That's great for a side project or a demo, but what happens when you have your application running on a cluster?  You could have sticky sessions but if your node goes down your stuck with having to re-authenticate.

Here is a quick code snippit of how to set this up within spring boot.  


{% highlight java %}
import org.apache.catalina.Context;
import org.springframework.boot.context.embedded.tomcat.TomcatContextCustomizer;
import org.springframework.boot.context.embedded.tomcat.TomcatEmbeddedServletContainerFactory;
import org.springframework.boot.context.web.SpringBootServletInitializer;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import de.javakaffee.web.msm.MemcachedBackupSessionManager;

@Configuration
public class ServletInit extends SpringBootServletInitializer {

@Bean
public TomcatEmbeddedServletContainerFactory containerCustomizer() {
  TomcatEmbeddedServletContainerFactory containerFactory = new TomcatEmbeddedServletContainerFactory();
  final MemcachedBackupSessionManager manager = new MemcachedBackupSessionManager();
  manager.setMemcachedNodes("n1:localhost:11211");
  TomcatContextCustomizer cust = new TomcatContextCustomizer() {
      @Override
      public void customize(Context arg0) {
        arg0.setManager(manager);
      }
    };

    containerFactory.addContextCustomizers(cust);

    return containerFactory;
  }
}
{% endhighlight %}


[springboot]:      http://projects.spring.io/spring-boot/
