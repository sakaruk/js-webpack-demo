
---

### **1. Setup the Project**
1. **Create a new project folder:**
   ```bash
   mkdir js-webpack-demo
   cd js-webpack-demo
   ```
2. **Initialize a `package.json` file:**
   ```bash
   npm init
   ```

---

### **2. Install Required Tools**
1. **Install Webpack and necessary plugins:**
   ```bash
   npm install webpack webpack-cli html-webpack-plugin webpack-dev-server --save-dev
   ```

2. **Install Babel (for ES6+ transpilation):**
   ```bash
   npm install @babel/core @babel/preset-env babel-loader --save-dev
   ```

---

### **3. Create the `src/` Folder**
1. **Set up your source files:**
   ```bash
   mkdir src
   touch src/index.html src/index.js src/module1.js
   ```

2. **Add content to the files:**
   - `src/index.html`:
     ```html
     <!DOCTYPE html>
     <html>
     <head>
       <title>Webpack Demo</title>
     </head>
     <body>
       <h1>Webpack Bundling Demo</h1>
       <p>Open the console to see the output!</p>
     </body>
     </html>
     ```

   - `src/module1.js`:
     ```javascript
     export const greet = (name) => `Hello, ${name}!`;
     ```

   - `src/index.js`:
     ```javascript
     import { greet } from './module1';

     const message = greet('Students');
     console.log(message);
     ```

---

### **4. Configure Webpack**
1. **Create a `webpack.config.js` file:**
   ```javascript
   const path = require('path');
   const HtmlWebpackPlugin = require('html-webpack-plugin');

   module.exports = {
     entry: './src/index.js',
     output: {
       path: path.resolve(__dirname, 'dist'),
       filename: 'bundle.js',
       clean: true, // Cleans the output directory before building
     },
     plugins: [
       new HtmlWebpackPlugin({
         template: './src/index.html',
         filename: 'index.html',
       }),
     ],
     module: {
       rules: [
         {
           test: /\.js$/,
           exclude: /node_modules/,
           use: {
             loader: 'babel-loader',
             options: {
               presets: ['@babel/preset-env'],
             },
           },
         },
       ],
     },
     mode: 'development',
     devServer: {
       static: {
         directory: path.join(__dirname, 'dist'),
       },
       open: true,
       port: 8080,
     },
   };
   ```

---

### **5. Add Scripts to `package.json`**
Update the `scripts` section:
```json
"scripts": {
  "start": "webpack serve --open",
  "build": "webpack"
}
```

---

### **6. Run and Test the Project**
1. **To start the development server:**
   ```bash
   npm start
   ```
   - This will automatically open the browser at `http://localhost:8080` and serve the files from the `dist/` folder.

2. **To build the project for production:**
   ```bash
   npm run build
   ```
   - This will generate a `dist/` folder containing the bundled JavaScript and HTML.
