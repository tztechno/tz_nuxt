はい、ローカルストレージを使用してデータを保存する方法は、サーバーサイドのバックエンドがなくても、静的HTMLファイル上で実現可能です。以下は、静的HTMLファイル上で同様のToDoアプリを作成する方法の例です。

### 静的HTMLファイルでのToDoアプリ

#### HTML部分
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Todo List</title>
  <script src="https://unpkg.com/vue@next"></script>
  <script src="https://unpkg.com/vue-demi@0.13.0-alpha.0"></script>
  <script src="https://unpkg.com/@vue/composition-api@latest"></script>
</head>
<body>
  <div id="app">
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

  <script>
    const { createApp, reactive, onMounted, watch } = Vue;

    createApp({
      setup() {
        const state = reactive({
          newTodo: '',
          todos: []
        });

        onMounted(() => {
          const savedTodos = localStorage.getItem('todos');
          if (savedTodos) {
            state.todos = JSON.parse(savedTodos);
          }
        });

        watch(
          () => state.todos,
          (newTodos) => {
            localStorage.setItem('todos', JSON.stringify(newTodos));
          },
          { deep: true }
        );

        const addTodo = () => {
          if (state.newTodo.trim() !== '') {
            state.todos.push({ text: state.newTodo, done: false });
            state.newTodo = '';
          }
        };

        const removeTodo = (index) => {
          state.todos.splice(index, 1);
        };

        return {
          state,
          addTodo,
          removeTodo
        };
      }
    }).mount('#app');
  </script>
</body>
</html>
```

### 説明

1. **HTML構造**:
    - `<div id="app">` 内にToDoリストのUI要素（入力フィールド、リスト、ボタン）を配置しています。
  
2. **Vue.jsのインポート**:
    - `<script src="https://unpkg.com/vue@next"></script>`: Vue 3をCDNから読み込んでいます。
    - `<script src="https://unpkg.com/vue-demi@0.13.0-alpha.0"></script>` と `<script src="https://unpkg.com/@vue/composition-api@latest"></script>`: Composition APIの互換性を提供するために読み込んでいます。

3. **Vueアプリケーションのセットアップ**:
    - `createApp`関数を使ってVueアプリケーションを作成し、`setup`関数内でアプリケーションのロジックを定義します。
    - `reactive`関数を使って、リアクティブな状態を管理します。
    - `onMounted`フックで、コンポーネントがマウントされたときにローカルストレージから保存されたタスクを読み込みます。
    - `watch`関数で、`state.todos`の変更を監視し、変更があればローカルストレージに保存します。

4. **タスクの追加と削除**:
    - `addTodo`メソッドで、新しいタスクを追加します。
    - `removeTodo`メソッドで、指定されたインデックスのタスクを削除します。

この方法で、バックエンドがなくてもローカルストレージを使用してデータを永続化するシンプルなToDoアプリを静的HTMLファイル上で実現できます。