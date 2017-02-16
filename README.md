# OMG Counters ☝️️👇
![cool badge](https://img.shields.io/badge/omg-counters-ff69b4.svg)
![increment decrement](https://img.shields.io/badge/%E2%98%9D%EF%B8%8F%EF%B8%8F%20increment-%F0%9F%91%87%20decrement-blue.svg)
![so cool](https://img.shields.io/badge/so-cool-brightgreen.svg)

Increment/decrement ↕️️ counters using various frontend frameworks.

### _When a hello world is too simple, but a todo app is too complex._

![counter](https://cloud.githubusercontent.com/assets/943555/23040607/f434064e-f45f-11e6-8ca4-a4858dd62b28.gif)

_No counters were harmed in the making of these examples._

### Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [jQuery](#jquery)
- [React](#react)
- [Redux + React](#redux--react)
- [Hyperapp](#hyperapp)
- [Vue.js](#vuejs)
- [Elm](#elm)
- [Cycle.js](#cyclejs)
- [Jumpsuit](#jumpsuit)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


# jQuery

```js
// html
// ----
// <h1 class="count"></h1>
// <button class="increment">Increment</button>
// <button class="decrement">Decrement</button>

let count = 0
$('.count').text(count)
$('.increment').on('click', () => $count.text(++count))
$('.decrement').on('click', () => $count.text(--count))
```

# React

```JS
class Counter extends React.Component {
  state = {count: 0}

  increment = e =>
    this.setState({ count: this.state.count + 1 })

  decrement = e =>
    this.setState({ count: this.state.count - 1 })

  render = () =>  
    <div>
      <h1>{this.state.count}</h1>
      <button onClick={this.increment}>Increment</button>
      <button onClick={this.decrement}>Decrement</button>
    </div>
}
```

# Redux + React

```JS
const counter = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT': return state + 1
    case 'DECREMENT': return state - 1
    default: return state
  }
}

const { createStore } = Redux
const store = createStore(counter)

var Counter = ({ count, onIncrement, onDecrement }) => (
  <div>
    <h1>{count}</h1>
    <button onClick={onIncrement}>Increment</button>
    <button onClick={onDecrement}>Decrement</button>
  </div>  
)

const render = () => {
  ReactDOM.render(
    <Counter
       count={store.getState()}
       onIncrement={()=> store.dispatch({type: 'INCREMENT'})}
       onDecrement={()=> store.dispatch({type: 'DECREMENT'})}
    />,
    document.querySelector('body')
  )
}

store.subscribe(render)
render()
```

# Hyperapp

```JS
app({
  model: 0,
  update: {
    add: model => model + 1,
    sub: model => model - 1
  },
  view: (model, actions) =>
    <div>
      <h1>{model}</h1>
      <button onclick={actions.add}>Increment</button>
      <button onclick={actions.sub}>Decrement</button>
    </div>
})
```

# Vue.js

```js
// HTML
// ----
// <div id="app">
//   <h1>{{ count }}</h1>
//   <button v-on:click="increment">Increment</button>
//   <button v-on:click="decrement">Decrement</button>
// </div>

new Vue({
  el: '#app',
  data: { count: 0 },
  methods: {
  	increment: function() { this.count++ },
  	decrement: function() { this.count-- },
  }
})
```

# Elm

```elm
import Html exposing (beginnerProgram, div, h1, button, text)
import Html.Events exposing (onClick)


main =
  beginnerProgram { model = 0, view = view, update = update }


view model =
  div []
    [ h1 [] [ text (toString model) ]
    , button [ onClick Increment ] [ text "increment" ]
    , button [ onClick Decrement ] [ text "decrement" ]
    ]


type Msg = Increment | Decrement


update msg model =
  case msg of
    Increment ->
      model + 1

    Decrement ->
      model - 1
```

# Cycle.js

```js
const xs = xstream.default
const {div, button, h1, makeDOMDriver} = CycleDOM

const main = (sources) => {
  const action$ = xs.merge(
    sources.DOM.select('.dec').events('click').mapTo(-1),
    sources.DOM.select('.inc').events('click').mapTo(+1)
  )
  const count$ = action$.fold((x, y) => x + y, 0)
  const vdom$ = count$.map(count =>
    div([
      h1(count.toString()),
      button('.inc', 'Increment'),
      button('.dec', 'Decrement')
    ])
  )
  return { DOM: vdom$ }
}
```

# Jumpsuit

```js
const CounterState = State({
  initial: { count: 0 },
  increment: ({ count }) => ({ count: count + 1 }),
  decrement: ({ count }) => ({ count: count - 1 })
})

const Counter = Component({
  render() {
    return (
      <div>
        <h1>{ this.props.count }</h1>
        <button onClick={ Actions.increment }>Increment</button>
        <button onClick={ Actions.decrement }>Decrement</button>
      </div>
    )
  }
}, (state) => ({ count: state.counter.count }))

const globalState = { counter: CounterState }
Render(globalState, <Counter/>)
```
