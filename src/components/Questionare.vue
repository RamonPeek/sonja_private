<template>
  <v-container>
    <v-row class="d-flex justify-center">
      <v-col cols="9" xxl="7" class="pe-10">
        <div>
          <v-card class="pa-3 elevation-0 rounded-xxl mt-16" :style="{backgroundColor: rgbToHex(category.color), transform: 'rotate(-3deg)'}">
            <v-card class="bg-white pa-3 elevation-0 rounded-xxl">
              <v-card class="pa-12 elevation-0 rounded-xxl" :style="{backgroundColor: rgbToHex(category.color)}">
                <div class="ma-12" :style="{ transform: 'rotate(3deg)'}">
                  <h1 class="text-white pb-3">{{ currentQuestion.title }}</h1>
                  <p class="text-white pb-8 question-text">{{ currentQuestion.question }}</p>
                  <v-checkbox hide-details="auto" v-for="(answer, index) in currentQuestion.answers" :key="index"
                    v-model="givenAnswers" class="text-white answer-label-text pt-1"
                    :value="answer"
                  >
                    <template v-slot:label>
                      <span class="answer-label-text ps-6 pb-1">{{ answer.text }}</span>
                    </template>
                  </v-checkbox>
                  <div class="d-flex justify-end">
                    <v-col cols="2">
                      <v-btn @click="answer" :disabled="storingAnswer || !givenAnswers?.length" class="mt-10" rounded="xl" size="x-large" block>Volgende</v-btn>
                    </v-col>
                  </div>
                </div>
              </v-card>
            </v-card>
          </v-card>
      </div>
      </v-col>
      <v-col cols="3">
        <img :src="require('@/assets/logo.jpeg')" style="max-width: 100%">
        <div class="mt-4">
          <b style="font-size: 2rem" class="ps-4">
            {{ category.title }}
          </b>
          <div class="pt-2">
            <div :style="{'border-left': '2px solid ' + rgbToHex(category.color)}">
              <p class="ps-4" style="font-size: 1.6rem" :style="{color: rgbToHex(category.color), fontWeight: subCategory.id == currentQuestion.id ? 'bold' : '400'}"
              v-for="subCategory in category.parts" :key="subCategory.id">
                {{ subCategory.title }}
              </p>
            </div>
          </div>
        </div>
      </v-col>
    </v-row>
  </v-container>
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
<style scoped>

.rounded-xxl {
  border-radius:180px;
}

h1 {
  font-size: 5rem;
}

.question-text {
  font-size: 2.5rem;
}

.answer-label-text {
  font-size: 2rem;
}

</style>