# 🗂️ Estructura del proyecto refactorizado

```
sealeticas-campos/
├── index.html          ← App (sin base de datos, solo ~128 KB)
├── signs.json          ← Base de datos de señaléticas
├── imagenes/           ← Imágenes PNG de cada señalética
│   ├── 001_PROHIBIDO_EL_INGRESO_AREA_RESTRINGIDA.png
│   ├── 002_...png
│   └── ...
├── manifest.json
├── sw.js
└── netlify.toml
```

---

## ✅ Cómo agregar una nueva señalética

### 1. Prepara la imagen
- Formato: **PNG**
- Nombre: `056_NOMBRE_DE_LA_SEÑAL.png` (número correlativo + nombre en mayúsculas con guiones bajos)
- Colócala en la carpeta `imagenes/`

### 2. Edita `signs.json`
Agrega un nuevo objeto al final del arreglo:

```json
{
  "id": 56,
  "name": "NOMBRE DE LA SEÑAL",
  "category": "Obligación",
  "file": "imagenes/056_NOMBRE_DE_LA_SEÑAL.png"
}
```

**Categorías disponibles:**
- `Prohibición`
- `Obligación`
- `Advertencia`
- `Emergencia`
- `Información`

### 3. Sube los cambios a GitHub
```bash
git add imagenes/056_NOMBRE_DE_LA_SEÑAL.png
git add signs.json
git commit -m "Agrega señal #56: NOMBRE DE LA SEÑAL"
git push
```

**Netlify despliega automáticamente en ~1 minuto. ¡Listo!**

---

## 🔧 Configuración inicial (una sola vez)

### Paso 1 — Crea el repositorio en GitHub
1. Ve a [github.com](https://github.com) → **New repository**
2. Nombre: `sealeticas-campos`
3. Visibilidad: **Private** (recomendado)
4. Clic en **Create repository**

### Paso 2 — Sube los archivos
```bash
# En tu computadora, dentro de la carpeta del proyecto:
git init
git add .
git commit -m "Proyecto inicial refactorizado"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/sealeticas-campos.git
git push -u origin main
```

### Paso 3 — Conecta Netlify con GitHub
1. Ve a [app.netlify.com](https://app.netlify.com)
2. **Add new site** → **Import an existing project**
3. Selecciona **GitHub** → elige el repo `sealeticas-campos`
4. Configuración de build:
   - **Build command:** *(dejar vacío)*
   - **Publish directory:** `.` (un punto)
5. Clic en **Deploy site**

### Paso 4 — Activa deploy automático
Ya está activado por defecto. Cada `git push` a `main` redespliega el sitio.

---

## 💡 Tips

- **¿Sin Git?** Puedes arrastrar la carpeta completa a Netlify en
  `app.netlify.com` → tu sitio → **Deploys** → zona de drag & drop.
- **Editar signs.json online:** Ve al repo en GitHub → clic en `signs.json`
  → ícono de lápiz ✏️ → edita → **Commit changes**.
- El `sw.js` (service worker) cachea los archivos para modo offline.
  Cuando actualices `signs.json` o imágenes, los usuarios verán los
  cambios al refrescar la app.
