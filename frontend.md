# 環境構築
1. Node.jsをインストール
   - node.jsはjavascriptを実行する環境
   - npxやnpmコマンドが使えるようになる
2. `npm install -g typescript`でtypescriptのコンパイラをインストール
   - `tsc hogehoge.ts`でコンパイル。hogehoge.jsが生成される。
   - `node hogehoge.js`でjavascriptの実行

## Reactプロジェクトの作成
1. `npx create-react-app --template typescript <プロジェクト名>`でプロジェクトを作成
  - `--template typescript`を書かなければjavascriptでプロジェクトが作成される
2. `npm start`でlocalhostサーバを起動

# 基本知識
- `.ts`:普通のTypeScriptコード
- `.tsx`:コード内にXMLタグが書けるTypeScript
- `.js`:普通のJavaScriptコード
- `.jsx`:コード内にXMLタグが書けるJavaScript

すべてtsx/jsxにしてもよいが、純粋なアルゴリズムの処理と明示的に分離する意味で、拡張子を使い分けたほうが良いとか
tsx/jsxならUIが絡んでいる、ts/jsならUIが絡んでいないみたいに

## useStateで状態管理

### その1
``` typescript
import React, { useState } from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <MakeButton />
      </header>
    </div>
  );
}

function MakeButton() {
  const [count, setCount] = useState(0);
  const buttonClick = () => { setCount(count + 1); };
  return (<button onClick={buttonClick}> {count} </button>);
}

export default App;
``` 

### その2
``` typescript
function MakeButton() {
  const [array, setArray] = useState([0, 1, 2]);
  const buttonClick = (i: number) => {
    const newArray = array.concat();// 配列のコピー
    newArray[i]++;
    setArray(newArray);
    // 更新されないダメな例↓
    // array[i]++;
    // setArray(array);
  };
  return (<div>
    {array.map((x, i) =>
      <button key={i} onClick={() => buttonClick(i)}>{x}</button>
    )}
  </div>);
}
export default App;
```

## useRefでタグを参照する
``` typescript
import React, { useState, useRef } from 'react';
import './App.css';

function App() {
  const inputElement = useRef<HTMLInputElement>(null);
  const [output, setOutput] = useState("");
  const buttonClick = () => {
    setOutput(inputElement.current?.value ?? "");
  };
  return (
    <div className="App">
      <header className="App-header">
        <input ref={inputElement} />
        <button onClick={buttonClick}> ボタン </button>
        {output}
      </header>
    </div>
  );
}

export default App;
``{

## useEffectでUI以外の処理を書く
``` typescript
import React, { useState, useEffect } from 'react';
import './App.css';

function App() {
  const [state, setState] = useState(0);
  const update = () => { setState(state + 1); };
  useEffect(() => {
    const timeId = setInterval(update, 1000);
    return () => clearInterval(timeId);
  }, [state]);
  return (
    <div className="App">
      <header className="App-header">
        {state}
      </header>
    </div>
  );
}

export default App;
```

## useMemoとuseCallbackでメモ化して軽量化
useMemoは関数の結果をキャッシュしておける機能で、同じ入力には同じ出力を返す関数につけるものです。
``` typescript
import React, { useState, useMemo } from 'react';
import './App.css';

function App() {
  const [state, setState] = useState(1e9);
  const [count, setCount] = useState(0);

  const totalWithMemo = useMemo(() => {
    let sum = 0;
    for (let i = 0; i < state; ++i)
      sum += i;
    return sum;
  }, [state]);
  return (
    <div className="App">
      <header className="App-header">
        <button onClick={() => { setState(state + 1); }}>重い計算</button>
        sum 0 to {state} = {totalWithMemo}
        <button onClick={() => { setCount(count + 1); }}>軽い計算</button>
        {count}
      </header>
    </div>
  );
}

export default App;
```
