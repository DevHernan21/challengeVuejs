<template>
  <div>
    <v-card class="pa-10">
      <v-row>
        <v-col cols="12" md="12"> Add your new Product </v-col>
      </v-row>
      <v-spacer></v-spacer>
      <form @submit.prevent="sendForm">
        <v-row>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="form.name"
              label="Name "
              prepend-icon="mdi-rename-box"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="form.description"
              label="Description "
              prepend-icon="mdi-text-box"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="form.code"
              label="Code "
              prepend-icon="mdi-barcode"
              type="number"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="form.price"
              label="Price"
              prepend-icon="mdi-cash"
              type="number"
              :rules="priceRules"
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="form.currency"
              label="Currency "
              prepend-icon="mdi-currency-usd"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field v-model="form.v" label="__v " type="number">
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="6">
            <v-text-field
              type="text"
              v-model="form.sku"
              prepend-icon="mdi-barcode"
              label="SKU "
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              type="text"
              v-model="form.pictures"
              prepend-icon="mdi-image-filter-drama"
              label="URL Pictures "
            >
            </v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-divider></v-divider>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="12">
            <v-btn
              class="ma-2 float-right"
              color="deep-purple lighten-5"
              type="submit"
            >
              Create
            </v-btn>
          </v-col>
        </v-row>
      </form>
    </v-card>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "AddProduct",
  data() {
    return {
      form: {
        name: "",
        description: "",
        code: 0,
        price: 0,
        pictures: [],
        currency: "$",
        v: 0,
        sku: "",
      },
      priceRules: [
        (v) => !!v || "Price is required",
        (v) => v > 0 || "Price must be greater than 0"
        ],
    };
  },
  components: {},
  methods: {
    sendForm() {
      console.log(this.form)
      const formData = {
        name: this.form.name,
        description: this.form.description,
        code: this.form.code,
        price: this.form.price,
        pictures: this.form.pictures,
        currency: this.form.currency,
        __v: this.form.v,
        SKU: this.form.sku,
      };
      axios
        .post(
          "http://vps.churrasco.digital:3005/addproduct",
          formData,
          {
            headers: {
              Authorization: `Bearer ${localStorage.getItem("challenge_token")}`,
              
            },
            
          }
        )
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    },
        
    
  },
};
</script>
<style scoped>
</style>