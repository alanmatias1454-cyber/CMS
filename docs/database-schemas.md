# Diagrama de relaciones de la base de datos

El proyecto utiliza **Firebase Firestore** para almacenar la información de los usuarios autenticados.

```mermaid
erDiagram
    USUARIOS {
        string uid PK
        string nombre
        boolean activo
    }