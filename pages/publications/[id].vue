<template>

    <div class="flex items-start justify-between max-w-7xl mx-auto my-12 bg-red-50">
        <div class="w-64 flex-shrink-0">
            <img :src="article.imageUrl" alt="Card Image" class="w-full h-full object-cover">
        </div>
        <div class="flex-1 px-10 py-8  text-teal-600">
            <div class="text-3xl font-medium">{{ article.title_zh }}</div>
            <div class="text-3xl font-medium">{{ article.title_pt }}</div>
            <div class="text-xl text-gray-700 line-clamp-2  pt-5">{{ article.author }}</div>
        </div>
    </div>


    <div class="grid grid-cols-2 gap-8 max-w-7xl mx-auto my-12">
        <div>
            <div class="text-3xl font-medium text-gray-900 mb-2">
                簡介<br>Descrição
            </div>
            <div class="text-gray-700">{{ article.description }}</div>
        </div>
        <div>
        <div class="text-3xl font-medium text-gray-900 mb-2">
            詳情（印刷版）<br>Detalhes (Versão Impressa)
        </div>
        <div v-html="article.print" class="text-gray-700"/>
    </div>
</div>

</template>


<script setup>
const route = useRoute()
console.log(route.params)

const article = {
        id: 1,
        imageUrl: '/images/books/publication-r008-443x653.jpg',
        title_zh: '實用葡漢翻譯教程 ',
        title_pt: 'Aspectos Teórico-Práticos de Tradução - Português / Chinês',
        author: '李長森、崔維孝',
        description:'Manuais e livros didáticos na área da língua portuguesa.',
        readMoreUrl: '#',
        print: '<p>Capa mole<br>405 Páginas<br>Dezembro 2002 - 1.ª edição<br>ISBN: 9993733334 '
    };
</script>