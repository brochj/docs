#  local storage
## Salvando dados
```js
class TechList extends Component {
  state = {
    newTech: '',
    techs: []
  }

  componentDidUpdate(_, prevState){
    if(prevState.techs !== this.state.techs){
      localStorage.setItem('techs', JSON.stringify(this.state.techs))
    }
  }
```

## Lendo os dados
```js
componentDidMount(){
    const techs = localStorage.getItem('techs');
    if(techs){
      this.setState({techs: JSON.parse(techs)})
    }
  }
```