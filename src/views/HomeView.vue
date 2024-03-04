<template>
  <div>
    <div>
      <b-breadcrumb :items="items"></b-breadcrumb>
    </div>
    <div>
      <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        aria-controls="my-table"
      ></b-pagination>
    </div>
    <div>
      <b-table
        id="my-table"
        :items="data"
        :per-page="perPage"
        :current-page="currentPage"
        small
      ></b-table>
    </div>
  </div>
</template>

<script>
import {datos} from '../data'
export default {
  data() {
    return {
      data:datos,
      items: [
        {
          text: "Pagina principal",
          active: true,
        },
      ],
      perPage: 3,
      currentPage: 1,
    };
  },
  methods:{
    a(){
      console.log(this.data);
    }
  },
  computed: {
      rows() {
        return this.data.length
      }
    }
};
</script>

<style></style>
