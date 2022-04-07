<template>
  <div class="home mt-2">
    <div class="container">
      <div v-for="question in questions" :key="question.uuid">
        <div class="card shadow bg-body m-5 rounded" v-on:click="goToQuestion(question.slug)">
          <div class="card-header">
            Posted by:
            <span class="question-author">{{ question.author }}</span>
          </div>
          <div class="card body p-4 p-2 mb-3 border-0">
            <h3>{{ question.content }}</h3>
            <p class="mb-0 card-text text-muted">
              Answers: {{ question.answers_count }}
            </p>
          </div>
       
        
      </div>
      </div>
      <div class="my-4">
        <button v-show="next" @click="getQuestions" class="btn btn-sm btn-outline-success w-100"> Load More </button>
        </div>
    </div>
  </div>
     
</template>

<script>
// @ is an alias to /src
import { axios } from "@/common/api.service.js";

export default {
  name: "HomeView",
  data() {
    return {
      questions: [],
      next: null,
    };
  },
  methods: {
    async getQuestions() {
      let endpoint = "/api/v1/questions/";
      if(this.next){
        endpoint = this.next
      }
      try {
        const response = await axios.get(endpoint);
        console.log(response);

        this.questions.push(...response.data.results);

        if (response.data.next) {
          this.next = response.data.next;
        } else {
          this.next = null;
        }
        console.log(this.questions);
      } catch (error) {
        console.log(error.response);
        alert(error.response.statusText);
      }
    },
    goToQuestion(slug){
      window.location.href = `/question/${slug}/`
    }
  },
  created() {
    this.getQuestions();
  },
};
</script>

<style>
.question-author {
  font-weight: bold;
  color: rgba(200,45,28,1);
}
.card:hover{
   cursor: pointer;
}
</style>