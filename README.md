# for-editor-markdown

based on the [for-editor](https://github.com/kkfor/for-editor)

### Instalação

```js
npm install for-editor -S
```

### Usar

```js
import React, { Component } from 'react'
import ReactDOM from 'react-dom'
import Editor from 'for-editor'

class App extends Component {
  constructor() {
    super()
    this.state = {
      value: ''
    }
  }

  handleChange(value) {
    this.setState({
      value
    })
  }

  render() {
    const { value } = this.state
    return <Editor value={value} onChange={() => this.handleChange()} />
  }
}

ReactDOM.render(<App />, document.getElementById('root'))
```

### Api

#### Atributos

| name        | type    | default     | description                        |
| ----------- | ------- | ----------- | ---------------------------------- |
| value       | String  | -           | Conteúdo da caixa de entrada                         |
| placeholder | String  | Comece a editar... | Placeholder text                           |
| lineNum     | Boolean | true        | Se deve exibir o número da linha                       |
| style       | Object  | -           | 编辑器样式                         |
| height      | String  | 600px       | Altura de editor                         |
| preview     | Boolean | false       | Modo de pré-visualização                           |
| expand      | Boolean | false       | Modo tela cheia                           |
| subfield    | Boolean | false       | Modo de coluna dupla (válido quando o modo de visualização está ativado)       |
| language    | String  | pt-BR       | Idioma (suporte pt-BR: português do Brasil, en: inglês) |
| toolbar     | Object  | Do seguinte modo        | Barra de ferramentas personalizada                       |

```js

toolbar: {
  h1: true,
  h2: true,
  h3: true,
  h4: true,
  img: true,
  link: true,
  code: true,
  preview: true,
  expand: true,
  undo: true,
  redo: true,
  save: true,
  subfield: true,
}
```

#### Eventos

| name     | params 参数   | default | description    |
| -------- | ------------- | ------- | -------------- |
| onChange | String: value | -       | Retorno de chamada quando o conteúdo muda |
| onSave   | String: value | -       | Retorno de chamada ao salvar     |
| addImg   | File: file    | -       | Retorno de chamada ao adicionar uma imagem |

##### Upload de imagem

```js
class App extends Component {
  constructor() {
    super()
    this.state = {
      value: '',
    }
    this.$vm = React.createRef()
  }

  handleChange(value) {
    this.setState({
      value
    })
  }

  addImg($file) {
    this.$vm.current.$img2Url($file.name, 'file_url')
    console.log($file)
  }

  render() {
    const { value } = this.state

    return (
      <Editor
        ref={this.$vm}
        value={value}
        addImg={($file) => this.addImg($file)}
        onChange={value => this.handleChange(value)}
      />
    )
  }
}
```

#### Teclas de atalho

| name   | description  |
| ------ | ------------ |
| tab    | 两个空格缩进 |
| ctrl+s | 保存         |
| ctrl+z | 上一步       |
| ctrl+y | 下一步       |


### Licença

for-editor is [MIT Licence](./LICENSE).
