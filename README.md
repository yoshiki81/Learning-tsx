# React × TypeScript プロジェクト

## 環境構築
- [Node.jsインストール](https://github.com/yoshiki81/Atomic-Design/blob/main/summary/node.md)
- [Create React App](https://github.com/yoshiki81/Atomic-Design/blob/main/summary/env.md)
- [Create React Appなしで環境構築](https://kosuke-space.com/react-typescript-without-create-react-app)

## 開発を始める手順

```
#1
npx create-react-app my-app --template typescript

#2
cd my-app

#3
npm start
yarn start

#4
http://localhost:3000/ にアクセスして動作を確認しながら開発を進めることができる
```

## TypeScriptの便利機能

### axios
```
axios.get<Array<TodoType>>("URL").then((response) => {
  setTodos(response.data);
})
```

- `response.data`  
.dataプロパティはレスポンスデータを格納している


### カスタムデータ型を定義する[type]  
```
type TodoType = {
    userId: number;
    title: string;
    completed?: boolean;
};
```
- **セミコロン区切り**  
各プロパティはセミコロンで区切って定義する

- **type**  
カスタムデータ型を定義することを宣言するためのキーワード

- **プロパティ?**  
「?」はそのプロパティが必須ではないことを示す

### 型を指定する
#### ① 変数に型を指定する
```
props: TodoType
```

#### ② メソッドに型を指定する
```
const [todos, setTodos] = useState<Array<TodoType>>([]);
axios.get<Array<TodoType>>("URL")
```

### カスタム型をファイル(.ts)で定義する・使う
#### 定義する
カスタムデータ型を他のファイルで使いまわせるようにファイルに定義する

#### 使い方
- **① 全てのプロパティを使う**  
```
<Array<TodoType>>
```

- **② 必要なプロパティを指定する**  
```
props: Pick<TodoType, "userId" | "title" | "completed">
```

- **③ 不要なプロパティを省く**  
```
props: Omit<TodoType, "id">
```


## その他
### 相対パス「./~」
同階層であることを示す。

### 三項演算子
構文
```
条件式 ? trueの時の値 : falseの時の値;
```
