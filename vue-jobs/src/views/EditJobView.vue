<script setup>
import router from '@/router';
import { reactive, onMounted } from 'vue';

import { useRoute } from 'vue-router';
import { useToast } from 'vue-toastification';
import axios from 'axios';


const route = useRoute();

const jobId = route.params.id;

const state = reactive({
  job: {},
  isLoading: true,
});




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
});

onMounted(async () => {
  try {
    const response = await axios.get(`/api/jobs/${jobId}`);
    state.job = response.data;
    // Populate form fields after fetching job data
    form.type = state.job.type;
    form.title = state.job.title;
    form.description = state.job.description;
    form.salary = state.job.salary;
    form.location = state.job.location;
    form.company.name = state.job.company.name;
    form.company.description = state.job.company.description;
    form.company.contactEmail = state.job.company.contactEmail;
    form.company.contactPhone = state.job.company.contactPhone;
  } catch (error) {
    console.error('Error fetching job:', error);
  } finally {
    state.isLoading = false;
  }
});

const toast = useToast();

const handleSubmit = async () => {
  const updatedJob = {
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
    await axios.put(`/api/jobs/${jobId}`, updatedJob);
    toast.success('Job Updated Successfully');
    router.push(`/jobs/${jobId}`);
  } catch (error) {
    console.error('Error updating job:', error);
    toast.error('Failed to update job');
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
          <h2 class="text-3xl text-center font-semibold mb-6">Editar Vaga</h2>

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
              v-model="form.title"
              id="name"
              name="name"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="eg. Beautiful Apartment In Miami"
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
              placeholder="Add any job duties, expectations, requirements, etc"
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
            <label class="block text-gray-700 font-bold mb-2"> Location </label>
            <input
              type="text"
              v-model="form.location"
              id="location"
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
              v-model="form.company.name"
              id="company"
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
              v-model="form.company.contactEmail"
              id="contact_email"
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
              v-model="form.company.contactPhone"
              id="contact_phone"
              name="contact_phone"
              class="border rounded w-full py-2 px-3"
              placeholder="Optional phone for applicants"
            />
          </div>

          <div>
            <button
              class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline"
              type="submit"
            >
            Editar Vaga
            </button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>