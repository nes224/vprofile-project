# Use the official OpenJDK 11 image as the build image
FROM openjdk:11 AS BUILD_IMAGE

# Install Maven and Git
RUN apt-get update && apt-get install -y maven git

# Clone the Git repository and build the project
RUN git clone https://github.com/devopshydclub/vprofile-project.git
WORKDIR /vprofile-project
RUN git checkout docker
RUN mvn clean install

# Create a dedicated stage for the final image
FROM tomcat:9-jdk11-openjdk-slim

# Copy the WAR file from the build stage to Tomcat's webapps directory
COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose the default Tomcat port
EXPOSE 8080

# Start Tomcat
CMD ["catalina.sh", "run"]
