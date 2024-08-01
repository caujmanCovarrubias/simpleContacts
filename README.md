# SimpleContacts

SimpleContacts es una aplicación web simple para gestionar una agenda de contactos. Permite agregar, editar, eliminar y filtrar contactos de una manera fácil y organizada. 

## Características

- **Agregar Contacto**: Permite agregar un nuevo contacto con detalles como nombre, correo electrónico, dirección, teléfono, país y ciudad.
- **Editar Contacto**: Permite editar la información de un contacto existente.
- **Eliminar Contacto**: Permite eliminar un contacto de la lista.
- **Filtrar Contactos**: Permite filtrar contactos por nombre, correo electrónico o país.
- **Interfaz Responsiva**: La interfaz se adapta a diferentes tamaños de pantalla usando Bootstrap.

## Requisitos

- Node.js
- npm (Node Package Manager)
- json-server (para simular una API REST)

## Instalación

1. Clona el repositorio:

    ```bash
    git clone https://github.com/tu-usuario/simplecontacts.git
    cd simplecontacts
    ```

2. Instala las dependencias:

    ```bash
    npm install
    ```

3. Inicia json-server para servir la base de datos:

    ```bash
    json-server --watch db.json
    ```

4. Inicia la aplicación Vue:

    ```bash
    npm run serve
    ```

5. Abre tu navegador y navega a `http://localhost:8080`.

## Uso

### Agregar un Contacto

1. Haz clic en el botón "Agregar".
2. Completa los campos del formulario.
3. Haz clic en el botón "Guardar" para agregar el contacto.

### Editar un Contacto

1. Haz clic en el botón "Editar" junto al contacto que deseas editar.
2. Modifica los campos del formulario.
3. Haz clic en el botón "Guardar" para guardar los cambios.

### Eliminar un Contacto

1. Haz clic en el botón "Eliminar" junto al contacto que deseas eliminar.
2. Confirma la eliminación.

### Filtrar Contactos

1. Escribe en el campo de filtro para buscar contactos por nombre, correo electrónico o país.


