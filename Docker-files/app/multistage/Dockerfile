FROM maven:3.9.9-eclipse-temurin-21-jammy AS build_image

# Clone the repository
RUN git clone https://github.com/akhileehh/javappdata.git /javappdata

# Set the working directory to the cloned repository
WORKDIR /javappdata

# Checkout the docker branch and build the project
RUN git checkout vprofile-docker && mvn clean install -DskipTests

# Second stage - Tomcat deployment
FROM tomcat:10-jdk21

# Remove the default webapps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the built WAR file from the build stage
COPY --from=build_image /javappdata/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]
