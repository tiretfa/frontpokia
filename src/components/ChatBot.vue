<script>
    import ChatBotAnswer from './ChatBotAnswer.vue';
    import ChatBotQuestion from './ChatBotQuestion.vue';
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
                this.messages.push({"type":1, "message": "blablabla"})
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
