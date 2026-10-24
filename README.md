# Bravo API - Colección de Postman y Documentación

Colección documentada y modular de peticiones HTTP (Postman) creada exclusivamente para fines didácticos, de investigación técnica y aprendizaje sobre el consumo e integración de servicios REST.

---

> [!WARNING]
> ### ⚠️ Descargo de Responsabilidad (Aviso Legal)
>
> **Este proyecto ha sido desarrollado exclusivamente con propósitos educativos y de análisis técnico.**
>
> - **Propiedad Intelectual:** La especificación técnica (spec), colecciones, estructura de endpoints, peticiones (requests), nombres de parámetros y todo lo relacionado con la API son **propiedad intelectual exclusiva de Provisiones Bravo / Grupo Bravo**. Este proyecto no reclama ningún derecho, autoría ni titularidad sobre dicha arquitectura.
> - **Sin Asociación Comercial:** Este proyecto es completamente independiente y **no está asociado, vinculado, respaldado, patrocinado ni afiliado de ninguna manera con Provisiones Bravo / Grupo Bravo / Supermercados Bravo**, ni con ninguna de sus empresas matrices, filiales o subsidiarias.
> - **Marcas y Referencias:** Los nombres comerciales, marcas registradas y logotipos pertenecen exclusivamente a sus respectivos titulares. Su uso es puramente descriptivo, técnico y con fines de compatibilidad educativa (*fair use*).
> - **Prohibición de Mal Uso:** Se prohíbe terminantemente el uso de esta información o de sus archivos para realizar actividades maliciosas, ataques a sistemas, sobrecarga de servidores, extracción masiva abusiva de datos (*scraping*), suplantación de identidad o cualquier actividad que contravenga las leyes aplicables o los términos de servicio de terceros.
> - **Responsabilidad Exclusiva del Usuario:** El autor no se hace responsable por el uso inapropiado, descuidado o ilegal que terceras personas puedan hacer de este material. Cualquier uso corre bajo la entera responsabilidad del usuario final.
>
> 👉 Para consultar el texto legal completo, lea nuestro documento de [Descargo de Responsabilidad (DISCLAIMER.md)](DISCLAIMER.md).

---

## 📁 Estructura del Repositorio

El repositorio está organizado para permitir importar la suite completa o utilizar peticiones individuales según la necesidad:

```text
bravo-api/
├── bravo-api-collection.json           # Colección completa de Postman (v2.1.0)
├── requests/                           # Peticiones individuales parametrizadas
│   ├── public/                         # Endpoints públicos
│   │   ├── login.postman_collection.json
│   │   ├── list-articulos.postman_collection.json
│   │   ├── list-articulo-con-precio.postman_collection.json
│   │   ├── list-seccion.postman_collection.json
│   │   ├── get-photos.postman_collection.json
│   │   └── catalogos-images.postman_collection.json
│   └── private/                        # Endpoints que requieren sesión/token
│       ├── get-articulo-by-id.postman_collection.json
│       ├── get-cliente-direccion.postman_collection.json
│       ├── get-favoritos.postman_collection.json
│       ├── search-product.postman_collection.json
│       └── logout.postman_collection.json
├── DISCLAIMER.md                       # Aviso legal y descargo de responsabilidad detallado
├── LICENSE                             # Licencia del proyecto (GPL-2.0)
└── README.md                           # Documentación del proyecto
```

---

## 🚀 Endpoints Documentados

### 1. Módulo Público (`PUBLIC`)
Peticiones accesibles sin necesidad de cabeceras de autorización privadas:

- **`POST /public/auth/login`**: Inicia sesión mediante formulario (`codUsuario` y `claveUsuario`). Al autenticarse con éxito, el script de prueba de Postman asigna automáticamente el token de respuesta a la variable de entorno `X-Auth-Token`.
- **`GET /public/articulo/list`**: Obtiene el listado de productos disponibles con soporte de paginación y ordenamiento.
- **`GET /public/seccion/list`**: Lista las secciones y categorías de artículos disponibles.
- **`GET /public/articulo/searchSuggestions`**: Búsqueda asistida de productos mediante sugerencias.
- **Recursos Multimedia**: Direcciones URL estructuradas para obtener imágenes de catálogos y secciones.

### 2. Módulo Privado (`PRIVATE`)
Peticiones que requieren la cabecera `X-Auth-Token` (obtenida tras el login):

- **`GET /private/cliente/direccion/list`**: Lista las direcciones asociadas al usuario y zonas de entrega.
- **`GET /private/cliente/favorito/check`**: Verifica el estado de artículos marcados como favoritos.
- **`GET /public/articulo/get`**: Consulta el detalle específico de un artículo dado su ID.
- **`POST /private/auth/logout`**: Cierra la sesión activa invalidando el token.

---

## ⚙️ Configuración y Variables de Postman

La colección y los archivos individuales utilizan variables para evitar exponer credenciales o datos privados:

| Variable | Tipo | Valor Sugerido / Defecto | Descripción |
| :--- | :--- | :--- | :--- |
| `baseUrl` | URL | `https://bravova-api.superbravo.com.do` | Dominio base para las llamadas a la API REST. |
| `resourcesBaseUrl` | URL | `https://bravova-resources.superbravo.com.do` | Dominio del CDN para recursos estáticos e imágenes. |
| `User-Agent` | Cadena | `okhttp/4.12.0` | Cabecera User-Agent emulada para las peticiones. |
| `codUsuario` | Cadena | *(Tu cédula / usuario)* | Identificador para el inicio de sesión. |
| `claveUsuario` | Cadena (Secreta) | *(Tu contraseña)* | Contraseña de acceso a la cuenta. |
| `X-Auth-Token` | Cadena | *(Dinámico)* | Token de sesión generado automáticamente tras ejecutar `LOGIN`. |
| `idTienda` | Entero | `1008` | Identificador de la tienda física para consultar catálogo y stock. |
| `idSeccion` | Entero | `8` | Identificador de sección / categoría de productos. |
| `idArticulo` | Entero | `27775` | Identificador de artículo para consultas de detalle y favoritos. |
| `size` | Cadena | `300x300` | Resolución de imagen para solicitudes al CDN de fotos. |
| `idexternoArticulo` | Cadena | `000000` | Código externo / SKU del producto para obtener su foto. |
| `version_imagen` | Entero | `1` | Parámetro de versión para invalidar caché de imágenes. |

> [!TIP]
> Al ejecutar la petición `LOGIN`, el script de prueba asignará automáticamente el token a la variable `X-Auth-Token` tanto en las variables de colección como en el entorno activo, facilitando la ejecución inmediata de las peticiones privadas.

---

## 📥 Cómo Empezar

Sigue esta guía paso a paso para importar y probar la colección en tu entorno de Postman o por línea de comandos:

### 1. Clonar el Repositorio
```bash
git clone https://github.com/obeduri/bravo-api.git
cd bravo-api
```

### 2. Importar en Postman
1. Abre la aplicación de **Postman**.
2. Haz clic en el botón superior **Import** (o arrastra los archivos a la interfaz).
3. Selecciona tu método de trabajo:
   - **Colección Completa (Recomendado):** Importa el archivo `bravo-api-collection.json`. Tendrás acceso a todos los endpoints organizados en carpetas `PUBLIC` y `PRIVATE`.
   - **Peticiones Individuales:** Si solo requieres probar endpoints específicos, puedes importar cualquier archivo de la carpeta `requests/public/` o `requests/private/`.

### 3. Configurar tus Credenciales
1. Haz clic sobre la colección **BRAVO-API** importada en la barra lateral izquierda.
2. Ve a la pestaña **Variables**.
3. En la columna *Current Value* (Valor Actual), asigna tus credenciales:
   - `codUsuario`: Tu número de cédula o usuario.
   - `claveUsuario`: Tu contraseña personal (marca el campo como tipo *Secret* si deseas ocultar el texto).
4. Guarda los cambios (**Ctrl+S** o **Cmd+S**).

### 4. Flujo de Prueba Recomendado
1. **Iniciar Sesión:** Abre la petición `PUBLIC > LOGIN` y presiona **Send**.
   - Si las credenciales son válidas, recibirás una respuesta `200 OK`.
   - El script de prueba integrado asignará automáticamente el token retornado a la variable `X-Auth-Token`.
2. **Consultar Catálogo y Productos:**
   - Prueba `PUBLIC > LIST ARTICULOS` para listar productos disponibles en la tienda configurada (`idTienda=1008`).
   - Prueba `PUBLIC > SEARCH PRODUCT` cambiando el parámetro `model.nombreArticulo` (ej. `Arroz`, `Leche`).
3. **Probar Endpoints Privados:**
   - Abre `PRIVATE > GET CLIENTE DIRECCION` o `PRIVATE > GET FAVORITOS` y ejecuta **Send**.
   - No necesitas copiar ni pegar ningún token manualmente: la autenticación se gestiona de forma automática mediante la cabecera `X-Auth-Token`.
4. **Cerrar Sesión:**
   - Al terminar, ejecuta `PRIVATE > LOGOUT`. El servidor revocará el token y el script limpiará la variable de sesión.

---

### 💡 Ejecución desde la Terminal con Newman (Opcional)

Si prefieres ejecutar pruebas automatizadas por consola sin abrir Postman:

```bash
npx newman run bravo-api-collection.json \
  --env-var "codUsuario=TU_CEDULA" \
  --env-var "claveUsuario=TU_CLAVE" \
  --folder "PUBLIC"
```

---

## 📄 Licencia

Este repositorio se distribuye bajo los términos de la licencia [GNU General Public License v2.0](LICENSE).
