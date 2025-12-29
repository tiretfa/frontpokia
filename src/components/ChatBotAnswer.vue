<script>
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
        methods:{
            async ask() {
                this.isLoading = true
                const response = await fetch('http://localhost:8000/chatbot', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({ q: this.question })
                })

                const reader = response.body.getReader()
                const decoder = new TextDecoder('utf-8')

                while (true) {
                    const { value, done } = await reader.read()
                    if (done) break

                    let chunk = decoder.decode(value, { stream: true })
                    this.answer += chunk.replace(/\n/g, '')
                }

                this.isLoading = false
            }
        }
        
    }
    
</script>

<template>
    <div>A: {{ answer }}</div>
</template>

<style scoped>
</style>
