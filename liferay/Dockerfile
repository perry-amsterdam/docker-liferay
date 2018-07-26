# Based on oracle-jdk 1.8 from airdock
FROM airdock/oracle-jdk:1.8

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get autoremove -y

# Install unzip
RUN apt-get update && apt-get install -y unzip && apt-get install -y wget

# Download and install liferay
RUN wget https://sourceforge.net/projects/lportal/files/Liferay%20Portal/7.1.0%20GA1/liferay-ce-portal-tomcat-7.1.0-ga1-20180703012531655.zip

RUN unzip liferay-ce-portal-tomcat-7.1.0-ga1-20180703012531655.zip -d /opt
RUN rm liferay-ce-portal-tomcat-7.1.0-ga1-20180703012531655.zip

RUN mkdir -p /opt
RUN ln -s  /opt/liferay-ce-portal-7.1.0-ga1 /opt/liferay-portal
RUN ln -s /opt/liferay-portal/tomcat-9.0.6 /opt/liferay-portal/tomcat
RUN ls /opt/liferay-portal/tomcat/bin/catalina.sh -all

# Add configuration files
ADD resources/portal-ext.properties /opt/liferay-portal/portal-ext.properties
ADD resources/portal-setup-wizard.properties /opt/liferay-portal/portal-setup-wizard.properties
ADD resources/setenv.sh /opt/liferay-portal/tomcat/bin/setenv.sh

# Liferay data will be stored in a separate data volume
VOLUME /opt/liferay-portal/data

# Expose port 8080
EXPOSE 8080

# Set JAVA_HOME
ENV JAVA_HOME /srv/java/jdk1.8.0_112/

# Execute liferay
ENTRYPOINT ["/opt/liferay-portal/tomcat/bin/catalina.sh"]
CMD ["run"]
