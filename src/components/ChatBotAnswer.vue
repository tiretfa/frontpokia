<script>
    import axios from 'axios';
    export default{
        props:['question'],
        data(){
            return {
                answer: '',
                isLoading: false
            }
        },
        created(){
            this.ask()
        },
        watch:{
            answer(newAnswer){
                this.answer = newAnswer
            }
        },
        methods:{
            async ask() {
                this.isLoading = true
                await axios.post(
                    'http://localhost:8000/chatbot',
                    { 'q': this.question },
                    {
                        responseType: 'stream',
                        onDownloadProgress: (progressEvent) => {
                            const dataChunk = progressEvent.event.target.response
                            this.answer += dataChunk
                        }
                    }
                )
                .finally(()=>{
                    this.isLoading = false
                })
            }
        }
        
    }
    
</script>

<template>
    <div>A: {{ answer }}</div>
</template>

<style scoped>
</style>
