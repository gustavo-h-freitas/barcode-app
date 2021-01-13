<template>
  <div class='home'>
    <h2>Digite aqui seu código de barra</h2>
    <input type='text' v-model='value'>
    <div class='bar'>
      <barcode :value='value' id='barcode'/>
    </div>
    <div class='btn'>
      <button @click='generate_img()'>Gerar imagem</button>
    </div>
  </div>
</template>

<script>
import barcode from 'vue-barcode'
import html2canvas from 'html2canvas'
export default {
  name: 'Home',
  data () {
    return {
      value: ''
    }
  },
  methods: {
    generate_img () {
      if (this.value !== '') {
        html2canvas(document.querySelector('#barcode')).then(canvas => {
          var a = document.createElement('a')
          a.href = canvas.toDataURL('image/jpeg').replace('image/jpeg', 'image/octet-stream')
          a.download = 'file.jpg'
          a.click()
        })
      }
    }
  },
  components: {
    barcode
  }
}
</script>

<style>
*{
  font-family: 'Courier New', Courier, monospace;
}
.home{
  width: 100vw;
  height: 100vh;
  padding: 16px;
  background: #ecff3c;
}

.home h2{
  margin: 0;
  color: #1a1a1a;
}

.home input{
  width: 100%;
  height: 36px;
  font-size: 16px;
  padding: 6px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, .25);
  border: none;
  border-radius: 6px;
  outline: none;
}

.bar{
  max-width: 100vw;
  overflow: auto;
  display: flex;
  height: 400px;
  justify-content: center;
  align-items: center;
}

.btn{
  width: 100%;
}

.btn button{
  width: 100%;
  border: none;
  border-radius: 6px;
  box-shadow: 0 2px 6px rgba(55, 55, 55, .25);
  font-size: 22px;
  padding: 16px;
  border: 1px solid #fff;
  color: #e6e6e6;
  font-weight: 700;
  background: #889040;
}
</style>
