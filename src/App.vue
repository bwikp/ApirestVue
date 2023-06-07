<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { useRoute, useRouter } from 'vue-router'
import axios from 'axios';
import { onBeforeMount, ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue'
const route = useRoute()
const router = useRouter()
const AllCateogire = ref([])

const oneCategorie = ref({})
const fetchAllcategorie = async () => {
  const categorie = await axios.get('http://localhost:8000/api/categorie/')
  console.log(categorie.data)
  AllCateogire.value = categorie.data
}
onBeforeMount(async () => {
  await fetchAllcategorie()
})

const editCategorie = async () => {
  const editJson = await axios.put('http://localhost:8000/api/categorie/7/update', { "name": "ONE PIECE" })
  console.log(editJson.data)
}
editCategorie();
const show = ref(false)
</script>
''
<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>

        <div v-for="categorie in  AllCateogire">
          <p>{{ categorie.name }}</p>
        </div>
        <button @click="d.Modal()">open</button>

        <dialog>
          <form method="dialog">
            <button>OK</button>
          </form>
        </dialog>

      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

#dialogue {
  background-color: antiquewhite;
  height: 20px;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
