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
