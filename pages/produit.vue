<script setup>
const query = gql`
  query Produits {
    produits {
      createdAt
      id
      publishedAt
      texte
      titre
      updatedAt
      image {
        id
        handle
        fileName
        mimeType
        url
      }
    }
  }
`;

const { data } = await useAsyncQuery(query);
</script>

<template>
  <h1 class="text-3xl my-8">Projects</h1>
  <p class="text-lg mb-8">Here are some of my projects on GitHub.</p>
  <section class="grid grid-cols-2 gap-10">
    <div v-for="produit in data?.produits" :key="produit.id"
      class="p-8 border-4 my-4 rounded-lg hover:bg-gray-50">
      <a :href="produit.url" target="_blank">
        <h2 class="text-2xl text-indigo-800 font-semibold mb-2 hover:underline">{{ produit.titre }}</h2>
      </a>
      <p>{{ produit.texte }}</p>
      
      <!-- Ajoutez la balise img pour afficher l'image -->
      <img :src="produit.image.url" :alt="produit.titre" class="w-full h-auto mt-4" />
      
      <div class="mt-4">
        <!-- Ajustez les propriétés en fonction de vos données GraphQL -->
        <!-- Vous n'avez pas de propriété forks et watchers dans vos données GraphQL -->
      </div>
    </div>
  </section>
</template>
