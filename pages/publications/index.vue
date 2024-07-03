<template>
    <div class="relative h-96 w-full">
    <img src="/images/publication-banner-1920x1441.jpg" alt="Header Background"
        class="absolute inset-0 h-full w-full object-cover" />
    <div class="absolute inset-0 flex flex-col items-center justify-center bg-black/20 p-8 text-white">
        <h1 class="text-4xl font-bold mb-4">PUBLICAÇÕES</h1>
        <p class="text-lg mb-8">
            Descubra todas as publicações do FLT
        </p>
        <a href="#" class="inline-block bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded">
            所有出版物 Todas as Publicações
        </a>
    </div>
</div>
<template v-for="publication in publications">
<div class="flex items-start justify-between max-w-7xl mx-auto my-12 bg-red-50">
    <div class="w-64 flex-shrink-0">
        <img :src="publication.cover_url" alt="Card Image" class="w-full h-full object-cover">
    </div>
    <div class="flex-1 px-10 py-8  text-teal-600">
        <NuxtLink :href="'publications/'+publication.id">
        <div class="text-3xl font-medium">{{ publication.title_zh }}</div>
        <div class="text-3xl font-medium">{{ publication.title_pt }}</div>
        <div class="text-xl text-gray-700 line-clamp-2  pt-5">{{ publication.author }}</div>
        </NuxtLink>
    </div>
</div>
</template>
</template>


<script setup>
const runtimeConfig = useRuntimeConfig();
const route = useRoute()
const publications = ref(null)

onMounted(async () => {
  const response = await fetch(runtimeConfig.public.DATA_SOURCE+`publications?unit=flt&cat=${route.query.cat}`)
  publications.value = await response.json()
})

</script>