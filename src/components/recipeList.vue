<template>
  <div id="Hey" class="flex justify-center flex-wrap sm:mx-20">
    <v-card class="mx-auto mt-10" max-width="600" v-for="recipie in recipie" :key="recipie.id">
      <v-card-title class="text-center text-3xl mb-10 bg-gray-200 flex justify-between">
        {{recipie.message}}
        <v-btn @click="$emit('delete:recipie', recipie.id)">Delete</v-btn>
      </v-card-title>

      <v-card-subtitle class="text-xl font-semibold py-4">Foreword:</v-card-subtitle>

      <v-card-text class>
        <div>{{recipie.guide}}</div>

        <div>
          <p class="text-xl font-semibold py-4">Instructions:</p>
          <p v-for="step in recipie.stepper" :key="step" class="p-5 pt-0">{{step}}</p>
        </div>
      </v-card-text>

      <v-card-actions>
        <v-btn color="orange" text>Share</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "Hey",
  props: {
    recipie: Array,
    steps: String
  }
};
</script>

<style scoped>
.card {
  height: 28em;
  width: 45em;
  background-color: #394a6d;
  color: white;
}
.name {
  background-color: #2e3c58;
  padding-bottom: 0.1em;
}
</style>