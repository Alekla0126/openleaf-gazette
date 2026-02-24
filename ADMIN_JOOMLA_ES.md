# OpenLeaf Gazette - Guia de uso en Joomla Admin

## 1) Instalar plugin

1. Entra a `Joomla Administrator`.
2. Ve a `System -> Install -> Extensions`.
3. Sube el ZIP del plugin.
4. Ve a `System -> Manage -> Plugins` y habilita `Content - OpenLeaf Gazette`.

## 2) Configurar PDF desde el panel Admin

1. Abre el plugin `Content - OpenLeaf Gazette`.
2. Ajusta estos campos:
   - `Modo por defecto`: `Native`
   - `PDF por defecto (desde Admin)`: selecciona tu PDF en Media Manager
   - `Modo visual por defecto (native)`: `Screen`
   - `Intentar fullscreen automaticamente`: `No`
   - `Mostrar boton descargar (native)`: `Si`
3. Guarda.

Con esto, el shortcode minimo funciona sin poner ruta del PDF:

```text
{openleaf}
```

## 3) Donde usarlo

- Articulo (`com_content`): pega `{openleaf}` en el texto del articulo.
- Modulo `Custom` en posicion de plantilla:
  1. Crea/edita modulo tipo `Custom`.
  2. Pega `{openleaf}`.
  3. Activa `Prepare Content = Yes`.
- Componente propio:
  - Ejecuta `onContentPrepare` sobre el texto antes de renderizar la vista.

## 4) Ejemplo con parametros manuales

```text
{openleaf mode="native" file="images/pdfs/ucips-gazette-base3f-27012026-prueba.pdf" fit="screen" autofullscreen="0" download="1"}
```
