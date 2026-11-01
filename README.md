# Java-SpringBoot-BeansFactory

[![Java 17](https://img.shields.io/badge/Java-17-orange.svg)](https://www.oracle.com/java/)
[![Spring Framework](https://img.shields.io/badge/Spring%20Framework-5%2F6-green.svg)](https://spring.io/projects/spring-framework)
[![Maven](https://img.shields.io/badge/Build-Maven-blue.svg)](https://maven.apache.org/)

Aplicación demostrativa desarrollada con **Java 17**, **Maven** y **Spring Framework**. El proyecto muestra cómo crear y obtener un bean mediante un contexto de Spring configurado en XML, incluyendo la definición de su alcance y un alias.

> Aunque el repositorio se llama `Java-SpringBoot-BeansFactory`, este ejemplo usa Spring Framework directamente; no incluye Spring Boot ni expone una API web.

---

## 🚀 Características principales

- **Contenedor de Spring:** carga un `ApplicationContext` desde un archivo XML.
- **Configuración XML:** define el bean `curso`, su argumento de constructor y su alias.
- **Alcance prototype:** cada solicitud del bean al contenedor puede crear una instancia nueva.
- **Ejemplo de dominio:** la clase `Curso` contiene propiedades para representar un curso.
- **Ejecución sencilla:** la clase `Main` obtiene el bean e imprime su identificador.
- **Build con Maven:** el proyecto está configurado para compilarse con Java 17 y empaquetarse como WAR.

---

## 🛠️ Stack tecnológico

| Componente | Tecnología | Versión / detalle |
| :--- | :--- | :--- |
| **Lenguaje** | Java | 17 |
| **Contenedor de dependencias** | Spring Framework | `spring-beans` 5.3.20 y `spring-context` 6.1.20 |
| **Gestión de dependencias y build** | Maven | `pom.xml` |
| **Empaquetado** | WAR | Configurado en Maven |
| **Configuración del contexto** | XML | `applicationContex.xml` |

---

## 📂 Estructura del proyecto

```text
Java-SpringBoot-BeansFactory/
├── pom.xml
├── src/
│   └── main/
│       ├── java/com/example/spring/
│       │   ├── curso/
│       │   │   └── Curso.java
│       │   └── main/
│       │       └── Main.java
│       ├── resources/
│       │   ├── application.properties
│       │   └── applicationContex.xml
│       └── webapp/
│           └── WEB-INF/
│               └── web.xml
└── README.md
```

### Componentes principales

- **`Curso`**: POJO serializable con atributos `id`, `codigo`, `descripcion` y `cantidaAlumnos`.
- **`applicationContex.xml`**: registra el bean `curso` con alcance `prototype`, le asigna el identificador `10` mediante el constructor y declara el alias `cursoalias`.
- **`Main`**: crea un `ClassPathXmlApplicationContext`, solicita el bean `curso` e imprime su identificador.

---

## ⚙️ Guía de inicio rápido

### Requisitos previos

- **JDK 17**
- **Maven**

### 1. Compilar el proyecto

Desde la raíz del repositorio, ejecuta:

```bash
mvn clean compile
```

### 2. Ejecutar el ejemplo

```bash
mvn compile exec:java -Dexec.mainClass="com.example.spring.main.Main"
```

La salida esperada es:

```text
10
```

El identificador corresponde al valor configurado para el constructor del bean `curso` en `applicationContex.xml`.

### 3. Empaquetar como WAR

```bash
mvn package
```

---

## 🧩 Ejemplo de configuración del bean

El archivo `applicationContex.xml` define el bean y su alias:

```xml
<bean id="curso" class="com.example.spring.curso.Curso" scope="prototype">
    <constructor-arg name="id" value="10" />
</bean>
<alias name="curso" alias="cursoalias" />
```

La clase principal accede al bean por su nombre:

```java
ApplicationContext context =
        new ClassPathXmlApplicationContext("applicationContex.xml");
Curso curso = (Curso) context.getBean("curso");
System.out.println(curso.getId());
```
