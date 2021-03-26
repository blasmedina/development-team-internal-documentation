# Codificación

El desarrollo de software, contempla muchas etapas de las cuales aca no se profundizara en 100%, pero si, se planteara algunas de las BUENAS PRACTICAS que adoptado como equipo de desarrollo.

## Reglas de desarrollo

### Estructura de carpeta y archivos

Se sugiere que el código fuente del proyecto este dentro de la carpeta `scr`. Ademas que nombre de los archivos deben estar `lowerCamelCase`.

### Base de datos

- Tanto las **tablas** como los **atributos** se definen en ingles.
- Las **tablas** se definen en `UpperCamelCase` y en plural. _Ejemplo:_ `Roles`.
- Los **id** son de tipo `UUID`, específicamente `UUIDV4`. _Ejemplo:_ `41559151-e4b7-4c1d-929a-012a4af797c5`.
- Los **atributos** se definen `lowerCamelCase`. _Ejemplo:_ `name`.
- Las **claves foráneas** (Foreign key) se definen en `UpperCamelCase` ocupando el siguiente formato `{NombreEntidadEnSingular}Id`. _Ejemplo:_ `RoleId`.

### JavaScript

- Las **variables** se definen en `lowerCamelCase` y en ingles.

### Commit

Para mejorar la identificación de los commit se sugiere utilizar [GitMoji](https://gitmoji.carloscuesta.me/), lo que también nos lleva a sugerir [Commit Atómico](https://es.wikipedia.org/wiki/Commit_at%C3%B3mico).

### Formato de código

A la hora de codificar y respaldar tu código con alguna herramienta de control de versiones, mantener un estándar de formateado de código es primordial. Por se se sugiere utilizar la herramienta `Prettier`, el cual es clave dejar su configuración dentro del mismo proyecto. Para esto se crea un archivo en la raíz de proyecto con el nombre `.prettierrc` con el siguiente contenido.

```json
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 120,
  "tabWidth": 2
}
```

Si ya cuentas con un código fuente no formateado, se deja el siguiente comando para aplicar el formateado de código luego de crear el archivo de configuración `.prettierrc` en la raíz de proyecto.

```sh
npx prettier --write .
```

> Si tu IDE es Visual Studio Code, se aconseja instalar la extension de prettier. https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode

### DRY: Dont repeat yourself

No repitas código, modulariza tus desarrollos. Repetir partes de código a lo largo de un desarrollo solo sirve para dificultar el mantenimiento y aumentar la probabilidad de cometer errores. Agrupa en funciones las operaciones que se repitan, y aíslala del resto del código, el esfuerzo necesario para el mantenimiento del código disminuirá. Si estos trozos de código son requeridos por otros ficheros, no solo elimínalos del flujo natural, si no que colócalo en un fichero aparte y accesible por todos los elementos del código.

### No inventes

Si ya se disponen de módulos y librerías ya testeadas y optimizadas, no pierdas el tiempo en un desarrollo. Los IDE actuales disponen de librerías que te ayudarán en tus desarrollos.

### Comenta tu código

Para facilitar el entendimiento de las ideas que se codifican, te sugerimos comentar tu código.

> Si tu IDE es Visual Studio Code, te dejamos aca una extension te que puede ayudar. https://marketplace.visualstudio.com/items?itemName=cschlosser.doxdocgen

### Divide y vencerás

Divide los desarrollos complejos en varios más sencillos. Enrocarse en buscar una solución que abarque todas las posibilidades o funcionalidades te va a hacer perder mucho el tiempo. Divide el desarrollo en funcionalidades y prográmarlas atendiendo a su función principal y a la integración con el resto.

### Optimización

No todas las instrucciones y módulos necesitan la misma capacidad de procesamiento intenta utilizar siempre las más sencillas.

### Seguridad

Durante el desarrollo de nuestro software tenemos que tener en cuenta los siguientes puntos:

- El acceso a los ficheros (tanto de forma física, como permisos).
- La posibilidad de modificar el código en la misma ejecución o la inyección sql.
- Desbordamiento de buffer al hacer uso de un array sin tamaño controlado.
- Formateo de los datos de entrada (en formularios).
- Actualización del IDE y las funciones. Una función obsoleta puede originar un agujero de seguridad en nuestro código.
- Uso de contraseñas en el código. Las contraseñas deben estar cifradas y en la base de datos.

### Monitoreo de cambios

Nodemon es una utilidad que monitorea los cambios en el código fuente que se esta desarrollando y automáticamente re inicia el servidor. Es una herramienta muy útil para desarrollo de aplicaciones en nodojs.

Comando para instalar

```bash
npm install --save-dev nodemon
```

Para la configuración, se debe crear un archivo en la raíz con el nombre `nodemon.json` y con el siguiente contenido.

```json
{
  "ignore": [".git", "node_modules/**/*"],
  "watch": ["bin/**/*", "src/**/"],
  "env": {
    "NODE_ENV": "development",
    "DEBUG": "*,-express:router:*,-express:application,-morgan,-sequelize:connection:*"
  },
  "exec": "npm run start",
  "ext": "js,json"
}
```

Para la integración, debes agregar el siguiente script dentro del `package.json` del proyecto:

```json
{
  "scripts": {
    "dev": "nodemon"
  }
}
```
