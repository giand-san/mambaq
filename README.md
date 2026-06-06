# MAMBAQ — Arte con Inteligencia Artificial

**Museo de Arte Moderno de Barranquilla · Álvaro Cepeda Samudio**

> Transforma los dibujos de los niños en obras de arte inspiradas en los grandes maestros, usando Inteligencia Artificial directamente en el navegador.

---

##  ¿Qué es MAMBAQ?

MAMBAQ es una aplicación web **mobile-first** desarrollada para el Museo de Arte Moderno de Barranquilla como parte de un programa interdisciplinario de la **Universidad Simón Bolívar**. Permite a niños y familias escanear sus dibujos, clasificarlos con IA y exhibirlos en una galería digital interactiva.

---

##  Funcionalidades

- ** Escanear dibujos** — Carga una foto o imagen desde el dispositivo
- ** Mejorar imagen** — Ajustes automáticos de contraste, saturación, nitidez y brillo
- ** Clasificador de IA** — Identifica el tipo de dibujo usando Teachable Machine de Google (sin enviar datos al servidor)
- ** Galería interactiva** — Museo digital con todas las obras guardadas
- ** Guardado en base de datos** — Almacena título, autor, edad e imagen de cada obra

---

##  Estructura del proyecto

```
mambaq/
├── index.html
├── CSS/
│   └── style.css
├── JS/
│   └── app.js
├── PHP/
│   ├── bdMambaq.php          # Conexión a la base de datos
│   ├── guardarObra.php       # Guardar obra (POST)
│   ├── listasObras.php       # Listar obras (GET)
│   └── obtenerImagen.php     # Servir imagen por ID (GET)
├── package.json
└── README.md
```



---

## Tecnologías

| Capa | Tecnología |
|---|---|
| Frontend | HTML5, CSS3, JavaScript (Vanilla) |
| IA / Clasificador | [Teachable Machine](https://teachablemachine.withgoogle.com/) · TensorFlow.js |
| Backend | PHP 8+ |
| Base de datos | MySQL |
| Fuentes | Playfair Display · DM Sans (Google Fonts) |

---

## Instalación local

### Requisitos
- PHP 8+
- MySQL
- Servidor local (XAMPP, Laragon, WAMP, etc.)

### Pasos

**1. Clona el repositorio**
```bash
git clone https://github.com/giand-san/mambaq.git
cd mambaq
```

**2. Crea la base de datos**

Abre phpMyAdmin y ejecuta:

```sql
CREATE DATABASE mambaq_bd CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

USE mambaq_bd;

CREATE TABLE obras (
  id INT AUTO_INCREMENT PRIMARY KEY,
  titulo VARCHAR(255) NOT NULL,
  autor VARCHAR(255) NOT NULL,
  edad VARCHAR(50),
  imagen_original LONGBLOB,
  imagen_original_mime VARCHAR(100),
  imagen_original_nombre VARCHAR(255),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**3. Configura la conexión en `PHP/bdMambaq.php`**

```php
$host          = "localhost";
$usuario_db    = "tu_usuario";
$contrasena_db = "tu_contraseña";
$nombre_db     = "mambaq_bd";
```

**4. Abre en el navegador**

Coloca el proyecto dentro de `htdocs` (XAMPP) o `www` (Laragon) y accede a:
```
http://localhost/mambaq/
```

---

##  Despliegue en producción

### Opción A — InfinityFree (PHP + MySQL gratis)
1. Crea cuenta en [infinityfree.com](https://infinityfree.net)
2. Crea un hosting y una base de datos MySQL
3. Sube los archivos por el File Manager a `htdocs/`
4. Actualiza `PHP/bdMambaq.php` con las credenciales del hosting
5. Ejecuta el SQL de creación de tabla en el phpMyAdmin del hosting

### Opción B — Supabase + Render (sin PHP)
Migrar el backend a [Supabase](https://supabase.com) (PostgreSQL + Storage) y desplegar el frontend como **Static Site** en [Render](https://render.com). Requiere reemplazar los archivos PHP por llamadas al SDK de Supabase desde `app.js`.

---

##  Modelo de IA

El clasificador usa un modelo entrenado con **Teachable Machine** de Google:

- **URL del modelo:** `https://teachablemachine.withgoogle.com/models/GOsD0dAnf/`
- Reconoce categorías de dibujos infantiles
- Se ejecuta completamente en el navegador — sin envío de datos a ningún servidor

---

## 🔧 Limpiar el repositorio

El repo actualmente contiene carpetas de `node_modules`. Para limpiarlas:

```bash
# 1. Crea el .gitignore
echo "node_modules/" > .gitignore

# 2. Elimina las carpetas del historial de git
git rm -r --cached node_modules/
git add .gitignore
git commit -m "chore: remove node_modules from repo"
git push
```

---

##  Equipo

Desarrollado como proyecto académico en la **Universidad Simón Bolívar — Barranquilla**

| Nombre |
|---|
| Jhosua Esteban Rubio Yasno |
| Sharon Nicoll Gasca Yepes |
| Gian David Sanchez de la Ossa |

---

##  Sobre el museo

El **Museo de Arte Moderno de Barranquilla (MAMBAQ) — Álvaro Cepeda Samudio** es una institución cultural dedicada a la preservación y difusión del arte moderno y contemporáneo en el Caribe colombiano.

**Álvaro Cepeda Samudio** (1926–1972) fue uno de los grandes escritores del Caribe colombiano, parte del legendario Grupo de Barranquilla junto a Gabriel García Márquez. Su legado inspira esta iniciativa que une arte, niñez e innovación tecnológica.

---

## Licencia

Proyecto desarrollado con fines educativos y culturales para el MAMBAQ y la Universidad Simón Bolívar. Todos los derechos reservados.
