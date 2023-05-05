<script setup>
    import axios from 'axios';
    import { ref } from 'vue';
    import { useRoute,useRouter } from 'vue-router'
    
    const route = useRoute()
    const router = useRouter()
    
    console.log(route)
    const caracter = ref({})
    const getData = async() => {
        try{
            const response = await axios.get(`https://valorant-api.com/v1/agents/${route.query.id}`)
            caracter.value = response.data.data
        }catch(e){
            router.push('/error')
        }
        }
    getData()
</script>

<template>
    <h1>Welcome {{ caracter?.displayName }}</h1>
    <img :src="caracter?.displayIcon" />
</template>