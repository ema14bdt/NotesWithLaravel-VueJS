<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Módulo de Notas
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="md:grid md:grid-cols-3 md:gap-6">
          <div class="md:col-span-1">
            <div class="px-4 sm:px0">
              <h3 class="text-lg text-gray-900">Listado de notas</h3>
              <p class="text-sm text-gray-600">
                Toma el registro correcto y ejecuta cualquier función (ver,
                editar o eliminar)
              </p>
            </div>
          </div>
          <div class="md:col-span-2 mt-5 md:mt-0">
            <div class="shadow bg-white md:rounded-md p-4">
              <div class="flex justify-between">
                <input
                  type="text"
                  class="form-input rounded-md shadow-sm"
                  placeholder="Buscar..."
                  v-model="q"
                />

                <inertia-link
                  :href="route('notes.create')"
                  class="
                    bg-blue-500
                    hover:bg-blue-700
                    text-white
                    font-bold
                    py-2
                    px-4
                    rounded-md
                  "
                >
                  Crear
                </inertia-link>
              </div>
              <hr class="my-6" />
              <table>
                <tr v-for="note in notes" :key="note.id">
                  <td class="border px-4 py-2">
                    {{ note.excerpt }}
                  </td>
                  <td class="px-2 py-1">
                    <inertia-link
                      :href="route('notes.show', note.id)"
                      class="
                        bg-green-500
                        hover:bg-green-700
                        text-white
                        font-bold
                        py-1
                        px-2
                        rounded-md
                      "
                    >
                      Ver
                    </inertia-link>
                  </td>
                  <td class="px-2 py-1">
                    <inertia-link
                      :href="route('notes.edit', note.id)"
                      class="
                        bg-yellow-500
                        hover:bg-yellow-700
                        text-white
                        font-bold
                        py-1 
                        px-2
                        rounded-md
                      "
                    >
                      Editar
                    </inertia-link>
                  </td>
                  <td class="px-2 py-1">
                    <form @submit.prevent="deleteNote(note.id)">
                      <button
                        type="submit"
                        class="
                          bg-red-500
                          hover:bg-red-700
                          text-white
                          font-bold
                          py-1
                          px-2
                          rounded-md
                        "
                      >
                        Eliminar
                      </button>
                    </form>
                  </td>
                </tr>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout";

export default {
  components: {
    AppLayout,
  },
  props: {
    notes: Array,
  },
  data() {
    return {
      q: "",
    };
  },
  watch: {
    q: function (value) {
      this.$inertia.replace(this.route("notes.index", { q: value }));
    },
  },
  methods: {
    deleteNote(id) {
      if (confirm("¿Estás seguro de eliminar esta nota?")) {
        this.$inertia.delete(this.route("notes.destroy", { id }));
      }
    },
  },
};
</script>
