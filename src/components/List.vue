<template>
  <div>
    <h1>Task</h1>

    <table border="1px">
      <tr>
        <td>userId:</td>
        <td>id:</td>
        <td>title:</td>
      </tr>
      <tr v-for="item in album" v-bind:key="item.id">
        <td>{{ item.userId }}</td>
        <td>{{ item.id }}</td>
        <td>{{ item.title }}</td>
      </tr>
    </table>
    <br /><br />

    <input type="number" placeholder="Enter userId" v-model="UserId"/><br /><br />
    <input type="number" placeholder="Enter id" v-model="Id"/><br /><br />
    <input type="text" placeholder="Enter title" v-model="Title"/> <br /><br />
    <button v-on:click="sum">Add User</button>

  </div>
</template>
<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);

export default {
  name: "jsonTable",
  data() {
    return {
      album: null,
      UserId: null,
      Id: null,
      Title: null
    };
  },
  mounted() {
    Vue.axios
      .get("https://jsonplaceholder.typicode.com/albums")
      .then((response) => {
        this.album = response.data;
      });
  },
  methods: {
    sum(){
        this.album.push({ userId: this.UserId, id: this.Id, title: this.Title })
    }
  }
};
</script>