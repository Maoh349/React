# コンポーネント（component）
## コンポーネントの違い

### Class Component（クラスコンポーネント）
``` js
import React, {Component} from 'react'

class Button extends Component {
  render() {
    return <button>Say, {this.props.hello}</button>
  }
}
export default Button;
```

### Functional Component（関数コンポーネント）
``` js
import React from 'react';

const Button = (props) => {
  return <button>Say, {props.hello}</button>
};
export default Button;
```

 - 関数コンポーネントのほうが記述量が少ない
 - 昔はクラスでないとできないことがあった
 - 現在はReact Hooksで同じ機能が使える

## 名前付きexport
``` js
// helper.js
export const addTax = {price} => {
  return Math.floor(price * 1.1)
}
export const getWild = () => {
  console.log('Get wild and touch')
}

//index.js
export {default as Article} from './Article'
export {default as Content} from './Content'
export {default as Title} from './Title'
```

## 名前付きimport
```js
import {Content, Title} from "./index";

const Article = (props) => {
  return (
    <div>
      <Title title={props.title} />
      <Content content={props.content} />
    </div
  };
};
export default Article;
```
 - 原則1ファイル１モジュール
 - ただし状機能方法で1ファイルから複数モジュールをexport可能
 - Reactではエントリポイントでよく使う？
 - エントリポイントでは別名exportも併用する？

# Hooks
 - クラスコンポーネントでしか使えなかった
   - コンポーネント内で状態を管理するstate
   - コンポーネントの時間の流れに基づくライフサイクル
 - Hooksにより関数コンポーネントでも使えるように
 - Hooks=クラスコンポーネントの機能に接続する

## useState
1. useStateによるstateの宣言
```js
const [state, setState] = useState(initialState)
現在の状態　　　　　更新関数　　　　　　　　初期値
```
2. stateの更新
  ```js
setState(newState)
更新関数　　新しい値
```
4. 具体例
```js
const [message, setMessage] = useState('hooks is cool')
const [likes, setLikes] = useState(0)
const [isPublished, setIsPublished] = useState(false)
```

## propsとstateの違い
 - 両者ともに再描画のきっかけになるが
   - propsは引数のようにコンポーネントに渡される値
   - stateはコンポーネントの内部で宣言・制御される値
  
## propsへ関数を渡す際の注意点
### OKな関数の渡し方
```js
<PublishButton isPublished={isPublished} onClick={publishArticle} />
<PublishButton isPublished={isPublished} onClick={() => publishArticle()} />
```

### NGな関数の渡し方（無限レンダリングが起きる）
```js
<PublishButton isPublished={isPublished} onClick={publishArticle()} />
```
