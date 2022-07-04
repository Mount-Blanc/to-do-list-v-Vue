<script setup>
import { ref, onMounted, computed, watch } from 'vue'

const todos = ref([])
const name = ref('')

const input_content =ref('')
const input_category = ref(null)

const todos_asc = computed ( () => todos.value.sort((a,b) => {
  return b.createdAt - a.createdAt
}))

const addTodo = () => {
  if ( input_content.value.trim() === '' || input_category.value === null) {
    return
  }

  todos.value.push({
    contentLinput_content.value,
    category:input_category.value,
    done:false,
    createdAt: new Date().getTime()
  })
}
watch(todos, newVal => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, { deep:true })

watch(name, (newVal) => {
  localStorage.setItem('name', newVal)
})

onMounted (() => {
  name.value = localStorage.getItem('name') || ''
})

</script>

<template>
  
  <main class="app">

    <section class="greeting">
      <h2>
        What's up, <input type="text" placeholder="Name Here"
        v-model="name" />
      </h2>
    </section>

    <section class="create-todo">
      <h3>CREATE A TODO</h3>
    </section>

    <form @submit.prevent="addTodo">
    <h4>What's on your todo list?</h4>
    <input
    type="text"
    placeholder="e.g. make a video"
    v-model="input_content"/>

    <h4>Pick a category</h4>

    <div class="options">

      <label>
        <input type="radio" 
        name="category"
        id="category1"
        value='business'/>
        <span class="bubble business"></span>
        <div>Business</div>
      </label>


      <label>
        <input type="radio" 
        name="category"
        id="category1"
        value='personal'/>
        <span class="bubble personal "></span>
        <div>Personal</div>
      </label>

    </div>
    <input type="submit" value="Add todo"/>
    </form>
</main>

</template>

<style>
@import './assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
