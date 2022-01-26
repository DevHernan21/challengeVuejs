<template>
  <div>
    <Header />
    <div>
      <v-card>
        <v-card-title>
          Products
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
          <v-spacer></v-spacer>

          <v-dialog v-model="dialog" max-width="600px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                class="ma-2 float-right"
                color="deep-purple lighten-5"
                v-bind="attrs"
                v-on="on"
                >New Product
              </v-btn>
            </template>
            <AddProduct />
            <v-spacer></v-spacer>
            <v-btn text @click="dialog = false"> Cancel </v-btn>
          </v-dialog>
        </v-card-title>
        <v-data-table
          :headers="headers"
          :items="products"
          :search="search"
        >
        </v-data-table>
      </v-card>
    </div>
    <Footer />
  </div>
</template>
<script>
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import AddProduct from "@/components/AddProduct.vue";

import axios from "axios";

export default {
  name: "Products",
  data() {
    return {
      search: "",
      headers: [
        {
          text: "ID",
          align: "start",
          sortable: false,
          value: "_id",
        },
        { text: "SKU", value: "SKU" },
        { text: "Name", value: "name" },
        { text: "Description", value: "description" },
        { text: "Code", value: "code" },
        { text: "Price", value: "price" },
      ],
      products: [],
      dialog: false,
    };
  },
  components: {
    Header,
    Footer,
    AddProduct,
  },
  mounted: function () {
    if (localStorage.getItem("challenge_token")) {
      this.getProducts();
    } else {
      this.$router.push("/");
    }
  },
  methods: {
    getProducts: function () {
      axios
        .get("http://vps.churrasco.digital:3005/products", {
          headers: {
            Authorization: "Bearer " + localStorage.getItem("challenge_token"),
          },
        })
        .then((response) => {
          console.log(response.data);
          this.products = response.data;
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