# Based on ubuntu with oracle java 7
FROM relateiq/oracle-java7

RUN apt-get update && apt-get install -y curl unzip

# install liferay
RUN curl -O -s -k -L -C - http://downloads.sourceforge.net/project/lportal/Liferay%20Portal/6.2.3%20GA4/liferay-portal-tomcat-6.2-ce-ga4-20150416163831865.zip \
    && unzip liferay-portal-tomcat-6.2-ce-ga4-20150416163831865.zip -d /opt \
    && rm liferay-portal-tomcat-6.2-ce-ga4-20150416163831865.zip

RUN ln -s /opt/liferay-portal-6.2-ce-ga4 /opt/liferay-portal
RUN ln -s /opt/liferay-portal/tomcat-7.0.42 /opt/liferay-portal/tomcat

# add configuration files
ADD resources/portal-ext.properties /opt/liferay-portal/portal-ext.properties
ADD resources/portal-setup-wizard.properties /opt/liferay-portal/portal-setup-wizard.properties
ADD resources/setenv.sh /opt/liferay-portal/tomcat/bin/setenv.sh

# volumes
VOLUME /opt/liferay-portal/data

# Ports
EXPOSE 8080

# Set JAVA_HOME
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle/

# EXEC
ENTRYPOINT ["/opt/liferay-portal/tomcat/bin/catalina.sh"]
CMD ["run"]