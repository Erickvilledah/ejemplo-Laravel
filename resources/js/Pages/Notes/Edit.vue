<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import Welcome from '@/Components/Welcome.vue';
import { Link } from '@inertiajs/vue3';
import { useForm } from '@inertiajs/vue3';

const props = defineProps ({note: Object});

const form = useForm({
    titulo:props.note.titulo,
    contenido:props.note.contenido
});

const submit = () => {
    form.put(route('notas.update',props.note.id), form);
};
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Mis notas - Erick Villeda
            </h2>
        </template>


        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="md:grid md:grid-cols-3 md:gap-6">
                    <div class="md:col-span-1">
                        <div class="px-4 sm:px0">
                            <h3 class="text-lg text-black">Editar mi nota</h3>
                            <p class="text-sm text-black">
                                {{ note.title }}
                            </p>
                        </div>
                    </div>
                    <div class="md:col-span-2 mt-5 md:mt-0">
                        <div class="shadow bg-white md:rounded-md p-4">
                            <form @submit.prevent="submit">
                                <label class="block font-medium text-sm text-gray-700">
                                    Resumen
                                </label>
                                <textarea
                                    class = "form-input w-full rounded-md shadow-sm"
                                    v-model = "form.titulo"
                                ></textarea>
                                <label class = "block font-medium text-sm text-gray-700">
                                    Contenido
                                </label>
                                <textarea
                                    class="form-input w-full rounded-md shadow-sm"
                                    v-model = "form.contenido"
                                    rows="8"
                                ></textarea>
                                <button class="font-bold py-2 px-4 rounded-md bg-blue-500">
                                    Editar
                                </button>
                            </form>
                           <hr class="my-6">
                           <Link :href="route('notas.index')">
                                Volver
                            </Link>

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
