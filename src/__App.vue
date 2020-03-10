<template>
  <div id="app">
    <div class="container">
      <div v-for="(todo, key) in todos" :class="['flexitem', key]" :key="key">
        <h1>{{ todo.title }}</h1>
        <p v-if="key === 'todo'">
          <input
            type="text"
            placeholder="TODOを入力しましょう！"
            v-model="newitemtitle"
            v-on:keyup.enter="addbutton"
          />
          <button v-on:click="addbutton">add</button>
        </p>
        <draggable tag="ul" v-bind:options="{group:'items'}" v-model="todo.list">
          <li v-for="(item) in todo.list" v-bind:key="item.id">
            <label v-bind:class="{ done: item.ischecked }">
              <input type="checkbox" v-model="item.ischecked" />
              {{item.title}}
              <button v-on:click="deleteTodo(item, todo.list)">delete</button>
            </label>
          </li>
        </draggable>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
export default {
  components: {
    draggable
  },
  data: function() {
    return {
      todos: {
        wait: {
          title: '未着手',
          list: []
          },
        doing: {
          title: '進行中',
          list: []
        },
        todo: {
          title: 'TODOリスト',
          list: []
        },
        approval: {
          title: '確認待ち',
          list: []
        },
        complate: {
          title: '完了',
          list: []
        }
      },
      newitemtitle: "",
      id: 0
    };
  },
  methods: {
    addbutton: function() {
      if (this.newitemtitle === "") return;
      this.todos.todo.list.push({
        title: this.newitemtitle,
        ischecked: false,
        id: this.id++
      });
      this.newitemtitle = "";
    },
    deleteTodo: function(item, todos) {
      if (confirm("本当に削除しますか？")) {
        const index = todos.findIndex(todo => todo.id === item.id);
        todos.splice(index, 1);
      }
    },
  }
};
</script>
<style>
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html,
body,
div,
span,
applet,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}
body {
  line-height: 1;
}
ol,
ul {
  list-style: none;
}
blockquote,
q {
  quotes: none;
}
blockquote:before,
blockquote:after,
q:before,
q:after {
  content: "";
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
</style>
<style>
h1 {
  font-size: 30px;
  font-weight: bold;
  padding: 20px;
  text-align: center;
}

.container {
  display: flex;
  height: 100%;
  justify-content: start;
}

.flexitem {
  width: 100%;
}

.wait {
  background: blueviolet;
}

.doing {
  background: lightblue;
}

.todo {
  background: lightslategray;
  text-align: center;
}

.approval {
  background: lightgreen;
}

.complate {
  background: lightpink;
}

.done {
  text-decoration: line-through;
}

li {
  list-style: none;
  padding: 15px;
  cursor: pointer;
  border: 1px solid grey;
}
</style>