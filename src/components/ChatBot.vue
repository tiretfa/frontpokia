<script>
    import ChatBotAnswer from './ChatBotAnswer.vue';
    import ChatBotQuestion from './ChatBotQuestion.vue';
    import axios from 'axios';
    export default{
        components:{
            ChatBotAnswer,
            ChatBotQuestion
        },
        data(){
            return{
                question:'',
                messages: [
                    {"type":0, "message":"Bonjour, ça va?"},
                    {"type":1, "message":"Ouai bah nickel!"},
                    {"type":0, "message":"Parfait"},
                    {"type":1, "message":"Bah ouai Parfait"},
                ]
            }
        },
        methods: {
            ask(question){
                this.messages.push({"type":0, "message": question})
                axios.get('http://localhost:8000').then(response =>{
                    this.messages.push({"type":1, "message": response.data.Hello});
                })
                this.question = ''
            }
        }
    }
</script>

<template>
   <div>
    <component 
      v-for="m in messages"
      :is="m.type === 0 ? 'ChatBotQuestion' : 'ChatBotAnswer'"
      :message="m.message"
    />
  </div>
    <input v-model="question" placeholder="écrit moi dessus" v-on:keyup.enter="ask(question)"></input>
</template>

<style scoped>
</style>
