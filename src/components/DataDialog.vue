<template>
  <div v-if="dialog.type == 'delete'" class="contenedor">
    <div class="textCont">
      <div class="texto">
        <p>{{ dialog.texto }}</p>
        <div class="categoryCont">
          <p><span>ID:</span> {{ dialog.id }}</p>
          <p><span>NOMBRE:</span> {{ dialog.name }}</p>
          <p><span>DESCRIPCIÓN:</span> {{ dialog.description }}</p>
        </div>
      </div>
      <div class="btnCont">
        <div class="Btn" @click="dialog.acept">ACEPTAR</div>
        <div class="Btn" @click="dialog.cancel">CANCELAR</div>
      </div>
    </div>
  </div>
  <div v-if="dialog.type == 'recategorize'" class="contenedor">
    <div class="textCont">
      <div class="texto">
        <p>{{ dialog.texto }}</p> 
      </div>
      <select name="type" id="type" v-model="selected">
        <option v-for="category in dialog.categorys" :key="category.id" :value="category.id">{{ category.name }}</option>
      </select>
      <div class="btnCont">
        <div class="Btn" @click="recategorizeCard">ACEPTAR</div>
        <div class="Btn" @click="dialog.cancel">CANCELAR</div>
      </div>
    </div>
  </div>
  <div v-if="dialog.type == 'rol'" class="contenedor">
    <div class="textCont">
      <div class="texto">
        <p>{{ dialog.texto }}</p> 
      </div>
      <select name="type" id="type" v-model="selected">
        <option value="ADMIN">ADMIN</option>
        <option value="USER">USER</option>
      </select>
      <div class="btnCont">
        <div class="Btn" @click="recategorizeRol">ACEPTAR</div>
        <div class="Btn" @click="dialog.cancel">CANCELAR</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name:"DataDialog",
  props: {
  },
  emits: ["update-type", "update-rol"],
  computed: {
    dialog() {
      return this.$store.getters.getDialog
    },
  },
  data() {
    return {
      selected: null,
    };
  },
  methods:{
    recategorizeCard() {
      this.$emit('update-type', this.selected);
    },
    recategorizeRol() {
      this.$emit('update-rol', this.selected);
    },
  },
};
</script>

<style scoped>
  .contenedor{
    z-index: 2;
    position: absolute;
    width: 100%;
    height: 100%;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    background-color: rgba(0, 0, 0, 0.5);
  }
  .textCont{
    position: relative;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
    width: 50%;
    height: 50%;
    border: 1px solid aqua;
    background-color: rgba(0, 0, 0, 0.5);
  }
  .texto{
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: aqua;
  }
  .categoryCont{
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-wrap: wrap;
    padding: 20px;
  }
  .categoryCont p{
    display: flex;
    align-items: center;
    justify-content: flex-start;
    width: 100%;
    border: 1px solid aqua;
    margin: 1px;
    border-radius: 5px;
  }
  .categoryCont span{
    width: 30%;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }
  .btnCont{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
  }
  .Btn{
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 3%;
    border: 1px solid aqua;
    color: aqua;
    cursor: pointer;
    margin-top: 10px;
    padding: 10px 50px;
  }
  .texto{
    width: 80%;
    text-align: right;
  }
</style>