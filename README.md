# Proyecto TaskMaster

---

## Descripción del Proyecto

**TaskMaster** es una aplicación sencilla de gestión de tareas en Java, construida con **Maven**. Este proyecto te guiará por los fundamentos de Maven: desde la creación del proyecto y la gestión de dependencias hasta las pruebas unitarias, el empaquetado y el uso de **perfiles** para diferentes entornos.

Actualmente, la aplicación añade y lista tareas en la consola, mostrando también el ambiente de ejecución configurado.

---

## Pasos Rápidos para Configurar y Ejecutar

Sigue estos pasos para poner en marcha TaskMaster:

1.  **Crea el proyecto Maven:**
    ```bash
    mvn archetype:generate -DgroupId=com.equipo.taskmaster -DartifactId=taskmaster -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    cd taskmaster
    ```

2.  **Actualiza `src/main/java/com/equipo/taskmaster/App.java`** con el código completo proporcionado en las instrucciones originales, incluyendo la línea `System.out.println("Ambiente: " + System.getProperty("env.name"));`.

3.  **Añade la dependencia `commons-lang3` a tu `pom.xml`**:
    ```xml
    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.12.0</version>
    </dependency>
    ```

4.  **Actualiza `src/test/java/com/equipo/taskmaster/AppTest.java`** con la prueba unitaria:
    ```java
    package com.equipo.taskmaster;
    import static org.junit.Assert.assertEquals;
    import org.junit.Test;
    public class AppTest {
        @Test
        public void testAddTask() {
            App.tasks.clear();
            App.addTask("Terminar ejercicio Maven");
            assertEquals(1, App.tasks.size());
        }
    }
    ```
    Ejecuta las pruebas: `mvn test`

5.  **Añade los plugins `maven-compiler-plugin` y `exec-maven-plugin` a tu `pom.xml`** (dentro de la sección `<build><plugins>`) para compilar y ejecutar:
    ```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>11</source>
                    <target>11</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>3.1.0</version>
                <configuration>
                    <mainClass>com.equipo.taskmaster.App</mainClass>
                </configuration>
            </plugin>
        </plugins>
    </build>
    ```
    Luego, empaqueta y ejecuta:
    ```bash
    mvn clean package
    mvn exec:java
    ```

6.  **Añade perfiles (`dev` y `prod`) a tu `pom.xml`** (dentro de la sección `<profiles>`):
    ```xml
    <profiles>
        <profile>
            <id>dev</id>
            <properties>
                <env.name>Desarrollo</env.name>
            </properties>
        </profile>
        <profile>
            <id>prod</id>
            <properties>
                <env.name>Producción</env.name>
            </properties>
        </profile>
    </profiles>
    ```
    Ejecuta con un perfil, por ejemplo, `dev`: `mvn exec:java -Pdev`

---

## Comandos Maven Clave

* **`mvn test`**: Ejecuta las pruebas.
* **`mvn clean package`**: Limpia, compila, prueba y empaqueta el JAR.
* **`mvn exec:java`**: Ejecuta la aplicación principal.
* **`mvn exec:java -P[nombre_perfil]`**: Ejecuta con un perfil específico.

---

## Dependencias y Plugins

* **Dependencia**: `org.apache.commons:commons-lang3:3.12.0` (utilidades).
* **Plugins**:
    * `maven-compiler-plugin`: Compila el código Java (versión 3.8.1, Java 11).
    * `exec-maven-plugin`: Ejecuta la clase principal de la aplicación.

---

## Aprendizaje y Desafíos con Maven

* **Mayor Aprendizaje**: La **gestión de perfiles (profiles)** para diferentes entornos ha sido un gran descubrimiento, ofreciendo flexibilidad para configurar el proyecto sin modificar el código.
* **Mayor Desafío**: Depurar errores de **classpath y la configuración de plugins** (como `exec-maven-plugin`). Entender la estructura del `pom.xml` fue crucial para superar estos problemas.

---
