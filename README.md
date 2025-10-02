# 🛩️ Flight Booking Study Project
## Proyecto de Estudio Completo para Evaluación Backend IBERIA

Este proyecto implementa un sistema completo de reservas de vuelos siguiendo los estándares y patrones documentados en el playbook de IBERIA.

## 📁 Estructura del Proyecto

```
flight-booking-study/
├── README.md                           # Este archivo
├── environment-setup/                  # Configuración del entorno
├── module-01-architecture/             # Patrones arquitectónicos
│   ├── 3-layers-implementation/
│   ├── vsa-implementation/
│   └── hexagonal-implementation/
├── module-02-api-design/               # Diseño de APIs REST
├── module-03-testing/                  # Testing y JaCoCo
├── module-04-observability/            # OpenTelemetry y monitoring
├── module-05-cicd/                     # GitHub Actions y CI/CD
├── module-06-technical-debt/           # Gestión de deuda técnica
└── final-project/                      # Proyecto integrador final
```

## 🎯 Objetivos de Aprendizaje

- [ ] Dominar los 3 patrones arquitectónicos de IBERIA
- [ ] Diseñar APIs REST siguiendo estándares
- [ ] Implementar testing con >80% coverage
- [ ] Configurar observabilidad completa
- [ ] Crear pipelines de CI/CD
- [ ] Gestionar Technical Debt correctamente

## 🚀 Plan de Estudio

### Módulo 1: Arquitectura (Semana 1-2)
- Patrones: 3-Layers, VSA, Hexagonal
- Criterios de decisión arquitectónica
- Implementación práctica

### Módulo 2: API Design (Semana 2)
- REST API standards
- OpenAPI 3.1 specification
- Contract testing

### Módulo 3: Testing (Semana 3)
- Unit, Integration, E2E testing
- JaCoCo configuration
- Coverage >80%

### Módulo 4: Observabilidad (Semana 4)
- Logs, Metrics, Traces
- OpenTelemetry implementation
- GDPR compliance

### Módulo 5: CI/CD (Semana 5)
- GitHub Actions
- Automated testing
- Deployment strategies

### Módulo 6: Technical Debt (Semana 6)
- Identificación y clasificación
- Gestión y priorización
- Refactoring strategies

## 📚 Referencias

- [IBERIA Development Fundamentals Checklist](../docs/development-fundamentals-checklist.md)
- [Architecture Decision Guide](../docs/design/architecture/architecture_decision_guide.md)
- [REST API Design](../docs/design/design-pattern/rest-api-design.md)
- [Testing Guidelines](../docs/Testing/01-Unit%20Test/01-Unit-Test.md)
- [Observability Practices](../docs/observability/recommended-practices.md)

## 🛠️ Tecnologías Utilizadas

- **Java 21** - Lenguaje principal
- **Spring Boot 3.x** - Framework web
- **Maven** - Gestión de dependencias
- **JUnit 5** - Testing framework
- **JaCoCo** - Code coverage
- **OpenTelemetry** - Observabilidad
- **OpenAPI 3.1** - API specification
- **GitHub Actions** - CI/CD

---

*Siguiente paso: [Configurar Entorno de Desarrollo](environment-setup/)*