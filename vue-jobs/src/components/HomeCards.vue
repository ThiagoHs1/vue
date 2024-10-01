<script setup>
    import Card from '@/components/Card.vue';
    import { RouterLink } from 'vue-router';
</script>

<template>
  <section class="py-4">
    <div class="container-xl lg:container m-auto">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
        <!-- Card para desenvolvedores -->
        <Card>
          <h2 class="text-2xl font-bold">Para desenvolvedores</h2>
          <p class="mt-2 mb-4">
            Descubra seu trabalho em Vue e começe sua carreira
          </p>
          <RouterLink
            to="/jobs"
            class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700"
          >
            Trabalhos em Vue
          </RouterLink>
        </Card>

        <!-- Card para empregadores -->
        <Card bg="bg-green-100">
          <h2 class="text-2xl font-bold">Para empregadores</h2>
          <p class="mt-2 mb-4">
            Liste seu trabalho e descubra o desenvolvedor Vue perfeito
          </p>
          <RouterLink
            to="/jobs/add"
            class="inline-block bg-green-500 text-white rounded-lg px-4 py-2 hover:bg-green-600"
          >
            Adicionar Trabalho
          </RouterLink>
        </Card>
      </div>
    </div>
  </section>
</template>
