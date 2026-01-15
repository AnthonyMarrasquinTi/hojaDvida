# 🚀 Despliegue en Render.com

## 📋 Variables de Entorno Requeridas

Configura estas variables en el dashboard de Render:

### Django Configuration
- `SECRET_KEY`: Clave secreta de Django (generada automáticamente por Render)
- `DEBUG`: `False`
- `ALLOWED_HOSTS`: Tu dominio en Render (ej: `tu-app.onrender.com`)

### Azure Blob Storage
- `AZURE_STORAGE_CONNECTION_STRING`: Connection string de Azure Storage
- `AZURE_STORAGE_CONTAINER`: Nombre del contenedor (default: `certificados`)

### Base de Datos (Futuro)
- `DATABASE_URL`: URL de PostgreSQL (opcional, por ahora usa SQLite)

## 📁 Archivos Creados/Modificados

### ✅ Creados:
- `requirements.txt` - Todas las dependencias Python
- `build.sh` - Script de build con dependencias de sistema
- `render.yaml` - Configuración de Render
- `DEPLOYMENT_README.md` - Esta guía

### ✅ Modificados:
- `config/settings.py` - Configuración para producción con WhiteNoise

## 🚀 Pasos de Despliegue

1. **Sube tu código a GitHub**
2. **Conecta Render con tu repo**
3. **Configura las variables de entorno** (ver arriba)
4. **Render ejecutará automáticamente:**
   - `build.sh` (instala dependencias del sistema)
   - `pip install -r requirements.txt`
   - `python manage.py collectstatic`
   - `python manage.py migrate`
   - Inicia con gunicorn

## ⚠️ Errores Comunes y Soluciones

### 1. WeasyPrint no funciona
- ✅ `build.sh` instala todas las dependencias del sistema
- ✅ Incluye `libcairo2`, `libpango`, etc.

### 2. Archivos estáticos no cargan
- ✅ WhiteNoise está configurado en `settings.py`
- ✅ `collectstatic` se ejecuta en el build

### 3. PDFs no se generan
- ✅ Todas las dependencias están en `requirements.txt`
- ✅ Build script instala dependencias del sistema

### 4. Azure Storage no conecta
- ✅ Variables de entorno configuradas correctamente
- ✅ Connection string válida

### 5. Base de datos
- ✅ SQLite funciona out-of-the-box
- ✅ Preparado para PostgreSQL en el futuro

## 🔍 Verificación Post-Despliegue

1. **Visita tu URL en Render**
2. **Login al admin** (`/admin/`)
3. **Visualiza la hoja de vida**
4. **Descarga PDFs** (Check y Check All)
5. **Verifica que los certificados carguen** desde Azure

## 📞 Soporte

Si algo no funciona:
1. Revisa los logs en Render
2. Verifica las variables de entorno
3. Confirma que Azure Storage esté accesible
4. Prueba localmente con `DEBUG=True`

¡Tu aplicación debería funcionar perfectamente en producción! 🎉
