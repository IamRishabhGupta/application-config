

# Application Configuration Repository

This repository serves as a centralized configuration store for microservices using Spring Cloud Config. It holds configuration files for different environments like development, default, and production.

## **Table of Contents**
- [Overview](#overview)
- [Configuration Files](#configuration-files)
- [Environment Configuration](#environment-configuration)
- [Using Configurations](#using-configurations)
- [Spring Cloud Config Server Setup](#spring-cloud-config-server-setup)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)

## **Overview**
Spring Cloud Config provides server and client-side support for externalized configuration in a distributed system. This repository contains the configuration files for the microservices.

## **Configuration Files**
- **`application-dev.properties`**: Development environment configuration.
- **`application-default.properties`**: Default configuration.
- **`application-prod.properties`**: Production environment configuration.

### **Configuration Example**
#### **application-dev.properties**
```properties
# Development specific properties
server.port=8081
job.title=Software Engineer - DEV
job.description=Developing and maintaining software applications in DEV
```

#### **application-default.properties**
```properties
# Default properties
server.port=8080
job.title=Software Engineer
job.description=Developing and maintaining software applications
```

#### **application-prod.properties**
```properties
# Production specific properties
server.port=80
job.title=Software Engineer - PROD
job.description=Developing and maintaining software applications in PROD
```

## **Environment Configuration**
The `application.properties` in your microservices must specify which profile to use. Here’s how to set it up:

```properties
spring.profiles.active=dev
```

The profile can be switched by changing the `spring.profiles.active` value in the service’s `application.properties` file or by passing it as an argument:

```bash
java -jar job-service.jar --spring.profiles.active=prod
```

## **Using Configurations**
Microservices connect to the Spring Cloud Config Server to fetch their configurations. Ensure your service’s `application.properties` points to the Config Server:

```properties
spring.application.name=jobms
spring.cloud.config.uri=http://localhost:8888
```

## **Spring Cloud Config Server Setup**
Ensure the Config Server is set up to read from this repository:

#### **Config Server Application**
Add the following dependencies in `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

#### **Config Server `application.properties`**
```properties
server.port=8888
spring.cloud.config.server.git.uri=https://github.com/yourusername/application.config
```

## **Security**
For security, you may want to:
- Restrict access to this repository.
- Use encryption and decryption for sensitive data (e.g., passwords).

### **Encrypting Properties**
To encrypt sensitive properties, you can use Spring Cloud Config’s encryption support. Add encrypted values in your property files and manage the keys securely.

## **Contributing**
If you wish to contribute:
1. Fork the repository.
2. Create a new branch.
3. Commit your changes.
4. Open a pull request.

## **License**
This repository is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
