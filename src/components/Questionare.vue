<template>
  <div>
    {{ storingAnswer }}
    {{ givenAnswers }}
    <div class="d-flex justify-center">
      <v-col cols="12" xs="12" sm="12" md="12" lg="12" xl="9" xxl="8">
        <v-card class="pa-3 elevation-0 rounded-pill" :style="{backgroundColor: rgbToHex(category.color)}">
          <v-card class="bg-white pa-3 elevation-0 rounded-pill">
            <v-card class="pa-12 elevation-0 rounded-pill" :style="{backgroundColor: rgbToHex(category.color)}">
              <div class="ma-12">
                <h1 class="text-white pb-3">{{ currentQuestion.title }}</h1>
                <p class="text-white pb-3">{{ currentQuestion.question }}</p>
                <v-checkbox hide-details="auto" v-for="(answer, index) in currentQuestion.answers" :key="index"
                  v-model="givenAnswers" class="text-white"
                  :value="answer" :label="answer.text"
                ></v-checkbox>
                <v-btn @click="answer" :disabled="storingAnswer || !givenAnswers?.length">Answer</v-btn>
              </div>
            </v-card>
          </v-card>
        </v-card>
      </v-col>
    </div>
  </div>
</template>

<script>

export default {
  name: 'QuestionaireComponent',
  emits: ["answered"],
  props: {
    category: {
      type: Object,
      required: true
    },
    currentQuestion: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      givenAnswers: [],
      storingAnswer: false
    }
  },
  methods: {
    rgbToHex(color) {
      return "#" + (1 << 24 | color.r << 16 | color.g << 8 | color.b).toString(16).slice(1);
    },
    answer() {
      if(this.givenAnswers?.length) {
        this.storingAnswer = true;
          setTimeout(() => {
            this.$emit("answered", {
              categoryId: this.category.id,
              questionId: this.currentQuestion.id,
              answerValues: this.givenAnswers
            });
            this.givenAnswers = [];
            this.storingAnswer = false;
          }, 250)
      }
    }
  }
}
</script>
