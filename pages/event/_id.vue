<template>
  <div class="mx-4">
    <h1>#{{ eventId }} {{ event.title }}</h1>
    <h5 class="mb-2">
      {{ event.time }}, {{ new Date(event.date).toDateString() }}
    </h5>
    <div style="padding-top: 0.1em; padding-bottom: 0.1rem" class="text-sm mb-2 px-3 bg-red-200 text-gray-800 rounded-full">
      <span class="text-red-800 text-base">Categoría: </span> {{ event.category }}
    </div>
    <div style="padding-top: 0.1em; padding-bottom: 0.1rem" class="text-sm mb-2 px-3 bg-gray-200 text-gray-800 rounded-full">
      <span class="text-gray-800 text-base">Organizador: </span> {{ event.organizer }}
    </div>
    <div style="padding-top: 0.1em; padding-bottom: 0.1rem" class="text-sm mb-2 px-3 bg-blue-200 text-gray-800 rounded-full">
      <span class="text-blue-800 text-base">Ubicación: </span> {{ event.location }}
    </div>
    <p class="text-lg ml-3">
      Descripción: {{ event.description }}
    </p>
  </div>
</template>

<script>
export default {
  async asyncData ({ $axios, params }) {
    try {
      const response = await $axios.get(`http://localhost:3000/events/${params.id}`)
      return {
        event: response.data
      }
    } catch (error) {
      error({
        statusCode: 503,
        message: `Error al cargar el evento ${params.id}. Intenta otra vez, por favor.`
      })
    }
  },
  computed: {
    eventId () {
      return this.$route.params.id
    }
  },
  head () {
    // <-- property used by vue-meta to add header tags
    return {
      title: `${this.event.title}`, // <-- For our title tag
      meta: [
        {
          hid: 'description',
          name: 'description', // <-- for our meta description tag
          content:
            `Detalle del evento ${this.eventId} en nuestra App de eventos`
        }
      ]
    }
  }
}
</script>
