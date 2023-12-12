## Configuración de Css  e Imagenes
Para configurar Css con webpack instalar el siguiente paquete:
>#
> **yarn add -D css-loader style-loader**
>#  

Adicional introducir el siguiente bloque de código dentro del bloque de **module:{ }** dentro de la sección **rules: [ ]** de ***webpack.config.js***:  

```  
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
```  
## Imagenes  
Configuración para trabajar con imagenes en webpack.  
> Primero crearemos un archivo de configuaración de typescript para no tener problemas de tipos, crear un archivo den el ***root*** del filesystem con el nombre: ***declarations.d.ts*** e introducir las lineas:  
>>  declare module '*.png'  
>>  declare module '*.svg'  
#
Adicional introducir el siguiente bloque de código entro de ***webpack.config.js***:  

```  
      {
        test: /\.(?:ico|gif|png|jpg|jpeg)$/i,
        type: 'asset/resource',
      },
      {
        test: /\.(woff(2)?|eot|ttf|otf|svg|)$/,
        type: 'asset/inline',
      },

```  
#
### Ejemplo  

Por lo que el archivo de configuración de webpack es decir el archivo ***webpack.config.js*** deberá quedar así:  
  
```


const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: path.resolve(__dirname, '..', './src/index.tsx'),
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
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(?:ico|gif|png|jpg|jpeg)$/i,
        type: 'asset/resource',
      },
      {
        test: /\.(woff(2)?|eot|ttf|otf|svg|)$/,
        type: 'asset/inline',
      },
    ],
  },
  output: {
    path: path.resolve(__dirname, '..', './build'),
    filename: 'bundle.js',
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, '..', './src/index.html'),
    }),
  ],
  stats: 'errors-only',
}

```
#