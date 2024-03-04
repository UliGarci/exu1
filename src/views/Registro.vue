<template>
  <div>
    <div><b-breadcrumb :items="items"></b-breadcrumb></div>
    <div class="col col-sm-3">
      <b-form @submit.prevent="onSubmit">
        <b-form-group class="fstyle" label="Nombre:">
          <b-form-input
            v-model="form.nombre"
            type="text"
            placeholder="Ingrese su nombre"
            required
          ></b-form-input>
          <p v-if="errors.nombre">{{ errors.nombre }}</p>
        </b-form-group>

        <b-form-group class="fstyle" label="Edad:">
          <b-form-input
            type="number"
            v-model="form.edad"
            placeholder="Ingrese su edad"
            min="1"
            max="100"
          ></b-form-input>
        </b-form-group>

        <b-form-group class="fstyle" label="Cuatrimestre:">
          <b-form-input
            v-model="form.cuatrimestre"
            placeholder="Ingrese el cuatrimestre 1-12"
            type="number"
            min="1"
            max="12"
          ></b-form-input>
        </b-form-group>

        <b-form-group class="fstyle" label="Carrera:">
          <b-form-input v-model="form.carrera" placeholder="Ingrese carrera"> </b-form-input>
          <p v-if="errors.carrera">{{ errors.carrera }}</p>
        </b-form-group>

        <b-form-group class="fstyle">
          <b-button type="submit" variant="primary">Submit</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
        </b-form-group>
        
      </b-form>
    </div>
  </div>
</template>

<script>
import { datos } from "../data";
export default {
  data() {
    return {
      items: [
        {
          text: "Pagina principal",
          to: "/home",
        },
        {
          text: "Registro",
          active: true,
        },
      ],
      form: {
        nombre: "",
        carrera: "",
        edad: "",
        cuatrimestre: "",
        id: "",
      },
      errors: {},
      validado: false,
    };
  },
  methods: {
    onSubmit(event) {
      const regex = /[^a-zA-Z]/g;
      this.errors = {};
      this.validado = true;
      if (regex.test(this.form.nombre)) {
        this.errors.nombre = "Solo se permiten letras";
        this.validado = false;
      }

      if (regex.test(this.form.carrera)) {
        this.errors.carrera = "Solo se permiten letras";
        this.validado = false;
      }

      if (this.validado === true) {
        const lastId = datos.length > 0 ? datos[datos.length - 1].id : 0;
        let newId = lastId + 1;
        this.form.id = newId;
        datos.push({ ...this.form });
        alert("Se registro exitosamente")
        this.form.nombre = "";
        this.form.carrera = "";
        this.form.cuatrimestre=""
        this.form.edad= ""
      }
    },
  },
};
</script>

<style>
.fstyle{
  margin-top: 15px;
  margin-left: 25px;
}
</style>
