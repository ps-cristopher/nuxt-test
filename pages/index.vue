<template>
  <div>
    <h1>Eventos</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'

export default {
  components: {
    EventCard
  },
  async asyncData ({ $axios }) {
    try {
      const response = await $axios.get('http://localhost:3000/events')
      return {
        events: response.data
      }
    } catch (error) {
      error({
        statusCode: 503,
        message: 'Error al cargar los datos. Intenta otra vez, por favor.'
      })
    }
  },
  head () {
    // <-- property used by vue-meta to add header tags
    return {
      title: 'Lista de eventos' // <-- For our title tag
    }
  }
}
</script>
