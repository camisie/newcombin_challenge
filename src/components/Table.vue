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
          v-for="member in members"
          v-bind:key="member.ssn"
      >
        <td>{{member.firstName}}</td>
        <td>{{member.lastName}}</td>
        <td>{{member.address}}</td>
        <td>{{member.ssn}}</td>
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
      members: [],
    }
  },

  mounted() {
    fetch("http://localhost:8081/api/members")
        .then(res => res.json())
        .then(data => this.members = data)
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