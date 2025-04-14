# Despliegue de la Aplicación PokeDex en Microsoft Azure

Este documento explica paso a paso cómo se realizó el despliegue de la aplicación **PokeDex** utilizando los servicios de **Azure for Students**. El objetivo fue publicar la aplicación en la nube para que sea accesible públicamente y cumpla con los requisitos del caso de estudio.

---

## Requisitos Previos

Antes del despliegue, se contó con lo siguiente:

- Cuenta activa de **Azure for Students**.
- Código fuente de la aplicación PokeDex obtenido desde GitHub:  
  👉 [https://github.com/rcuello/ac4dem1a/tree/master/sistemas-distribuidos/poke-dex-lab](https://github.com/rcuello/ac4dem1a/tree/master/sistemas-distribuidos/poke-dex-lab)
- Cuenta de GitHub con un repositorio llamado `pokedex`.

---

## 1. Preparación del Proyecto

### 📁 Estructura del proyecto

Se descargó el código fuente de PokeDex y se organizó adecuadamente en el repositorio personal de GitHub.  
Se verificó que los archivos principales estuvieran en la raíz del proyecto (`index.html`, `main.js`, `styles.css`, etc.)

> 📌 Si la aplicación está basada solo en HTML/CSS/JS (sin backend), se recomienda usar **Static Web Apps** de Azure.

---

## 2. Acceso al Portal de Azure

Se ingresó al portal de administración:  
👉 [https://portal.azure.com](https://portal.azure.com)

![enter image description here](https://learn.microsoft.com/es-es/azure/devtest/offer/media/how-to-change-directory-tenants-visual-studio-azure/identity.png)
---

## 3. Creación del Recurso: Static Web App

### 🔧 Pasos:

1. Se buscó el recurso ****Azure App Service**** en el buscador de Azure.
2. Se hizo clic en **Crear**.
3. Se llenaron los siguientes datos:
   - **Nombre del recurso**: `pokedex-static-app`
   - **Región**: La más cercana geográficamente.
   - **Plan de tarifa**: Free (Gratuito)
   - **Origen del código**: GitHub
   - **Repositorio y rama**: Se seleccionó el repositorio `pokedex` y rama `main`.

![enter image description here](https://miro.medium.com/v2/resize:fit:1400/1*vN0cUicKr8UCfcqkhQVEcQ.png)

---

## 4. Configuración del flujo de despliegue

Azure generó automáticamente un **workflow de GitHub Actions**, que se agregó al repositorio en la carpeta `.github/workflows`.

> 📌 Este archivo se encarga de desplegar automáticamente la aplicación cada vez que se suben cambios a GitHub.

![enter image description here](https://nelson.cloud/how-to-enable-manual-runs-of-github-actions-workflows/manual-run-enabled.webp)

---

## 5. Verificación del Despliegue

Después de unos minutos, Azure desplegó automáticamente la app. Se accedió a la URL proporcionada por Azure:

👉 `https://pokedex-static-app.azurestaticapps.net` *(Ejemplo: la URL exacta depende del nombre que elegiste)*

Se verificó que la aplicación cargue correctamente y sin errores.



---

## 6. Escaneo de Seguridad

Una vez desplegada la app, se realizó un análisis de seguridad usando:

👉 [https://securityheaders.com](https://securityheaders.com)

### Resultado:
- Se obtuvo una calificación de seguridad de: `_____` *(completa según tu caso)*
- Se analizó qué encabezados faltaban y se consideraron mejoras.

![enter image description here](https://dotrungquan.info/wp-content/uploads/2024/04/CleanShot-2024-04-05-at-10.18.51-1024x458.png?v=1712287152)

---

## 7. Mejoras de Seguridad (si aplica)

Se añadieron encabezados de seguridad mediante metaetiquetas en el archivo `index.html` como:

```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self';">
<meta http-equiv="X-Frame-Options" content="DENY">
<meta http-equiv="X-Content-Type-Options" content="nosniff">
