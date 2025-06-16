# SoundWaveDb---Taller-expresiones-regulares

## Integrantes 
yo David Alberto Medina 
Diosito

## Descripción del Sistema

SoundWave es una plataforma de streaming de música similar a Spotify que permite a los usuarios descubrir, reproducir y gestionar música. El sistema incluye funcionalidades para artistas, álbumes, canciones, playlists de usuarios y un sistema de recomendaciones basado en géneros musicales.

## Estructura de la Base de Datos

La base de datos está compuesta por 5 colecciones principales:

- **usuarios**: Información de los usuarios registrados
- **artistas**: Datos de los artistas musicales
- **albums**: Información de los álbumes musicales
- **canciones**: Catálogo de canciones disponibles
- **playlists**: Listas de reproducción creadas por usuarios

## Cómo crear la base de datos en MongoDB

1. Conectarse a MongoDB:
```bash
mongosh
```

2. Crear la base de datos:
```javascript
use soundwave_db
```

3. Importar cada colección usando los archivos JSON:

```bash
# Importar usuarios
mongoimport --db soundwave_db --collection usuarios --file coleccion_usuarios.json --jsonArray

# Importar artistas
mongoimport --db soundwave_db --collection artistas --file coleccion_artistas.json --jsonArray

# Importar álbumes
mongoimport --db soundwave_db --collection albums --file coleccion_albums.json --jsonArray

# Importar canciones
mongoimport --db soundwave_db --collection canciones --file coleccion_canciones.json --jsonArray

# Importar playlists
mongoimport --db soundwave_db --collection playlists --file coleccion_playlists.json --jsonArray
```

## Archivos de Colecciones

- `coleccion_usuarios.json` → Colección **usuarios**
- `coleccion_artistas.json` → Colección **artistas**
- `coleccion_albums.json` → Colección **albums**
- `coleccion_canciones.json` → Colección **canciones**
- `coleccion_playlists.json` → Colección **playlists**

## Consultas con Expresiones Regulares

### 1. Validar correos electrónicos con formato válido
```javascript
db.usuarios.find({ "email": { "$regex": "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$", "$options": "i" } })
```
**Utilidad**: Validación de integridad de datos para identificar usuarios con emails malformados que requieren corrección.

### 2. Encontrar usuarios con correos de Gmail
```javascript
db.usuarios.find({ "email": { "$regex": "@gmail\\.com$", "$options": "i" } })
```
**Utilidad**: Segmentación de usuarios para campañas de marketing específicas para usuarios de Gmail.

### 3. Buscar usuarios de ciudades que contengan "Bogotá"
```javascript
db.usuarios.find({ "ubicacion.ciudad": { "$regex": "Bogotá", "$options": "i" } })
```
**Utilidad**: Personalización de contenido y eventos locales para usuarios de Bogotá.

### 4. Buscar usuarios con códigos postales colombianos (formato 6 dígitos)
```javascript
db.usuarios.find({ "ubicacion.ciudad": { "$regex": "^[0-9]{6}$" } })
```
**Utilidad**: Validación de datos de ubicación para servicios de entrega y eventos locales.

### 5. Buscar usuarios con biografías que mencionen "música"
```javascript
db.usuarios.find({ "biografia": { "$regex": "música", "$options": "i" } })
```
**Utilidad**: Identificar usuarios con interés explícito en música para programas de usuarios premium.

### 6. Encontrar usuarios con géneros favoritos que incluyan subgéneros de rock
```javascript
db.usuarios.find({ "generos_favoritos": { "$regex": "rock|metal|punk|grunge", "$options": "i" } })
```
**Utilidad**: Segmentación para campañas de marketing de festivales de rock y metal.

### 7. Buscar artistas con biografías que mencionen "rock"
```javascript
db.artistas.find({ "biografia": { "$regex": "rock", "$options": "i" } })
```
**Utilidad**: Curación automática de contenido para playlists de rock.

### 8. Encontrar artistas latinoamericanos por país
```javascript
db.artistas.find({ "pais": { "$regex": "Colombia|Argentina|México|Chile|Perú|Venezuela", "$options": "i" } })
```
**Utilidad**: Curación de contenido para playlists de música latina y promoción regional.

### 9. Encontrar artistas verificados con redes sociales activas
```javascript
db.artistas.find({ 
  "verificado": true, 
  "redes_sociales": { "$regex": "@[a-zA-Z0-9_]{3,}", "$options": "i" } 
})
```
**Utilidad**: Integración con redes sociales para promoción cruzada y marketing colaborativo.

### 10. Encontrar artistas con redes sociales de Instagram
```javascript
db.artistas.find({ "redes_sociales": { "$regex": "@[a-zA-Z0-9_]+", "$options": "i" } })
```
**Utilidad**: Integración con redes sociales para promoción cruzada.

### 11. Buscar álbumes cuyo título contenga "Love"
```javascript
db.albums.find({ "titulo": { "$regex": "Love", "$options": "i" } })
```
**Utilidad**: Curación automática para playlists románticas y de San Valentín.

### 12. Encontrar álbumes con descripciones que mencionen "debut"
```javascript
db.albums.find({ "descripcion": { "$regex": "debut", "$options": "i" } })
```
**Utilidad**: Sección especial para primeros álbumes de artistas emergentes.

### 13. Buscar álbumes que contengan números en el título
```javascript
db.albums.find({ "titulo": { "$regex": "[0-9]", "$options": "i" } })
```
**Utilidad**: Identificar álbumes numerados o con años en el título.

### 14. Encontrar álbumes de géneros que terminen en "pop"
```javascript
db.albums.find({ "genero": { "$regex": "pop$", "$options": "i" } })
```
**Utilidad**: Filtrado específico para todos los subgéneros de pop (K-pop, electropop, etc.).

### 15. Buscar álbumes con productores que contengan "Records"
```javascript
db.albums.find({ "productor": { "$regex": "Records", "$options": "i" } })
```
**Utilidad**: Análisis de distribución por discográficas y sellos musicales.

### 16. Encontrar canciones cuyo título empiece con "The"
```javascript
db.canciones.find({ "titulo": { "$regex": "^The ", "$options": "i" } })
```
**Utilidad**: Mejora en algoritmos de búsqueda considerando artículos en inglés.

### 17. Buscar canciones con letras que contengan "amor"
```javascript
db.canciones.find({ "letra": { "$regex": "amor", "$options": "i" } })
```
**Utilidad**: Curación automática de canciones románticas para playlists temáticas.

### 18. Buscar canciones instrumentales
```javascript
db.canciones.find({ "letra": { "$regex": "^Instrumental$", "$options": "i" } })
```
**Utilidad**: Playlists para concentración, estudio y música de fondo para establecimientos.

### 19. Buscar canciones con géneros que contengan "electronic"
```javascript
db.canciones.find({ "genero": { "$regex": "electronic", "$options": "i" } })
```
**Utilidad**: Agrupación de todos los subgéneros electrónicos para eventos y festivales.

### 20. Encontrar canciones con colaboraciones (feat.)
```javascript
db.canciones.find({ "titulo": { "$regex": "feat\\.|ft\\.", "$options": "i" } })
```
**Utilidad**: Sección especial de colaboraciones musicales y promoción cruzada.

### 21. Encontrar playlists públicas con alta interacción
```javascript
db.playlists.find({ 
  "publica": true, 
  "seguidores": { "$gte": 1000 } 
})
```
**Utilidad**: Promoción de playlists populares y análisis de tendencias de curación musical.

### 22. Encontrar playlists con descripciones que mencionen "party"
```javascript
db.playlists.find({ "descripcion": { "$regex": "party", "$options": "i" } })
```
**Utilidad**: Curación de contenido para eventos sociales y celebraciones.

### 23. Encontrar playlists multiidioma con tags internacionales
```javascript
db.playlists.find({ "tags": { "$regex": "k-pop|j-pop|latin|spanish|english|french", "$options": "i" } })
```
**Utilidad**: Promoción de diversidad musical y contenido multicultural.

### 24. Encontrar playlists con tags que contengan "chill"
```javascript
db.playlists.find({ "tags": { "$regex": "chill", "$options": "i" } })
```
**Utilidad**: Recomendaciones para momentos de relajación y música ambiente.

### 25. Buscar playlists creadas por usuarios con nombres que empiecen con "DJ"
```javascript
db.playlists.find({ "creador": { "$regex": "^DJ", "$options": "i" } })
```
**Utilidad**: Sección especial de playlists profesionales de DJs para eventos y fiestas.

## Casos de Uso Empresariales

Estas consultas permiten a SoundWave:

1. **Personalización**: Recomendar contenido basado en ubicación, preferencias y comportamiento
2. **Marketing Segmentado**: Dirigir campañas específicas a grupos demográficos
3. **Curación Automática**: Crear playlists temáticas automáticamente
4. **Análisis de Mercado**: Entender tendencias musicales y demográficas de usuarios
5. **Mejora de Búsqueda**: Algoritmos de búsqueda más inteligentes y flexibles
6. **Promoción de Artistas**: Identificar y promocionar contenido específico según contexto