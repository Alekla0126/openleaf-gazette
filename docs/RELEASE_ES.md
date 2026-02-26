# OpenLeaf Gazette - Release y distribucion

## Objetivo

Publicar una version nueva del plugin con:
- ZIP instalable para Joomla.
- Artifact en GitHub Actions.
- Release de GitHub con el ZIP adjunto.

## Pre-requisitos

- Rama objetivo: `main`
- Workflow CI/CD activo en `.github/workflows/cicd.yml`
- Version actualizada en `gacetaflipbook.xml`

## Paso 1: actualizar version

En `gacetaflipbook.xml`:
- `<version>X.Y.Z</version>`
- (opcional) actualizar `creationDate`

## Paso 2: generar ZIP local

```bash
./scripts/build-zip.sh
```

Salida esperada:
- `dist/plg_content_openleaf_gazette-X.Y.Z.zip`

## Paso 3: validacion minima

```bash
/Applications/XAMPP/xamppfiles/bin/php -l gacetaflipbook.php
unzip -l dist/plg_content_openleaf_gazette-X.Y.Z.zip
```

## Paso 4: commit y push

```bash
git add gacetaflipbook.php gacetaflipbook.xml README.md ADMIN_JOOMLA_ES.md docs/
git commit -m "Add section-based PDF mapping and release docs"
git push origin main
```

## Paso 5: tag de distribucion

```bash
git tag vX.Y.Z
git push origin vX.Y.Z
```

## Paso 6: verificar distribucion en GitHub

En GitHub:
1. Actions -> workflow `CI-CD Plugin ZIP`.
2. Confirmar `Build Joomla Plugin ZIP` completado.
3. Releases -> `vX.Y.Z` con ZIP adjunto.

## Instalacion local recomendada (si falla subida web)

Si Joomla muestra `There was an error uploading this file to the server`, usar CLI:

```bash
/Applications/XAMPP/xamppfiles/bin/php \
  /Applications/XAMPP/xamppfiles/htdocs/lms/joomla/cli/joomla.php \
  extension:install --path "/ruta/al/plg_content_openleaf_gazette-X.Y.Z.zip"
```

## Capturas sugeridas para documentacion

- `docs/screenshots/01-admin-dashboard.png`
- `docs/screenshots/02-plugin-list-openleaf.png`
- `docs/screenshots/03-plugin-config-openleaf.png`
- `docs/screenshots/04-plugin-config-map-example.png`
