<template>
  <div id="app">
    <header class="app-header">
      <h1>My Calendar</h1>
    </header>
    <main class="app-main">
      <WeeklyCalendar 
        :events="events" 
        @add-event="addEvent"
        @edit-event="editEvent"
        @delete-event="deleteEvent"
      />
    </main>
    <EventModal 
      v-if="showEventModal"
      :event="selectedEvent"
      :selected-date="selectedDate"
      @save="saveEvent"
      @delete="deleteEvent"
      @close="closeEventModal"
    />
  </div>
</template>

<script>
import WeeklyCalendar from './components/WeeklyCalendar.vue'
import EventModal from './components/EventModal.vue'

export default {
  name: 'App',
  components: {
    WeeklyCalendar,
    EventModal
  },
  data() {
    return {
      events: [],
      showEventModal: false,
      selectedEvent: null,
      selectedDate: null
    }
  },
  mounted() {
    this.loadEventsFromStorage()
  },
  methods: {
    addEvent(date) {
      this.selectedEvent = null
      this.selectedDate = date
      this.showEventModal = true
    },
    editEvent(event) {
      this.selectedEvent = event
      this.selectedDate = event.date
      this.showEventModal = true
    },
    deleteEvent(eventId) {
      this.events = this.events.filter(event => event.id !== eventId)
      this.saveEventsToStorage()
    },
    saveEvent(eventData) {
      if (this.selectedEvent) {
        const index = this.events.findIndex(e => e.id === this.selectedEvent.id)
        if (index !== -1) {
          this.events[index] = { ...eventData, id: this.selectedEvent.id }
        }
      } else {
        const newEvent = {
          ...eventData,
          id: Date.now()
        }
        this.events.push(newEvent)
      }
      this.saveEventsToStorage()
      this.closeEventModal()
    },
    closeEventModal() {
      this.showEventModal = false
      this.selectedEvent = null
      this.selectedDate = null
    },
    saveEventsToStorage() {
      try {
        localStorage.setItem('calendar-events', JSON.stringify(this.events))
      } catch (error) {
        console.error('Failed to save events to localStorage:', error)
      }
    },
    loadEventsFromStorage() {
      try {
        const savedEvents = localStorage.getItem('calendar-events')
        if (savedEvents) {
          this.events = JSON.parse(savedEvents)
        } else {
          this.events = [
            {
              id: 1,
              title: 'Team Meeting',
              date: '2025-01-13',
              time: '10:00',
              color: '#3B82F6'
            },
            {
              id: 2,
              title: 'Lunch with Sarah',
              date: '2025-01-14',
              time: '12:30',
              color: '#10B981'
            }
          ]
          this.saveEventsToStorage()
        }
      } catch (error) {
        console.error('Failed to load events from localStorage:', error)
        this.events = []
      }
    }
  }
}
</script>