# Dockerizing a base images with:
#
#   - Debian Stretch
#   - Oracle JDK 8u131
#   - Apache Tomcat 8.5.14
#
# Build:    docker build -t ermac/tomcat:8.5.14 .
#
# Run:      docker run -ti ermac/tomcat:8.5.14 bash
#
# Example:  docker run -it --rm ermac/tomcat:8.5.14 java -version
# Example:  docker run -p 8080:8080 -d ermac/tomcat:8.5.14

FROM ermac/oracle:jdk8u131

MAINTAINER Fabio Martino <fabiomartino@libero.it>

# Set environment
ENV CATALINA_HOME /opt/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH

# Get and install Tomcat
RUN (apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install unzip wget)
RUN (wget --progress=bar:force -O /tmp/tomcat8.tar.gz http://www.apache.org/dist/tomcat/tomcat-8/v8.5.14/bin/apache-tomcat-8.5.14.tar.gz &&\
  cd /opt &&\
  tar zxf /tmp/tomcat8.tar.gz &&\
  rm /tmp/tomcat8.tar.gz &&\
  mv /opt/apache-tomcat* ${CATALINA_HOME})

ADD tomcat-users.xml $CATALINA_HOME/conf/tomcat-users.xml

EXPOSE 8009 8080 8443 80 443

WORKDIR $CATALINA_HOME/bin

# Launch Tomcat on startup
CMD ["/opt/tomcat/bin/catalina.sh", "run"]
