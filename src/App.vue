<template>
<div id="app">

  <div class="container">

    <div class="app__main">
      <img @click="addNewItem" class="app__plus" :src="app_plus" alt="">

      <ul class="app__list">
        <li class="app__list-item" v-for="(todo, index) in todos" :key="index">
          <input type="checkbox" name="" v-model="todo.completed" value="todo.title">
          <span :class="[todo.completed ? 'is--active' : 'app__list-text']">{{todo.title}}
      <span class="app__trash"><img @click="removeTodo(index)" :src="app_trash"></img></span></span>
        </li>
      </ul>

      <div class="app__back1"></div>
      <div class="app__back2"></div>
      <div class="app__back3"></div>

    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
    app_plus: "plus.png",
    app_trash: "trash.png",
      todos: [
        // {title: "Play soccer with friends", completed: false},
        // {title: "Open Photoshop", completed: true},
        // {title: "Finish client work", completed: false},
        // {title: "Give away some PSDs", completed: true},
        // {title: "Post a new shot to Dribble", completed: false},
        // {title: "Example", completed: false}
      ]
    }
  },
  created() {
    fetch('https://jsonplaceholder.typicode.com/todos').then(function(data) {
      return data.json()
    }).then(response => {
      for (var i = 0; i < response.length; i++) {
        if (i < 10) {
          this.todos.push(response[i]);
        }
      }
    })
  },
  methods: {
    removeTodo(index) {
      this.$delete(this.todos, index);
    },
    addNewItem() {
      let newTodo = window.prompt("Add New Think To Do!");
      this.todos.push({
        title: newTodo,
        completed: false
      })
    }
  }
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Open+Sans:400,700');

/*
Table of contents
=====================
// 1. Variables
// 2. Placeholders
// 3. Functions
// 4. Font Faces
// 5. Base
// 6. Layout
// 7. Block + element
// 8. Modifier
// 9. State
// 10. Animations
// 11. Media Queries
=====================
*/

// 1. Variables

$background_color: #f7f4f4;

$white: #ffffff;
$main_font: #8b8f97;

$checkbox_color: #6bb3ca;
$checkbox_inactive: #d0d0d0;

$border_color: #d9d7d7;

$divider_color: #f2e3df;

$shadow_color: #f7f7f7;

// 2. Placeholders
%text--center {
    text-align: center;
}

%box--center {
    margin: 0 auto;
}

%flex {
    display: flex;
}

%pointer {
    cursor: pointer;
    user-select: none;
}

%transition {
    transition: all 0.3s;
}

%border {
    border: 1px solid $border_color;
}

%absolute {
    position: absolute;
}

%box {
    width: 470px;
    min-height: 241px;
    background: $white;
    box-shadow: 0 2px 15px $shadow_color;
    border-radius: 2px;
}

// 3. Functions
@function prc($el, $target) {
    @return (100% * $el) / $target;
}

// 4. Font Faces
// @font-face {
//     font-family: LucidaGrande;
//     src: url("./assets/fonts/LucidaGrande.ttf");
// }

// 5. Base
* {
    box-sizing: border-box;
    outline: none;
}

#app {
    font: normal 62.5% 'Open-sans', 'sans-serif';
    color: $main_font;
    width: 100%;
    min-height: 100vh;
    margin: 0;
    padding: 0;
}

ul {
    list-style: none;
    font-size: 1rem;
    margin: 45px 0 0;
    padding: 0;
}

li {
    @extend %flex;
    align-items: center;
    width: 98%;
    border-top: 1px solid $border_color;
    text-align: left;
    margin-left: 2%;
}

input[type=checkbox] {
    margin: 0 30px 0 10px;
    filter: sepia(40%) hue-rotate(130deg) saturate(400%);
    display: block;
}
input[type=checkbox]:checked {
    margin: 0 30px 0 10px;
    filter: sepia(0);
}

// 6. Layout
// 7. Block + element

.container {
    min-width: 266px;
    max-width: 100%;
    height: 100%;
}

.app__main {
    @extend %box;
    @extend %border;
    position: relative;
}

.app__back1 {
    z-index: -1;
    transform: translateY(-234px) scaleX(.95);
    @extend %box;
    @extend %border;
    @extend %absolute;
}

.app__back2 {
    z-index: -2;
    transform: translateY(-230px) scaleX(.90);
    @extend %box;
    @extend %border;
    @extend %absolute;
}

.app__back3 {
    z-index: -3;
    transform: translateY(-226px) scaleX(.85);
    @extend %box;
    @extend %border;
    @extend %absolute;
}

.app__list-text {
    width: 100%;
    @extend %flex;
    padding: 5px 10px;
    border-left: 4px double $divider_color,;
}

.app__trash {
    padding-left: 5px;
    margin: 0 15px 0 auto;
    @extend %pointer;
    visibility: hidden;
}

.app__plus {
    @extend %absolute;
    z-index: 234;
    top: 15px;
    left: 75px;
    padding: 5px;
}

// 8. Modifier
// 9. State

li:hover .app__trash {
    visibility: visible;
    padding-left: 5px;
    margin: 0 15px 0 auto;
    @extend %pointer;
}

.is--active {
    text-decoration: line-through;
    @extend %flex;
    width: 100%;
    padding: 5px 10px;
    border-left: 4px double $divider_color,;
}

.app__plus:hover {
    box-shadow: 0 0 50px $main_font;
    @extend %transition;
    @extend %pointer;
    border-radius: 4px;
}

// 10. Animations
// 11. Media Queries
</style>
