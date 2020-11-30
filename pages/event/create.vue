<template>
  <div>
    <h1>Crear evento</h1>
  </div>
</template>

<script>
export default {
  head () {
    // <-- property used by vue-meta to add header tags
    return {
      title: 'Nuevo Evento', // <-- For our title tag
      meta: [
        {
          hid: 'description',
          name: 'description', // <-- for our meta description tag
          content:
            'Crear un nuevo evento en nuestra App de eventos'
        }
      ]
    }
  }
}
</script>
