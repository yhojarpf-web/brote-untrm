# Guía: publicar la encuesta del Brote ETA – UNTRM

Tiene 3 archivos:

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La encuesta (lo que verán los participantes). Se sube a GitHub. |
| `Code.gs` | El código que guarda cada respuesta en su Hoja de cálculo de Google. **No** se sube a GitHub. |
| `GUIA.md` | Esta guía. |

Tiempo aproximado: 15–20 minutos.

---

## Parte 1 · Crear la hoja donde llegarán las respuestas

1. Entre a <https://sheets.google.com> con su cuenta de Google y cree una hoja en blanco. Póngale un nombre, por ejemplo **Respuestas Brote ETA UNTRM**.
2. En el menú, vaya a **Extensiones → Apps Script**. Se abrirá una pestaña nueva con un editor de código.
3. Borre todo lo que aparece en el editor (`function myFunction() {…}`).
4. Abra el archivo `Code.gs` (con el Bloc de notas sirve), copie **todo** su contenido y péguelo en el editor.
5. Presione el ícono de guardar 💾 (o Ctrl + S).

## Parte 2 · Publicar el script como aplicación web

1. Arriba a la derecha, pulse **Implementar → Nueva implementación**.
2. Junto a "Seleccionar tipo", pulse el engranaje ⚙️ y elija **Aplicación web**.
3. Complete así:
   - **Descripción:** Encuesta ETA
   - **Ejecutar como:** Yo (su correo)
   - **Quién tiene acceso:** **Cualquier usuario** ← importante, para que respondan sin iniciar sesión
4. Pulse **Implementar**.
5. Google pedirá **Autorizar acceso**. Elija su cuenta. Si aparece "Google no ha verificado esta aplicación", pulse **Configuración avanzada → Ir a (nombre del proyecto) (no seguro)** → **Permitir**. Es normal: la aplicación es suya.
6. Copie la **URL de la aplicación web**. Termina en `/exec`, por ejemplo:
   `https://script.google.com/macros/s/AKfycb…/exec`

> Para comprobar que funciona, pegue esa URL en el navegador: debe mostrar `{"ok":true,"mensaje":"El servicio de la encuesta está activo."}`

## Parte 3 · Conectar la encuesta con la hoja

1. Abra `index.html` con el Bloc de notas (clic derecho → Abrir con → Bloc de notas).
2. Busque (Ctrl + F) esta línea, cerca del inicio del código:
   ```
   const SCRIPT_URL = "";
   ```
3. Pegue su URL entre las comillas:
   ```
   const SCRIPT_URL = "https://script.google.com/macros/s/AKfycb…/exec";
   ```
4. Guarde el archivo.
5. **Prueba:** abra `index.html` con doble clic (se abre en su navegador), responda la encuesta y envíela. Revise que aparezca una fila nueva en la pestaña **Respuestas** de su hoja.

## Parte 4 · Subir la encuesta a GitHub Pages

1. Entre a <https://github.com> e inicie sesión (o cree una cuenta gratuita).
2. Pulse **+ → New repository**.
   - **Repository name:** por ejemplo `encuesta-eta-untrm`
   - Márquelo como **Public** (necesario para GitHub Pages gratuito; solo se publica el formulario, **las respuestas quedan privadas en su hoja de Google**).
   - Pulse **Create repository**.
3. En el repositorio nuevo, pulse **uploading an existing file** (o **Add file → Upload files**), arrastre **solo** `index.html` y pulse **Commit changes**.
4. Vaya a **Settings → Pages**. En **Branch**, elija **main** y la carpeta **/ (root)**, y pulse **Save**.
5. Espere 1–2 minutos y recargue la página. Arriba aparecerá su enlace:
   `https://SU-USUARIO.github.io/encuesta-eta-untrm/`

Ese es el enlace que envía a los participantes (puede acortarlo con bit.ly si quiere).

## Parte 5 · Descargar las respuestas en Excel

En su hoja de Google: **Archivo → Descargar → Microsoft Excel (.xlsx)**.

La hoja se actualiza sola con cada respuesta; descárguela cuando la necesite.

**Antes de enviar el enlace, borre las filas de prueba** de la pestaña Respuestas (deje la fila 1 de encabezados).

---

## Preguntas frecuentes

**¿Cómo cambio una pregunta o el menú?**
Edite `index.html` (o pídamelo) y vuelva a subirlo a GitHub con **Add file → Upload files**, reemplazando el anterior. El enlace no cambia.

**Modifiqué `Code.gs`, ¿qué hago?**
En Apps Script: **Implementar → Gestionar implementaciones → ✏️ Editar → Versión: Nueva versión → Implementar**. La URL se mantiene.

**¿Qué pasa si un participante pierde la conexión?**
La encuesta guarda el avance en su celular. Al volver a abrir el enlace, continúa donde se quedó, y puede presionar "Enviar" de nuevo.

**¿Y si alguien envía dos veces?**
Cada envío lleva un ID único; si el mismo envío llega dos veces, la hoja lo ignora. Si una persona llena la encuesta dos veces desde cero, use la columna **DNI o código** para detectar duplicados.

**¿Quién puede ver las respuestas?**
Solo quienes tengan acceso a su hoja de Google. El enlace de GitHub muestra únicamente el formulario.
