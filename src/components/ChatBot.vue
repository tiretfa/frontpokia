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
                questions: [],
                isLoading: false
            }
        },
        methods: {
            chat(question){
                this.questions.push(question)
                this.question = ''
            }
        }
    }
</script>

<template>
    <div v-for="q in questions">
        <ChatBotQuestion :question="q"/>
        <ChatBotAnswer :question="q"/>
    </div>
    <input v-model="question" placeholder="écrit moi dessus" v-on:keyup.enter="chat(question)"></input>
</template>

<style scoped>
</style>
