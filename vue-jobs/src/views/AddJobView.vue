<script setup>
import { reactive } from 'vue';

const form = reactive({
  type: 'Full-Time',
  title: '',
  description: '',
  salary: '',
  location: '',
  company: {
    name: '',
    description: '',
    contactEmail: '',
    contactPhone: '',
  },
  contact: '',
});

const handleSubmit = async () => {
  const newJob = {
    title: form.title,
    type: form.type,
    location: form.location,
    description: form.description,
    salary: form.salary,
    company: {
      name: form.company.name,
      description: form.company.description,
      contactEmail: form.company.contactEmail,
      contactPhone: form.company.contactPhone,
    },
  };

  try {
    const response = await axios.post('/api/jobs', newJob);
    toast.success('Serviço adicionado com sucesso');
    router.push(`/jobs/${response.data.id}`);
  } catch (error) {
    console.error('Erro em adicionar o serviço:', error);
    toast.error('Falha em adicionar o serviço');
  }
};
</script>

<template>
    <section class="bg-green-50">
      <div class="container m-auto max-w-2xl py-24">
        <div
          class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0"
        >
          <form @submit.prevent="handleSubmit">
            <h2 class="text-3xl text-center font-semibold mb-6">Adicionar Vaga</h2>
  
            <div class="mb-4">
              <label for="type" class="block text-gray-700 font-bold mb-2"
                >Tipo de Vaga</label
              >
              <select
                v-model="form.type"
                id="type"
                name="type"
                class="border rounded w-full py-2 px-3"
                required
              >
                <option value="Full-Time">Tempo Integral</option>
                <option value="Part-Time">Meio Período</option>
                <option value="Remote">Remoto</option>
                <option value="Internship">Estágio</option>
              </select>
            </div>
  
            <div class="mb-4">
              <label class="block text-gray-700 font-bold mb-2"
                >Nome da Vaga</label
              >
              <input
                type="text"
                id="name"
                name="name"
                v-model="form.title"
                class="border rounded w-full py-2 px-3 mb-2"
                placeholder="Exemplo: Desenvolvedor Front-End"
                required
              />
            </div>
            <div class="mb-4">
              <label for="description" class="block text-gray-700 font-bold mb-2"
                >Descrição</label
              >
              <textarea
                id="description"
                v-model="form.description"
                name="description"
                class="border rounded w-full py-2 px-3"
                rows="4"
                placeholder="Adicione as responsabilidades, expectativas, requisitos da vaga, etc."
              ></textarea>
            </div>
  
            <div class="mb-4">
              <label for="type" class="block text-gray-700 font-bold mb-2"
                >Salário</label
              >
              <select
                id="salary"
                v-model="form.salary"
                name="salary"
                class="border rounded w-full py-2 px-3"
                required
              >
                <option value="Under $50K">Abaixo de R$ 50K</option>
                <option value="$50 - 60K">R$ 50K - R$ 60K</option>
                <option value="$60 - 70K">R$ 60K - R$ 70K</option>
                <option value="$70 - 80K">R$ 70K - R$ 80K</option>
                <option value="$80 - 90K">R$ 80K - R$ 90K</option>
                <option value="$90 - 100K">R$ 90K - R$ 100K</option>
                <option value="$100 - 125K">R$ 100K - R$ 125K</option>
                <option value="$125 - 150K">R$ 125K - R$ 150K</option>
                <option value="$150 - 175K">R$ 150K - R$ 175K</option>
                <option value="$175 - 200K">R$ 175K - R$ 200K</option>
                <option value="Over $200K">Acima de R$ 200K</option>
              </select>
            </div>
  
            <div class="mb-4">
              <label class="block text-gray-700 font-bold mb-2"> Localização </label>
              <input
                type="text"
                id="location"
                v-model="form.location"
                name="location"
                class="border rounded w-full py-2 px-3 mb-2"
                placeholder="Localização da Empresa"
                required
              />
            </div>
  
            <h3 class="text-2xl mb-5">Informações da Empresa</h3>
  
            <div class="mb-4">
              <label for="company" class="block text-gray-700 font-bold mb-2"
                >Nome da Empresa</label
              >
              <input
                type="text"
                id="company"
                v-model="form.company.name"
                name="company"
                class="border rounded w-full py-2 px-3"
                placeholder="Nome da Empresa"
              />
            </div>
  
            <div class="mb-4">
              <label
                for="company_description"
                class="block text-gray-700 font-bold mb-2"
                >Descrição da Empresa</label
              >
              <textarea
                id="company_description"
                v-model="form.company.description"
                name="company_description"
                class="border rounded w-full py-2 px-3"
                rows="4"
                placeholder="O que sua empresa faz?"
              ></textarea>
            </div>
  
            <div class="mb-4">
              <label
                for="contact_email"
                class="block text-gray-700 font-bold mb-2"
                >E-mail de Contato</label
              >
              <input
                type="email"
                id="contact_email"
                v-model="form.company.contactEmail"
                name="contact_email"
                class="border rounded w-full py-2 px-3"
                placeholder="Endereço de e-mail para candidatos"
                required
              />
            </div>
            <div class="mb-4">
              <label
                for="contact_phone"
                class="block text-gray-700 font-bold mb-2"
                >Telefone de Contato</label
              >
              <input
                type="tel"
                id="contact_phone"
                v-model="form.company.contactPhone"
                name="contact_phone"
                class="border rounded w-full py-2 px-3"
                placeholder="Telefone opcional para candidatos"
              />
            </div>
  
            <div>
              <button
                class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline"
                type="submit"
              >
                Adicionar Vaga
              </button>
            </div>
          </form>
        </div>
      </div>
    </section>
</template>
