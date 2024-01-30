<template>
  <div>
    <b-form>
      <b-row>
        <b-col cols="12" sm="12" md="4">
          <b-form-group id="name-group" label="Nombre:" label-for="name-input">
            <b-form-input
              id="name-input"
              type="text"
              placeholder="Ingresa tu nombre"
              v-model="v$.name.$model"
              @blur="v$.name.$touch"
              :state="v$.name.$dirty ? !v$.name.$error : null"
            >
            </b-form-input>
            <b-form-invalid-feedback v-if="v$.name.$error"
              >Campo obligatorio</b-form-invalid-feedback
            >
          </b-form-group>
        </b-col>
        <b-col cols="12" sm="12" md="4">
          <b-form-group id="surname-group">
            <label for="surname-input">Apellido paterno:</label>
            <b-form-input
              id="surname-input"
              type="text"
              placeholder="Ingresa tu apellido paterno"
              v-model="v$.surname.$model"
              @blur="v$.surname.$touch"
              :state="v$.surname.$dirty ? !v$.surname.$error : null"
            >
            </b-form-input>
            <b-form-invalid-feedback v-if="v$.surname.$error"
              >Campo obligatorio</b-form-invalid-feedback
            >
          </b-form-group>
        </b-col>
        <b-col cols="12" sm="12" md="4">
          <b-form-group id="lastname-group">
            <label for="lastname-input">Apellido materno:</label>
            <b-form-input
              id="lastname-input"
              type="text"
              placeholder="Ingresa tu apellido materno"
              v-model="v$.lastname.$model"
              @blur="v$.lastname.$touch"
              :state="v$.lastname.$dirty ? !v$.lastname.$error : null"
            >
            </b-form-input>
            <b-form-invalid-feedback v-if="v$.lastname.$error"
              >Campo obligatorio</b-form-invalid-feedback
            >
          </b-form-group>
        </b-col>
      </b-row>
      <b-row class="mt-4">
        <b-col cols="12" sm="12" md="4">
          <b-form-group
            id="cp-group"
            label="Código postal:"
            label-for="cp-input"
          >
            <b-form-input
              id="cp-input"
              type="text"
              placeholder="Ingresa tu código postal"
              @keypress="signal"
              min="0"
              maxlength="5"
              v-model="v$.postalCode.$model"
              @blur="v$.postalCode.$touch"
              :state="v$.postalCode.$dirty ? !v$.postalCode.$error : null"
            >
            </b-form-input>
            <b-form-invalid-feedback v-if="v$.postalCode.$error"
              >Campo obligatorio</b-form-invalid-feedback
            >
          </b-form-group>
        </b-col>
        <b-col cols="12" sm="12" md="4">
          <b-form-group id="street-group">
            <label for="street-input">Calle:</label>
            <b-form-input
              id="street-input"
              type="text"
              placeholder="Ingresa tu calle"
              v-model="v$.street.$model"
              @blur="v$.street.$touch"
              :state="v$.street.$dirty ? !v$.street.$error : null"
            >
            </b-form-input>
            <b-form-invalid-feedback v-if="v$.street.$error"
              >Campo obligatorio</b-form-invalid-feedback
            >
          </b-form-group>
        </b-col>
        <b-col cols="12" sm="12" md="4">
          <b-form-group id="number-group">
            <label for="number-input">Número (#):</label>
            <b-form-input
              id="number-input"
              type="text"
              placeholder="Ingresa el número de tu dirección"
              v-model="v$.number.$model"
              @blur="v$.number.$touch"
              :state="v$.number.$dirty ? !v$.number.$error : null"
            >
            </b-form-input>
            <b-form-invalid-feedback v-if="v$.number.$error"
              >Campo obligatorio</b-form-invalid-feedback
            >
          </b-form-group>
        </b-col>
      </b-row>
      <b-row class="mt-4">
        <b-col cols="12" sm="12" md="4">
          <b-form-group id="city-group" label="Ciudad:" label-for="city-input">
            <b-form-input
              id="city-input"
              type="text"
              placeholder="Ingresa tu ciudad"
              v-model="v$.city.$model"
              @blur="v$.city.$touch"
              :state="v$.city.$dirty ? !v$.city.$error : null"
            >
            </b-form-input>
            <b-form-invalid-feedback v-if="v$.city.$error"
              >Campo obligatorio</b-form-invalid-feedback
            >
          </b-form-group>
        </b-col>
        <b-col cols="12" sm="12" md="4">
          <b-form-group id="birthday-group">
            <label for="birthday-input">Fecha de nacimiento:</label>
            <b-form-input
              id="birthday-input"
              type="date"
              placeholder="Ingresa tu fecha de naciemiento"
            >
            </b-form-input>
          </b-form-group>
        </b-col>
        <b-col cols="12" sm="12" md="4">
          <b-form-group id="email-group">
            <label for="email-input">Correo electrónico:</label>
            <b-form-input
              id="email-input"
              type="email"
              placeholder="Ingresa el número de tu dirección"
              v-model="v$.email.$model"
              @blur="v$.email.$touch"
              :state="v$.email.$dirty ? !v$.email.$error : null"
            >
            </b-form-input>
            <b-form-invalid-feedback v-if="!v$.email.required"
              >Campo obligatorio</b-form-invalid-feedback
            >
            <b-form-invalid-feedback v-if="v$.email.email && v$.email.required"
              >Correo no válido</b-form-invalid-feedback
            >
          </b-form-group>
        </b-col>
        <b-col cols="12" sm="12" class="mt-4">
          <b-form-group>
            <label for="email-input">Fotografía:</label>
            <b-form-file
              multiple
              placeholder="Selecciona un archivo"
              browse-text="Buscar"
            ></b-form-file>
          </b-form-group>
        </b-col>
      </b-row>
      <b-row class="mt-4">
        <b-col cols="12" sm="12" class="d-flex flex-row-reverse">
          <b-button variant="secondary">
            Enviar
          </b-button>
        </b-col>
      </b-row>
    </b-form>
  </div>
</template>
ß
<script>
import Vue from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required, email } from "@vuelidate/validators";
// const signal = (event) => {
//   if ((event.charCode >= 48 && event.charCode <= 57) || event.charCode == 46)
//     return true;
//   else return false;
// };
export default Vue.extend({
  name: "FormValidation",
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      name: "",
      surname: "",
      lastname: "",
      postalCode: "",
      street: "",
      number: "",
      city: "",
      birthday: "",
      email: "",
      photo: "",
    };
  },
  methods: {
    signal(event) {
      // Verifica si el evento contiene un dígito del 0 al 9
      if (event.keyCode >= 48 && event.keyCode <= 57) {
        return true; // Permitir dígitos del 0 al 9
      } else {
        event.preventDefault(); // Previene la acción predeterminada del evento
        return false; // Rechazar cualquier otro carácter
      }
    },
  },
  validations() {
    return {
      name: { required },
      surname: { required },
      lastname: {},
      postalCode: { required },
      street: { required },
      number: { required },
      city: { required },
      birthday: {},
      email: { required, email },
    };
  },
});
</script>
