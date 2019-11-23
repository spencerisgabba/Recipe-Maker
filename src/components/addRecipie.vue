<template>
  <v-app class="form-group flex items-center flex-col">
    <v-form
      lazy-validation
      v-model="valid"
      ref="form"
      id="addRecipe"
      @submit.prevent="handleSubmit"
    >
      <v-card>
        <v-text-field
          class="px-5 pt-5 instruct"
          :rules="titleRules"
          v-model="recipie.message"
          label="Title"
          required
        ></v-text-field>
      </v-card>
      <v-card>
        <v-textarea
          v-model="recipie.guide"
          :rules="sumRules"
          name="input-7-1"
          label="Recipe Summary"
          class="instruct p-5"
          required
        ></v-textarea>
      </v-card>
      <v-slider
        v-model="steps"
        label="Steps"
        min="2"
        max="6"
        thumb-label="always"
        ticks="always"
        tick-size="10"
        class="mt-10"
      ></v-slider>
      <v-stepper v-model="e1" class="w-full">
        <v-stepper-header>
          <template v-for="n in steps">
            <v-stepper-step :key="`${n}-step`" :complete="e1 > n" :step="n" editable>Step {{ n }}</v-stepper-step>

            <v-divider v-if="n !== steps" :key="n"></v-divider>
          </template>
        </v-stepper-header>

        <v-stepper-items>
          <v-stepper-content v-for="n in steps" :key="`${n}-content`" :step="n">
            <v-card class="mb-12" color=" lighten-1" height="200px">
              <v-textarea v-model="recipie.stepper[n]" :rows="8" auto-grow outlined></v-textarea>
            </v-card>

            <v-btn color="blue" @click="nextStep(n)">Next Step</v-btn>
          </v-stepper-content>
        </v-stepper-items>
      </v-stepper>
      <v-btn
        type="submit"
        form="addRecipe"
        class="text-white text-xl p-2 mt-5 mb-10 btn"
      >Add Recipie</v-btn>
      <v-snackbar :timeout="3000">
        Successfully Added Recipe!
        <v-btn dark text @click="snackbar = false">Close</v-btn>
      </v-snackbar>
    </v-form>
  </v-app>
</template>

<script>
export default {
  name: "add",
  data() {
    return {
      e1: 1,
      steps: 2,
      valid: true,

      titleRules: [v => !!v || "Title is required"],
      sumRules: [v => !!v || "Summary is required"],
      recipie: {
        message: "",
        guide: "",
        stepper: ["", ""]
      }
    };
  },
  watch: {
    steps(val) {
      if (this.e1 > val) {
        this.e1 = val;
      }
    }
  },
  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        this.snackbar = true;
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },

    handleSubmit() {
      if (this.$refs.form.validate()) {
        this.$emit("add:recipie", this.recipie);

        // this.$refs.form.reset();
        this.snackbar = true;
      }
    },
    nextStep(n) {
      if (n === this.steps) {
        this.e1 = 1;
      } else {
        this.e1 = n + 1;
      }
    }
  }
};
</script>

<style scoped>
.stepper {
  width: 60em;
}
.instruct {
  width: 50em;
}

.input {
  border: 3px solid #3c9d9b;
}

.btn {
  background-color: rgb(63, 174, 218);
  border: 2px solid black;
}
</style>