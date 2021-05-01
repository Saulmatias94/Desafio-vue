<template>
  <div id="IngresoDatos" class="p-2">
    <b-container class="border border-primary rounded py-2">
      <b-form @submit="onSubmit" @reset="limpiar" v-if="show">
        <h1 class="text-center">Añadir un producto.</h1>

        <b-form-group id="input-group-1" label="Nombre:" label-for="input-1">
          <b-form-input
            id="input-1"
            v-model="form.nombres"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-2"
          label="Descripcion"
          label-for="input-2"
        >
          <b-form-input
            id="input-2"
            v-model="form.descripcion"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Precio:" label-for="input-3">
          <span class="inline">$</span>
          <b-form-input
            id="input-3"
            v-model="form.precio"
            required
            type="number"
            min="1"
            step="1"
          ></b-form-input>
          
        </b-form-group>
        <b-button
          v-show="form.update"
          @click="update2"
          variant="success"
          class="m-2"
          >Editar</b-button
        >
        <b-button
          v-show="form.update == false"
          type="submit"
          variant="primary"
          class="m-2"
          >Añadir Producto</b-button
        >
        <b-button v-show="form.update == false" type="reset" variant="danger"
          >Limpiar</b-button
        >
      </b-form>

      <b-col class="">
        <b-table
          responsive
          hover
          :items="items"
          :fields="fields"
          :tbody-tr-class="rowClass"
          class="table table-bordered border-primary"
        >
          <template #cell(precio)="row">
            <span>${{ row.item.precio }}</span>
          </template>
          <template #cell(botones)="row">
            <b-button
              :disabled="form.update"
              variant="success"
              size="sm"
              @click="update(row.item.id)"
              class="m-1"
            >
              Editar
            </b-button>
            <b-button
              :disabled="form.update"
              variant="danger"
              size="sm"
              @click="deleteUser(row.item.id)"
            >
              Eliminar
            </b-button>
          </template>
        </b-table>
      </b-col>

      <b-card class="mt-3" header="Form Data Result">
        <pre class="m-0">{{ items }}</pre>
      </b-card>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "IngresoDatos",
  data() {
    return {
      form: {
        nombres: "",
        descripcion: "",
        precio: "",
        signo: "$",
        update: false,
      },
      show: true,
      items: [],
      fields: [
        { key: "nombres", label: "Nombre" },
        { key: "descripcion", label: "Descripcion", class: "text-center" },
        { key: "precio", label: "Precio", class: "text-center" },
        { key: "botones", label: "Cambios", class: "text-center" },
      ],
      con: 0,
    };
  },
  methods: {
    rowClass(item) {
      if (!item.update) return "table-default";
      if (item.update) return "table-waryarning";
    },
    onSubmit(event) {
      event.preventDefault();
      this.items.push({
        id: this.con,
        nombres: this.form.nombres,
        descripcion: this.form.descripcion,
        precio: this.form.precio,
        update: false,
      });
      this.form.nombres = "";
      this.form.descripcion = "";
      this.form.precio = "";
      this.con++;
    },
    deleteUser(id) {
      for (let i = 0; i < this.items.length; i++) {
        if (id == this.items[i].id) {
          this.items.splice(i, 1);
        }
      }
    },
    update(id) {
      for (let i = 0; i < this.items.length; i++) {
        if (id == this.items[i].id) {
          this.form.nombres = this.items[i].nombres;
          this.form.descripcion = this.items[i].descripcion;
          this.form.precio = this.items[i].precio;
          this.form.update = true;
          this.items[i].update = true;
        }
      }
    },
    update2() {
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i].update) {
          this.items[i].nombres = this.form.nombres;
          this.items[i].descripcion = this.form.descripcion;
          this.items[i].precio = this.form.precio;
          this.items[i].update = false;
          this.form.nombres = "";
          this.form.descripcion = "";
          this.form.precio = "$";
          this.form.update = false;
        }
      }
    },
    limpiar() {
      this.form.nombres = "";
      this.form.descripcion = "";
      this.form.precio = "";
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
  },
};
</script>
