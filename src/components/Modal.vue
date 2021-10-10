<template>
    <div class="overlay" @click.self="data={}" v-if="data.id">
        <div class="modal" >
            <div class="modal__img">
                <a :href="data.image">
                <img :src="data.image" alt="">
                </a>
            </div>
            <div class="modal__info">
                <h3>{{data.title}} (prodcut id: {{data.id}})</h3>
                <strong>$ {{data.price}}</strong>
                <p class="modal__category">{{data.category}}</p>
                <p>{{data.rating.rate}}/5  (voted by <strong>{{data.rating.count}} </strong> people)</p>
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
        props: ["data"]
    }
</script>
<style >
.overlay{
    position: fixed;
    inset: 0;
    background: hsla(55, 50%, 0%, .3);
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1;
}
.modal{
        width: clamp(300px,100vw,700px);
        background: var(--light);
        padding:20px;
        border-radius: var(--radius);
        box-shadow: 0 0 10px 0 rgb(40 40 40 / 30%);
        display: flex;
        flex-wrap: wrap;
}
.modal__info{
    width: calc(100% * 8 / 12);
    text-align: left;
    padding: 10px;
}
.modal__img{
    width: calc(100% * 4 / 12);
}
.modal__bottom{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
.modal__bottom p{
width: 100%;
}
.modal__bottom strong{
padding: 10px 20px;
border-bottom: 1px solid var(--dark);
}
.modal__bottom a {
  padding: 0 20px;
  height: 40px;
  border-radius: var(--radius);
  background-color: var(--success);
  color: var(--light);
  display: flex;
  justify-content: center;
  align-items: center;
  text-decoration: none;
}
</style>