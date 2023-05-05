<script setup>
    import axios from 'axios';
    import { ref } from 'vue';
    import { RouterLink } from 'vue-router'
    // import response from '../mocks/respnse.json'
    const valorantData = ref([])

    const getData = async () => {
        try{
            const response = await axios.get('https://valorant-api.com/v1/agents')
            valorantData.value = response.data.data.map(caracter => {
                return {
                    id: caracter.uuid,
                    name: caracter.displayName
                }
            })
        }catch(e){
            console.error(e)
        }
    }
    getData()
</script>

<template>
    <h1>VALORANT GOD</h1>
    <section v-if="valorantData.length > 0">
        <RouterLink v-for="caracter in valorantData" :to="`/valorant/${caracter.name}?id=${caracter.id}`">
            <p>{{ caracter.name }}</p>
        </RouterLink>
    </section>
</template>