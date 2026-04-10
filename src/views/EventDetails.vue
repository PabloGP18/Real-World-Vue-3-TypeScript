<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import EventService from '@/services/EventService'

interface EventItem {
  id: number
  title: string
  time: string
  date: string
  location: string
  description: string
}

export default defineComponent({
  props: {
    id: {
      type: String,
      required: true
    }
  },
  data(): { event: EventItem | null } {
    return {
      event: null
    }
  },
  created() {
    EventService.getEvent(this.id)
      .then(response => {
        this.event = response.data as EventItem
      })
      .catch(error => {
        console.log(error)
      })
  }
})
</script>
