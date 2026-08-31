# 🍗 Analista Pechuga

**Aplicación PWA para control de mermas de pechuga de pollo — Planta DOLZ**

Analiza visualmente las mermas producidas al limpiar recortes de pechugas de pollo y estima qué porcentaje corresponde a carne de pechuga recortada en exceso vs. grasa/cartílago (recorte correcto).

---

## ¿Cómo funciona?

La app analiza pixel a pixel la imagen en espacio de color HSL y clasifica cada punto como:

| Clasificación | Color en segmentación | Descripción |
|---|---|---|
| **Pechuga (merma)** | 🔴 Rojo | Tono rosa-salmón, saturación moderada |
| **Grasa / recorte OK** | 🔵 Azul | Blanco-crema, baja saturación |
| **Fondo (excluido)** | ⬛ Atenuado | Caja amarilla DOLZ, bolsa roja |

**% Pechuga = nPixelesPechuga / (nPixelesPechuga + nPixelesGrasa) × 100**

> El análisis es 100% local en el dispositivo. No se envían datos a ningún servidor.

---

## Instalación en móvil

### Android
1. Abre la URL en Chrome
2. Aparece un banner «Instalar app» → pulsa **Instalar**
3. La app se añade a la pantalla de inicio

### iOS (Safari)
1. Abre la URL en Safari
2. Pulsa el botón **Compartir** (cuadrado con flecha)
3. Selecciona **Añadir a pantalla de inicio**

---

## Despliegue en GitHub Pages

1. Crea un repositorio en GitHub (ej: `analista-pechuga`)
2. Sube **todo el contenido** de esta carpeta (no la carpeta en sí)
3. Ve a **Settings → Pages → Source: Deploy from branch → main / root**
4. La app estará en: `https://<usuario>.github.io/analista-pechuga/`

> ⚠️ Tras subir a GitHub Pages, la URL base cambia. Verifica que el service worker se registra correctamente (Chrome DevTools → Application → Service Workers).

---

## Notas de uso en planta

- Fotografiar **con buena iluminación** (luz blanca uniforme)
- Enfocar la caja desde **arriba, perpendicular** a la superficie
- La caja debe estar **razonablemente llena** — si hay mucha bolsa roja visible, la cobertura del análisis será baja
- El indicador **"Cobertura análisis"** indica qué % de la imagen pudo clasificarse; por debajo del 12% aparece aviso

---

## Historial

Los análisis se guardan localmente en el navegador (localStorage).  
Máximo 30 entradas. Se pueden borrar desde la propia app.

---

## Versiones

| Versión | Fecha | Cambios |
|---|---|---|
| **v1.0** | 2026-08-31 | Primera versión — análisis HSL, segmentación visual, historial local |

---

## Stack técnico

- HTML + CSS + JS puro (sin frameworks)
- Canvas API para procesamiento de imagen
- Service Worker para uso offline
- localStorage para historial

Calibrado específicamente para el entorno DOLZ:  
caja amarilla + bolsa roja/naranja + merma de pechuga de pollo bajo iluminación industrial.
