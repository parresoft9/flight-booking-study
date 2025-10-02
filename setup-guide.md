# 🛠️ Guía de Configuración del Entorno de Desarrollo

## Requisitos Previos

### Software Necesario
- **Java 17** (OpenJDK recomendado) - esto es lo que dice IBERIA? en planetaX estamos con java 21
- **Maven 3.9.9+**
- **Git**
- **IDE** (IntelliJ IDEA recomendado)
- **Docker** (para bases de datos y servicios)

### Verificación de Instalación
```bash
# Verificar Java
java -version
# Debe mostrar: openjdk version "17.0.x"
# En mi caso: openjdk version "21.0.6" 2025-01-21 LTS

# Verificar Maven
mvn -version
# Debe mostrar: Apache Maven 3.9.9
# En mi caso: Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937

# Verificar Git
git --version
# En mi caso: git version 2.39.5 (Apple Git-154)

# Verificar Docker
docker --version
# En mi caso: Docker version 27.5.0, build a187fa5d2d
```

## 📦 Estructura Base del Proyecto

### 1. Crear Proyecto Base Maven
```bash
# Navegar al directorio de estudio
cd flight-booking-study/

# Crear estructura base con Maven archetype
mvn archetype:generate \
  -DgroupId=com.iberia.flightbooking \
  -DartifactId=flight-booking-base \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DarchetypeVersion=1.4 \
  -DinteractiveMode=false
```

### 2. Configuración Maven Base (pom.xml)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.iberia.flightbooking</groupId>
    <artifactId>flight-booking-base</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>Flight Booking System - IBERIA Study</name>
    <description>Sistema de reservas de vuelos para estudio de patrones IBERIA</description>

    <properties>
        <!-- Java Version -->
        <java.version>17</java.version>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>

        <!-- Spring Boot -->
        <spring.boot.version>3.2.0</spring.boot.version>
        
        <!-- Testing -->
        <junit.version>5.10.2</junit.version>
        <mockito.version>5.8.0</mockito.version>
        <jacoco.version>0.8.13</jacoco.version>
        
        <!-- OpenTelemetry -->
        <opentelemetry.version>1.32.0</opentelemetry.version>
        
        <!-- API Documentation -->
        <springdoc.version>2.3.0</springdoc.version>
        
        <!-- Coverage Thresholds - IBERIA Standards -->
        <jacoco.instruction.minimum>0.80</jacoco.instruction.minimum>
        <jacoco.branch.minimum>0.65</jacoco.branch.minimum>
        <jacoco.line.minimum>0.80</jacoco.line.minimum>
    </properties>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>${spring.boot.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <dependencies>
        <!-- Spring Boot Starters -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>

        <!-- Database -->
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <scope>runtime</scope>
        </dependency>

        <!-- API Documentation -->
        <dependency>
            <groupId>org.springdoc</groupId>
            <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
            <version>${springdoc.version}</version>
        </dependency>

        <!-- Testing -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>

        <!-- OpenTelemetry -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        
        <dependency>
            <groupId>io.micrometer</groupId>
            <artifactId>micrometer-tracing-bridge-otel</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!-- Spring Boot Plugin -->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>${spring.boot.version}</version>
            </plugin>

            <!-- Maven Compiler Plugin -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.12.1</version>
                <configuration>
                    <source>${java.version}</source>
                    <target>${java.version}</target>
                </configuration>
            </plugin>

            <!-- Maven Surefire Plugin (Unit Tests) -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.2.3</version>
                <configuration>
                    <includes>
                        <include>**/*Test.java</include>
                    </includes>
                    <excludes>
                        <exclude>**/*IntegrationTest.java</exclude>
                        <exclude>**/*IT.java</exclude>
                        <exclude>**/*AcceptanceTest.java</exclude>
                        <exclude>**/*AT.java</exclude>
                        <exclude>**/*E2ETest.java</exclude>
                    </excludes>
                    <argLine>${argLine}</argLine>
                </configuration>
            </plugin>

            <!-- JaCoCo Plugin - IBERIA Configuration -->
            <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>${jacoco.version}</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>report</id>
                        <phase>test</phase>
                        <goals>
                            <goal>report</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>check</id>
                        <phase>verify</phase>
                        <goals>
                            <goal>check</goal>
                        </goals>
                        <configuration>
                            <rules>
                                <rule>
                                    <element>BUNDLE</element>
                                    <limits>
                                        <limit>
                                            <counter>INSTRUCTION</counter>
                                            <value>COVEREDRATIO</value>
                                            <minimum>${jacoco.instruction.minimum}</minimum>
                                        </limit>
                                        <limit>
                                            <counter>BRANCH</counter>
                                            <value>COVEREDRATIO</value>
                                            <minimum>${jacoco.branch.minimum}</minimum>
                                        </limit>
                                        <limit>
                                            <counter>LINE</counter>
                                            <value>COVEREDRATIO</value>
                                            <minimum>${jacoco.line.minimum}</minimum>
                                        </limit>
                                    </limits>
                                </rule>
                            </rules>
                        </configuration>
                    </execution>
                </executions>
                <configuration>
                    <excludes>
                        <!-- Exclude configuration classes -->
                        <exclude>**/config/**</exclude>
                        <!-- Exclude DTOs and entities -->
                        <exclude>**/dto/**</exclude>
                        <exclude>**/entity/**</exclude>
                        <!-- Exclude main application class -->
                        <exclude>**/FlightBookingApplication.class</exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## 📂 Estructura de Directorios

```bash
flight-booking-base/
├── pom.xml
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/iberia/flightbooking/
│   │   │       ├── FlightBookingApplication.java
│   │   │       ├── config/
│   │   │       ├── domain/
│   │   │       ├── application/
│   │   │       └── infrastructure/
│   │   └── resources/
│   │       ├── application.yml
│   │       └── static/
│   └── test/
│       └── java/
│           └── com/iberia/flightbooking/
├── target/
└── README.md
```

## 🏃 Comandos de Verificación

```bash
# Compilar proyecto
mvn clean compile

# Ejecutar tests con coverage
mvn clean test jacoco:report

# Verificar thresholds de coverage
mvn clean verify

# Ejecutar aplicación
mvn spring-boot:run

# Generar documentación API
# http://localhost:8080/swagger-ui.html
```

## 🔧 Configuración IDE (IntelliJ IDEA)

### 1. Importar Proyecto
1. File → Open → Seleccionar `pom.xml`
2. Import as Maven project
3. Use SDK: Java 17

### 2. Configurar Code Style
```xml
<!-- .idea/codeStyles/Project.xml -->
<component name="ProjectCodeStyleConfiguration">
  <code_scheme name="Project" version="173">
    <option name="LINE_SEPARATOR" value="&#10;" />
    <option name="RIGHT_MARGIN" value="120" />
  </code_scheme>
</component>
```

### 3. Plugins Recomendados
- **SonarLint** - Análisis de calidad en tiempo real
- **JaCoCo** - Visualización de coverage
- **OpenAPI Generator** - Generación de código desde specs

## 🐳 Servicios Docker (Opcional)

```yaml
# docker-compose.yml
version: '3.8'
services:
  postgres:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: flightbooking
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: admin123
    ports:
      - "5432:5432"
    
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
```

---

**Siguiente paso:** [Módulo 1 - Patrones de Arquitectura](../module-01-architecture/)