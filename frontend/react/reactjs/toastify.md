# React Tostify

```bash
yarn add react-toastify
```

### app.js

```js
...
import { Provider } from 'react-redux';
import { ToastContainer } from 'react-toastify';
...
function App() {
  return (
    <Provider store={store}>
      <BrowserRouter>
        <Header />
        <Routes />
        <GlobalStyles />
        <ToastContainer autoClose={3000} />
      </BrowserRouter>
    </Provider>
..
```

### Nos estilos globais `global.js`

```js
import "react-toastify/dist/ReactToastify.css";
```

### Utilizando

```js
import { toast } from "react-toastify";

function foo() {
  toast.error("Some error");
}
```
