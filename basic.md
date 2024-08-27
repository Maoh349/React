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
