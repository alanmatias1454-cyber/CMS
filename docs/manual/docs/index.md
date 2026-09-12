# CMS - Manual de Instalación y Uso

## 1. Introducción

CMS es un proyecto web orientado a servicios audiovisuales, marketing digital y desarrollo web.

El proyecto presenta diferentes secciones para mostrar información, servicios, trabajos realizados y formas de contacto.

Además, incorpora un sistema de autenticación mediante Google y una base de datos utilizando Firebase Firestore para gestionar la información de los usuarios.

El proyecto utiliza principalmente:

- HTML
- CSS
- JavaScript
- Firebase Authentication
- Firebase Firestore
- MkDocs para la documentación

---

## 2. Requisitos

Para utilizar o modificar el proyecto se necesita:

- Windows, macOS o Linux.
- Un navegador web actualizado.
- Git.
- Visual Studio Code u otro editor de código.
- Python.
- MkDocs.
- Una cuenta de Google para probar la autenticación.
- Un proyecto configurado en Firebase.

---

## 3. Instalación

### 3.1. Clonar el repositorio

El proyecto se encuentra almacenado en un repositorio de Git.

Para descargarlo, abrir PowerShell o una terminal y ejecutar:

```bash
git clone https://github.com/alanmatias1454-cyber/CMS.git
```

Luego ingresar a la carpeta del proyecto:

```bash
cd CMS
```

---

## 4. Estructura del proyecto

La estructura principal del proyecto contiene los archivos necesarios para el funcionamiento de la página y su documentación.

Una estructura simplificada es:

```text
CMS/
├── index.html
├── docs/
│   ├── manual/
│   │   ├── docs/
│   │   │   ├── index.md
│   │   │   └── stylesheets/
│   │   │       └── extra.css
│   │   └── mkdocs.yml
│   └── database-schemas.md
├── 0627.mp4
├── 0704 (1).mp4
└── pagina video.mp4
```

El archivo `index.html` contiene la página principal del proyecto.

La carpeta `docs/manual/` contiene el manual de instalación y uso realizado con MkDocs.

---

## 5. Ejecución del proyecto web

El proyecto puede ejecutarse utilizando un servidor local.

Una vez descargado el repositorio, se puede abrir el archivo:

```text
index.html
```

desde un navegador.

El proyecto también utiliza Firebase para determinadas funciones, por lo que es necesario contar con la configuración correspondiente dentro del código.

---

## 6. Configuración de Firebase

El proyecto utiliza Firebase para implementar la autenticación y la base de datos.

Dentro del código JavaScript se inicializa Firebase utilizando una configuración del proyecto:

```javascript
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);
```

También se configura el proveedor de autenticación de Google:

```javascript
const provider = new GoogleAuthProvider();
```

Estos elementos permiten conectar la página con Firebase Authentication y Firebase Firestore.

---

## 7. Inicio de sesión con Google

El proyecto permite iniciar sesión mediante una cuenta de Google.

Para utilizar esta función:

1. Abrir la página principal.
2. Ir a la sección **Contacto**.
3. Presionar **Iniciar sesión con Google**.
4. Seleccionar una cuenta de Google.
5. Autorizar el acceso si es solicitado.

Una vez realizada la autenticación, Firebase proporciona la información del usuario autenticado.

La aplicación utiliza:

```javascript
auth.currentUser
```

para obtener el usuario que inició sesión.

---

## 8. Gestión de usuarios

El proyecto incorpora funciones para gestionar el usuario autenticado.

En la sección **Contacto** se encuentran las siguientes opciones:

- Iniciar sesión con Google.
- Modificar usuario.
- Dar de baja.

### 8.1. Modificar usuario

La función de modificación permite cambiar el nombre almacenado para el usuario autenticado.

La información se actualiza en Firestore mediante:

```javascript
updateDoc(doc(db, "usuarios", usuario.uid), {
    nombre: nuevoNombre
});
```

Después de realizar la operación, se informa al usuario que la modificación se realizó correctamente.

### 8.2. Dar de baja

La opción **Dar de baja** permite desactivar al usuario.

La aplicación actualiza el campo `activo` del documento correspondiente:

```javascript
updateDoc(doc(db, "usuarios", usuario.uid), {
    activo: false
});
```

De esta manera, el usuario queda marcado como inactivo dentro de la base de datos.

---

## 9. Base de datos

El proyecto utiliza **Firebase Firestore** como base de datos.

La información de los usuarios se almacena en la colección:

```text
usuarios
```

Cada documento utiliza el `uid` del usuario autenticado como identificador.

Los datos utilizados incluyen:

| Campo | Descripción |
|---|---|
| `uid` | Identificador único del usuario |
| `nombre` | Nombre del usuario |
| `activo` | Estado del usuario |

El diagrama de relaciones de la base de datos se encuentra en:

```text
docs/database-schemas.md
```

---

## 10. Documentación con MkDocs

El manual del proyecto fue desarrollado utilizando **MkDocs** y el tema **Material**.

La configuración se encuentra en:

```text
docs/manual/mkdocs.yml
```

El archivo configura el nombre del sitio, el tema y la hoja de estilos adicional.

La hoja de estilos personalizada se encuentra en:

```text
docs/manual/docs/stylesheets/extra.css
```

---

## 11. Ejecutar el manual

Para ejecutar la documentación localmente, ubicarse en la carpeta raíz del proyecto:

```powershell
cd C:\Users\alvar\OneDrive\Desktop\CMS
```

Luego ejecutar:

```powershell
py -m mkdocs serve -f docs/manual/mkdocs.yml
```

MkDocs iniciará un servidor local.

El manual estará disponible en:

```text
http://127.0.0.1:8000/
```

La terminal debe permanecer abierta mientras se utiliza el servidor.

---

## 12. Modificar la documentación

Para modificar el contenido del manual se debe editar:

```text
docs/manual/docs/index.md
```

Después de guardar los cambios con:

```text
Ctrl + S
```

MkDocs detectará los cambios y volverá a generar la documentación automáticamente.

Si el navegador no actualiza los cambios, se puede utilizar:

```text
Ctrl + F5
```

---

## 13. Modificar los estilos

Los estilos personalizados del manual se encuentran en:

```text
docs/manual/docs/stylesheets/extra.css
```

En este archivo se pueden modificar aspectos como:

- Colores.
- Tipografías.
- Fondos.
- Espaciado.
- Tamaños de texto.
- Estilos de botones.
- Diseño responsive.

El proyecto utiliza una apariencia principalmente oscura para mantener una estética consistente con la página principal.

---

## 14. Solución de problemas

### 14.1. MkDocs no reconoce el comando

Si PowerShell muestra que `mkdocs` no se reconoce como comando, utilizar:

```powershell
py -m mkdocs serve -f docs/manual/mkdocs.yml
```

### 14.2. Error indicando que no existe `mkdocs.yml`

Verificar que la ruta utilizada sea:

```text
docs/manual/mkdocs.yml
```

El comando completo es:

```powershell
py -m mkdocs serve -f docs/manual/mkdocs.yml
```

### 14.3. Los cambios de CSS no aparecen

Comprobar que el archivo se encuentre en:

```text
docs/manual/docs/stylesheets/extra.css
```

y que `mkdocs.yml` contenga:

```yaml
extra_css:
  - stylesheets/extra.css
```

Luego guardar los cambios y actualizar el navegador con:

```text
Ctrl + F5
```

### 14.4. No funciona el inicio de sesión con Google

Verificar que:

- Firebase Authentication esté habilitado.
- El proveedor Google esté habilitado.
- El dominio utilizado para realizar las pruebas esté autorizado en Firebase.
- La configuración de Firebase utilizada por el proyecto sea correcta.

---

