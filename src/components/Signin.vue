<template>
    <div class="overlay" @click.self="closer" v-if="opened">
        <div class="modal" >
            <div class="col-12">
               <input type="email" name="email" id="email" :placeholder="signdata.email" class="col-12">
               <input type="password" name="password" id="password" :placeholder="signdata.password" class="col-12">
            </div>
            <div class="col-12 modal__bottom">
                <p>
                      <slot></slot>
                </p>
                 <slot name="links"></slot>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        props: ["signdata", "opened"],
      mounted() {
          console.log(this.signdata)
      },
      methods: {
          closer(){
              return this.$emit("closer")
          }
      },
    }
</script>
