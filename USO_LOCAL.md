# Uso de rshk-jsifenlib como dependencia local

Para utilizar esta librería en otros proyectos de tu misma máquina (sin necesidad de publicarla en internet), la mejor forma es instalarla en tu repositorio **Maven Local** (`~/.m2/repository`). 

De esta forma, cualquier gestor de dependencias como Maven o Gradle podrá encontrarla y resolverla automáticamente.

## Requisitos previos

- Tener **Java 8** instalado y configurado (ya que la librería hace uso de paquetes como `javax.xml.soap` que fueron extraídos del JDK en versiones superiores).
- Ejecutar los comandos desde la raíz del proyecto `rshk-jsifenlib`.

## Paso 1: Publicar a Maven Local

Abre una terminal en la carpeta raíz de este proyecto y ejecuta el siguiente comando:

**En Linux / macOS:**
```bash
./gradlew publishToMavenLocal -x test
```

**En Windows:**
```cmd
gradlew.bat publishToMavenLocal -x test
```

Este comando compilará el proyecto y lo instalará en tu directorio local de Maven.

## Paso 2: Importar en tu nuevo proyecto

Una vez publicado, puedes ir a tu otro proyecto y agregar esta librería como si fuera una dependencia cualquiera.

### Si tu otro proyecto usa Gradle (`build.gradle` o `build.gradle.kts`)

1. Asegúrate de tener habilitado el repositorio `mavenLocal()` en la sección de repositorios:

```groovy
repositories {
    mavenCentral()
    mavenLocal() // <-- Es obligatorio agregar esta línea
}
```

2. Añade la dependencia a tu proyecto:

```groovy
dependencies {
    implementation 'com.roshka.sifen:rshk-jsifenlib:0.2.4'
}
```

### Si tu otro proyecto usa Maven (`pom.xml`)

No necesitas declarar el repositorio local (Maven lo busca allí por defecto). Simplemente agrega la dependencia dentro del bloque `<dependencies>`:

```xml
<dependency>
    <groupId>com.roshka.sifen</groupId>
    <artifactId>rshk-jsifenlib</artifactId>
    <version>0.2.4</version>
</dependency>
```

> **Nota de versión:** Si en el futuro actualizas la versión de este proyecto en su archivo `build.gradle`, recuerda correr de nuevo el comando del **Paso 1** y actualizar el número de `<version>` en tu proyecto destino.
