<template>
  <div class="logInFormDiv">
    <v-container>
      <v-form v-model="valid">
        <v-row>
          <v-col cols="12" md="4">
            <v-text-field v-model="name" :rules="nameRules" label="Name" required></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="4">
            <v-text-field v-model="pw" :rules="pwRules" :counter="8" label="Password" required></v-text-field>
          </v-col>
        </v-row>
      </v-form>
      <v-row>
        <v-col cols="12" md="4">
          <div class="error">{{error}}</div>

          <v-btn color="primary">Log in</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  data() {
    return {
      pw: "",
      name: "",
      valid: false,
    };
  },
  props: {
    nameRules: {
      type: Array,
      required: false,
      default: function () {
        return;
        [
          function (input: String): String {
            let errorMessage = "";
            if (input.length < 5) {
              errorMessage = "Name must be at least 5 characters";
              console.log("short");
            }
            return errorMessage;
          },
        ];
      },
    },

    pwRules: {
      type: Array,
      required: false,
      default: function () {
        return;
        [
          function (input: String): String {
            let errorMessage = "";
            if (input.length < 8) {
              errorMessage = "Password must be at least 8 characters";
            }
            return errorMessage;
          },
        ];
      },
    },
  },
  computed: {
    error() {
      if (this.name.length === 0) {
        return "Required";
      } else if (this.name.length < 5) {
        return "Name must be at least 5 characters";
      }
    },
  },
});
</script>

<style scoped>
.logInFormDiv {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.logInFormDiv button {
  max-width: 8rem;
}
.error {
  max-width: 8rem;
}
.row {
  justify-content: center;
}
button {
  justify-content: center;
}
</style>