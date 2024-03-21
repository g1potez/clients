<script>
import DataForm from './components/DataForm.vue';
export default {
  components: {
    DataForm
  },
  methods: {
    handleSubmit() {
      document.querySelector('.client-result').style.display = 'flex';
    },
    close() {
      location.reload();
    }
  }
}
</script>

<template>
  <div class="clients">
    <div class="logo">
      <h1>Clients</h1>
    </div>
    <div class="clients-content">
      <h4>Создать клиента</h4>
      <form class="clients-form" @formSubmitted.prevent="handleSubmit">
        <DataForm @formSubmitted="handleSubmit"/>
      </form>
    </div>
  </div>
  <div class="client-result">
    <div class="close" @click="close">✖</div>
    <div class="content">
      <h2>Клиент успешно создан!</h2>
    </div>
  </div>
</template>

<style scoped lang="sass">
@import './assets/variables.sass'

.clients
  background-color: #fff
  width: 400px
  height: 630px
  border-radius: 10px
  padding: 20px
  box-shadow: 0 0 15px #858585
  @media (max-width: 455px)
    width: 300px
    height: 750px
  &::before
    content: ""
    z-index: -1
    width: 800px
    height: 300px
    background-color: $mainColor
    position: absolute
    transform: translate(-25%, 50%) skew(10deg, 10deg)
    @media (max-width: 860px)
      width: 550px
      transform: translate(-15%, 50%) skew(10deg, 10deg)
    @media (max-width: 590px)
      display: none
  .logo
    text-align: center
    margin: 20px 0
    h1
      color: $mainColor
  .clients-content
    width: 100%
    overflow-x: hidden
    h4
      text-align: center
      margin-bottom: 20px
    .clients-form
      display: flex

.client-result
  display: none
  position: absolute
  left: 0
  top: 0
  width: 100%
  height: 100%
  background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7))
  +flexCenter
  .close
    cursor: pointer
    color: #fff
    font-size: 30px
    position: absolute
    right: 20px
    top: 10px
    transition: 0.3s
    &:hover
      color: #323232
  .content
    background-color: #fff
    border-radius: 10px
    width: 500px
    text-align: center
    padding: 50px
    h2
      color: $mainColor
</style>
