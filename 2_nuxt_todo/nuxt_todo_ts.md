TypeScriptを使用してNuxt.jsプロジェクトを作成した場合、型定義を含めるためにコードに若干の変更が必要です。以下は、TypeScriptでのシンプルなToDoアプリのコード例です。

### 1. Nuxtプロジェクトのセットアップ

プロジェクトディレクトリを作成し、Nuxt.jsとTypeScriptをインストールします。

```bash
npx create-nuxt-app todo-app
cd todo-app
```

インストール中に、「Choose the package manager」という質問に対して「npm」を選び、「Choose programming language」では「TypeScript」を選びます。他の質問はデフォルト設定で問題ありません。


$$$
🎉  Successfully created project todo-app

  To get started:

        cd todo-app
        yarn dev

  To build & start for production:

        cd todo-app
        yarn build
        yarn start
$$$

### 2. ページの作成

`pages/index.vue`ファイルを以下のように編集します。

```vue
<template>
  <div>
    <h1>Todo List</h1>
    <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new todo" />
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.done" />
        <span :style="{ textDecoration: todo.done ? 'line-through' : 'none' }">{{ todo.text }}</span>
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

interface Todo {
  text: string;
  done: boolean;
}

export default defineComponent({
  data() {
    return {
      newTodo: '',
      todos: [] as Todo[]
    };
  },
  mounted() {
    const savedTodos = localStorage.getItem('todos');
    if (savedTodos) {
      this.todos = JSON.parse(savedTodos);
    }
  },
  watch: {
    todos: {
      handler(newTodos: Todo[]) {
        localStorage.setItem('todos', JSON.stringify(newTodos));
      },
      deep: true
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, done: false });
        this.newTodo = '';
      }
    },
    removeTodo(index: number) {
      this.todos.splice(index, 1);
    }
  }
});
</script>

<style>
/* スタイルは必要に応じて追加してください */
</style>
```

### 3. 開発サーバーの起動

開発サーバーを起動して、アプリケーションを確認します。

```bash
npm run dev
```

これでブラウザで `http://localhost:3000` を開くと、TypeScriptで作成されたToDoアプリが表示されるはずです。

### 説明

1. `lang="ts"`を使って、スクリプトセクションでTypeScriptを使用しています。
2. `defineComponent`を使ってコンポーネントを定義しています。
3. `Todo`インターフェースを定義して、タスクの型を指定しています。
4. `data`メソッドで`newTodo`と`todos`の初期値を設定しています。`todos`は`Todo`型の配列です。
5. `mounted`フックでローカルストレージからタスクを読み込みます。
6. `watch`プロパティでタスクの変更を監視し、変更があればローカルストレージに保存します。
7. `addTodo`メソッドで新しいタスクを追加し、`removeTodo`メソッドでタスクを削除します。

以上の手順で、TypeScriptを使ったNuxt.jsのシンプルなToDoアプリが完成します。
