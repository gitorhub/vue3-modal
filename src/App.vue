<template>
  <h1>Create Modal with Vue :)</h1>
  <teleport to='#modals'>
    <button @click="togglePopup" class="btn">Login</button>
    <Signin :signdata="sign" @closer=(togglePopup) :opened="opened">
      <template v-slot:links>
        <p>Nothing but fake Login</p>
        <a href="#" @click="togglePopup">Fake Login</a>
      </template>
    </Signin>
  </teleport>
  <Modal :data="singledata">
    <strong>Go To</strong>
    <template v-slot:links>
      <a href="#" @click.self="singledata={}">Homepage</a>
      <a href="#">Cart</a>
    </template>
  </Modal>
  <div class="all-items">
    <span class="one-item" v-for="(d, i) in data" :key="i" @click="openModal(d)">
      <img :src="d.image" alt="">
      <h5>{{d.title}}</h5>
      <p class="price">$ {{d.price}} </p>
    </span>
  </div>
</template>
<script>
  import Modal from './components/Modal.vue'
  import Signin from './components/Signin.vue'
  export default {
    name: 'App',
    components: {
      Modal,
      Signin
    },
    data() {
      return {
        data: [],
        singledata: {},
        sign: {
          email: "Enter email",
          password: "Enter password",
        },
        opened: false,
      }
    },
    methods: {
      openModal(d) {
        this.singledata = d;
      },
      togglePopup() {
        this.opened = !this.opened
      },
    },
    created() {
      const options = {
        endpoint: "https://fakestoreapi.com/products"
      }
      fetch(options.endpoint)
        .then(res => res.json())
        .then(data => {
          this.data = data
        })
        .catch(err => console.log(err))
    }
  }
</script>
<style>
  #app,
  #modals {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>