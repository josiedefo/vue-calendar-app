<template>
  <div class="modal-overlay" @click="close">
    <div class="modal-content" @click.stop>
      <div class="modal-header">
        <h3>{{ event ? 'Edit Event' : 'Create New Event' }}</h3>
        <button @click="close" class="close-btn">&times;</button>
      </div>
      
      <form @submit.prevent="save" class="event-form">
        <div class="form-group">
          <label for="title">Event Title</label>
          <input 
            id="title"
            v-model="formData.title" 
            type="text" 
            placeholder="Enter event title"
            required
          />
        </div>
        
        <div class="form-group">
          <label for="date">Date</label>
          <input 
            id="date"
            v-model="formData.date" 
            type="date" 
            required
          />
        </div>
        
        <div class="form-group">
          <label for="time">Time</label>
          <input 
            id="time"
            v-model="formData.time" 
            type="time" 
            required
          />
        </div>
        
        <div class="form-group">
          <label>Color</label>
          <div class="color-picker">
            <div 
              v-for="color in colors" 
              :key="color"
              class="color-option"
              :class="{ active: formData.color === color }"
              :style="{ backgroundColor: color }"
              @click="formData.color = color"
            ></div>
          </div>
        </div>
        
        <div class="form-actions">
          <button type="button" @click="close" class="btn-cancel">Cancel</button>
          <button 
            v-if="event" 
            type="button" 
            @click="deleteEvent" 
            class="btn-delete"
          >
            Delete
          </button>
          <button type="submit" class="btn-save">{{ event ? 'Update' : 'Create' }} Event</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EventModal',
  props: {
    event: {
      type: Object,
      default: null
    },
    selectedDate: {
      type: String,
      default: null
    }
  },
  data() {
    return {
      colors: [
        '#3B82F6', // Blue
        '#10B981', // Green
        '#F59E0B', // Yellow
        '#EF4444', // Red
        '#8B5CF6', // Purple
        '#06B6D4', // Cyan
        '#EC4899', // Pink
        '#84CC16'  // Lime
      ],
      formData: {
        title: '',
        date: '',
        time: '',
        color: '#3B82F6'
      }
    }
  },
  mounted() {
    if (this.event) {
      this.formData = { ...this.event }
    } else if (this.selectedDate) {
      this.formData.date = this.selectedDate
    }
  },
  methods: {
    save() {
      this.$emit('save', { ...this.formData })
    },
    close() {
      this.$emit('close')
    },
    deleteEvent() {
      if (confirm('Are you sure you want to delete this event?')) {
        this.$emit('delete', this.event.id)
        this.$emit('close')
      }
    }
  }
}
</script>