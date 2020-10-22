<template>
  <div class="">
  
    <h1 class="text-center text-gray-900 text-4xl mt-32 mb-16">Datatable with <span class="font-bold text-indigo-600">Vue</span></h1>

    <div class="p-8 mt-6 lg:mt-0 rounded shadow bg-white mb-10">
      <table id="table" class="stripe hover " style="width:100%; padding-top: 1em;  padding-bottom: 1em;">
        <thead>
          <tr>
            <th data-priority="1">#</th>
            <th data-priority="2">Code</th>
            <th data-priority="3">Title</th>
            <th data-priority="4">Price</th>
            <th data-priority="5">Description</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody class="">
          <tr v-for="(product, i) in this.products" :key="product.id">
            <th scope="row" class="font-medium">{{i}}</th>
            <th class="font-normal">{{product.code}}</th>
            <th class="font-normal">{{product.title}}</th>
            <th class="font-normal">{{product.price}}</th>
            <th class="font-normal">{{product.description}}</th>
            <th class="lg:flex items-center">
              <button class="bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 px-4 mr-2 mb-1 lg:mb-0 rounded">Edit</button>
              <button class="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded">Delete</button>
            </th>
          </tr>
        </tbody>
      </table>  
    </div>

  </div>
</template>

<script>
import axios from 'axios';
import $ from 'jquery';
import datatables from 'datatables';

export default {
  name: 'DataTable',
  data() {
    return {
      products: []
    }
  },

  beforeCreate(){
    axios.defaults.headers.common['token'] = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1ZjgwODdiMTA0YzcxMjA0NDNmMzA1MDIiLCJpYXQiOjE2MDIzMDczNTQsImV4cCI6MTYwMjM5Mzc1NH0.RVJKpm7TwM2btK233M10KBuQLg2N5SIRdgM8giZ1a1Q';
  },

  mounted() {
    this.getProducts();
  },

  methods: {

    getProducts() {
      const URL = 'http://localhost:5000/api/product/list';
      axios.get(URL)
        .catch((err) => {
          console.error(err);
        })
        .then((response) => {
          this.products = response.data;
          this.initDatatable();
        });
    },

    // initialize DataTable
    initDatatable(){  
      $(function(){
        $('#table').DataTable({
          responsive: true
        })
        .columns.adjust();
      });
    }

  }
}
</script>
