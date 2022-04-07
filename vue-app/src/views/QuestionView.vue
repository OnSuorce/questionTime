<template>
  <div class="container">
    <div v-if="question" class="mt-5">
      <h1>{{ question.content }}</h1>
      <p class="mb-0">
        Posted by:
        <span class="question-author">{{ question.author }}</span>
      </p>
      <p>{{question.created_at}}</p>
    </div>
    <div v-else>
      <h2 class="error text-center mt-5">
        There was an error retrieving this question
      </h2>
    </div>
    <hr>

    <div v-if="question">
      <AnswerComponent v-for="answer in answers" :key="answer.uuid" :answer="answer"/>
    </div>
    <div class="my-4">
        <button v-show="next" @click="getQuestions" class="btn btn-sm btn-outline-success w-100"> Load More </button>
        </div>
  </div>
</template>

<script>
import { axios } from "@/common/api.service.js";
import AnswerComponent from "@/components/answer.vue"
export default {
  components:{
    AnswerComponent
  },
  name: "question-view",
  props: {
    slug: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      question: {},
      answers: [],
      loadingAnswers: false,
      next: null
    };
  },
  created() {
    this.getQuestionData();
    this.getAnswers();
  },
  methods: {
    async getQuestionData() {
      let endpoint = `/api/v1/questions/${this.slug}/`;
      if(this.next){
        endpoint = this.next
      }
      try {
        const response = await axios.get(endpoint);

        if(response.status != 404){
          this.question = response.data;
          
        }
    
      } catch (error) {
        console.log(error.response);
        
      }
    },
    async getAnswers() {
      let endpoint = `/api/v1/questions/${this.slug}/answers`;
      if(this.next){
        endpoint = this.next
      }

      this.loadingAnswers = true
      try {
        const response = await axios.get(endpoint);
        console.log(response);

        this.answers.push(...response.data.results);
        this.loadingAnswers = false
        if (response.data.next) {
          this.next = response.data.next;
        } else {
          this.next = response.data.next;
        }
        console.log(this.questions);
      } catch (error) {
        console.log(error.response);
        alert(error.response.statusText);
      }
    }
  },
};
</script>

<style>
.error{
  color: red;
}
</style>