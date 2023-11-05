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

### コンポーネント自体の型指定

```
export const Text: FC<Props> = (props) => {
    const { color, fontSize } = props;
    return <p style={{color, fontSize}}>テキストです</p>;
};
```

```
export const Todo: FC<Omit<TodoType, "id">> = (props) => {
    const { title, userId, completed = false } = props;
    const completedMark = completed ? "[完]" : "[未]";
    return <p>{`${completedMark} ${title}(ユーザー:${userId})`}</p>;
}
```

- **FC (Functional Components)**  
関数コンポーネントの型を指定するためのキーワード。  
(v18以降、**children**プロパティは含まれなくなった)

### Optional Chaining(オプショナルチェイニング)
「null安全」なコードを書くために用いる。  
`null`や`undefined`のプロパティを誤って参照しないようにしつつ、記述量を押さえることもできる。

```
# ?. 演算子
<dd>{user.hobbies?.join(" / ")}</dd>
```
- **?.演算子**  
プロパティの値が`null`または`undefined`の際に、`undefined`を返す。

- 参考[[optional chaining](https://typescriptbook.jp/reference/values-types-variables/object/optional-chaining)]


## その他
- [ESLint + Prettier設定](https://amateur-engineer.com/code-formatter-prettier-eslint/)
- [外部ライブラリの型定義について](https://www.udemy.com/course/react_stepup/learn/lecture/24823614#content)
### 相対パス「./~」
同階層であることを示す。

### 三項演算子
構文
```
条件式 ? trueの時の値 : falseの時の値;
```


