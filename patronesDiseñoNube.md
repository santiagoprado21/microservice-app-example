# Patrones de Diseño de Nube

Este documento describe dos patrones de diseño de nube aplicados en el proyecto: **External Configuration Store** y **Gateway Aggregation**. Se detallan sus implementaciones, ventajas y ejemplos concretos dentro del sistema.

---

## 🛠️ External Configuration Store (Almacén de Configuración Externa)

Este patrón se basa en externalizar la configuración de los servicios fuera del código fuente, permitiendo una mayor flexibilidad y mantenibilidad.

### 📦 Implementación

Se implementa a través del archivo `docker-compose.yaml`, donde se definen variables de entorno para cada servicio:

```yaml
# Configuración del servicio users-api
users-api:
  environment:
    - SERVER_PORT=8083
    - JWT_SECRET=PRFT

# Configuración del servicio auth-api
auth-api:
  environment:
    - ZIPKIN_URL=http://zipkin:9411/api/v2/spans
    - AUTH_API_PORT=8000
    - USERS_API_ADDRESS=http://users-api:8083
    - JWT_SECRET=PRFT

# Configuración del servicio todos-api
todos-api:
  environment:
    - TODO_API_PORT=8082
    - JWT_SECRET=PRFT
    - REDIS_HOST=redis-queue
    - REDIS_PORT=6379
    - REDIS_CHANNEL=log_channel
```

### ✅ Ventajas

- Separación entre la configuración y el código.
- Permite cambiar configuraciones sin recompilar ni desplegar nuevamente.
- Soporta múltiples entornos (desarrollo, pruebas, producción).
- Facilita la centralización y gestión de configuraciones.

---

## 🌐 Gateway Aggregation (Agregación de Gateway)

Este patrón consiste en tener un punto de entrada único (frontend) para el cliente, que distribuye las peticiones a los servicios correspondientes, agrega sus respuestas y entrega una única respuesta al usuario.

### 📦 Implementación

El frontend se configura también en el `docker-compose.yaml`:

```yaml
frontend:
  environment:
    - AUTH_API_ADDRESS=http://auth-api:8000
    - TODOS_API_ADDRESS=http://todos-api:8082
```

### 🔁 Flujo de Petición

1. El cliente realiza una petición al frontend (Vue.js).
2. El frontend valida la autenticación mediante `auth-api`.
3. Si está autenticado, consulta los datos de tareas en `todos-api`.
4. También puede obtener información del usuario desde `users-api`.
5. Une la información y devuelve una respuesta completa al cliente.

### ✅ Ventajas

- El cliente interactúa con un único endpoint.
- Centraliza la lógica de autenticación.
- Permite la agregación de datos desde múltiples servicios.
- Mejora la seguridad ocultando la arquitectura interna.
- Simplifica el manejo de errores y transformación de respuestas.