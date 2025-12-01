
# StudyAtHomeV2 - Guía para correr la app en Android Studio (Ionic + Capacitor + FastAPI)

Este archivo explica cómo ejecutar **StudyAtHomeV2  ** en un emulador Android usando Android Studio, Capacitor y FastAPI.

---

## 📌 Requisitos previos

### ✔ Frontend (Ionic + Angular)
- Node.js instalado
- Ionic CLI (`npm install -g @ionic/cli`)
- Proyecto StudyAtHome clonado

### ✔ Backend (FastAPI)
En la carpeta `backend_fastapi`:
1. Crear entorno virtual:
   ```
   python -m venv venv
   ```
2. Activarlo:
   ```
   venv\Scripts\activate
   ```
3. Instalar dependencias:
   ```
   pip install fastapi uvicorn pydantic
   ```

### ✔ Android
- Android Studio instalado
- Al menos 1 AVD creado (Pixel 3a recomendado)

---

# 🚀 1. Iniciar Backend FastAPI

En `backend_fastapi/`:

```
venv\Scripts\activate
uvicorn main:app --reload
```

Debe aparecer:
```
Uvicorn running on http://127.0.0.1:8000
```

---

# 🚀 2. Ajustar URL del API para Android

En `src/app/services/api.ts` cambia:

```
http://127.0.0.1:8000
```

por:

```
http://10.0.2.2:8000
```

> **Importante:** 10.0.2.2 = alias interno en emuladores Android para acceder a tu PC.

---

# 🚀 3. Construir la app Ionic

En la raíz del proyecto:

```
ionic build
```

---

# 🚀 4. Sincronizar Capacitor

```
npx cap sync android
```

---

# 🚀 5. Abrir Android Studio

```
npx cap open android
```

Android Studio abrirá el proyecto nativo en:

```
android/
```

---

# 🚀 6. Ejecutar en el emulador

En Android Studio:

1. Selecciona tu AVD (Pixel 3a o Medium Phone)
2. Haz clic en **Run ▶️**
3. La app se instalará en el emulador y se abrirá automáticamente.

---

# 📸 7. Permisos de Cámara

La primera vez que uses la cámara en la página **Apuntes**, Android pedirá el permiso.

Si no aparece:

1. Ir a **Settings** del emulador  
2. Apps → StudyAtHome  
3. Permissions → Camera → **Allow**

---

# 📡 8. Probar conexión con FastAPI

Desde Android, la app debe usar:

- `GET /asignaturas`
- `POST /recordatorios`
- Etc.

En la consola de FastAPI verás solicitudes como:

```
GET /asignaturas
POST /recordatorios
```

---

# 🌐 9. Modo sin conexión

Si apagas FastAPI:

- La app mostrará un mensaje amarillo de *"Modo sin conexión"*
- Usará datos guardados en Ionic Storage

Esto demuestra:
✔ fallback offline  
✔ persistencia local  
✔ comportamiento robusto ante fallas

---

# 🎉 ¡Listo!  
Tu app ya puede ejecutarse en Android Studio con backend real y modo offline.
