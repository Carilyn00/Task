FROM centos:6.10

# Tomcat
WORKDIR /opt/apache-tomcat
RUN curl -O https://www-us.apache.org/dist/tomcat/tomcat-9/v9.0.19/bin/apache-tomcat-9.0.19.tar.gz \
 && tar xzf apache-tomcat-9.0.19.tar.gz \
 && useradd -s /sbin/nologin tomcat \
 && chown -R tomcat:tomcat /opt/apache-tomcat \
 && echo "export JAVA_HOME=$(dirname $(readlink $(readlink $(which java))) | sed -e 's#/bin.*##')" >> ~/.bash_profile \
 && source ~/.bash_profile
ENV CATALINA_HOME /opt/apache-tomcat/apache-tomcat-9.0.19

# Deploy
WORKDIR /opt/apache-tomcat/apache-tomcat-9.0.19/webapps
COPY target/uranus-*.war .
RUN mv uranus-*.war uranus.war

CMD $CATALINA_HOME/bin/startup.sh && /bin/bash
