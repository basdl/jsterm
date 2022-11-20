This repository is a serial console utility to debug and access serial interfaces. The template for this application is [HTerm](https://www.der-hammer.info/pages/terminal.html), a fabulous application to debug serial interfaces. This repository aims to take this application into the 21st century.

---

## TODO

- Add transmit controls
- Add status flags for the SerialPort
- Add overlay if [SerialPort WebApi](https://developer.mozilla.org/en-US/docs/Web/API/Web_Serial_API) is not supported.
- Add copy and paste features
- Add save to file feature

## Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:8080](http://localhost:8080). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```
