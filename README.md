# Configuración Básica de Template para una Aplicación de React con TypeScript y Webpack

¡Hola y bienvenido a mi repositorio!

En este gist, encontrarás la configuración básica de un template para crear una aplicación frontend utilizando React con TypeScript y Webpack.


## Utilidad

Este template te proporciona una estructura inicial para desarrollar aplicaciones React con TypeScript, aprovechando la potencia de Webpack para la gestión de módulos y la construcción del proyecto.

Con esta configuración básica, podrás:

-   Desarrollar componentes en React utilizando TypeScript para una mejor calidad de código.
-   Utilizar Webpack para empacar y optimizar tu aplicación.
-   Disfrutar de las ventajas de la tipificación estática proporcionada por TypeScript.
-   Configurar entornos de desarrollo y producción de manera eficiente.

Este template sirve como punto de partida para construir aplicaciones robustas y escalables con tecnologías modernas. ¡Espero que sea útil para tu desarrollo!


## ¿Porqué debería usar ***webpack***?
Webpack es una herramienta de construcción (bundler) para proyectos web que simplifica la gestión y optimización de recursos. Su utilidad radica en:

-   **Empaquetamiento de Módulos:** Webpack permite organizar y empacar módulos de JavaScript, CSS, y otros archivos, facilitando la modularidad en el desarrollo.

-   **Optimización de Recursos:** Combina y minimiza archivos, reduciendo el tamaño de los activos para mejorar la eficiencia de carga de la aplicación.

-   **Gestión de Dependencias:** Administra las dependencias del proyecto, lo que simplifica la inclusión de bibliotecas externas y mejora la coherencia del código.

-   **Desarrollo Eficiente:** Facilita el desarrollo proporcionando un servidor de desarrollo con recarga automática y herramientas como Hot Module Replacement (HMR) para una experiencia de desarrollo más ágil.


En resumen, Webpack es esencial para optimizar, organizar y mejorar el flujo de trabajo en proyectos web, brindando eficiencia y mejor rendimiento en la entrega de aplicaciones.


## Iniciar aplicación 
Para iniciar aplicación se debe instalar los módulos de node, con tu gestor de paquetes de elección, **recuerda que este proyecto usamos yarn si quieres usar npm asegurate de realizar los cambios pertinentes**,  siguiendo los pasos siguientes en una terminal escribe los siguiente: 
#
Crear archivo ***package.json*** con el siguiente comando:
 >#
 >**yarn init**
 >#
#
Instalación de dependencias necesarias para configurar proyecto:
>#
>**yarn add react react-dom**  
 >**yarn add -D typescript @types/react @types/react-dom**  
 >**yarn add -D @babel/core @babel/preset-env @babel/preset-react @babel/preset-typescript @babel/plugin-transform-runtime**  
 >**yarn add -D webpack webpack-cli webpack-dev-server html-webpack-plugin**  
 >**yarn add -D babel-loader**  
 >#
#
Configurar y crear archivo llamado **tsconfig.json** en el ***root*** de la aplicación.
>#
 >**yarn tsc --init --outDir dist/ --rootDir src**  
 **NOTA:** si usas este comando no olvides descomentar la linea **"jsx":  "preserve",** el archivo de configuración.  
ó  
 >**tsconfig personalizado:**  
 >#
```
  
{
  "compilerOptions": {
    "target": "ES5" /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', or 'ESNEXT'. */,
    "module": "ESNext" /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. */,
    "moduleResolution": "node" /* Specify module resolution strategy: 'node' (Node.js) or 'classic' (TypeScript pre-1.6). */ /* Type declaration files to be included in compilation. */,
    "lib": [
      "DOM",
      "ESNext"
    ] /* Specify library files to be included in the compilation. */,
    "jsx": "react-jsx" /* Specify JSX code generation: 'preserve', 'react-native', 'react' or 'react-jsx'. */,
    "noEmit": true /* Do not emit outputs. */,
    "isolatedModules": true /* Transpile each file as a separate module (similar to 'ts.transpileModule'). */,
    "esModuleInterop": true /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */,
    "strict": true /* Enable all strict type-checking options. */,
    "skipLibCheck": true /* Skip type checking of declaration files. */,
    "forceConsistentCasingInFileNames": true /* Disallow inconsistently-cased references to the same file. */,
    "resolveJsonModule": true
    // "allowJs": true /* Allow javascript files to be compiled. Useful when migrating JS to TS */,
    // "checkJs": true /* Report errors in .js files. Works in tandem with allowJs. */,
  },
  "include": ["src/**/*"]
}

```
#
Configurar y crear archivo llamado **.babelrc** en el ***root*** de la aplicación.
```

{
  "presets": [
    "@babel/preset-env",
    [
      "@babel/preset-react",
      {
        "runtime": "automatic"
      }
    ],
    "@babel/preset-typescript"
  ],
  "plugins": [
    [
      "@babel/plugin-transform-runtime",
      {
        "regenerator": true
      }
    ]
  ]
}

```
#
Configurar y crear archivo llamado **webpack.config.js** en el ***root*** ó puedes crear una carpeta con el nombre de tu elección y crear ahí el archivo de configuración de webpack.

```

const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: path.resolve(__dirname, '..', './src/index.tsx'), //---> recuerda crear index dentro de src/index.tsx
  resolve: {
    extensions: ['.tsx', '.ts', '.js'],
  },
  module: {
    rules: [
      {
        test: /\.(ts|js)x?$/,
        exclude: /node_modules/,
        use: [
          {
            loader: 'babel-loader',
          },
        ],
      },
],
},
  output: {
    path: path.resolve(__dirname, '..', './build'),
    filename: 'bundle.js',
  },
  mode: 'development',
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, '..', './src/index.html'), //---> recuerda crear un archivo index.html dentro de carpeta src/
    }),
  ],
stats: 'errors-only',
}

```
#
Crea él script dentro de ***packcage.json*** para poner online la aplicación:
>#
>**"start":"webpack serve --config webpack/webpack.config.js --port 3001 --open",**  
>**"build":"webpack --config webpack/webpack.config.js",**  
>**"test":"echo \"Error: no test specified\" && exit 1"**  
>#