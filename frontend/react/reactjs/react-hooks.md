# React Hooks

```bash
yarn add eslint-plugin-react-hooks -D
```

```js
// .eslintrc.js
...
plugins: [
  ...
  'react-hooks'
],
...
rules: {
  ...
  'react-hooks/rules-of-hooks': 'error',
  'react-hooks/exhaustive-deps': 'warn'
}
```

## useEffect()

- Executa apenas quando a tela é criada
- Versão do `componentDidMount`

```js
useEffect(() => {}, []);
```

- Executa quando a tela criada e quando há alterações em `var1` e `var2`.
- Versão do `componentDidUpdate`

```js
useEffect(() => {}, [var1, var2]);
```

- Versão do `componentDidWillUnmount`

```js
useEffect(()=>{
  ...
  return ()=>{} //Funcao executada quando a tela deixa de existir

}, [])
```

### funcões assíncronas

- Precisa definir uma nova função `async` dentro do `useEffect`.

#### Forma correta

```js
useEffect(() => {
  async function loadProducts() {
    const response = await api.get("products");
  }

  loadProducts();
}, []);
```

#### Forma errada

```js
useEffect(async () => {
  const response = await api.get("products");
}, []);
```

## useMemo()

- Indicado para quando se faz muitos cálculos e os resultados desses cálculos devem ser renderizados.

#### Forma não indicada

```js
return(
  <strong>{tech.length}<strong>
)
```

- Não é indicada pois toda vez que o componente será renderizado ele terá que fazer o cálculo de `.length`

#### Forma indicada

```js
const techSize = useMemo(()=> tech.length, [tech])
...
return(
  <strong>{techSize}<strong>
)
```

- Agora o valor de `techSize` não muda, a não ser que haja uma alteração em `tech`.

## useCallback()

- Similar ao `useMemo()`, porém ele retorna uma função
- Ele serve para retirar as funções aninhadas (que estão dentro do componente), pois cada vez que o componente é chamado, suas funções internas tem que ser criadas do zero.
- Geralmente utilizado apenas em funcões que lidam com estados e props do componente.

#### Forma não indicada

```js
function App(){
  function add(){
    ...
  }
  return (...);
}
```

#### Forma indicada

```js
const handleAdd = useCallback(()=>{

}, [var1, var2])
...
return(...);
```

- Agora `handleAdd` só é recriado quando há alteraçao em `var1` e `var2`

## Hooks com redux

### Convertendo o uso das states

```js
// Sem Hooks
import { connect } from 'react-redux';
...
function Header({cartSize}) {
  return (
    <span>{cartSize} itens</span>
  );
}

export default connect(state => ({
  cartSize: state.cart.length,
}))(Header);
```

```js
//com hooks
import { useSelector } from 'react-redux';
...
export default function Header() {
  const cartSize = useSelector(state => state.cart.length)

  return (
    <span>{cartSize} itens</span>
  );
}
```

### Convertendo o uso das actions

```js
import { useSelector, useDispatch } from 'react-redux';
import * as CartActions from '../../store/modules/cart/actions';

export default function Home() {

  const amount = useSelector(state => state.cart.amount);

  const dispatch = useDispatch();

  function handleAddProduct(id) {
    dispatch(CartActions.addToCartRequest(id));
  }

  return (...);
}

```
