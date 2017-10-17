<template lang="html">
  <div class="size margin">

    <div class="esp-btn container wrap align-items-center justify-content-center">

	   <div class="flex-basis-100">
       <a class="btn" @click="toggleShow">+ Escolher desenho</a>
       <my-upload field="img"
               @crop-success="cropSuccess"
               @crop-upload-success="cropUploadSuccess"
               @crop-upload-fail="cropUploadFail"
               v-model="show"
               url="/upload"
               lang-type="pt-br"
               img-format="png">
       </my-upload>
	   </div>

     <div class="flex-grow-1 container wrap align-items-center justify-content-center">
       <input v-model="newSizeNumber" v-on:keyup.enter="addNewSize" placeholder="Ex: 10cm / Digitar apenas os números" class="input">
       <button type="button" name="button" class="btn" @click="addNewSize">
         Adicionar tamanho
       </button>
     </div>

     <div class="">
       <button type="flex-basis-100 button" name="button" class="btn primary btn-print" @click="pdf">
         Imprimir
       </button>
     </div>

    </div>

      <div class="container wrap justify-content-start align-items-start" id="tela">
      	<div class="container column" v-for="(index, x) in sizes" :key="index.id">
          <div class="img-tattoo">
            <button class="btn btn-small danger btn-remove" v-on:click="removeSize(x)">x</button>
        	  <img :src="imgDataUrl" height="auto" :style="{ width: index.width + 'cm'}">
          </div>
          <small class="">{{index.width}} cm</small>
      	</div>
      </div>
  </div>
</template>

<script>
import 'babel-polyfill'
import myUpload from 'vue-image-crop-upload'

export default {
  components: {
    myUpload
  },
  data() {
    return {
      show: false,
      imgDataUrl: 'https://instagram.fbfh3-1.fna.fbcdn.net/t51.2885-15/e35/21294520_275844862907983_67354703633055744_n.jpg',
      sizes: [{
          id: 1,
          width: 9
        },
        {
          id: 2,
          width: 8
        },
        {
          id: 3,
          width: 5
        },
        {
          id: 4,
          width: 4
        },
        {
          id: 5,
          width: 2
        },
      ],
      nextSizeId: 6,
      newSizeNumber: ''
    }
  },
  methods: {

    pdf: function() {
      const tela = document.getElementById('tela').innerHTML
      const tela_impressao = window.open('about:blank')

      tela_impressao.document.write(tela)
      tela_impressao.document.body.style.display = 'flex'
      tela_impressao.document.body.style.flexWrap = 'wrap'
      tela_impressao.window.print()
      tela_impressao.window.close()

    },
    addNewSize: function() {
      this.sizes.push({
        id: this.nextSizeId++,
        width: this.newSizeNumber
      })
      this.newSizeNumber = ''
    },

    removeSize: function(x) {
      console.log(x)
      this.sizes.splice(x, 1)
    },

    toggleShow() {
      this.show = !this.show
    },
    cropSuccess(imgDataUrl, field) {
      this.imgDataUrl = imgDataUrl
    },
    cropUploadSuccess(jsonData, field) {
      // console.log(jsonData)
      console.log('field: ' + field)
    },
    cropUploadFail(status, field) {
      // console.log(status)
      console.log('field: ' + field)
    }
  }
}
</script>


<style lang="scss" scoped>
small {
    margin-left: 5px;
    font-weight: 900;
}
.btn.btn-print {
    &:hover {
        background: #37ca5c;
    }
}
.btn {
    &:hover {
        background: #333;
        color: #fff;
    }
}
.img-tattoo {
    border: 1px solid #333;
    margin: 5px;
    position: relative;
}
.img-tattoo .btn-remove {
    position: absolute;
    top: 0;
    right: 0;
    display: none;
}
.img-tattoo:hover .btn-remove {
    display: block;
}
.btn.danger {
    font-weight: 900;
    font-size: 16px;
    line-height: 16px;
    &:hover {
        background: #333!important;
    }
}
a {
    color: #333;
}
.esp-btn {
    margin-top: 50px;
    margin-bottom: 50px;
    box-sizing: border-box;
}

.btn.btn-small {
    width: 40px;
    margin-left: 10px;
}
.input {
    height: 61px;
    line-height: 61px;
    padding-left: 10px;
    box-sizing: border-box;
    width: 300px;
    border-radius: 4px;
    border: none;
    background: transparent;
    border: 1px solid #ededed;
}
</style>
