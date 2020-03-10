<template>
  <div id="app">
    <div class="container">
      <div class="flexitem item1">
        <h1>未着手</h1>
        <h3>タスク数：{{items1.length}}</h3>
        <draggable tag="ul" v-bind:options="{group:'items'}" v-model="items1">
          
          <!-- コンポーネント候補: start -->
          <li v-for="(item,index) in items1" v-bind:key="item.id">
            <!-- コンポーネント候補: start -->
            <label v-bind:class="{ done: item.ischecked }">
              <input type="checkbox" v-model="item.ischecked" />
              {{item.title}}
              <button v-on:click="deletebutton1(index)">delete</button>
            </label>
            <!-- コンポーネント候補:end -->
          </li>
          <!-- コンポーネント候補:end -->
        </draggable>
      </div>
      <div class="flexitem item2">
        <h1>進行中</h1>
        <h3>タスク数：{{items2.length}}</h3>
        <draggable tag="ul" v-bind:options="{group:'items'}" v-model="items2">
          <li v-for="(item,index) in items2" v-bind:key="item.id">
            <label v-bind:class="{ done: item.ischecked }">
              <input type="checkbox" v-model="item.ischecked" />
              {{item.title}}
              <button v-on:click="deletebutton2(index)">delete</button>
            </label>
          </li>
        </draggable>
      </div>

      <div class="flexitem item3">
        <h1>TODOリスト</h1>
        <h3>タスク数：{{items3.length}}</h3>
        <p>
          <input
            type="text"
            placeholder="TODOを入力しましょう！"
            v-model="newitemtitle"
            v-on:keyup.enter="addbutton"
          />
          <button v-on:click="addbutton">add</button>
        </p>

        <draggable tag="ul" :options="{group:'items'}" v-model="items3">
          <li v-for="(item,index) in items3" v-bind:key="item.id">
            <label v-bind:class="{ done: item.ischecked }">
              <input type="checkbox" v-model="item.ischecked" />
              {{item.title}} : {{ item.timestamp | moment }}
              <button
                v-on:click="deletebutton3(index)"
              >delete</button>
              <button>edit</button>
            </label>
          </li>
        </draggable>
      </div>

      <div class="flexitem item4">
        <h1>確認待ち</h1>
        <h3>タスク数：{{items4.length}}</h3>
        <draggable tag="ul" v-bind:options="{group:'items'}" v-model="items4">
          <li v-for="(item,index) in items4" v-bind:key="item.id">
            <label v-bind:class="{ done: item.ischecked }">
              <input type="checkbox" v-model="item.ischecked" />
              {{item.title}}
              <button v-on:click="deletebutton4(index)">delete</button>
            </label>
          </li>
        </draggable>
      </div>
      <div class="flexitem item5">
        <h1>完了</h1>
        <h3>タスク数：{{items5.length}}</h3>
        <draggable tag="ul" v-bind:options="{group:'items'}" v-model="items5">
          <li v-for="(item,index) in items5" v-bind:key="item.id">
            <label v-bind:class="{ done: item.ischecked }">
              <input type="checkbox" v-model="item.ischecked" />
              {{item.title}}
              <button v-on:click="deletebutton5(index)">delete</button>
            </label>
          </li>
        </draggable>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import moment from "moment";
export default {
  components: {
    draggable
  },
  filters: {
    moment: function(date) {
      return moment(date).format("YYYY/MM/DD HH:mm");
    }
  },
  data: function() {
    return {
      items1: [],
      items2: [],
      items3: [],
      items4: [],
      items5: [],
      newitemtitle: "",
      id: 0
    };
  },

  methods: {
    addbutton: function() {
      if (this.newitemtitle === "") return;
      this.items3.push({
        title: this.newitemtitle,
        ischecked: false,
        id: this.id++
      });

      // localStorage.setItem("title", this.newitemtitle);
      // localStorage.setItem("id", this.id);
      // localStorage.setItem('title', JSON.stringify(this.newitemtitle));
      this.newitemtitle = "";
    },
    deletebutton1: function(index) {
      if (confirm("本当に削除しますか？")) {
        this.items1.splice(index, 1);
      }
    },
    deletebutton2: function(index) {
      if (confirm("本当に削除しますか？")) {
        this.items2.splice(index, 1);
      }
    },
    deletebutton3: function(index) {
      if (confirm("本当に削除しますか？")) {
        this.items3.splice(index, 1);
      }
    },
    deletebutton4: function(index) {
      if (confirm("本当に削除しますか？")) {
        this.items4.splice(index, 1);
      }
    },
    deletebutton5: function(index) {
      if (confirm("本当に削除しますか？")) {
        this.items5.splice(index, 1);
      }
    }
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
h3{
  font-size:23px;
  font-weight: bold;
  text-align: right;
  margin:0px 10px 0 10px;
}
.container {
  display: flex;
  height: 100%;
  justify-content: start;
}

.flexitem {
  width: 100%;
}

.item1 {
  background: blueviolet;
}

.item2 {
  background: lightblue;
}

.item3 {
  background: lightslategray;
  text-align: center;
}

.item4 {
  background: lightgreen;
}

.item5 {
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