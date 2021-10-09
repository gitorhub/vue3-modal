<template>
  <h1>Create Modal with Vue :)</h1>
  <Modal :data="singledata">
    <strong>Go To</strong>

    <template v-slot:links>
      <a href="#">Homepage</a>
      <a href="#">Cart</a>
    </template>

  </Modal>

  <div class="all-items">
    <span class="one-item" v-for="(d, i) in data" :key="i" @click="openModal(d)" >
      <img :src="d.image" alt="">
      <h5>{{d.title}}</h5>
      <p class="price">$ {{d.price}} </p>

    </span>

  </div>

</template>
<script>
  import Modal from './components/Modal.vue'

  export default {
    name: 'App',
    components: {
      Modal
    },
    data() {
      return {
        data: [],
        singledata: {},
      }
    },
    methods: {
      openModal(d) {
        this.singledata = d;
      }

    },
    created() {
      const options = {
        endpoint: "https://fakestoreapi.com/products"
      }
      fetch(options.endpoint)
        .then(res => res.json())
        .then(data => {
          this.data = data
          console.log(data)
        })
        .catch(err => console.log(err))
    },
  }
</script>
<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>