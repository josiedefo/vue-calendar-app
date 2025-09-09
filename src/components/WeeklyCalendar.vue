<template>
  <div class="weekly-calendar">
    <div class="calendar-header">
      <button @click="previousWeek" class="nav-btn">&larr;</button>
      <div class="header-center">
        <h2>{{ weekRange }}</h2>
        <button @click="goToToday" class="today-btn">Today</button>
      </div>
      <button @click="nextWeek" class="nav-btn">&rarr;</button>
    </div>
    
    <div class="calendar-grid">
      <div class="time-column">
        <div class="time-header"></div>
        <div 
          v-for="hour in hours" 
          :key="hour" 
          class="time-slot"
        >
          {{ formatHour(hour) }}
        </div>
      </div>
      
      <div 
        v-for="day in weekDays" 
        :key="day.date" 
        class="day-column"
      >
        <div class="day-header">
          <div class="day-name">{{ day.name }}</div>
          <div class="day-date">{{ day.date.split('-')[2] }}</div>
        </div>
        
        <div class="day-slots">
          <div 
            v-for="hour in hours" 
            :key="`${day.date}-${hour}`"
            class="hour-slot"
            @click="addEvent(day.date, hour)"
          >
            <div 
              v-for="event in getEventsForSlot(day.date, hour)"
              :key="event.id"
              class="event"
              :style="{ backgroundColor: event.color }"
              @click.stop="editEvent(event)"
              @contextmenu.prevent="deleteEvent(event.id)"
            >
              <div class="event-title">{{ event.title }}</div>
              <div class="event-time">{{ event.time }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WeeklyCalendar',
  props: {
    events: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      currentWeek: new Date(),
      hours: Array.from({ length: 12 }, (_, i) => i + 8)
    }
  },
  computed: {
    weekDays() {
      const startOfWeek = this.getStartOfWeek(this.currentWeek)
      const days = []
      
      for (let i = 0; i < 7; i++) {
        const date = new Date(startOfWeek)
        date.setDate(startOfWeek.getDate() + i)
        days.push({
          name: date.toLocaleDateString('en-US', { weekday: 'short' }),
          date: date.toISOString().split('T')[0]
        })
      }
      
      return days
    },
    weekRange() {
      const start = this.getStartOfWeek(this.currentWeek)
      const end = new Date(start)
      end.setDate(start.getDate() + 6)
      
      return `${start.toLocaleDateString('en-US', { month: 'long', day: 'numeric' })} - ${end.toLocaleDateString('en-US', { month: 'long', day: 'numeric', year: 'numeric' })}`
    }
  },
  methods: {
    getStartOfWeek(date) {
      const start = new Date(date)
      const day = start.getDay()
      const diff = start.getDate() - day
      start.setDate(diff)
      return start
    },
    previousWeek() {
      const newWeek = new Date(this.currentWeek)
      newWeek.setDate(this.currentWeek.getDate() - 7)
      this.currentWeek = newWeek
    },
    nextWeek() {
      const newWeek = new Date(this.currentWeek)
      newWeek.setDate(this.currentWeek.getDate() + 7)
      this.currentWeek = newWeek
    },
    goToToday() {
      this.currentWeek = new Date()
    },
    formatHour(hour) {
      const period = hour >= 12 ? 'PM' : 'AM'
      const displayHour = hour > 12 ? hour - 12 : hour === 0 ? 12 : hour
      return `${displayHour}:00 ${period}`
    },
    addEvent(date, hour) {
      this.$emit('add-event', date, hour)
    },
    editEvent(event) {
      this.$emit('edit-event', event)
    },
    deleteEvent(eventId) {
      if (confirm('Are you sure you want to delete this event?')) {
        this.$emit('delete-event', eventId)
      }
    },
    getEventsForSlot(date, hour) {
      return this.events.filter(event => {
        if (event.date !== date) return false
        const eventHour = parseInt(event.time.split(':')[0])
        return eventHour === hour
      })
    }
  }
}
</script>