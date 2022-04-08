<template>
<div class="form-group shadow-textarea">
  <label for="exampleFormControlTextarea6">Your answer:</label>
  <textarea :readonly="this.user_answered" v-model="answer" class="form-control z-depth-1 w-100" id="exampleFormControlTextarea6" rows="3" placeholder="Write something here..."></textarea>
  <button  @click="postAnswer" class="btn btn-sm btn-outline-success mt-2">Post</button>
  <button  @click="clear" class="btn btn-sm btn-outline-danger mx-3 mt-2">Clear</button>
</div>
</template>

<script>
import { axios } from "@/common/api.service.js";

export default {
    name: "AnswerBoxComponent",
    props:{
        slug: {
            type: String,
            required: true,
        },
        user_answered:{
            type: Boolean,
            required: true,
        }
    },
    methods:{
        async postAnswer(){
            console.log(this.answer)
            const endpoint = `/api/v1/questions/${this.slug}/answer`

            try {
            const response = await axios.post(endpoint,{
                body: this.answer
            });

            if(response.status != 404){
                this.question = response.data;
          
            }
    
            } catch (error) {
                console.log(error.response);
        
            }
        },
        clear(){
            this.answer = "";
        }
    },
    data(){
        return{
            answer: "",
        }
    },
    created(){
        console.log(this.slug)
    }


}
</script>

<style>

</style>