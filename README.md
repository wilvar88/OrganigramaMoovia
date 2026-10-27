# 🏢 Organigrama Dinámico Moovia | Executive Suite v2.1

Visualizador interactivo de organigrama corporativo de alta fidelidad para **Moovia**, diseñado con arquitectura moderna Vanilla CSS (Neumorfismo + Glassmorfismo), D3.js v7, SheetJS, soporte de posiciones vacantes, auto-guardado en JSON, auto-zoom por grupo y barra de herramientas colapsable. Optimizado para despliegue en **GitHub** y **Vercel**.

Repositorio oficial: [https://github.com/wilvar88/OrganigramaMoovia.git](https://github.com/wilvar88/OrganigramaMoovia.git)

---

## ✨ Novedades y Características Principales

1. **Auto-Guardado Automático en JSON al subir Excel**:
   - Al hacer clic en **"Subir Excel"** y seleccionar un archivo `.xlsx`, el sistema procesa toda la jerarquía y **guarda automáticamente el archivo `data/organigrama.json`** en el proyecto (cuando se ejecuta con el servidor local Node.js `npm start`).
   - Además, cuenta con guardado instantáneo en la memoria del navegador (`localStorage`) y descarga automática como respaldo si se abre como archivo estático.
   
2. **Auto-Zoom Inteligente por Grupo al Expandir (`+`)**:
   - Al pulsar el botón `+` para desplegar cualquier grupo o jefatura, la vista realiza una suave transición cinemática que **centra el grupo y ajusta el zoom al tamaño máximo posible** para que todos los colaboradores del equipo recién abierto sean visibles en el recuadro de la pantalla.
   - Al colapsar, se re-centra suavemente sobre el líder del equipo.

3. **Zona de Menú Colapsable (Recupera +25% de Espacio)**:
   - Botón **"▲ Ocultar Menú"** en la barra superior y pestaña flotante **"▼ Mostrar Menú"**.
   - Oculta el encabezado y barra de botones para maximizar la superficie visual del organigrama.
   - Atajo de teclado rápido: Presiona la tecla **`M`** para ocultar/mostrar el menú al instante.
   - Recuerda tu preferencia automáticamente en tu navegador.

4. **Gestión Inteligente de Vacantes y Renuncias (10 Columnas)**:
   - Identifica colaboradores con cargo `Vacante`.
   - Si un líder renunció o está vacante, vincula a los colaboradores a través de las columnas `"Nombre a Quien Reporta"` y `"Cargo a quien reporta"`.
   - Crea automáticamente la relación jerárquica con el cargo y el área correspondiente para evitar cargos huérfanos.

5. **Identidad Visual Moovia**:
   - Logo oficial de Moovia integrado en la esquina superior izquierda (`logo.png`).
   - Modo de exportación a presentación ejecutiva en formato 16:9 con alta resolución.

---

## 🚀 Despliegue Rápido en Vercel (Paso a Paso)

Este proyecto está optimizado como aplicación web estática de alto rendimiento para desplegarse en segundos en **Vercel**:

### Opción A: Despliegue con 1 Clic desde GitHub (Recomendado)
1. Ve a tu cuenta en [vercel.com](https://vercel.com) e inicia sesión (con tu cuenta de GitHub).
2. Haz clic en el botón **"Add New..."** -> **"Project"**.
3. En la lista de repositorios, selecciona **`OrganigramaMoovia`** (o importa `https://github.com/wilvar88/OrganigramaMoovia.git`).
4. Vercel detectará automáticamente la configuración (`vercel.json` y `package.json`). **No necesitas configurar comandos de build ni variables de entorno.**
5. Haz clic en **"Deploy"**.
6. ¡Listo! En menos de 20 segundos tendrás un enlace público HTTPS (ej. `https://organigrama-moovia.vercel.app`) con certificado SSL activo y CDN global. Cada vez que hagas `git push` a `main`, Vercel actualizará tu organigrama automáticamente.

### Opción B: Despliegue mediante Vercel CLI
Si prefieres usar la consola:
```bash
# Iniciar sesión en Vercel
vercel login

# Desplegar a producción
vercel --prod
```

---

## 💻 Comandos Git para Sincronizar con GitHub

Para subir tus últimos cambios a GitHub:

```bash
# 1. Verificar estado
git status

# 2. Agregar todos los archivos
git add .

# 3. Crear commit con las novedades
git commit -m "feat: auto-zoom grupos, menu colapsable, auto-guardado json y soporte moovia"

# 4. Asegurar rama main
git branch -M main

# 5. Enviar a GitHub
git push -u origin main
```

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

## 🛠️ Ejecución Local

Para probar localmente en tu equipo:
- **Modo Servidor Local (Recomendado)**:
  ```bash
  npm start
  # Abre http://localhost:3000
  ```
  Permite auto-guardado directo en disco del archivo `data/organigrama.json` al subir Excel.
- **Modo Navegador Directo**:
  Abre directamente `index.html` en Chrome, Edge o Firefox con doble clic.

---
*Desarrollado para Moovia con arquitectura moderna Vanilla CSS (Neumorfismo + Glassmorfismo), D3.js v7, SheetJS y html2canvas/jsPDF.*
