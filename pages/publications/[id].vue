<template>
    <div v-if="publication">
        <div class="flex items-start justify-between max-w-7xl mx-auto my-12 bg-red-50">
            <div class="w-64 flex-shrink-0">
                <img :src="publication.cover_url" alt="Card Image" class="w-full h-full object-cover">
            </div>
            <div class="flex-1 px-10 py-8  text-teal-600">
                <div class="text-3xl font-medium">{{ publication.title_zh }}</div>
                <div class="text-3xl font-medium">{{ publication.title_pt }}</div>
                <div class="text-xl text-gray-700 line-clamp-2  pt-5">{{ publication.author }}</div>
            </div>
        </div>

        <div class="grid grid-cols-2 gap-8 max-w-7xl mx-auto my-12">
            <div>
                <div class="text-3xl font-medium text-gray-900 mb-2">
                    簡介<br>Descrição
                </div>
                <div class="text-gray-700">{{ publication.description_zh }}</div>
            </div>
            <div>
                <div class="text-3xl font-medium text-gray-900 mb-2">
                    詳情（印刷版）<br>Detalhes (Versão Impressa)
                </div>
                <div v-html="publication.print" class="text-gray-700" />
            </div>
        </div>
    </div>
</template>


<script setup>
import { ref, onMounted } from 'vue'
const runtimeConfig = useRuntimeConfig();
const route = useRoute()
const publication = ref(null)

onMounted(async () => {
  const response = await fetch(runtimeConfig.public.DATA_SOURCE+`publications?unit=flt&id=${route.params.id}`)
  publication.value = await response.json()
})

</script>