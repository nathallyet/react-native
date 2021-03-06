# React Native

## O que é o React?

É a parte central, que cuida da componetização, e essa biblioteca central ela serve tanto para desenvolver aplicação para WEB(React DOM) como também aplicações para mobile(React Native).

## O que é o React Native?

Framework open source, Cross Platform(multiplataforma).
Todo código desenvolvidoéconvertido para a linguagem nativa do sistema operacional.
Conseguimos desenvolver aplicações para Android e iOS utilizando um código único.

Documentação: https://reactnative.dev.

## Como funciona o React Native?

Temos duas partes importantes em relação a uma aplicação React Native.

1° UI(User Interface): Interface Gráfica
A parte da interface gráfica é desenvolvido com o JSX, e o _JSX_ criado vai gerar componentes nativos tanto para iOS quanto para Android.
Ex.: No caso de uma _View_ JSX(no WEB é uma _div_) vai converter para o iOS em uma tag _UIView_ e para o Android em uma tag _android.View_.

2° JS(JavaScript): Lógica
A parte da lógica vai rodar dentro de hantimes JS que vão estar dentro dos dispositivos, no caso do iOS ele vai usar o _Webkit_ e no caso do Android ele vai usar o _V8_.

## Criando um emulador do celular Android no Android Studio

- Vamos em `More Actions` > `Virtual Device Manager` > `Create device` e selecionar o simulador `Pixel3` e clicar em `Next` e em seguida vai abrir uma janela para selecionarmos o a versão do sistema android que queremos usar > Após isso vai abrir uma nova janela para nomearmos esse emular, feito isso podemos clicar em `Finish`.

- Agora, temos o emulador disponível, e podemos abri-lo indo na action `play`.

## Criando um projeto 

### Iniciando um projeto com a CLI(Command Line Interface) do React Native

```
npx react-native init [nome-do-projeto]
```

- Concluindo a inicialização do projeto, vamos entrar na pasta do projeto criada e rodar o comando para inicializar o Metro Bundle(o qual vai compilar o JS e passar para o app conseguir renderizar):

```
npx react-native start
```

- Obs.: Antes de startar o android, é necessário se conectar a máquina virtual ao IP do emulador, rodando o comando abaixo:

```
adb connect 10.0.2.2:5555
```

- Vamos deixar rodando o Metro e abrir um novo terminal no diretório do projeto e realizar a instalação do Android:

```
yarn android ou npx react-native run-android
```

### Estrutura de pastas

- **__tests__** : onde vamos conseguir rodar o nosso app e testar;
- **.bundle** : criamos um bundle para rodar no android, ele vai ser responsavel por transcrever o que está escrito no projeto para ser reconhecido no android;
- **android** : nessa pasta teremos as configurações nativas do android;
- **ios** : nessa pasta teremos as configurações nativas do ios;
- **node_modules** : pasta de dependências do javascript;
- **.buckconfig**, **.eslintrc**, **flowconfig** : arquivos de configurações;
- **prettierrc.js** : arquivo de regras de código;
- **.ruby-version** : para guardar a versão do ruby que vamos rodar no ios; 
- **.watchmanconfig** : arquivo de configuração de watch;
- **App.js** : arquivo da aplicação;
- **babel.config.js** : arquivo de configuração do babel, já vem configurado, faz compilação para as versões mais antigas do JS;
- **Gemfile**, **Gemfile.lock** : arquivos de gems para o ruby;
- **index.js** : porta de entrada da aplicação em react native, ele importa o _AppREgistry_ do react native, e usa o método _registerCompent_ que vai registrar o componente raíz da aplicação(Componente chamado App);
- **metro.config.js** : arquivo de configuração do metro bundle;
- **package.json** : arquivo de dependências JS;
- **yarn.lock** : registro das dependências instaladas no app.

### Alterando estrutura de pastas

- Na raíz do projeto vamos criar uma pasta _src_ e vamos mover o arquivo _App.js_ para dentro dela e apagar todo o conteúdo dele.

- Dentro do arquivo _index.js_ vamos alterar a referência para o arquivo App para o novo que criamos dentro de _src_:

``` JS
/**
 * @format
 */

import {AppRegistry} from 'react-native';
import App from './src/App';
import {name as appName} from './app.json';

AppRegistry.registerComponent(appName, () => App);
```

- Isso ocasionou um erro no nosso emulador android. Para resolver esse problema, dentro do novo arquivo _App.js_ vamos criar uma constante _App_ que vai receber uma arrow funcion/_() =>_ que vai retornar/_return_ vazio/_null_ e em seguida exportar por padrão/_export default_ para que esse componente fique acessível:

``` JS
const App = () => {
  return null;
};

export default App;
```

- E para deixar tudo pronto para implementação de código JSX e dos componentes do react native, vamos importá-los:

``` JS
import React from 'react';
import {} from 'react-native';

const App = () => { // podemos criar diretamente uma função chamada App também
  return null;
};

export default App;
```

### Conhecendo o JSX

É uma extensão de sintaxe para JavaScript. É recomendado usar JSX com o React para descrever como a UI deveria parecer. 
JSX pode lembrar uma linguagem de template, mas que vem com todo o poder do JavaScript.
Nada mais é que código JavaScript com "cara" de HTML.

### Entendendo Sistema de Módulos do ECMAScript

#### Export

No modelo CommonJS podemos exportar valores atribuindo eles ao module.exports como no snippet abaixo:

``` JS
module.exports = 1
module.exports = NaN
module.exports = 'foo'
module.exports = { foo: 'bar' }
module.exports = [ 'foo', 'bar' ]
module.exports = function foo () {}
module.exports = () => {}
```

No ES6, os módulos são arquivos que dão `export` uma API (basicamente igual ao CommonJS). As declarações, variáveis, funções e qualquer coisa daquele módulo existem apenas nos escopos daquele módulo, o que significa que qualquer variável declarada dentro de um módulo não está disponível para outros módulos (a não ser que eles sejam exportados explicitamente como parte da API, e importados posteriormente no módulo que as usa).

#### Export padrão

Podemos simular o comportamento do CommonJS basicamente trocando o module.exports por export default:

``` JS
export default = 1
export default = NaN
export default = 'foo'
export default = { foo: 'bar' }
export default = [ 'foo', 'bar' ]
export default = function foo () {}
export default = () => {}
```

Ao contrário dos módulos no CommonJS, declarações export só podem ser colocadas no top level do código, e não em qualquer parte dele. Presumimos que essa limitação existe para tornar mais fácil a vida dos interpretadores quando vão identificar os módulos, mas, olhando bem, é uma limitação bem válida, porque não há muitas boas razões para que possamos definir exports dinâmicos dentro das funções da nossa API.

Um dos modos de ampliar sua performance é utilizando módulos, isto porque os módulos são compilados de modo estático, e antes do seu código sequer passar para o interpretador do browser (como o V8 por exemplo). Desta forma é possível extrair somente as partes do código que são realmente utilizadas na aplicação ao invés de importar o módulo todo, e isso só seria possível se os módulos fossem declarados no top level, porque qualquer coisa dentro de uma função se tornaria algo dinâmico, e não estático.

``` JS
function foo () {
    export default 'bar' // Syntax Error
}
foo()

// --- //

function foo () {
    return 'bar'
}
export default foo // OK!
```

#### Exports Nomeados

No CommonJS podemos simplesmente criar bindings de variáveis direto no `module.exports` que então teremos as propriedades sendo atualizadas em tempo real:

``` JS
module.exports.foo = 'bar'
```

Podemos replicar esse comportamento usando a sintaxe de exports nomeados. Ao invés de atribuir o valor para o module.exports, podemos declarar quaisquer variáveis que queremos exportar.

Note que o código abaixo não pode ser refatorado para extrair a declaração da variável para uma linha única (e depois usar um export foo), isto nos daria um erro de sintaxe, provando que, cada vez mais, o ES6 é a favor de análise estática ao invés de fluxos dinâmicos:

``` JS
export var foo = 'bar'
```

É importante ter em mente que estamos exportanto **bindings**, não valores.

#### Bindings. Não valores.

Um ponto importante de notar é que os módulos no ES6 não exportam valores ou referências, mas sim os **bindings** das variáveis. Isso, em prática, significa que uma variável chamada `foo`, que é exportada, vai ter um link à variável `foo` do módulo, e os valores atribuídos a elas serão sujeitos às mudanças de valores feitas em `foo`.

Se você tem um módulo `./a` como abaixo, o export de `foo` vai ser ligado a bar por 500ms e depois será alterado para `baz`:

``` JS
export var foo = 'bar'
setTimeout(() => foo = 'baz', 500)
```

#### Exportando listas

Como podemos ver abaixo, os módulos ES6 permitem que exportemos listas de membros nomeados no top level:

``` JS
var foo = 'bar'
var bar = 'foo'
export { foo, bar }
```

Se você prefere exportar alguma coisa com um nome diferente você pode usar export `{ foo as fuz }`, como abaixo:

``` JS
var foo = 'bar'
export { foo as fuz }
```

#### Melhores práticas com export

Todas essas possibilidades de exportar um módulo vão introduzir um pouco de confusão na cabeça das pessoas. Na maioria dos casos é encorajado utilizar apenas um `export default` (e fazer isso só no final do módulo). Então você pode importar a API como o nome do próprio módulo.

``` JS
var api = {
  foo: 'bar',
    baz: 'fooz'
}

export default api
```

#### Import

O import é a contraparte do export, ele pode ser usado para carregar um módulo a partir de outro.

Antes de qualquer coisa, a maneira como os módulos são carregados depende da implementação de cada lugar. No momento nenhum browser implementa um loader.

Para contornar o que foi dito acima, é possível utilizar-se de recursos como transpilers (tipo o Babel), para escrever código ES6 enquanto as equipes de desenvolvimento dos browsers se preocupam em como fazer o carregamento de módulos funcionar.

Um exemplo legal é o lodash. A linha a seguir simplesmente carrega a biblioteca do Lodash dentro do nosso módulo. No entanto, ele não cria nenhuma variável. Ele irá executar qualquer código no top level do Lodash.

``` JS
import 'lodash'
```

#### Importando padrões

No CommonJS temos uma importação utilizando o require:

``` JS
var _ = require('lodash')
```

Para importar um export default de outro módulo usando ES6 só precisamos escolher um nome. A sintaxe muda um pouco porque você não está importando o objeto em si, mas um binding. E isso torna mais fácil para ferramentas de análise:

``` JS
import _ from 'lodash'
```

#### Importando exports nomeados

A sintaxe é muito similar ao que usamos acima:

``` JS
import { map, reduce } from 'lodash'
```

É muito parecido com o destructuring assignment que temos na nova especificação.

Uma outra maneira que podemos também importar os export nomeados, é dar um alias para cada um, ou então apenas para um deles:

``` JS
import { cloneDeep as clone, map } from 'lodash'
```

#### Importando tudo

Se você quiser importar um namespace completo de um módulo. Diferente dos imports nomeados ou padrões, ele importa tudo.

Note que a sintaxe abaixo precisa vir seguida de um alias onde todos os bindings vão ser colocados. (Exports padrões vão ser colocados em alias.default):

``` JS
import * as _ from 'lodash'
```

### Componente SafeAreaView

Documentação: https://reactnative.dev/docs/safeareaview.

O objetivo de `SafeAreaView` é renderizar conteúdo dentro dos limites da área segura de um dispositivo. Atualmente, é aplicável apenas a dispositivos iOS com iOS versão 11 ou posterior.

`SafeAreaView` renderiza o conteúdo aninhado e aplica automaticamente o preenchimento para refletir a parte da visualização que não é coberta por barras de navegação, barras de guias, barras de ferramentas e outras visualizações ancestrais. Além disso, e mais importante, os preenchimentos do SafeAreaView refletem a limitação física da tela, como cantos arredondados ou entalhes da câmera (ou seja, a área da caixa do sensor no iPhone 13).

Podemos substituir a _View_ principal(igual uma div container) do nosso App pelo _SafeAreaView_

- No arquivo, _App.js_ vamos importar o componente SafeAreaView do react native:

``` JSX
import React from "react";
import { SafeAreaView } from "react-native";

const App = () => {
  return (
    <SafeAreaView>
      
    </SafeAreaView>
  );
}

export default App;
```

### Componente Text

Documentação: https://reactnative.dev/docs/text

Um componente React para exibir texto. `Text` suporta aninhamento, estilo e manuseio de toque.

- Vamos importar o componente Text do react native e inserir o componente _Text_ dentro do componente _SafeAreaView_:

``` JSX
import React from "react";
import { SafeAreaView, Text } from "react-native";

const App = () => {
  return (
    <SafeAreaView>
      <Text>Olá mundo!</Text>
    </SafeAreaView>
  );
}

export default App;
```

### Organizando Componentes

- Dentro de _src_ vamos criar uma pasta chamada _components_ e nela vamos criar um arquivo chamado Primeiro/_First_. 
E nele vamos criar um componente funcional:

``` JSX
import React from "react";
import {} from "react-native";

const First = () => {
  return (
    <Text>First Component</Text>
  );
}
```

- E dentro de _App.js_ vamos importar esse componente _First_ e referenciá-lo:

``` JSX
import React from "react";
import { SafeAreaView, Text } from "react-native";

import First from "./components/First";

const App = () => {
  return (
    <SafeAreaView>
      <Text>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

export default App;
```

### API StyleSheet

Documentação: https://reactnative.dev/docs/stylesheet

É uma abstração semelhante ao CSS StyleSheets.

Dicas de qualidade de código: Ao afastar os estilos da função de renderização, você torna o código mais fácil de entender. Nomear os estilos é uma boa maneira de adicionar significado aos componentes de baixo nível na função de renderização.

Obs.: O React Native utiliza o _flex box por padrão_, apenas com a diferença entre linhas e colunas, todas as views ele considera por coluna/_column_ ao invés de ser por linha/_row_ como é na web.

- Vamos importar a API StyleSheet do react native:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

const App = () => {
  return (
    <SafeAreaView>
      <Text>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

export default App;
```

- Dessa forma, essa API que importamos vai criar um objeto/folha de estilo. 
Agora, vamos criar uma constante chamada _styles_ que vai receber essa folha de estilo através da função _StyleSheet.create_ e essa função vai receber um objeto com a descrição dos estilos:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

const App = () => {
  return (
    <SafeAreaView>
      <Text>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({

});

export default App;
```

- - E dentro desse objeto _styles_ vamos criar um objeto(que funciona igual a uma classe de estilo) chamado _App_(poderia ser _container_, mas esse objeto vamos aplicar posteriormente na _SafeAreaView_):

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

const App = () => {
  return (
    <SafeAreaView>
      <Text>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  App: {
    
  }
});

export default App;
```

- Em seguida, vamos passar a propriedade _style_ para o componente _SafeAreaView_, e essa propriedade vai receber o objeto _App_ que se escontra dentro do objeto _styles_, dessa forma todas as propriedades relacionadas dentro do objeto _styles.App_ vai refletir no componente _SafeAreaView_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  App: {

  }
});

export default App;
```

- E para visualizarmos melhor essa aplicação, vamos aplicar um _background color_ nesse objeto _App_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  App: {
    backgroundColor: "pink",
  }
});

export default App;
```

- Obs.: O React Native utiliza o _flex box por padrão_, apenas com a diferença entre linhas e colunas, todas as views ele considera por coluna/_column_ ao invés de ser por linha/_row_ como é na web.
E para informarmos que esse _SafeAreaView_ pode crescer vamos aplicar a propriedade _flex 1_(o flex 1 vai permitir que essa view possa preencher todo o espaço disponível, ou seja, a tela inteira):

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  App: {
    backgroundColor: "pink",

    flex: 1,
  }
});

export default App;
```

- E para alinhar o conteúdo do eixo principal/_column_ ao centro vamos usar a propriedade _justify content_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  App: {
    backgroundColor: "pink",

    flex: 1,
    justifyContent: "center",
  }
});

export default App;
```

- E para alinhar os elementos no eixo cruzado/nesse caso é o eixo da _row_ vamos usar a propriedade _align items_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  App: {
    backgroundColor: "pink",

    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  }
});

export default App;
```

### Criando um arquivo de estilo

- Dentro de _src/components_ vamos criar um arquivo chamado _style.js_ e nele vamos importar o _StyleSheet_ do react native e em seguida criar podemos um objeto de estilo/folha de estilo chamando o _StyleSheet.create_ e exportar tudo por padrão/_export default_ para que fique acessível fora:

``` JSX
import { StyleSheet } from "react-native";

export default StyleSheet.create({
  
});
```

- E nele vamos criar um objeto de estilo/classe para aplicarmos nos textos padrões:

``` JSX
import { StyleSheet } from "react-native";

export default StyleSheet.create({
  textDefault: {
    fontSize: 24,
  }
});
```

- E para usarmos esse objeto de estilo fora desse arquivo vamos importá-lo(nesse caso vamos importá-lo dentro do componente _First_):

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "./style";

const First = () => {
  return (
    <Text>First Component</Text>
  );
}

export default First;
```

- E vamos aplicar no _Text_ através da propriedade _style_ acessando o objeto _textDefault_ de dentro do arquivo que nomeamos de _Style_ quando importamos:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "./style";

const First = () => {
  return (
    <Text style={Style.textDefault}>First Component</Text>
  );
}

export default First;
```

- E podemos fazer o mesmo no componente _App_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

import Style from "./components/style";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  App: {
    backgroundColor: "pink",

    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  }
});

export default App;
```

### console.warn

Ao invés de usarmos o _console.log_ podemos usar o _console.warn_ que ele irá mostrar/debbugar o valor que queremos visualizar em um _yellow box_ no próprio emulador.

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import First from "./components/First";

import Style from "./components/style";

const App = () => {
  console.warn("Opa!")

  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  App: {
    backgroundColor: "pink",

    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  }
});

export default App;
```

### Componente com Propriedades

- Em src/components vamos criar um componente funcional chamado _MinMax.js_:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "./style";

const MinMax = () => {
  return (
    <Text style={Style.textDefault}>
      O valor X é maior que o valor Y!
    </Text>
  );
}

export default MinMax;
```

- Em seguida, vamos importar esse componente _MinMax_ e referênciá-lo dentro do componente principal da nossa aplicação(_App.js_):

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

- Nota-se que o retorno da função/componente _MinMax_ espera receber valor Min e o valor Máx como parâmetro. Para isso, essa função vai receber esses parâmetros, que por padrão no React são chamados de props:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "./style";

const MinMax = (props) => {
  return (
    <Text style={Style.textDefault}>
      O valor X é maior que o valor Y!
    </Text>
  );
}

export default MinMax;
```

**Obs.:** Props são apenas leitura. Não conseguimos alterar uma propriedade. Se for necessário algum tratamento antes da renderização, podemos colocar em uma constante.

- Agora que estamos recebendo as _props_, se fizermos o debbug no _console_ podemos notar que _props_ é um objeto. Portanto, podemos acessar essas propriedades através de _props.[nome-atributo]_:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "./style";

const MinMax = (props) => {
  console.log(props)

  return (
    <Text style={Style.textDefault}>
      O valor {props.max} é maior que o valor {props.min}!
    </Text>
  );
}

export default MinMax;
```

- E no arquivo _App.js_ vamos e passar os valores de _min_ e _max_ via _props_ para o componente _MinMax_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";

const App = () => {
  // console.warn("Opa!")

  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

### React Fragment

Quando não envolvemos o código JSX com algum elemento é retornado o segunte erro: Adjacent JSX elements must be wrapped in an enclosing tag(Elementos JSX adjacentes devem ser agrupados em uma tag delimitadora).

- Como exemplo dentro de src/components vamos criar um componente chamado _Fragment_:

``` JSX
import React from "react";
import { View, Text } from "react-native";

import Style from "./style";

const Fragment = (props) => {
  return (
    <View>
      <Text style={Style.textDefault}>
        Adjacent JSX elements must be wrapped in an enclosing tag.
      </Text>
      <Text style={Style.textSecondary}>
        Cuidado com esse erro!
      </Text>
    </View>
  );
}

export default Fragment;
```

- Podemos notar que o conteúdo JSX está sendo delimitado por um elemento do tipo _View_. 

- Caso não queiramos que esse elemento seja colocado dentro de uma _View_, podemos usar o _React Fragment_:

``` JSX
import React from "react";
import { View, Text } from "react-native";

import Style from "./style";

const Fragment = (props) => {
  return (
    <React.Fragment>
      <Text style={Style.textDefault}>
        Adjacent JSX elements must be wrapped in an enclosing tag.
      </Text>
      <Text style={Style.textSecondary}>
        Cuidado com esse erro!
      </Text>
    </React.Fragment>
  );
}

export default Fragment;
```

- Ou sua sintaxe reduzida:

``` JSX
import React from "react";
import { View, Text } from "react-native";

import Style from "./style";

const Fragment = (props) => {
  return (
    <>
      <Text style={Style.textDefault}>
        Adjacent JSX elements must be wrapped in an enclosing tag.
      </Text>
      <Text style={Style.textSecondary}>
        Cuidado com esse erro!
      </Text>
    </>
  );
}

export default Fragment;
```

- Com a sintaxe reduzida, só não é possível utilizar atributos extras.

### Componente Button

- Dentro de src/components vamos criar um componente funcional chamado _Btn_ e iremos exportar ele por padrão e importar o elemento _Button_ do react native e referênciá-lo: 

``` JSX
import React from "react";
import { Button } from "react-native";

const Btn = (props) => {
  return (
    <Button />
  );
}

export default Btn;
```

- E vamos definir algumas propriedades desse elemento _Button_, como o _title_ dele e o evento _onPress_ que vai ser a função que vai ser executada quando esse botão for clicado:

``` JSX
import React from "react";
import { Button } from "react-native";

const Btn = (props) => {
  return (
    <Button 
      title="Executar"
      onPress={}
    />
  );
}

export default Btn;
```

- Podemos criar uma função _executar_ e passar essa função para o evento _onPress_ para que quando ele for chamado ele execute essa função _executar_:

``` JSX
import React from "react";
import { Button } from "react-native";

const Btn = (props) => {

  function executar() {
    console.log("Executando...")
  }

  return (
    <Button 
      title="Executar"
      onPress={executar}
    />
  );
}

export default Btn;
```

- E para visualizarmos isso em tela, vamos importar e referênciar esse componente _Btn_ no nosso arquivo _App.js_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

### Componente com Estado(useState)

- Dentro de src/components vamos criar um componente funcional chamado Contador/_Counter_ e iremos exportar ele por padrão e importar os elementos _Text_ e _Button_ do react native e referênciá-los(text vai receber o valor do contador e os buttons vai ser de +/incremento de -/decremento):

``` JSX
import React from "react";
import { Text, Button } from "react-native";

import Style from "./style";

const Counter = () => {
  return (
    <React.Fragment>
      <Text style={Style.textDefault}>0</Text>
      <Button title="-"/>
      <Button title="+"/>
    </React.Fragment>
  );
}

export default Counter;
```

- E para visualizarmos isso em tela, vamos importar e referênciar esse componente _Btn_ no nosso arquivo _App.js_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";
import Counter from "./components/Counter";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
      <Counter />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

- A partir do _useState_ conseguimos criar estado dentro do nosso componente. Então ao invés de criarmos uma variável simplesmente colocando o valor dela(nesse caso seria _count = 0_). Vamos chamar o _useState_ e passar o valor inicial. 
Só que essa função vai retornar um array com duas possições, a primeira possição vai ser o valor e a segunda posição vai ser uma função que vai ser usada para alterar esse valor. Como bem sabemos podemos usar atribuição via desestruturação (destructuring assignment). Ex.: const [a, b] = [1, 2], fica assim, a=1 e b=2. Desse modo, vamos usar o _destructuring_ para receber os dois valores do array que _useState_ retorna:

``` JSX
import React, { useState } from "react";
import { Text, Button } from "react-native";

import Style from "./style";

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>{count}</Text>
      <Button title="-"/>
      <Button title="+"/>
    </React.Fragment>
  );
}

export default Counter;
```

- Próximo passo, vamos criar funções que irão incrementar/_inc_ e decrementar/_dec_ o valor do contador. 
O que vamos fazer dentro dessa função? Vamos alterar o valor de _count_ ou seja, alterar o estado dele. Então, temos que chamar a função responsável por alterar o estado _setCount_ dentro das funções _inc_ e _dec_ para conseguirmos alterar o valor de _count_.
E vamos passar as funções _inc_ e _dec_ para o evento _onPress_ dentro do _buttons_:

``` JSX
import React, { useState } from "react";
import { Text, Button } from "react-native";

import Style from "./style";

const Counter = () => {
  const [count, setCount] = useState(0);

  function dec() {
    setCount(count - 1)
  }

  function inc() {
    setCount(count + 1)
  }

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>{count}</Text>
      <Button 
        title="-1"
        onPress={dec}
      />
      <Button 
        title="+1"
        onPress={inc}
      />
    </React.Fragment>
  );
}

export default Counter;
```

- Podemos também receber o valor inicial/_initialValue_ e o passo/_step_ do nosso contador via _props_ assim:

``` JSX
import React, { useState } from "react";
import { Text, Button } from "react-native";

import Style from "./style";

const Counter = (props) => {  
  const [count, setCount] = useState(props.initialValue);

  function dec() {
    setCount(count - props.step)
  }

  function inc() {
    setCount(count + props.step)
  }

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>{count}</Text>
      <Button 
        title="-"
        onPress={dec}
      />
      <Button 
        title="+"
        onPress={inc}
      />
    </React.Fragment>
  );
}

export default Counter;
```

- Desse modo, podemos passar o valor inicial/_initialValue_ e o passo/_step_ do nosso contador via _props_ onde nosso componente _Counter_ está sendo renderizado(_App.js_):

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";
import Counter from "./components/Counter";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
      <Counter initialValue={100} step={5}/>
    </SafeAreaView>
  );
}

// [...]

export default App;
```

- Podemos também tomar o cuidado de _initialValue_ e _step_ tenham valores padrão caso não seja passado via props, assim:

``` JSX
import React, { useState } from "react";
import { Text, Button } from "react-native";

import Style from "./style";

const Counter = ({ initialValue = 0, step = 1 }) => {  
  const [count, setCount] = useState(initialValue);

  function dec() {
    setCount(count - step)
  }

  function inc() {
    setCount(count + step)
  }

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>{count}</Text>
      <Button 
        title="-"
        onPress={dec}
      />
      <Button 
        title="+"
        onPress={inc}
      />
    </React.Fragment>
  );
}

export default Counter;
```

### Comunição Direta

A nossa aplicação em React é uma árvore de componentes. Podemos quebrar nossa aplicação em múltiplos componentes sempre visando o reuso a organização. E dentro dessa árvore de componentes é muito comum que tenhamos uma comunição direta e indireta.

- Para exemplificarmos melhor dentro de src/components vamos criar uma pasta chamada direta/_direct_ e dentro dela vamos criar os componentes funcionais Pai/_Dad_ e Filho/_Child_. 
No componente Filho/_Child_ queremos receber um texto dentro de props(_porps.text_) e um número(_props.number_). Resumindo, vamos esperar receber esses três valores a partir do componente pai:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

const Child = (props) => {
  return (
    <>
      <Text style={Style.textDefault}>{props.text}</Text>
      <Text style={Style.textSecondary}>{props.number}</Text>
    </>
  );
}

export default Child;
```

- Como funciona a comunicação de um componente pai, para um componente filho? 
Passamos via **props(propriedades)** aquilo que queremos passar do pai para o filho. 
Até porquê há uma relação direta, pois dentro do pai há uma referência direta/intância para o componente filho(import do componente filho, de tal forma que conseguimos passar as props para o filho).
Dessa forma, vamos passar os valores de _text_ e _number_ para o componente _Child_:

``` JSX
import React from "react";

import Child from "./Child";

const Dad = (props) => {
  return (
    <Child text="Comunicação Direta" number={23}/>
  );
}

export default Dad;
```

- E para visualizarmos isso em tela, vamos importar o componente _Dad_ dentro do componente _App_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";
import Counter from "./components/Counter";
import Dad from "./components/direct/Dad";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
      <Counter initialValue={100} step={5}/>
      <Dad />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

### Comunição Indireta

A comunicação indireta, ocorre quando precisamos passar informações do componente filho para o componente pai. Mas o componente filho não tem uma referência direta com o componente pai, então não temo como via propriedades(porps) intânciar um componente pai(senão o pai passaria a ser filho e o filho passaria a ser pai).

- Para exemplificarmos melhor dentro de src/components vamos criar uma pasta chamada indireta/_indirect_  e nela os componentes funcionais Pai/_DadIndirect_ e Filho/_Child_.

- Vamos inserir dentro dos Componetes a extrutura básica de um Componente funcional. Lembrando que o componente _Dad_ leva a referência do componente filho:

``` JSX DadIndirect.js
import React from "react";
import { Text } from "react-native";

import Style from "../style";

import Child from "./Child";

const DadIndirect = (props) => {
  return (
    <>
      <Text style={Style.textDefault}>Comunicação Indireta</Text>
      <Child />
    </>
  );
}

export default DadIndirect;
```

``` JSX Child.js
import React from "react";
import { View } from "react-native";

const Child = (props) => {
  return (
    <View></View>
  );
}

export default Child;
```

- E vamos importar esse componente no nosso arquivo principal(_App.js_):

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";
import Counter from "./components/Counter";
import Dad from "./components/direct/Dad";
import DadIndirect from "./components/indirect/DadIndirect";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
      <Counter initialValue={100} step={5}/>
      <Dad />
      <DadIndirect />
    </SafeAreaView>
  );
}

// [...]
export default App;
```

- Vamos supor que no componente filho/_Child_ temos um botão, e quando clicarmos nele as informações vão ser enviadas para o componente pai/_DadIndirect_.

``` JSX
import React from "react";
import { Button } from "react-native";

const Child = (props) => {
  return (
    <Button 
      title="Enviar informações"
    />
  );
}

export default Child;
```

Mas de fato como é feito a comunicação do sentido do filho enviar dados para o pai? Já que o filho não tem nenhum tipo de comunicação direta com o pai, diferente do pai que tem o componente filho(dentro dele)... 
Fazemos isso com uma **função via props_**, ou seja, passamos uma função do pai/_DadIndirect_ para o filho/_Child_ e **quando o filho chamar essa função(acontece um evento)**, dessa forma, temos como passar informações para o pai.

- Agora, vamos criar uma função _numberRandom_ e ela receber os valores _min_ e _max_ e essa função vai gerar um número aleatório entre os valores _min_ e _max_ fornecidos.
E vamos adicionar o evento _onPress_ do button que vai receber uma function e chamar a função callback _numberRandom_ que vai pegar os valores de _props.min_ e _props.max_: 

``` JSX
import React from "react";
import { Button } from "react-native";

const Child = (props) => {

  function numberRandom(min, max) {
    return parseInt(Math.random() * (max - min) + min);
  }

  return (
    <Button 
      title="Enviar informações"
      onPress={function() {
        numberRandom(props.min, props.max)
      }}
    />
  );
}

export default Child;
```

- E como vamos devolver esse número gerado aleatóriamente para o componente pai/_DadIndirect_? Via props. Vamos enviar dentro da propriedade _function_ a função que irá exibir valor(_displayValue_) para o componente filho, além dos valores _min_ e _max_:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

import Child from "./Child";

const DadIndirect = (props) => {
  
  function displayValue(number) {
    console.log(number)
  }

  return (
    <>
      <Text style={Style.textDefault}>Comunicação Indireta</Text>
      <Child 
        min={1}
        max={60}
        function={displayValue}
      />
    </>
  );
}

export default DadIndirect;
```

- O que significa que dentro do filho vamos ter dentro de _props_ esse atributo _function_ e podemos chamá-la através de _props.function_. 
No button vamos rastrear o evento de click com o método _onPress_ e dentro vamos receber uma função que vai chamar a função callback _numberRandom_, essa função vai retornar um número que vamos armazenar dentro da constante _n_.
Em seguida, podemos passar esse número _n_ gerado aleatóriamente como parâmetro para a função _displayValue_ do componente pai que está dentro da propriedade function(_props.function_):

``` JSX
import React from "react";
import { Button } from "react-native";

const Child = (props) => {

  function numberRandom(min, max) {
    return parseInt(Math.random() * (max - min)) + min;
  }

  return (
    <Button 
      title="Enviar informações"
      onPress={function() {
        const n = numberRandom(props.min, props.max)
        props.function(n)
      }}
    />
  );
}

export default Child;
```

- E vamos receber esse valor no componente pai/_DadIndirect_ e mostrar na tela, mas para isso precisamos criar um estado para controlar esse valor:

``` JSX
import React, { useState } from "react";
import { Text } from "react-native";

import Style from "../style";

import Child from "./Child";

const DadIndirect = (props) => {

  const [state, setState] = useState(0);
  
  function displayValue(number) {
    setState(number)
  }

  return (
    <>
      <Text style={Style.textDefault}>Comunicação Indireta</Text>
      <Text style={Style.textSecondary}>{state}</Text>
      <Child 
        min={1}
        max={60}
        function={displayValue}
      />
    </>
  );
}

export default DadIndirect;
```

### Diferenciando iOS e Android 

- Para entendermos melhor como isso funciona, dentro de src/components vamos criar um componente funcional chamado Diferenciar/_Differentiate_ e nele vamos importar a API _Platform_ do react native:

``` JSX
import React from "react";
import { Text, Platform } from "react-native";

import Style from "./style";

const Differentiate = () => {
  return (
    <Text style={Style.textDefault}>Diferenciando iOS e Android</Text>
  );
}

export default Differentiate;
```

- E vamos fazer uma estrutura condicional para que quando o sistema operacional/_OS_ for igual a "android" vai renderizar na tela o texto ""Android" e se for "ios" vai renderizar o texto "iOS", e se não for nenhum dos dois, vai renderizar "Não Identificado!":

``` JSX
import React from "react";
import { Text, Platform } from "react-native";

import Style from "./style";

const Differentiate = () => {
  let platform = '';

  if (Platform.OS === 'android') {
    platform = "Android";
  } else if(Platform.OS === 'ios') {
    platform = "iOS"
  } else {
    platform = "Não identificado!"
  }

  return (
    <>
      <Text style={Style.textDefault}>Diferenciando iOS e Android</Text>
      <Text style={Style.textSecondary}>{platform}</Text>
    </>
  );
}

export default Differentiate;
```

- E para visualizarmos isso em tela, vamos importar esse componente _Differentiate_ no componente principal da aplicação(_App_):

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";
import Counter from "./components/Counter";
import Dad from "./components/direct/Dad";
import DadIndirect from "./components/indirect/DadIndirect";
import Differentiate from "./components/Differentiate";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
      <Counter initialValue={100} step={5}/>
      <Dad />
      <DadIndirect />
      <Differentiate />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

### Renderização condicional

- Para entendermos melhor como funciona, dentro de src/components vamos criar um componente funcional chamado ParImpar/_OddEven_:

``` JSX
import React from "react";
import { View, Text } from "react-native";

import Style from "./style";

const OddEven = (props) => {
  return (
    <View>
    
    </View>
  );
}

export default OddEven;
```

- Vamos receber um número/_number_ via vamos renderizar trechos de JSX condicionalmente usandando operadores ternários. Se _number_ for par então(?) será exibido um _Text Par_ senão(:) _Text Ímpar_. Inicialmente _number_ vai ser 0:

``` JSX
import React from "react";
import { View, Text } from "react-native";

import Style from "./style";

const OddEven = ({number = 0}) => {
  return (
    <View>
      <Text style={Style.textDefault}>
        Renderização Condicional de Código JSX. Solução: Operadores Ternários.
      </Text>
      {number % 2 === 0
        ? <Text style={Style.textSecondary}>Par</Text>
        : <Text style={Style.textSecondary}>Ímpar</Text>
      }
    </View>
  );
}

export default OddEven;
```

- E vamos importar esse componente _OddEven_ no componente _App_ e instânciá-lo passando o valor para _number_ via props:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";
import Counter from "./components/Counter";
import Dad from "./components/direct/Dad";
import DadIndirect from "./components/indirect/DadIndirect";
import Differentiate from "./components/Differentiate";
import OddEven from "./components/OddEven";

const App = () => {
  // console.warn("Opa!")

  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
      <Counter initialValue={100} step={5}/>
      <Dad />
      <DadIndirect />
      <Differentiate />
      <OddEven number={3}/>
    </SafeAreaView>
  );
}

// [...]

export default App;
```

### Componente com filho(props.children)

Quando quisermos referênciar um componente dentro de outro, vamos usar props.children, para resgatar os filhos que são passados dentro de determinado componente(componentes passados dentro do corpo de outro componente).

- Para entendermos melhor essa relação, dentro de src/components vamos criar uma pasta chamada relação/_relationship_ e nessa pasta vamos criar os componentes funcionais pai/_DadRelationship_ e o filho/_ChildRelationship_. Lembrando que o componente _DadRelationship_ leva a referência do componente filho e nesse caso o filho vai receber do pai via props _name_ e _surname_:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

import ChildRelationship from "./ChildRelationship";

const DadRealationship = (props) => {
  return (
    <>
      <Text style={Style.textDefault}>Componente com filhos</Text>
      <ChildRelationship name="Nathallye" surname="Tavares"/>
      <ChildRelationship name="Paulo" surname="Bacelar"/>
    </>
  );
}

export default DadRealationship;
```

``` JSX
import React, { useState } from "react";
import { Text } from "react-native";

import Style from "../style";

const ChildRelationship = (props) => {
  return (
    <Text style={Style.textDefault}>
      {props.name} {props.surname}
    </Text>
  );
}

export default ChildRelationship;
```

- E para visualizarmos isso em tela, vamos importar o componente _DadRealationship_ dentro do componente _App_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";
import Counter from "./components/Counter";
import Dad from "./components/direct/Dad";
import DadIndirect from "./components/indirect/DadIndirect";
import Differentiate from "./components/Differentiate";
import OddEven from "./components/OddEven";
import DadRealationship from "./components/relationship/DadRelationship";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
      <Counter initialValue={100} step={5}/>
      <Dad />
      <DadIndirect />
      <Differentiate />
      <OddEven number={3}/>
      <DadRealationship />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

- Mas se quisermos enviar desses dados dos filhos pelo componente principal(_App_)? Vamos importar Tanto o componente Pai quando o seu filho dentro de _App.js_. E vamos enviar as propriedades no componente filho, assim:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import DadRealationship from "./components/relationship/DadRelationship";
import ChildRelationship from "./components/relationship/ChildRelationship";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <DadRealationship>
        <ChildRelationship name="Nathallye" surname="Tavares"/>
        <ChildRelationship name="Paulo" surname="Bacelar"/>        
      </DadRealationship>
    </SafeAreaView>
  );
}

// [...]

export default App;
```

- E como conseguirmos mostrar o que está sendo enviado dentro do componente _App_? A partir das propriedades/_props_ que estamos recendo como parâmetro dentro do componente _DadRelationship_. Vamos pegar os filhos que estão sendo enviados via props para esse componente(_props.children_):

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

import ChildRelationship from "./ChildRelationship";

const DadRealationship = (props) => {
  return (
    <>
      <Text style={Style.textDefault}>Componente com filhos</Text>
      {props.children}
    </>
  );
}

export default DadRealationship;
```

### Renderizando Lista #01

- Para entendermos melhor, em src/components vamos criar pasta chamada _products_ e dentro dela um arquivo js chamado _products_.

- Nesse arquivo vamos retornar um array de objetos e vamos exportá-lo por padrão:

``` JS
export default [
  { id: 1, name: "Caderno", price: 19.99 },
  { id: 2, name: "Caneta", price: 1.99 },
  { id: 3, name: "Lápis", price: 1.99 },
  { id: 4, name: "Borracha", price: 1.20 },
  { id: 5, name: "Apontador", price: 3.99 }
]
```

- Temos os dados, e a idéia é transformar esses dados em elementos visuais na tela. Para isso, em src/components/products vamos criar um componente funcional chamando _ListProducts_:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

const ListProducts = () => {
  return (
    <Text style={Style.textDefault}>
      Lista de Produtos
    </Text>
  );
}

export default ListProducts;
```

- E para visualizarmos em tela as alterações, vamos importar o componente _ListProducts_ dentro do componente _App_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";
import Counter from "./components/Counter";
import Dad from "./components/direct/Dad";
import DadIndirect from "./components/indirect/DadIndirect";
import Differentiate from "./components/Differentiate";
import OddEven from "./components/OddEven";
import DadRealationship from "./components/relationship/DadRelationship";
import ChildRelationship from "./components/relationship/ChildRelationship";
import ListProducts from "./components/products/ListProducts";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
      <Counter initialValue={100} step={5}/>
      <Dad />
      <DadIndirect />
      <Differentiate />
      <OddEven number={3}/>
      <DadRealationship>
        <ChildRelationship name="Nathallye" surname="Tavares"/>
        <ChildRelationship name="Paulo" surname="Bacelar"/>        
      </DadRealationship>
      <ListProducts />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

- Agora, dentro do componente _ListProducts_ vamos importar o arquivo com os produtos(_products.js_).:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProducts = () => {
  return (
    <Text style={Style.textDefault}>
      Lista de Produtos
    </Text>
    
  );
}

export default ListProducts;
```

Em seguida, para percorrer essa lista de produtos/_products_ e renderizar em tela, vamos utilizar o método _map_(transforma um array em um novo array com elementos modificados). E para esse _map_ para cada produto percorrido/_product_ vamos passar uma função que vai retornar um trecho JSX interpolando as informações do produto.
Com isso, ele vai transformar o array de objetos, em um novo array com trechos JSX:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProducts = () => {
  return (
    <>
      <Text style={Style.textDefault}>
        Lista de Produtos
      </Text>

      {products.map(product => {
        return (
          <Text>{product.id}) {product.name} tem preço R${product.price}</Text>
        )
      })}

    </>
  );
}

export default ListProducts;
```

- A lista está sendo renderizada, mas no log podemos notar a seguinte advertência "Each child in a list should have a unique "key" prop", isso ocorre, pois sempre que geramos uma lista de elementos o React solicita que seja definido o atributo _key_ que deve ter um valor único, para caso ocorra alguma mudança o React consegue de forma muito precisa alterar apenas aquele elemento modificado. Nesse caso podemos usar o _id_ do _product_:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProducts = () => {
  return (
    <>
      <Text style={Style.textDefault}>
        Lista de Produtos
      </Text>

      {products.map(product => {
        return (
          <Text key={product.id}>
            {product.id}) {product.name} tem preço R${product.price}
          </Text>
        )
      })}

    </>
  );
}

export default ListProducts;
```

- Outra forma de exibir essa lista é criando uma função, chamada de _getList_ por exemplo, e dentro dela podemos retornar o _map_ no array de objetos _products_, o qual para cada elemento/_product_ que ele percorrer vai ser passada uma função que vai retornar um trecho JSX interpolando as informações do produto.
E dentro do JSX vamos chamar essa função. Essa função vai ser chamada no momento em que o componente for renderizado:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProducts = () => {

  function getList() {
    return products.map(product => {
      return (
        <Text key={product.id} style={Style.textSecondary}>
          {product.id}) {product.name} tem preço R${product.price}
        </Text>
      )
    })
  }

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>
        Lista de Produtos
      </Text>

      {getList()}
    </React.Fragment>
  );
}

export default ListProducts;
```

### Renderizando Lista com o Componente FlatList

- Para entendermos melhor como funciona esse componente, vamos duplicar o componente _ListProducts_ e renomear a cópia para _ListProductsV2_:

``` JSX
import React from "react";
import { Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProductsV2 = () => {

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>
        Lista de Produtos V2
      </Text>
    </React.Fragment>
  );
}

export default ListProductsV2;
```

- E em seguida, vamos importar esse novo componente dentro do componente principal _App.js_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

import First from "./components/First";
import MinMax from "./components/MinMax";
import Random from "./components/Random";
import Fragment from "./components/Fragment";
import Btn from "./components/Btn";
import Counter from "./components/Counter";
import Dad from "./components/direct/Dad";
import DadIndirect from "./components/indirect/DadIndirect";
import Differentiate from "./components/Differentiate";
import OddEven from "./components/OddEven";
import DadRealationship from "./components/relationship/DadRelationship";
import ChildRelationship from "./components/relationship/ChildRelationship";
import ListProducts from "./components/products/ListProducts";
import ListProductsV2 from "./components/products/ListProductsV2";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      <Text style={Style.textDefault}>Olá mundo!</Text>
      <First />
      <MinMax min={10} max={20} />
      <Random min={0} max={100}/>
      <Fragment />
      <Btn />
      <Counter initialValue={100} step={5}/>
      <Dad />
      <DadIndirect />
      <Differentiate />
      <OddEven number={3}/>
      <DadRealationship>
        <ChildRelationship name="Nathallye" surname="Tavares"/>
        <ChildRelationship name="Paulo" surname="Bacelar"/>        
      </DadRealationship>
      <ListProducts />
      <ListProductsV2 />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

- Agora, voltando no componente _ListProductsV2_ vamos importar o componente _FlatList_ do react native e referênciá-lo:

``` JSX
import React from "react";
import { FlatList, Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProductsV2 = () => {

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>
        Lista de Produtos V2
      </Text>
      <FlatList />
    </React.Fragment>
  );
}

export default ListProductsV2;
```

- Será necessário passar alguns atributos para ele... o atributo _data_ que serão os dados, nesse caso são os produtos/_products_, definido esse atributo _data_ podemos definir o atributo _renderItem_... o atributo _renderItem_ vai receber uma função(pode ser uma arrow function), e essa função vai receber uma atributo e dentro desse atributo teremos o _item_({item}) que será percorrido na lista:

``` JSX
import React from "react";
import { FlatList, Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProductsV2 = () => {

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>
        Lista de Produtos V2
      </Text>

      <FlatList 
        data={products}
        renderItem={({ item: product }) => { // podemos alterar o nome do atributo item para product, por exemplo.
          
        }}
      />
    </React.Fragment>
  );
}

export default ListProductsV2;
```

- Por fim, a função vai retornar/_return_ o JSX concatenando as informações de _item_/_product_:

``` JSX
import React from "react";
import { FlatList, Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProductsV2 = () => {

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>
        Lista de Produtos V2
      </Text>

      <FlatList 
        data={products}
        renderItem={({ item: product }) => { 
          return (
            <Text style={Style.textSecondary}>
              {product.id}) {product.name} tem preço R${product.price}
            </Text>
          )      
        }}
      />
    </React.Fragment>
  );
}

export default ListProductsV2;
```

- Também vamos precisar irformar uma chave/_key_ por meio do atributo _keyExtractor_, que na verdade é uma função, e basicamente essa função vai receber o item/_i_ e vai retornar o que será a chave, nesse caso será o _id_(_i.id_). Nesse caso, ele vai reclamar, pois espera um valor do tipo _string_ e para contornar isso podemos interpolar o valor _i.id_:

``` JSX
import React from "react";
import { FlatList, Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProductsV2 = () => {

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>
        Lista de Produtos V2
      </Text>

      <FlatList 
        data={products}
        // keyExtractor={i => i.id}
        keyExtractor={i => `${i.id}`}
        renderItem={({ item: product }) => { 
          return (
            <Text style={Style.textSecondary}>
              {product.id}) {product.name} tem preço R${product.price}
            </Text>
          )      
        }}
      />
    </React.Fragment>
  );
}

export default ListProductsV2;
```

- Podemos também abstrair tudo que está dentro do atributo _renderItem_ para uma função e em seguida chamar ela dentro dele:

``` JSX
import React from "react";
import { FlatList, Text } from "react-native";

import Style from "../style";

import products from "./products";

const ListProductsV2 = () => {

  const renderProduct = ({ item: product }) => { 
    return (
      <Text style={Style.textSecondary}>
        {product.id}) {product.name} tem preço R${product.price}
      </Text>
    )      
  }

  return (
    <React.Fragment>
      <Text style={Style.textDefault}>
        Lista de Produtos V2
      </Text>

      <FlatList 
        data={products}
        keyExtractor={i => `${i.id}`}
        renderItem={renderProduct}
      />
    </React.Fragment>
  );
}

export default ListProductsV2;
```

### Componente Controlado

- Para entendermos melhor como funciona um componente controlado, dentro da pasta componentes vamos criar um componente funcional chamado _Input_:

``` JSX
import React from "react";
import { View } from "react-native";

import Style from "./style";

const Input = (props) => {
  return (
    <View>
      
    </View>
  );
}

export default Input;
```

- Em seguida, para visualizarmos em tela, vamos importar esse componente dentro do arquivo de renderização principal(_App.js_):

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

// [...]
import Input from "./components/Input";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      {/*...*/}

      <Input />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

- Vamos importar o componente _TextInput_ e referênciá-lo dentro da _View_ desse componente funcional _Input_.
O _TextInput_ é um componente fundamental para inserir texto no aplicativo por meio de um teclado. Adereços fornecem configuração para vários recursos, como correção automática, capitalização automática, texto de espaço reservado e diferentes tipos de teclado, como um teclado numérico:

``` JSX
import React from "react";
import { TextInput, View } from "react-native";

import Style from "./style";

const Input = (props) => {
  return (
    <View>
      <TextInput />
    </View>
  );
}

export default Input;
```

- Vamos definir algumas propriedades nesse _TextInput_, como o _placeholder_ para criar um campo que já conseguimos inserir dados.
Agora, temos aqui inicialmente um componente não controlado:

``` JSX
import React from "react";
import { TextInput, View } from "react-native";

import Style from "./style";

const Input = (props) => {
  return (
    <View>
      <TextInput 
        placeholder="Digite seu nome"
      />
    </View>
  );
}

export default Input;
```

- E para criarmos um componente controlado. No componente _Input_ vamos definir uma variável com estato. Vamos importar o _useState_ do React e criar uma variável com o destructuring, sendo que a primeira posição vai receber o valor inicial e a segunda posição vai receber a função _set_ para alterar a variável. 
Em seguida, podemos inserir no _TextInput_ o atributo _value_ que vai receber a variável de estado _state_:

``` JSX
import React, { useState } from "react";
import { TextInput, View } from "react-native";

import Style from "./style";

const Input = (props) => {
  const [state, setState] = useState("Teste");

  return (
    <View>
      <TextInput 
        placeholder="Digite seu nome"
        value={state}
      />
    </View>
  );
}

export default Input;
```

- Podemos notar no Android Studio o componente _Input_ está com o valor que definimos inicialmente. Mas como é um componente controlado não conseguimos alterar o valor do input. O que ele chama de verdade absoluta são os dados, ou seja, o estado do componente não mudou, não foi chamada em nenhum momento a função _setState_ para mudar o dado. Resumindo, não conseguimos mudar o estado de um componente diretamente a partir da interface, primeiro temos que mudar o estado, para quando esse estado mudar aí sim conseguimos refletir essa mudança na interface gráfica. O caminho é unidirecional, o estado muda e altera a interface gráfica. A interface gráfica não altera o estado(isso acontece indiretamente a partir dos eventos).

- Então, nesse caso, como conseguimos alterar o valor do input? Podemos mudar ele pegando o evento _onChangeText_, esse evento vai ser chamado toda vez que digitarmos. E esse evento vai receber como parâmentro exatamente o texto atual(que está dentro de _state_) que vai chamar por uma função arrow a função callback _setState_ e passar para ela o estado atual/_state_:

``` JSX
import React, { useState } from "react";
import { TextInput, View } from "react-native";

import Style from "./style";

const Input = (props) => {
  const [state, setState] = useState("Teste");

  return (
    <View>
      <TextInput 
        placeholder="Digite seu nome"
        value={state}
        onChangeText={state => setState(state)}
      />
    </View>
  );
}

export default Input;
```

### Flexbox

Um elemento passa a ser um flexbox quando marcamos com a propriedade _display: flex_ e ele passa a ser um _flex-container_.

[image!](x-special/nautilus-clipboardcopyfile:///home/nathallye/Downloads/WhatsApp%20Image%202022-06-09%20at%2016.07.25.jpeg)

Dentro desse container temos os _flex items_.
O eixo principal desse container chamamos de _main axis_ e o eixo adjacente/alternativo/do outro sentido _cross axis_.

### Componente Quadrado

- Para facilitar o entendimento, dentro de src/components vamos criar uma pasta chamada _layout_ e dentro dela vamos criar um componente funcional chamado Quadrado/_Square_:

``` JSX
import React from "react";
import { View } from "react-native";

import Style from "./style";

const Square = (props) => {
  return (
    <View>

    </View>
  );
}

export default Square;
```

- Em seguida, vamos aplicar a propriedade _style_ na _View_ que vai receber um obejto de estilo e nele vamos definir o _height_ e _width_ de 50 para o elemento ficar quadrado e um _blackground_ para visualizarmos melhor:

``` JSX
import React from "react";
import { View } from "react-native";

const Square = (props) => {
  return (
    <View style={{
      height: 50,
      width: 50, 
      backgroundColor: "#000"
    }}
    />
  );
}

export default Square;
```

- Só que, vamos receber a cor do componente via props e caso não seja passada a cor/_color_, vai ser usada a cor default:

``` JSX
import React from "react";
import { View } from "react-native";

const Square = (props) => {
  return (
    <View style={{
      height: 50,
      width: 50, 
      backgroundColor: props.color || "#000"
    }}
    />
  );
}

export default Square;
```

- Vamos importar esse componente _Square_ dentro do componente de renderização principal e passar a cor/_color_ via props:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

// [...]
import Square from "./components/layout/Square";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      {/*...*/}
      <ListProducts />
      <ListProductsV2 />
      <Input />
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </SafeAreaView>
  );
}

// [...]

export default App;
```

### Usando Flexbox #01

- Dentro de src/components/layout vamos criar um componente funcional chamado _FlexboxV1_:

``` JSX
import React from "react";
import { View } from "react-native";

const FlexboxV1 = (props) => {
  return (
    <View>

    </View>
  );
}

export default FlexboxV1;
```

- Em seguida, vamos mover de dentro de App.js os componentes _Square_(vamos importar o componente _Square_ para que tudo ocorra sem erros):

``` JSX
import React from "react";
import { View } from "react-native";

import Square  from "./Square";

const FlexboxV1 = (props) => {
  return (
    <View>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

export default FlexboxV1;
```

- Após isso, vamos importar o _StyleSheet_ do react native dentro desse componente  _FlexboxV1_.
E criar um objeto de estilo que vamos armazenar dentro da constante chamada _styles_ e dentro desse objeto de _styles_ vamos criar um objeto com o nome _FlexV1_ que vamos referênciar através do _style_ dentro da _View_:

``` JSX
import React from "react";
import { StyleSheet, View } from "react-native";

import Square  from "./Square";

const FlexboxV1 = (props) => {
  return (
    <View style={styles.FlexV1}>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

const styles = StyleSheet.create({
  FlexV1: {
    
  }
});

export default FlexboxV1;
```

- E dentro do componente de renderização principal vamos importar esse componente _FlexboxV1_ no lugar de onde estava o componente _Square_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView, Text } from "react-native";

import Style from "./components/style";

// [...]
// import Square from "./components/layout/Square";
import FlexboxV1 from "./components/layout/FlexboxV1";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      {/* ... */}
      <FlexboxV1 />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

#### Propriedade flex 1 ou flexGrow 1

- Antes de tudo, vamos aplicar um backgroundColor _black_ no objeto _FlexV1_ que vai refletir na _View_ para visualizarmos melhor as alterações:

``` JSX
import React from "react";
import { StyleSheet, View } from "react-native";

import Square  from "./Square";

const FlexboxV1 = (props) => {
  return (
    <View style={styles.FlexV1}>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

const styles = StyleSheet.create({
  FlexV1: {
    backgroundColor: "black",
  }
});

export default FlexboxV1;
```

- Quando usamos a propriedade _flex 1_ ou _flexGrow 1_ significa que essa View/container vai crescer até ocupar todo espaço disponível em tela:

``` JSX
import React from "react";
import { StyleSheet, View } from "react-native";

import Square  from "./Square";

const FlexboxV1 = (props) => {
  return (
    <View style={styles.FlexV1}>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

const styles = StyleSheet.create({
  FlexV1: {
    backgroundColor: "black",
    flex: 1,
  }
});

export default FlexboxV1;
```

#### justifyContent

- Para trabalharmos com alinhamento em relação ao Eixo Principal/_main axis_(que nesse caso é a coluna/_column_) usamos o _justifyContent_. E essa propriedade tem algumas possibilidades, o padrão é o _flex-start_ que alinha os elementos/_flex items_ ao início do container(de cima para baixo), se usarmos o _flex-end_ todos serão alinhados ao final do container(de baixo para cima), e o _space-evenly_ vai separar os _items_ e espassar eles de forma igualitária(incluindo espaçamento no inicio e no fim):

``` JSX
import React from "react";
import { StyleSheet, View } from "react-native";

import Square  from "./Square";

const FlexboxV1 = (props) => {
  return (
    <View style={styles.FlexV1}>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

const styles = StyleSheet.create({
  FlexV1: {
    backgroundColor: "black",

    flex: 1,
    justifyContent: "space-evenly",
  }
});

export default FlexboxV1;
```

### Usando Flexbox #02

- Dentro de src/components/layout vamos criar um componente funcional chamado _FlexboxV2_:

``` JSX
import React from "react";
import { StyleSheet, View } from "react-native";

import Square  from "./Square";

const FlexboxV2 = (props) => {
  return (
    <View style={styles.FlexV2}>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

const styles = StyleSheet.create({
  FlexV2: {
    backgroundColor: "black",
  }
});

export default FlexboxV2;
```

- E dentro do componente de renderização principal vamos importar esse componente _FlexboxV2_ no lugar de onde estava o componente _FlexboxV1_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView } from "react-native";

import Style from "./components/style";

// [...]
// import Square from "./components/layout/Square";
import FlexboxV1 from "./components/layout/FlexboxV1";
import FlexboxV2 from "./components/layout/FlexboxV2";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      {/* ... */}
      <FlexboxV2 />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

- E para visualizarmos melhor como podemos organizar os elementos no eixo cruzado/_cross axis_(que nesse caso é no eixo da linha/_row_) vamos inserir uma largura/_width_ de 100%:

``` JSX
import React from "react";
import { StyleSheet, View } from "react-native";

import Square  from "./Square";

const FlexboxV2 = (props) => {
  return (
    <View style={styles.FlexV2}>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

const styles = StyleSheet.create({
  FlexV2: {
    backgroundColor: "black",

    width: "100%",
  }
});

export default FlexboxV2;
```

#### alignItemns

E para mecher no alinhamento dos elementos/_flex items_ no eixo cruzado/_cross axis_(que nesse caso é no eixo da linha/_row_) vamos usar a propriedade _alingItems_. E essa propriedade tem algumas possibilidades, o padrão é o _flex-start_ que alinha os elementos/_flex items_ ao início do container(da direita pra esquerda), e o _flex-end_ irá alinhar os elementos ao final do container(no final da linha) e o _center_ ao centro:

``` JSX
import React from "react";
import { StyleSheet, View } from "react-native";

import Square  from "./Square";

const FlexboxV2 = (props) => {
  return (
    <View style={styles.FlexV2}>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

const styles = StyleSheet.create({
  FlexV2: {
    backgroundColor: "black",

    width: "100%",
    alignItems: "center",
  }
});

export default FlexboxV2;
```

### Usando Flexbox #03

- Dentro de src/components/layout vamos criar um componente funcional chamado _FlexboxV3_:

``` JSX
import React from "react";
import { StyleSheet, View } from "react-native";

import Square  from "./Square";

const FlexboxV3 = (props) => {
  return (
    <View style={styles.FlexV3}>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

const styles = StyleSheet.create({
  FlexV3: {
    backgroundColor: "black",

  }
});

export default FlexboxV3;
```

- E dentro do componente de renderização principal vamos importar esse componente _FlexboxV3_ no lugar de onde estava o componente _FlexboxV2_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView } from "react-native";

import Style from "./components/style";

// ...
import FlexboxV3 from "./components/layout/FlexboxV3";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      {/* ... */}
      <FlexboxV3 />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

#### flexDirection 

- Essa propriedade vai definir qual o eixo principal do container(no caso do mobile o eixo principal por padrão é a coluna/_column_):

``` JSX
import React from "react";
import { StyleSheet, View } from "react-native";

import Square  from "./Square";

const FlexboxV3 = (props) => {
  return (
    <View style={styles.FlexV3}>
      <Square color="#ff801a"/>
      <Square color="#50d1f6"/>
      <Square color="#dd22c1"/>
      <Square color="#8312ed"/>
      <Square color="#36c9a7"/>
    </View>
  );
}

const styles = StyleSheet.create({
  FlexV3: {
    backgroundColor: "black",

    height: 350, // para melhorar a visualização do container
    width: "100%", // para melhorar a visualização do container

    flexDirection: "row",
  }
});

export default FlexboxV3;
```

### Componente de Classe: Método Render

Classe, nada mais é que uma forma diferente de escreve função.

Para entendermos melhor como funciona um componente baseado em classe, dentro da pasta src/components vamos criar uma pasta chamada _componente-class_ e dentro dela vamos criar um componente chamado Megasena.js.

- Vamos inserir dentro do Componete a extrutura básica de um Componente baseado em Classe: 

``` JSX
import React, { Component } from "react";
import { Text } from "react-native";

import Style from "../style";

class Megasena extends Component { // se não quisermos importar o Component do react podemos usar o React.Component
  
}

export default Megasena;
```

- Vale ressaltar que a função render é obrigatória em um componente baseado em classe para renderizar algo na tela:

``` JSX
import React, { Component } from "react";
import { Text } from "react-native";

import Style from "../style";

class Megasena extends Component { // se não quisermos importar o Component do react podemos usar o React.Component
  
}

export default Megasena;
```

- E para visualizarmos em tela vamos importar esse componente baseado em classe no componente de renderização principal da nossa aplicação(App):

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView } from "react-native";

import Style from "./components/style";

// [...]
import Megasena from "./components/componente-class/Megasena";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      {/* ... */}
      <Megasena />
    </SafeAreaView>
  );
}

// [...]

export default App;
```

### Componente de Classe: Passando Props

- Vamos passar para esse componente a quanridade de números que serão sorteados na megasena, então em App.js na referência ao componente _Megasena_ vamos passar um atributo _quantNumeros_:

``` JSX
import React from "react";
import { StyleSheet, SafeAreaView } from "react-native";

import Style from "./components/style";

// [...]
import Megasena from "./components/componente-class/Megasena";

const App = () => {
  return (
    <SafeAreaView style={styles.App}>
      {/* ... */}
      <Megasena quantNumeros={7}/>
    </SafeAreaView>
  );
}
```

- E agora, como podemos pegar essa propriedade que foi passada para o nosso componente baseado em classe? 
Podemos acessar ele a partir de _props_, só que **não diretamente props**, vamos usar o _this.props_, ou seja, **as propriedades que pertecem a instância dessa classe(this aponta para a instância/objeto atual)**:

``` JSX
import React, { Component } from "react";
import { Text } from "react-native";

import Style from "../style";

class Megasena extends Component {
  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.props.quantNumeros}</Text>
      </React.Fragment>
    );
  }
}

export default Megasena;
```

### Componente de Classe: Estado

- E como definimos estado dentro de um componente baseado em classe? 
Podemos definir o _state_ como propriedade e essa propriedade pode ser definida como um _objeto_(no caso da função também podemos ter um objeto, usando o hook useState e atribuir um objeto dentro dele). 
Aqui no caso temos um único estado que é o state acessando-o a partir da classe, e dentro dele vamos colocar todos os atributos necessários para nossa megasena. Inicialmente, o _state_ vai ter a _quantNumeros_ e ele vai inicializar com o valor que recebemos via _this.props_:

``` JSX
import React, { Component } from "react";
import { Text } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.props.quantNumeros}</Text>
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- E onde estamos renderizando diretamente o valor que recebemos a partir de _this.props.quantNumeros_ vamos passar a renderizar o valor de dentro do _state_ por meio do _this.state.quantNumeros_:

``` JSX
import React, { Component } from "react";
import { Text } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- Próximo passo, vamos inserir um _TextInput_ para enviarmos a quantidade de números/_quantNumeros_ que queremos sortear. 
Nesse _TextInput_ vamos aplicar as seguintes propriedades: _placeholder_ para criar visualizarmos a caixinha que devemos inserir essa quantidades; _value_ esse valor vai estar associado ao estado do componente, ou seja, _this.state.quantNumeros_ e aqui ele passa a ser um componente controlado e para alterarmos o valor associado a esse componente, primeiro alteramos o estado dele e dessa forma ele atualiza a interface gráfica... e vamos aterar o estado a partir do método/evento _onChangeText_ nesse método recebemos o novo _input_ que foi digitado e apartir desse texto chamamos uma função que recebe a função callback que irá alterar o estado do componente(nesse caso vamos criar uma função chamada _alterarQuantNumeros_):

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          placeholder="Quantidade de Números"
          value={this.state.quantNumeros}
          onChangeText={ input =>  }
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- Agora, vamos criar a função chamada _alterarQuantNumeros_ que vai receber o _input_ e vai alterar o valor da _quantNumeros_. 
Nessa função vamos alterar a _quantNumeros_ ou seja, alterar _state_. Assim como, no useState temos uma função que altera o estado, aqui dentro da classe também vamos ter **uma função para alterar o estado**, e o nome dela é _setState_. 
Então, temos que chamar essa função _setState_ dentro da função _alterarQuantNUmero_ para conseguirmos alterar o valor.
Em seguida, dentro da função _setState_ vamos passar um novo objeto para state(já que ele é um objeto), e nesse objeto vamos passar o atributo que queremos alterar(nesse caso é _quantNumeros_ que vai receber o valor que recebemos no parâmetro _input_ como novo valor):

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
  }

  alterarQuantNumeros(input) {
    this.setState({ quantNumeros: input })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          placeholder="Quantidade de Números"
          value={this.state.quantNumeros}
          onChangeText={ input => }
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- Em seguida, no método _onChangeText_ do nosso _TextInput_ vamos chamar a função _alterarQuantNumeros_ e passar como parâmetro o valor recebido no _input_:

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
  }

  alterarQuantNumeros(input) { 
    this.setState({ quantNumeros: input })
  }
  // alterarQuantNumeros = (input) => { 
    // this.setState({ quantNumeros: input })
  // }


  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          placeholder="Quantidade de Números"
          value={this.state.quantNumeros}
          onChangeText={ input => this.alterarQuantNumeros(input) }  // Para evitar um erro do this não apontar para a instância correta, vamos utilizar uma arrow function, ou ao invés de colocar uma função arrow aqui, podemos transformar a diretamente função alterarQuantNumeros em em uma arrow function, como demostrado no comentário acima
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

### Componente Mega-Sena #01

- Vamos querer também controlar o estado dos _numerosGerados_ e inicialment eles vão iniciar com um array vazio:

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros(input) {
    this.setState({ quantNumeros: input })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={this.state.quantNumeros}
          onChangeText={ input => this.alterarQuantNumeros(input) } // Para evitar um erro do this não apontar para a instância correta, vamos utilizar uma arrow function
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- Agora, vamos corrigir o erro de que no _value_ do _TextInput_ ele espera um valor do tipo _string_ e para converter esse número(valor numérico) em uma string vamos interpolar usando batik(``):

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { // Para evitar um erro do this não apontar para a instância correta, vamos utilizar arrow function
    this.setState({ quantNumeros: input })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- E como vamos receber o _input_ como um valor do tipo _string_ temos que converte-lo para um valor numérico, e conseguimos fazer isso apenas colocando um símbolo de _+_ na frente do valor que estamos passando:

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { // Para evitar um erro do this não apontar para a instância correta, vamos utilizar arrow function
    this.setState({ quantNumeros: +input })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- Agora, vamos fazer a parte de gerar os números de forma aleatória. Para isso, vamos criar uma função a qual vai receber como parâmetro um array de numeros/_nums_ e dentro dela vamos criar uma constante chamada _novo_ que vai receber um novo número que não está contido dentro do array _nums_, esse número alatório vai ser gerado a partir do método _Random_ o qual vai ser multiplicado por 60(o valor máximo que pode ser gerado):

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { 
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- E se o número _novo_ gerado já tiver incluso dentro do array _nums_ a função vai ser chamada novamente e passar novamente os _nums_, mas caso não esteja incluso vai ser retornado o número _novo_:

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { 
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- Agora, vamos criar a função _gerarNumeros_ a qual vai alterar o estado do array _numerosGerados_:

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { 
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    this.setState({ numerosGerados: [] })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- E vamos criar uma constante chamada _numerosGerados_ a qual vai receber um novo objeto _Array_ e iremos usar o método _fill_ para criar um array com o número de posições passadas para _quantNumeros_(this.state.quantNumeros) e apartir disso conseguimos chamar a função _reduce_:

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { 
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    const numerosGerados = Array(this.state.quantNumeros).fill().reduce()
    this.setState({ numerosGerados: [] })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- E agora, a partir do método _reduce_ vamos receber o array de números que vamos chamar de _n_ e vamos retornar a partir dele os números atuais(usando o operador spreed para pegar todos que já foram recebidos _...n_) e mais o novo número gerado a partir da função _gerarNumeroNaoContido_ passando o array de números já existente(_n_) como parâmetro para essa função:

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { // Para evitar um erro do this não apontar para a instância correta, vamos utilizar arrow function
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    const numerosGerados = Array(this.state.quantNumeros)
      .fill()
      .reduce(n => [...n, this.gerarNumeroNaoContido(n)], [])

    this.setState({ numerosGerados: [] })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- E agora, podemos passar esse array de _numeros_ gerado para alterar o estado do _numerosGerados_:

``` JSX
import React, { Component } from "react";
import { Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { // Para evitar um erro do this não apontar para a instância correta, vamos utilizar arrow function
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    const numerosGerados = Array(this.state.quantNumeros)
      .fill()
      .reduce(n => [...n, this.gerarNumeroNaoContido(n)], [])

    this.setState({ numerosGerados: numerosGerados }) // OU podemos colocar apenas ({ numerosGerados }), já ambos tem o mesmo nome
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- E agora, uma vez que chamarmos a função _gerarNumeros_ automáticamente esse novo array será setado. E para essa função ser chamada, vamos criar um componente _Button_ com o _title_ de "Gerar" e o evento _onPress_ que irá chamar essa função _gerarNumeros_(this.gerarNumeros):

``` JSX
import React, { Component } from "react";
import { Button, Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { // Para evitar um erro do this não apontar para a instância correta, vamos utilizar arrow function
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    const numerosGerados = Array(this.state.quantNumeros)
      .fill
      .reduce(n => [...n, this.gerarNumeroNaoContido(n)], [])

    this.setState({ numerosGerados: numerosGerados })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
        <Button 
          title="Gerar"
          onPress={this.gerarNumeros}
        /> 
      </React.Fragment>
    );
  }
}

export default Megasena;
```


- Então, vamos criar um novo componente _Text_ e dentro dele interpolar os _numerosGerados_ e como é um array vamos usar o método _join(',')_ para separar os números por virgula e visualizarmos melhor em tela:

``` JSX
import React, { Component } from "react";
import { Button, Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { // Para evitar um erro do this não apontar para a instância correta, vamos utilizar arrow function
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    const numerosGerados = Array(this.state.quantNumeros)
      .fill()
      .reduce(n => [...n, this.gerarNumeroNaoContido(n)], [])

    this.setState({ numerosGerados: numerosGerados })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
        <Button 
          title="Gerar"
          onPress={this.gerarNumeros}
        /> 
        <Text>
          { this.state.numerosGerados.join(',') }
        </Text>
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- E para ordenar os números sorteados podemos usar o método _sort_ o qual vai receber os valor _a_ e _b_ e vai ordenar como _a - b_ com esse critério ele vai ordenar de forma crescente:

``` JSX
import React, { Component } from "react";
import { Button, Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { // Para evitar um erro do this não apontar para a instância correta, vamos utilizar arrow function
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    const numerosGerados = Array(this.state.quantNumeros)
      .fill()
      .reduce(n => [...n, this.gerarNumeroNaoContido(n)], [])
      .sort((a, b) => a - b)

    this.setState({ numerosGerados: numerosGerados })
  }

  // Outra forma de fazer essa função, mais simples.
  // gerarNumeros = () => {
  //   const  { quantNumeros } = this.state 
  //   const numerosGerados = []

  //   for(let i = 0; i < quantNumeros; i++) {
  //     numerosGerados.push(this.gerarNumeroNaoContido(numerosGerados))
  //   }

  //   this.setState({ numerosGerados })
  // }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
        <Button 
          title="Gerar"
          onPress={this.gerarNumeros}
        /> 
        <Text>
          { this.state.numerosGerados.join(',') }
        </Text>
      </React.Fragment>
    );
  }
}

export default Megasena;
```

### Componente Mega-Sena #02

- Vamos criar um componente para exibir e estilizar os números sorteados da mega sena. Para isso, dentro de src/components/componente-class vamos criar um componente funcional chamado _NumeroMega.js_. Esse componente irá receber via props um numero o qual iremos interpolar ao componte _Text_ para exibirmos em tela:

``` JSX
import React from "react";
import { Text, View } from "react-native";

import Style from "../style";

const NumeroMega = ({ numero }) => {
  return (
    <View>
      <Text style={Style.textDefault}>{numero}</Text>
    </View>
  );
}

export default NumeroMega;
```

- E para melhorar a visualização vamos criar um objeto de estilo através do _StyleSheet_ e nele iremos criar objetos de estilo para a _View_ e para o _Text_, que iremos chamar de _Container_ e _Number_ respectivamente:

``` JSX
import React from "react";
import { StyleSheet, Text, View } from "react-native";

import Style from "../style";

const NumeroMega = ({ numero }) => {
  return (
    <View style={stylesNumeroMega.Container}>
      <Text style={[Style.textDefault, stylesNumeroMega.Number]}>
        {numero}
      </Text>
    </View>
  );
}

const stylesNumeroMega = StyleSheet.create({
  Container: {
    backgroundColor: "#000",
    
    height: 50,
    width: 50,

    margin: 5,
    borderRadius: 25,
  },
  Number: {
    color: "#FFF",
    fontSize: 24
  },
})

export default NumeroMega;
```

- E dentro do componente _Megasena_ para exibir os números através dos componentes _NumeroMega_ vamos criar uma função que iremos chamar de _exibirNUmeros_(essa função deve ser arrow para exibir o problema com o this). 
Nessa função, vamos criar uma constantes que iremos chamar de _numeros_ a qual vai receber os valores de _numerosGerados_(this.state.numerosGerados) em seguida, vai retornar _numeros_ chamando o método _map_ o qual irá receber cada um dos numeros/_numero_ e chamar uma função arrow a qual vai retornar/_return_ um trecho JSX:

``` JSX
import React, { Component } from "react";
import { Button, Text, TextInput } from "react-native";

import Style from "../style";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { 
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    const numerosGerados = Array(this.state.quantNumeros)
      .fill()
      .reduce(n => [...n, this.gerarNumeroNaoContido(n)], [])
      .sort((a, b) => a - b)

    this.setState({ numerosGerados: numerosGerados })
  }

  exibirNumeros = () => {
    const numeros = this.state.numerosGerados;
    return numeros.map(numero => {
      return
    })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
        <Button 
          title="Gerar"
          onPress={this.gerarNumeros}
        /> 
        <Text>
          { this.state.numerosGerados.join(',') }
        </Text>
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- Já criamos um componente _NumeroMega_ que vai retornar esse trecho JSX com cada número. Portanto, vamos importá-lo para dentro do componente _Megasena_ e retornar passando via props para o atributo _numero_ o numero que está sendo percorrido pelo map. Também não podemos de colocar a chave/_key_ para esse elemento, que nesse caso pode ser o próprio _numero_:

``` JSX
import React, { Component } from "react";
import { Button, Text, TextInput } from "react-native";

import NumeroMega from "./NumeroMega";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { 
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    const numerosGerados = Array(this.state.quantNumeros)
      .fill()
      .reduce(n => [...n, this.gerarNumeroNaoContido(n)], [])
      .sort((a, b) => a - b)

    this.setState({ numerosGerados: numerosGerados })
  }

  exibirNumeros = () => {
    const numeros = this.state.numerosGerados;
    return numeros.map(numero => {
      return <NumeroMega key={numero} numero={numero}/>
    })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
        <Button 
          title="Gerar"
          onPress={this.gerarNumeros}
        /> 
        <Text>
          { this.state.numerosGerados.join(',') }
        </Text>
      </React.Fragment>
    );
  }
}

export default Megasena;
```

- Desse modo, conseguimos chamar a função _exibirNumeros_ no lugar do componente Text que estava fazendo essa exibição:

``` JSX
import React, { Component } from "react";
import { Button, Text, TextInput } from "react-native";

import NumeroMega from "./NumeroMega";

class Megasena extends Component {

  state = {
    quantNumeros: this.props.quantNumeros,
    numerosGerados: [],
  }

  alterarQuantNumeros = (input) => { 
    this.setState({ quantNumeros: +input })
  }

  gerarNumeroNaoContido = (nums) => {
    const novo = parseInt(Math.random() * 60) + 1;
    return nums.includes(novo) ? this.gerarNumeroNaoContido(nums) : novo;
  }

  gerarNumeros = () => {
    const numerosGerados = Array(this.state.quantNumeros)
      .fill()
      .reduce(n => [...n, this.gerarNumeroNaoContido(n)], [])
      .sort((a, b) => a - b)

    this.setState({ numerosGerados: numerosGerados })
  }

  exibirNumeros = () => {
    const numeros = this.state.numerosGerados;
    return numeros.map(numero => {
      return <NumeroMega key={numero} numero={numero}/>
    })
  }

  render() {
    return (
      <React.Fragment>
        <Text>Componente baseado em Classe!</Text>
        <Text>Quantidade de Números para Sortear: {this.state.quantNumeros}</Text>
        <TextInput 
          keyboardType={"numeric"}
          style={{borderBottomWidth: 1}}
          placeholder="Quantidade de Números"
          value={ `${this.state.quantNumeros}` }
          onChangeText={ this.alterarQuantNumeros } 
        />
        <Button 
          title="Gerar"
          onPress={this.gerarNumeros}
        /> 
        {this.exibirNumeros()}
      </React.Fragment>
    );
  }
}

export default Megasena;
```