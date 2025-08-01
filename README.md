# Cloud Config Server

## Overview
This repository contains configuration files for a microservices-based system using Spring Cloud Config Server. The configuration manages multiple services across different environments (dev, prod).

## Services Configuration

### Discovery Server
- Port: 8761
- Eureka Server configuration
- Not registered with itself
- Environments: dev, prod

### Microservices

#### 1. Bidding Service
- Port: 8081
- Database: PostgreSQL
- Features:
  - Liquibase integration
  - Eureka client
  - Logging configuration

#### 2. Booking Service
- Port: 8082
- Eureka client integration
- Basic service configuration

#### 3. Identity Service
- Port: 8083
- Database: H2 (in-memory)
- Features:
  - JWT authentication
  - JPA configuration
  - H2 console enabled
  - Management endpoints exposed

#### 4. Interaction Service
- Port: 8084
- Basic service configuration
- Gateway tracing enabled

#### 5. Monitoring Service
- Port: 8085
- Gateway integration
- Logging configuration

#### 6. Tour Management Service
- Port: 8086
- Gateway integration
- Basic service configuration

#### 7. Transaction Service
- Port: 8087
- Gateway integration
- Basic service configuration

## Environment Configurations
Each service has three configuration files:
- `service-name.yml` - Default configuration
- `service-name-dev.yml` - Development environment
- `service-name-prod.yml` - Production environment

## Common Configurations

### Eureka Client
```yaml
eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka/
  instance:
    prefer-ip-address: true
```

### Logging
```yaml
logging:
  level:
    reactor:
      netty: INFO
    org:
      springframework:
        cloud:
          gateway: TRACE
```

## Security
- JWT secret key configured in identity service
- Token expiration: 24 hours (86400000 ms)

## Management & Monitoring
- Actuator endpoints exposed
- Health check details enabled
- Gateway tracing configured

## Port Allocation
- Discovery Server: 8761
- Bidding Service: 8081
- Booking Service: 8082
- Identity Service: 8083
- Interaction Service: 8084
- Monitoring Service: 8085
- Tour Management Service: 8086
- Transaction Service: 8087

## Usage
1. Start the Discovery Server first
2. Start the Config Server
3. Start other microservices
4. Services will automatically register with Eureka

## Note
All services are configured to use Eureka for service discovery and include basic logging and monitoring capabilities.
