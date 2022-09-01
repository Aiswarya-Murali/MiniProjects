<template>
    <v-card flat class="text-center">
        <v-card-title class="text-center">Quiz</v-card-title>
        <v-card v-if="!finished" outlined width="50%" class="ma-auto">
            <v-list dense v-for="q in questions" :key="q.id" v-show="q.id === tab">
                <div class="d-flex mx-3">
                <v-subheader>{{q.question}}</v-subheader>
                <v-card-subtitle class="mr-0 ml-auto">Score{{currentScore}}/{{questions.length}}</v-card-subtitle>
                </div>
                    <v-list-item-group
                        v-model="q.selected"
                        color="primary"
                        class="text-left"
                    >
                        <v-list-item
                        v-for="(item, i) in q.options"
                        :key="i"
                        class="text-left">
                        <v-list-item-content >
                           <v-btn min-width="100%" :color="i=== q.answer && i=== q.selected ? 'success' : i=== q.selected ? 'error': '#bdabab'" @click="q.selected = i"> <v-list-item-title v-text="item"></v-list-item-title></v-btn>
                        </v-list-item-content>
                        </v-list-item>
                    </v-list-item-group>
            </v-list>
            <v-btn color="success" primary v-if="tab===questions.length -1" @click="finished = true">Finish</v-btn>
            <v-btn color="success" primary v-else @click="tab = tab+1">Next question</v-btn>
        </v-card>
        <v-card v-else>
            <v-card-subtitle> Finished Quiz</v-card-subtitle>
            <v-card-text>Your score {{currentScore}}/{{questions.length}}</v-card-text>
        </v-card>
    </v-card>
</template>
<script setup>
  let tab = ref(0)
  let finished = ref(false)
  const questions = ref([
      {
          id: 0,
          question: 'What is Vue?',
          answer:0,
          options: [
              'Front end frame work',
              'Back end frame work',
              'IDE'
          ],
          selected: null,
      },
      {
          id: 1,
          question: 'What is Vuex',
          answer:1,
          options: [
              'Routing plugin',
              'State management library',
              'Vue template'
          ],
          selected: null,
      },
      {
          id: 2,
          question: 'What is VSCode',
          answer:2,
          options: [
              'Front end frame work',
              'Back end frame work',
              'IDE'
          ],
          selected: null,
      }
  ])
  const currentScore = computed(() => {
      let value = 0
      questions.value.map(q => {
          if (q.answer === q.selected) {
              value ++
          }
      })
      return value
  })

</script>