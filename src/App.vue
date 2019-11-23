<template>
  <div id="app">
    <v-card>
      <v-toolbar flat color="primary" dark>
        <v-toolbar-title>Recipe Manager</v-toolbar-title>
      </v-toolbar>
      <v-tabs centered show-arrows>
        <v-tab>
          <v-icon left>mdi-account</v-icon>My Recipies
        </v-tab>
        <v-tab>
          <v-icon left>mdi-lock</v-icon>Add Recipe
        </v-tab>

        <v-tab-item>
          <v-card flat>
            <v-card-text>
              <Hey v-bind:recipie="recipie" class="hey" @delete:recipie="deleteRecipie" />
            </v-card-text>
          </v-card>
        </v-tab-item>
        <v-tab-item>
          <v-card flat>
            <v-card-text>
              <add @add:recipie="addRecipie" />
            </v-card-text>
          </v-card>
        </v-tab-item>
      </v-tabs>
    </v-card>
  </div>
</template>

<script>
import Hey from "./components/recipeList";
import add from "./components/addRecipie";
import "./assets/css/main.css";

export default {
  name: "app",
  components: {
    Hey,
    add
  },
  data() {
    return {
      drawer: null,
      items: [
        { title: "Home", icon: "dashboard" },
        { title: "About", icon: "question_answer" }
      ],

      recipie: [
        {
          id: 1,
          message: "Fettuccine Alfredo",
          guide:
            "Fettucine Alfredo is one of my favorite dishes for its versatility. It has become a comfort food for me and my family. It's never hard to find good fettucine. And if you don't have the money you can make it with 3 ingredients.",
          stepper: [
            "Bring a salt water mixture to a low boil, add the fettucine.",
            "While the fettucine is boiling, heat alfredo sauce to a low simmer, leave covered until fettucine finishs",
            "Add Fettucine to Alfredo, along with one cup of pasta water. Simmer uncovered for 15 minutes then serve"
          ]
        },
        {
          id: 2,
          message: "Pesto Grilled Cheese",
          guide:
            "I first had this sandwich at a small restaurant and immediately went home to duplicate the recipe. I've been making my grilled cheese sandwiches this way ever since!",
          stepper: [
            "Bring a salt water mixture to a low boil, add the fettucine.",
            "While the fettucine is boiling, heat alfredo sauce to a low simmer, leave covered until fettucine finishs",
            "Add Fettucine to Alfredo, along with one cup of pasta water. Simmer uncovered for 15 minutes then serve"
          ]
        }
      ]
    };
  },
  methods: {
    deleteRecipie(id) {
      this.recipie = this.recipie.filter(recipie => recipie.id !== id);
    },
    addRecipie(message) {
      const lastId =
        this.recipie.length > 0 ? this.recipie[this.recipie.length - 1].id : 0;
      const id = lastId + 1;
      const newRecipie = { ...message, id };

      this.recipie = [...this.recipie, newRecipie];
    }
  }
};
</script>

<style>
#app {
  overflow-x: hidden;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
