# Vite Cheat Sheet

## General Overview

- **Vite** is a next-generation frontend build tool that is fast and highly optimized for modern web development.
- It supports frameworks like **Vue**, **React**, **Svelte**, and **Preact**, providing fast development server start times and optimized production builds.
- Uses **ES Modules (ESM)** in the browser, enabling instant hot module replacement (HMR).

---

## Basic Setup and Installation

1. **Create a new project using Vite:**
   - Run the following command and choose the desired framework:
     ```bash
     npm create vite@latest
     ```
     Then follow the prompts to select your framework (e.g., Vue, React, etc.).
2. **Install dependencies:**

   ```bash
   cd <project-folder>
   npm install
   ```

3. **Start the development server:**

   ```bash
   npm run dev
   ```

   The local server will typically start at `http://localhost:5173`.

4. **Build for production:**

   ```bash
   npm run build
   ```

5. **Preview the production build:**
   ```bash
   npm run preview
   ```

---

## Key Vite Commands

| Command              | Description                                                |
| -------------------- | ---------------------------------------------------------- |
| `npm run dev`        | Starts the development server with hot module replacement. |
| `npm run build`      | Builds the app for production.                             |
| `npm run preview`    | Preview the production build locally.                      |
| `vite`               | Run Vite directly (CLI mode).                              |
| `vite --host`        | Expose the dev server to the local network.                |
| `vite --port <port>` | Specify a port for the dev server.                         |
| `vite build`         | Perform a production build from CLI.                       |

---

## Configuration (vite.config.js)

- **Vite** supports customization via the `vite.config.js` file.
- Here’s an example of basic configuration:

```js
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";

export default defineConfig({
  plugins: [vue()],
  server: {
    port: 3000, // specify port
  },
  build: {
    outDir: "dist", // output directory for production build
  },
});
```

#### **Common Configurations:**

1. **Change default port:**

   ```js
   server: {
     port: 3000;
   }
   ```

2. **Set up alias:**

   ```js
   resolve: {
     alias: {
       '@': '/src'
     }
   }
   ```

3. **Proxy API requests:**
   ```js
   server: {
     proxy: {
       '/api': {
         target: 'http://backend.example.com',
         changeOrigin: true,
         rewrite: path => path.replace(/^\/api/, '')
       }
     }
   }
   ```

---

## Hot Module Replacement (HMR)

- Vite enables **Hot Module Replacement** out of the box.
- During development, any changes to a file will trigger an update in the browser without reloading the entire page.
- To use HMR, no additional setup is required for most projects:
  ```bash
  npm run dev
  ```

---

## Environment Variables

- Vite uses `.env` files to define environment variables, similar to other modern tools like Next.js.

1. **Create environment files** like `.env`, `.env.production`, `.env.development`.

2. **Example of a `.env` file:**

   ```
   VITE_API_URL=https://api.example.com
   ```

3. **Accessing environment variables in your code:**
   ```js
   const apiUrl = import.meta.env.VITE_API_URL;
   ```

- Variables prefixed with `VITE_` will be available in your client-side code.

---

## Plugins in Vite

- Vite supports an extensive plugin ecosystem.
- To use a plugin, install it and add it to the `plugins` array in your `vite.config.js`.

1. **Example of adding the Vue plugin:**

   ```bash
   npm install @vitejs/plugin-vue
   ```

   Then, in `vite.config.js`:

   ```js
   import vue from "@vitejs/plugin-vue";

   export default defineConfig({
     plugins: [vue()],
   });
   ```

2. **Some popular Vite plugins:**
   - **@vitejs/plugin-vue**: Vue.js plugin.
   - **@vitejs/plugin-react**: React plugin.
   - **vite-plugin-pwa**: Progressive Web App support.
   - **vite-plugin-eslint**: ESLint integration.

---

## Custom Scripts and Commands

1. **Building with different modes:**

   ```bash
   vite build --mode production
   ```

2. **Run with specific environment:**

   ```bash
   vite --mode development
   ```

3. **Running Vite without scripts:**
   You can run `vite` commands directly from the terminal, for example:
   ```bash
   vite build
   ```

---

## Using Vite with Frameworks

1. **React:**

   - Install React and the necessary plugin:
     ```bash
     npm install react react-dom @vitejs/plugin-react
     ```
   - Update `vite.config.js`:

     ```js
     import react from "@vitejs/plugin-react";

     export default defineConfig({
       plugins: [react()],
     });
     ```

2. **Vue:**

   - Install Vue and the plugin:
     ```bash
     npm install vue @vitejs/plugin-vue
     ```
   - Update `vite.config.js`:

     ```js
     import vue from "@vitejs/plugin-vue";

     export default defineConfig({
       plugins: [vue()],
     });
     ```

---

## Production Optimization

1. **Minification:**  
   Vite uses **esbuild** for minification, which is faster than traditional minifiers like Terser.

2. **Code Splitting:**  
   Vite automatically splits code into separate chunks based on imports, which improves the loading time of the application.

3. **Tree-shaking:**  
   Vite automatically performs tree-shaking to remove unused code during the build process.

4. **Lazy loading:**  
   Dynamic imports are supported out-of-the-box, enabling code splitting for different parts of your app.

---

## SSR (Server-Side Rendering) with Vite

- Vite supports **SSR** for Vue and React applications.
- Example configuration for a Vue SSR app:

  ```js
  export default defineConfig({
    build: {
      ssr: "src/entry-server.js",
    },
  });
  ```

- Vite provides tools for both client-side and server-side rendering, offering great flexibility in modern web applications.

---

## Useful Links

- [Vite Documentation](https://vitejs.dev/guide/)
- [Vite Plugin List](https://vitejs.dev/plugins/)
- [Vite GitHub](https://github.com/vitejs/vite)

---
