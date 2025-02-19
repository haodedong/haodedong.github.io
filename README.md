# memorial-day-project

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### 打docker包
    
    ```sh   
docker build -t lovebml:1.0 .
docker save -o lovebml.tar lovebml:1.0
docker load -i lovebml.tar
```
### 启动docker

    ```sh       
docker run -d -p 1314:80 --name lovebml lovebml:1.0
    ```