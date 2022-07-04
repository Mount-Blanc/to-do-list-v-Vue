<script setup>
import { ref, onMounted, computed, watch } from 'vue'

const todos = ref( [])
const name = ref('')

const input_content =ref('')
const input_category = ref(null)

const todos_asc = computed ( () => todos.value.sort((a,b) => {
  return b.createdAt - a.createdAt
}))


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
