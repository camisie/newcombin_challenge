<template>
  <div class="formDiv">
    <v-row>
      <v-col>
      <v-form
          ref="form"
          v-model="valid"
          lazy-validation
      >
        <v-text-field
          outlined
          v-model="formData.name"
          label="First Name"
          :rules="textRules"
          required
          >
        </v-text-field>

        <v-text-field
            outlined
            v-model="formData.lastName"
            label="Last Name"
            :rules="textRules"
            required
        >
        </v-text-field>

        <v-text-field
            outlined
            v-model="formData.address"
            label="Address"
            :rules="textRules"
            required
        >
        </v-text-field>

        <v-text-field
            outlined
            v-model="formData.ssn"
            label="SSN"
            :rules="ssnRules"
            required
        >
        </v-text-field>
      </v-form>
      </v-col>

      <v-col/>
    </v-row>

        <v-row>
          <v-col class="ml-lg-16" >
            <div class="buttons">
              <v-btn
                  class="mr-4"
                  @click="clear"
              >
                Reset
              </v-btn>

              <v-btn
                  class="mr-4"
                  :disabled="!valid"
                  @click="send"
              >
                Save
              </v-btn>
            </div>
          </v-col>
          <v-col>
          </v-col>
        </v-row>
    </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AppForm",
  data: () => ({
    valid: true,
    textRules: [
      v => !!v || "This field is required.",
      v => (v && v.replace(/^\s+|\s+$/gm,'').length > 1) || "This field must be at least 2 characters long."
    ],
    ssnRules: [
      v => !!v || "This field is required",
      v => (v && /^\d{3}-\d{2}-\d{4}$/.test(v)) || "This field must be in the format ###-##-####, just numbers",
      // v => (v && !this.ssns.includes(v)) || "This SSN is already in use."
    ],
    formData: {
      name: '',
      lastName: '',
      address: '',
      ssn: ''
    },
    ssns: [],
  }),

  methods: {
    clear(){
      this.formData = '';
    },
    async send () {
      this.$refs.form.validate();
      this.ssns.push(this.formData.ssn)
      await axios.post("http://localhost:8081/api/members", this.formData)
          .catch(err => console.log(err.message))
    },

  },

}
</script>

<style scoped>
form {
  width: 180%;
  margin: auto 35px;
  background: white;
}

v-text-field {
  display: block;
  width: 100%;
  box-sizing: border-box;
  border: 1px solid black;

}

.buttons {
  text-align: center;
  padding-left: 90px;
  margin-bottom: 100px;
  float: left;
  display:inline-flex;
}

.formDiv {
  background-color: white;
  width: 100%;
  height: 90%;
  align-content: center;
  text-align: left;
  margin-top: 10px;
  margin-bottom: 10px;
  margin-right: 20px;
  padding-right: 20px;
}

</style>