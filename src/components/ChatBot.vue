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
                messages: [],
                isLoading: false
            }
        },
        methods: {
            async ask(question){
                this.messages.push({"type":0, "message": question})
                let answer = ''
                const response = await axios.post(
                    'http://localhost:8000/chatbot',
                    {'q':question},
                    {
                        responseType: 'stream',
                        onDownloadProgress: (progressEvent) => {
                            const dataChunk = progressEvent.event.target.response
                            answer += dataChunk
                        }
                    }
                )
                .finally(()=>{
                    this.messages.push({"type":1, "message": answer});
                    this.isLoading = false
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
