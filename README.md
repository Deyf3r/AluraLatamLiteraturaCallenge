# Literatura Challenge 📚

Una aplicación de consola desarrollada en Spring Boot que permite buscar, guardar y consultar libros utilizando la API de Gutendex. El proyecto incluye funcionalidades para gestionar libros y autores con persistencia en base de datos.

## 🚀 Características

### Funcionalidades de Libros
- **Búsqueda de libros**: Busca libros por título utilizando la API de Gutendex
- **Guardado automático**: Los libros encontrados se guardan automáticamente en la base de datos
- **Prevención de duplicados**: Evita guardar libros que ya existen en la base de datos
- **Listado completo**: Visualiza todos los libros guardados en la base de datos

### Funcionalidades de Autores
- **Lista de autores**: Muestra todos los autores de los libros guardados
- **Autores vivos por año**: Consulta qué autores estaban vivos en un año específico
- **Gestión automática**: Los autores se crean automáticamente al guardar libros

### Datos Gestionados

#### Información de Libros
- Título
- Autor (primer autor de la lista)
- Resumen
- Categorías/Géneros
- Idiomas
- Número de descargas

#### Información de Autores
- Nombre completo
- Año de nacimiento
- Año de fallecimiento (si aplica)
- Lista de libros asociados

## 🛠️ Tecnologías Utilizadas

- **Java 17+**
- **Spring Boot 3.x**
  - Spring Data JPA
  - Spring Boot Starter Web
- **Base de Datos**: PostgreSQL/MySQL (configurable)
- **Jackson**: Para el manejo de JSON
- **Maven**: Gestión de dependencias

## 📁 Estructura del Proyecto

```
src/main/java/com/example/LiteraturaChallenge/
├── LiteraturaChallengeApplication.java  # Clase principal
├── MenuApp.java                         # Interfaz de usuario (consola)
├── BibliotecaService.java              # Lógica de negocio
├── Libros.java                         # Entidad Libro
├── Autores.java                        # Entidad Autor
├── ILibroRepo.java                     # Repositorio de Libros
├── IAutorRepo.java                     # Repositorio de Autores
└── obtenerDatos.java                   # Servicio para consultar API
```

## ⚙️ Configuración

### Requisitos Previos
- Java 17 o superior
- Maven 3.6+
- Base de datos (PostgreSQL recomendada)

### Configuración de Base de Datos

Configura tu archivo `application.properties`:

```properties
# Configuración de base de datos
spring.datasource.url=jdbc:postgresql://localhost:5432/literatura_db
spring.datasource.username=tu_usuario
spring.datasource.password=tu_contraseña

# Configuración JPA
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

## 🚀 Instalación y Ejecución

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/tu-usuario/literatura-challenge.git
   cd literatura-challenge
   ```

2. **Configurar la base de datos**
   - Crea una base de datos llamada `literatura_db`
   - Actualiza las credenciales en `application.properties`

3. **Ejecutar la aplicación**
   ```bash
   mvn spring-boot:run
   ```

## 📖 Uso de la Aplicación

Al ejecutar la aplicación, se mostrará un menú interactivo con las siguientes opciones:

1. **Buscar libro por título**: Busca y guarda un libro desde la API
2. **Listar libros registrados**: Muestra todos los libros en la base de datos
3. **Listar autores registrados**: Muestra todos los autores guardados
4. **Listar autores vivos en un determinado año**: Filtra autores por año de vida
5. **Salir**: Termina la aplicación

### Ejemplo de Uso

```
=== BIBLIOTECA DIGITAL ===
1. Buscar libro por título
2. Listar libros registrados
3. Listar autores registrados
4. Listar autores vivos en un determinado año
5. Salir

Seleccione una opción: 1
Ingrese el título del libro: Don Quijote

✅ Libro guardado exitosamente:
Título: Don Quixote
Autor: Cervantes Saavedra, Miguel de
Idiomas: [es]
Descargas: 12345
```

## 🔍 API Utilizada

Este proyecto utiliza la [API de Gutendex](https://gutendex.com/), que proporciona acceso gratuito a los libros del Proyecto Gutenberg.

**Endpoint utilizado**: `https://gutendx.com/books/?search={titulo}`

## 📊 Modelo de Datos

### Relaciones
- Un autor puede tener múltiples libros (One-to-Many)
- Un libro pertenece a un solo autor (Many-to-One)
- Los idiomas se almacenan como una colección de strings

### Consideraciones Especiales
- **Un solo autor por libro**: Aunque la API puede devolver múltiples autores, el sistema toma solo el primer autor para simplificar las consultas
- **Prevención de duplicados**: Se verifica que no existan libros o autores duplicados antes de guardar
- **Manejo de nulos**: Los campos opcionales (fechas de nacimiento/muerte, resumen) se manejan de forma segura

## 🤝 Contribución

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.

## 🐛 Problemas Conocidos

- La API de Gutendex puede tener límites de velocidad
- Algunos libros pueden no tener toda la información completa
- La búsqueda es sensible a la ortografía exacta
