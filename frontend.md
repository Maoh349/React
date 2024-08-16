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


