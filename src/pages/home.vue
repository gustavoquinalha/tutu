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
       <input v-model="newSizeNumber" v-on:keyup.enter="addNewSize" placeholder="Adicionar novo tamanho Ex: 400" class="input">
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
      	<div class="container column" v-for="x in sizes">
          <div class="img-tattoo">
            <button class="btn btn-small danger btn-remove" v-on:click="removeSize(index)">x</button>
        	  <img :src="imgDataUrl" :width="x.width + 'cm'" height="auto">
          </div>
      	</div>
      </div>
  </div>
</template>

<script>
import 'babel-polyfill'
import myUpload from 'vue-image-crop-upload'
import * as jsPDF from 'jspdf'

export default {
  components: {
    myUpload
  },
  data() {
    return {
      show: false,
      imgDataUrl: 'https://i.pinimg.com/564x/df/26/89/df268938fc471e3143d5acbf13396075.jpg',
      sizes: [{
          id: 1,
          width: 300
        },
        {
          id: 2,
          width: 250
        },
        {
          id: 3,
          width: 200
        },
        {
          id: 4,
          width: 150
        },
        {
          id: 5,
          width: 100
        },
      ],
      nextSizeId: 6,
      newSizeNumber: ''
    }
  },
  methods: {

    pdf: function() {
            var conteudo = document.getElementById('tela').innerHTML,
                tela_impressao = window.open('about:blank')

            tela_impressao.document.write(conteudo);
            tela_impressao.document.body.style.display='flex'
            tela_impressao.document.body.style.flexWrap='wrap'
            tela_impressao.window.print();
            tela_impressao.window.close();

    },
    //
    // pdf: function() {
    //   console.log("teste")
    //   var doc = new jsPDF()
    //
    //   doc.text('Hello world!', 10, 10)
    //   doc.save('a4.pdf')
    //
    // },

    addNewSize: function() {
      this.sizes.push({
        id: this.nextSizeId++,
        width: this.newSizeNumber
      })
      this.newSizeNumber = ''
    },

    removeSize: function(index) {
      this.sizes.splice(index, 1)
    },

    toggleShow() {
      this.show = !this.show
    },
    cropSuccess(imgDataUrl, field) {
      console.log('-------- crop success --------')
      this.imgDataUrl = imgDataUrl
    },
    cropUploadSuccess(jsonData, field) {
      console.log('-------- upload success --------')
      console.log(jsonData)
      console.log('field: ' + field)
    },
    cropUploadFail(status, field) {
      console.log('-------- upload fail --------')
      console.log(status)
      console.log('field: ' + field)
    }
  }
}
</script>


<style lang="scss" scoped>
.btn.btn-print {
  &:hover {
    background: #37ca5c
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
