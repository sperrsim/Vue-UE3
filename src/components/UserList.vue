<template>
  <div>
    <div v-if="error">
      <h2>Error: {{ error }}</h2>
    </div>
    <div v-else>
      <div v-if="loading">
        <h2>Loading data ....</h2>
      </div>
      <h1>Users</h1>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>UserName</th>
            <th>Address</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in data">
            <td>{{ item.name }}</td>
            <td>{{ item.username }}</td>
            <td>{{item.address.street}} {{item.address.suite}}, <br> {{item.address.zipcode}} {{item.address.city}} </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { useFetch } from '../composables/UseFetch.js';
export default {
  setup() {
    const { data, error, loading } = useFetch(
      'https://jsonplaceholder.typicode.com/users',
      {}
    );
    console.log(data.value);
    return {
      data,
      error,
      loading,
    };
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
}
table {
    border-collapse: collapse;
    margin: 25px 0;
    font-size: 0.9em;
    font-family: sans-serif;
    min-width: 400px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
    margin-left: auto;
    margin-right: auto;
}
thead tr {
  background-color: #009879;
    color: #ffffff;
    text-align: left;
}
th tr {
  padding: 12px 15px;
}
tbody tr {
  border-bottom: 1px solid #dddddd;
}
tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}
tbody tr.active-row {
    font-weight: bold;
    color: #009879;
}
</style>
