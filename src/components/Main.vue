<template>
  <div class="container-main">
    <div id="titlePage">
      <h1 class="mb-30">Random Gif Cat</h1>
    </div>

    <form action="">
      <div class="container-input">
        <div>
          <div class="w-50 text-end"><label class="" for="title">Título</label></div>
          <div class="w-50 text-start"><input id="title" type="text" minlength="1" v-model="selected.title"></div>
        </div>

        <div class="mt-05rem">
          <div class="w-50 text-end"><label for="filter">Filtro</label></div>
          <div class="w-50 text-start">
            <select id="filter" v-model="selected.filter">
              <option v-for="(option, index) in optFilter" :key="index" v-bind:value="option.value">{{option.text}}
              </option>
            </select>
          </div>
        </div>

        <div class="flex mt-05rem">
          <div class="w-50 text-end"><label for="color">Color</label></div>
          <div class="w-50 text-start">
            <div class="flex flex--start">
              <select id="color" v-model="selected.color">
                <option v-for="(option, index) in optColor" :key="index" v-bind:value="option.value">{{option.text}}
                </option>
              </select>
              <div class="container-color" :style="{backgroundColor:selected.color}">
              </div>
            </div>
          </div>
        </div>

        <div class="mt-05rem">
          <div class="w-50 text-end"><label for="size">Tamaño</label></div>
          <div class="w-50 text-start"><input type="number" name="size" min="1" max="1000" id="size"
              v-model="selected.size"></div>
        </div>

      </div>
      <button class="mt-30 mb-30" v-on:click="getCat($event)">Obtener mi gatito</button>
    </form>

    <div v-if="selected.img!=null">
      <img :src="selected.img" alt="img cat">
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Main',
    data() {
      return {
        selected: {
          title: '',
          filter: 'blur',
          color: 'red',
          size: null,
          img: null
        },
        optFilter: [{
          value: 'blur',
          text: 'blur'
        }, {
          value: 'mono',
          text: 'mono'
        }, {
          value: 'sepia',
          text: 'sepia'
        }, {
          value: 'paint',
          text: 'paint'
        }, {
          value: 'pixel',
          text: 'pixel'
        }],
        optColor: [{
          value: 'red',
          text: 'rojo'
        }, {
          value: 'blue',
          text: 'azul'
        }, {
          value: 'green',
          text: 'verde'
        }, {
          value: 'white',
          text: 'blanco'
        }, {
          value: 'yellow',
          text: 'amarillo'
        }]
      }
    },
    methods: {
      requestAPI() {
        let url =
          `https://cataas.com/cat/gif/says/${this.selected.title}?filter=${this.selected.filter}&color=${this.selected.color}&size=${this.selected.size}&type=or`;
        this.selected.img = url;
        return;
        /*
        fetch(url)
          .then(response => this.selected.img = console.log(response))
          .catch(err => console.log(err))
        */
      },
      getCat(event) {
        event.preventDefault();
        this.selected.img = null;
        if (this.selected.title != '' && this.selected.size > 0 && this.selected.size <= 1000)
          this.requestAPI();
        else
          alert('Debe ingresar un titulo y un tamaño de 1 a 1000')
      }
    }
  }
</script>

<style scoped>
  .container-main {
    width: 100%;
    min-height: 100vh;
    text-align: center;
    color: #2c3e50;
    background-color: #acdae2;
    padding: 60px 0;
  }

  .container-input {
    background-color: #ee837e;
    padding: 20px 5%;
    text-align: left;
  }

  .container-color {
    display: inline-block;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: white;
    margin-left: 0.5rem;
  }

  .inline-block {
    display: inline-block;
  }

  .mt-30 {
    margin-top: 30px;
  }

  .mb-30 {
    margin-bottom: 30px;
  }

  .mt-05rem {
    margin-top: 0.5rem;
  }

  input,
  select {
    margin-left: 0.5rem;
  }

  .flex {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .flex--start {
    justify-content: start;
  }

  .text-center {
    text-align: center;
  }

  .text-start {
    text-align: start;
  }

  .text-end {
    text-align: end;
  }

  .w-50 {
    display: inline-block;
    width: 50%;
  }

  label {
    display: inline-block;
  }
</style>