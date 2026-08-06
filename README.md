# driver-finance-releases

Canal de actualización de **DriverFinance**, una app de administración financiera para conductores
de plataformas. El código vive en otro repositorio, privado; aquí sólo está lo que la app necesita
poder descargar sin autenticarse.

## Qué hay aquí

- **`update.json`** — el manifiesto de versiones. La app lo lee al arrancar, compara el `versionCode`
  con el que tiene instalado y, si el de aquí es mayor, ofrece actualizar.
- **Las *releases*** — el APK de cada versión, adjunto a la etiqueta que le corresponde.

## Por qué es público

La app pide el manifiesto y el APK sin ninguna credencial: no tiene ninguna que ofrecer, y no debe
tenerla. En un repositorio privado GitHub le respondería 404 a las dos peticiones y el aviso de
actualización no aparecería nunca.

Nada de lo que hay aquí es secreto. El APK se le entrega igual a cualquiera que instale la app, y su
integridad no depende de que la URL sea difícil de encontrar: el manifiesto publica la huella SHA-256
y la app rechaza el archivo si no coincide.

## Publicar una versión

En este orden, que importa: primero se sube el APK y al final el manifiesto, para que nunca exista un
`update.json` que anuncie una descarga que todavía no está.

1. Compilar el APK firmado con la clave de siempre.
2. Crear la *release* con etiqueta `v<versionName>` y adjuntar el APK.
3. Comprobar que el APK se descarga sin sesión iniciada.
4. Actualizar `update.json` con `versionCode`, `versionName`, la URL del adjunto, el tamaño en bytes
   y la huella SHA-256, y hacer commit.

El `versionCode` nunca se reutiliza. GitHub sirve el contenido crudo con unos minutos de caché, así
que una versión recién publicada puede tardar ese rato en verse desde el teléfono.
