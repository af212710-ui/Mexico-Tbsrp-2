
# Bot de Discord - México TBSRP

Bot de Discord para servidor de roleplay con sistema completo de gestión de roles, warns, detenciones temporales y verificación de usuarios de Roblox.

## Características

- ✅ Sistema de verificación con Roblox
- ⚠️ Sistema de warns progresivos
- 🔒 Sistema de detenciones temporales
- 👮 Roles automáticos para seguridad pública
- 📊 Comandos de información de usuarios
- 🔓 Comandos de apertura/cierre de servidor

## Instalación

1. Clona el repositorio
2. Instala las dependencias: `npm install`
3. Configura las variables de entorno (ver abajo)
4. Ejecuta el bot: `node index.js`

## Variables de Entorno

Configura estas variables en tu plataforma de hosting:

```
DISCORD_TOKEN=tu_token_de_discord
DATABASE_URL=postgresql://usuario:contraseña@host:puerto/base_de_datos
```

## Comandos Disponibles

- `/abrir` - Anuncia apertura del servidor (Admin)
- `/cerrar` - Anuncia cierre del servidor (Admin)
- `/warn` - Sistema de warns progresivos (Moderadores)
- `/detener` - Detiene usuario temporalmente (Seguridad Pública)
- `/verificar` - Verifica cuenta de Roblox (Todos)
- `/info` - Información de usuario verificado (Todos)
- `/roltemp` - Asigna rol temporal (Admin)
- `/ayuda` - Lista de comandos

## Base de Datos

El bot requiere PostgreSQL con estas tablas:

```sql
CREATE TABLE roblox_verifications (
    id SERIAL PRIMARY KEY,
    discord_user_id VARCHAR(20) UNIQUE NOT NULL,
    roblox_username VARCHAR(50) NOT NULL
);

CREATE TABLE user_warns (
    id SERIAL PRIMARY KEY,
    discord_user_id VARCHAR(20) UNIQUE NOT NULL,
    warn_count INTEGER DEFAULT 0,
    last_warn_at TIMESTAMP
);

CREATE TABLE temporary_roles (
    id SERIAL PRIMARY KEY,
    discord_user_id VARCHAR(20) NOT NULL,
    role_id VARCHAR(20) NOT NULL,
    expires_at TIMESTAMP NOT NULL
);
```

## Deployment en Render

1. Conecta tu repositorio de GitHub
2. Configura las variables de entorno
3. El comando de inicio es: `node index.js`
4. Asegúrate de tener una base de datos PostgreSQL configurada
