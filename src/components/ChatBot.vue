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
                input:'',
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
                console.log(this.messages)
                this.messages.append({"type":0, "message": question})
                this.messages.append({"type":1, "message": "blablabla"})
                this.input = ''
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
    <div contenteditable="True" v-bind="input"></div>
    <button @click="ask('bye')"> Send</button>
</template>

<style scoped>
</style>
