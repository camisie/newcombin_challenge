<template>
  <div class="tableDiv">
  <v-simple-table height="300px">
    <template v-slot:default>
      <thead>
      <tr>
        <th class="text-left">
          First Name
        </th>
        <th class="text-left">
          Last Name
        </th>
        <th class="text-left">
          Address
        </th>
        <th class="text-left">
          SNN
        </th>
      </tr>
      </thead>
      <tbody>
      <tr
          v-for="user in users"
          :key="user.ssn"
      >
        <td>{{user.firstName}}</td>
        <td>{{user.lastName}}</td>
        <td>{{user.address}}</td>
        <td>{{user.ssn}}</td>
      </tr>

      </tbody>

    </template>

  </v-simple-table>
  </div>

</template>

<script>
export default {
  name: "AppTable",
  data () {
    return {
      users: [],
    }
  },
  mounted() {
    fetch("http://localhost:8081/api/members")
        .then(res => res.json())
        .then(data => this.users = data)
        .catch(err => console.log(err.message))
  }
}
</script>

<style scoped>

.tableDiv {
  background-color: white;
  width: 100%;
  height: 90%;
  align-content: center;
  text-align: left;
  margin-right: 20px;
  padding-right: 20px;
}

</style>