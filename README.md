# OpenLeaf Gazette

Open-source Joomla 5 content plugin for the UCIPS digital gazette.

## Features

- `embed` mode: uses external flipbook URLs (closest match to FlipHTML5 style).
- `native` mode: self-hosted PDF flipbook rendering with `pdf.js + StPageFlip`.
- Admin-first workflow: choose a default PDF in plugin settings and render with `{openleaf}`.
- Shortcodes supported:
  - `{gacetaflip ...}`
  - `{gacetaflipbook ...}`
  - `{openleaf ...}`
  - `{openleaf}`

## Installation

1. Joomla Administrator -> `System -> Install -> Extensions`.
2. Upload the plugin zip.
3. Enable `Content - OpenLeaf Gazette`.

## CI/CD ZIP publishing

- GitHub Actions workflow: `.github/workflows/cicd.yml`
- On every push/PR, CI builds the Joomla installable ZIP and uploads it as an artifact.
- On tags like `v1.1.0`, CD also uploads the ZIP file to the GitHub Release.
- Local build command:

```bash
./scripts/build-zip.sh
```

## Usage

### Option A: Joomla Admin (recommended)

1. Go to `System -> Manage -> Plugins`.
2. Open `Content - OpenLeaf Gazette`.
3. Set:
   - `Modo por defecto = Native`
   - `PDF por defecto (desde Admin) =` your file from Media Manager
   - `Modo visual por defecto (native) = Screen`
   - `Intentar fullscreen automaticamente = No`
   - `Mostrar boton descargar (native) = No`
4. Save.
5. In your article, module, or component text use:

```text
{openleaf}
```

### Option B: shortcode with explicit params

Embed mode:

```text
{openleaf mode="embed" url="https://online.fliphtml5.com/HmoralesZ/HCJ-gaceta-piloto-01/#p=26"}
```

Native mode:

```text
{openleaf mode="native" file="images/pdfs/ucips-gazette-base3f-27012026-prueba.pdf" start="1" maxpages="0" fit="screen" autofullscreen="0" download="0"}
```

### Template/module/component integration

- Article (`com_content`): place `{openleaf}` in the article body.
- Custom module in template position:
  - Create a `Custom` module.
  - Put `{openleaf}` in module content.
  - Enable module option `Prepare Content = Yes`.
- Custom component:
  - Trigger the content plugin event (`onContentPrepare`) on your text field before rendering.
  - Output the transformed text so `{openleaf}` is replaced by the viewer HTML.

## License

MIT
