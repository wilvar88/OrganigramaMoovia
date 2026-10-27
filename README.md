# 🏢 Organigrama Dinámico Corporativo | Executive Suite v2.0

Visualizador interactivo de organigrama corporativo de alta fidelidad, diseñado con arquitectura D3.js, SheetJS, soporte de posiciones vacantes, persistencia de datos (JSON y LocalStorage), y listo para despliegue inmediato en **Git** y **Vercel**.

---

## 🚀 Despliegue Rápido en Vercel (Paso a Paso)

Este proyecto está optimizado como aplicación web estática de alto rendimiento para desplegarse en segundos:

### 1. Inicializar y subir a tu repositorio Git (GitHub / GitLab / Bitbucket)
Si aún no has vinculado tu repositorio remoto, abre tu terminal en la carpeta del proyecto y ejecuta:

```bash
# 1. Comprobar que git está inicializado (ya lo dejamos inicializado para ti)
git status

# 2. Agregar todos los archivos y confirmar cambios
git add .
git commit -m "feat: organigrama corporativo v2 con soporte de vacantes, persistencia y logo"

# 3. Vincular con tu repositorio en GitHub (reemplaza TU_USUARIO y TU_REPO)
git remote add origin https://github.com/TU_USUARIO/TU_REPO.git
git branch -M main
git push -u origin main
```

### 2. Desplegar en Vercel con 1 Clic
1. Entra a [vercel.com](https://vercel.com) e inicia sesión.
2. Haz clic en **"Add New..."** -> **"Project"**.
3. Selecciona tu repositorio de GitHub recién subido.
4. Vercel detectará automáticamente la configuración (`vercel.json`). **No necesitas configurar variables de entorno ni comandos de build.**
5. Haz clic en **"Deploy"**. En 10 segundos tendrás tu enlace público HTTPS funcionando para toda tu organización.

---

## 💾 ¿Cómo funciona la Memoria y Persistencia de la Información?

Para darte máxima flexibilidad y compatibilidad con Vercel, el sistema cuenta con dos niveles de persistencia:

### Nivel 1: Memoria Automática en Navegador (`localStorage`)
- Cada vez que subes un archivo Excel (`.xlsx` o `.xls`) o cargas un archivo `.json`, el sistema **guarda automáticamente toda la estructura en la memoria de tu navegador**.
- Si recargas la página, cierras el navegador o abres la pestaña días después, tus datos y la jerarquía se cargarán inmediatamente sin pedirte volver a subir el archivo.

### Nivel 2: Memoria Oficial del Proyecto (`data/organigrama.json`)
- Las plataformas como Vercel y GitHub son de solo lectura en ejecución (no permiten que un navegador modifique directamente los archivos del servidor por seguridad).
- Por eso, la aplicación incluye el botón **"Guardar JSON"** en la barra superior.
- **Flujo recomendado para actualizar el organigrama para todos los usuarios en Vercel:**
  1. Abre la aplicación y sube tu nuevo archivo Excel con las novedades de personal.
  2. Haz clic en el botón **"Guardar JSON"** (se descargará `organigrama.json`).
  3. Reemplaza el archivo `organigrama.json` dentro de la carpeta `data/` del proyecto.
  4. Haz `git commit -am "actualizar organigrama"` y `git push`.
  5. ¡Listo! Vercel se actualizará al instante y cualquier persona que entre a tu enlace verá el nuevo organigrama.

---

## 📊 Estructura de Columnas del Excel (10 Columnas Oficiales)

Puedes descargar la plantilla oficial en cualquier momento haciendo clic en **"Descargar Plantilla"**. El archivo contiene las siguientes 10 columnas en orden:

| # | Columna | Obligatorio | Descripción |
|---|---------|-------------|-------------|
| 1 | **Documento** | Sí | Cédula, DNI o identificador único del colaborador (ej. `1001001`). |
| 2 | **Nombre** | Sí | Nombre completo del colaborador (o escribir `Vacante`). |
| 3 | **Foto del Colaborador** | Opcional | Enlace directo a imagen o enlace compartido de **Google Drive**. Si está vacío, se genera un avatar con las iniciales. |
| 4 | **Cargo** | Sí | Título oficial del cargo (ej. `Gerente de Tecnología & CTO`). |
| 5 | **Área** | Sí | Área o departamento operativo (ej. `Infraestructura Cloud`). |
| 6 | **Gerencia** | Sí | Gerencia o división a la que pertenece (ej. `Gerencia de Tecnología`). |
| 7 | **Nivel** | Sí | Nivel estratégico (ej. `Nivel 1 - Estratégico`, `Nivel 2 - Táctico`, etc.). |
| 8 | **Reporta A** | Opcional | Documento de identidad del jefe directo. |
| 9 | **Nombre a Quien Reporta** | Opcional | Nombre del jefe o líder directo (o escribir `Vacante`). |
| 10 | **Cargo a quien reporta** | Opcional | Título del cargo del jefe directo (ej. `Gerente de Operaciones & Supply Chain`). |

---

## ⚡ Manejo de Cargos Vacantes o Renuncias

¿Qué pasa si un líder o jefe renunció, el puesto está vacante o en proceso de selección?

1. **Si un cargo está vacante:**
   En la columna `Nombre` coloca **`Vacante`** (o `Posición Vacante`).
   - El sistema le dará automáticamente un diseño distintivo (borde punteado ámbar, insignia de "Posición Vacante" y avatar de convocatoria).
2. **Si las personas le reportan a un cargo vacante:**
   En las columnas de la persona que reporta coloca:
   - `Nombre a Quien Reporta`: **`Vacante`**
   - `Cargo a quien reporta`: Nombre del cargo vacante (ej. `Gerente de Operaciones & Supply Chain`)
   - **El sistema asocia automáticamente la persona con el cargo y el área correspondiente**, asegurando que la jerarquía esté 100% completa y ningún colaborador quede huérfano ni descolocado.
3. **Cargos vacantes implícitos:**
   Si ni siquiera existe la fila del cargo en el Excel pero varios colaboradores indican que le reportan a ese cargo vacante, el sistema genera la casilla vacante automáticamente para que todo el equipo quede agrupado bajo su jefatura correspondiente.

---

## 🖼️ Personalización del Logo de la Empresa

En la parte superior izquierda de la aplicación:
1. Deja tu archivo de logo en la carpeta raíz del proyecto con el nombre:
   - `logo.png` (o también compatible con `logo.svg`, `logo.jpg`, `logo.webp`).
2. ¡Listo! La aplicación lo detectará y mostrará automáticamente con alta resolución tanto en la barra superior como en la exportación a presentación PDF 16:9.
3. Si lo deseas, también puedes hacer clic sobre el logo en la aplicación para cargar un logo nuevo desde tu navegador.

---

## 🔍 Comportamiento de Zoom y Colapso Inicial

1. **Estado Inicial Contraído a Escala 100%:**
   - Al cargar la aplicación o subir un archivo, el organigrama **inicia contraído** (muestra al líder principal/CEO y sus líderes de primer nivel con los contadores de colaboradores a cargo `+N`).
   - El zoom arranca fijado exactamente al **100%** (`1.0x`) centrado en el líder superior.
2. **Modo de Zoom al Colapsar / Expandir:**
   - En el dock flotante inferior derecho dispones de:
     - Botón **`100%`**: Regresa inmediatamente a la escala 1:1 centrada.
     - Botón **`Auto-Ajustar / Manual`**: Te permite alternar entre que la vista se adapte automáticamente al expandir equipos grandes o se mantenga en escala manual según tu preferencia.
     - Botones **`Colapsar Todo`** y **`Expandir Todo`** en la barra de métricas.

---

## 🛠️ Ejecución Local

Para probar localmente en tu equipo:
- Simplemente abre el archivo `index.html` en tu navegador favorito (Chrome, Edge, Firefox, Safari).
- O si prefieres con un servidor local:
  ```bash
  npm start
  # Abre http://localhost:3000
  ```

---
*Desarrollado con arquitectura moderna Vanilla CSS (Neumorfismo + Glassmorfismo), D3.js v7, SheetJS y html2canvas/jsPDF.*
