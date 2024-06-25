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

    <div v-for="article in articles" :key="article.id"
        class="flex items-center justify-between max-w-7xl mx-auto my-12">
        <div class="w-1/2 pr-8">
            <img :src="article.imageUrl" :alt="article.title" class="w-full rounded-lg shadow-lg" />
        </div>
        <div class="w-1/2">
            <h2 class="text-3xl font-bold mb-2">{{ article.title }}</h2>
            <p class="text-gray-500 mb-4">{{ article.author }}</p>
            <p class="text-gray-700 mb-6">{{ article.description }}</p>
            <a :href="article.readMoreUrl"
                class="inline-block bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded">
                查看更多 VER MAIS
            </a>
        </div>
    </div>
</template>

<script setup>
const articles = [
    {
        id: 1,
        imageUrl: '/images/references-640x426.jpeg',
        title: '教材 Materiais Didácticos',
        author: 'Author Name 1',
        description:
            'Manuais e livros didáticos na área da língua portuguesa.',
        readMoreUrl: 'publications?materials',
    },
    {
        id: 2,
        imageUrl: '/images/materials-1-640x441.jpeg',
        title: '著作與參考書籍 Ensaios e Obras de Referência',
        author: 'Author Name 2',
        description:
            'Obras académicas sobre o universo lusófono, glossários e dicionários.',
        readMoreUrl: 'publications?books',
    }
];
</script>