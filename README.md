# Vue.js Calendar App 📅

A beautiful, modern calendar application built with Vue.js featuring weekly views, event management, and local storage persistence. Perfect for personal scheduling and time management.

![Vue.js](https://img.shields.io/badge/Vue.js-3.4.0-4FC08D?style=flat-square&logo=vue.js)
![Vite](https://img.shields.io/badge/Vite-5.0.0-646CFF?style=flat-square&logo=vite)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

## ✨ Features

### Core Functionality
- **📅 Weekly Calendar View** - Clean, intuitive weekly layout with time slots (8 AM - 7 PM)
- **➕ Event Creation** - Click any time slot to create new events
- **✏️ Event Editing** - Click existing events to modify details
- **🗑️ Event Deletion** - Right-click events or use delete button in modal
- **🎨 Color Coding** - 8 beautiful color options for event categorization
- **💾 Local Storage** - Automatic persistence between sessions

### User Experience
- **🏠 Today Button** - Quick navigation back to current week
- **📱 Responsive Design** - Works seamlessly on desktop and mobile
- **✨ Modern UI** - Beautiful glassmorphism design with smooth animations
- **⚡ Fast Performance** - Lightweight and optimized

### Technical Features
- **🔄 Real-time Updates** - Instant UI updates for all operations
- **💿 Data Persistence** - Browser localStorage integration
- **🎯 Event Management** - Full CRUD operations
- **📐 Responsive Grid** - Flexible time-slot layout

## 🚀 Quick Start

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/josiedefo/vue-calendar-app.git
   cd vue-calendar-app
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start development server**
   ```bash
   npm run dev
   ```

4. **Open your browser**
   Navigate to `http://localhost:5173`

## 🏗️ Project Structure

```
vue-calendar-app/
├── src/
│   ├── components/
│   │   ├── WeeklyCalendar.vue    # Main calendar grid component
│   │   └── EventModal.vue        # Event creation/editing modal
│   ├── App.vue                   # Root application component
│   ├── main.js                   # Application entry point
│   └── style.css                 # Global styles and themes
├── public/
├── index.html                    # HTML template
├── package.json                  # Dependencies and scripts
├── vite.config.js               # Vite configuration
└── README.md                    # This file
```

## 🎯 Usage Guide

### Creating Events
1. Click on any empty time slot in the calendar
2. Fill in event details (title, date, time, color)
3. Click "Create Event" to save

### Managing Events
- **Edit**: Click on any existing event to modify it
- **Delete**: 
  - Right-click on an event for quick deletion
  - Or open event modal and click "Delete" button

### Navigation
- **Week Navigation**: Use arrow buttons to move between weeks
- **Today Button**: Click "Today" to jump to current week instantly

### Event Colors
Choose from 8 beautiful colors to categorize your events:
- 🔵 Blue (Default)
- 🟢 Green
- 🟡 Yellow
- 🔴 Red
- 🟣 Purple
- 🔷 Cyan
- 🩷 Pink
- 🟢 Lime

## 🛠️ Development

### Available Scripts

```bash
# Start development server with hot reload
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

### Development Workflow

1. **Local Development**
   ```bash
   npm run dev
   ```
   The app will be available at `http://localhost:5173` with hot module replacement.

2. **Building**
   ```bash
   npm run build
   ```
   Creates optimized production build in `dist/` directory.

3. **Testing Production Build**
   ```bash
   npm run preview
   ```
   Serves the production build locally for testing.

## 📱 Browser Support

- ✅ Chrome (latest)
- ✅ Firefox (latest)
- ✅ Safari (latest)
- ✅ Edge (latest)
- ⚠️ IE11 (limited support)

## 🔧 Configuration

### Customizing Time Range
Edit the `hours` array in `WeeklyCalendar.vue`:
```javascript
// Current: 8 AM - 7 PM
hours: Array.from({ length: 12 }, (_, i) => i + 8)

// Example: 6 AM - 10 PM
hours: Array.from({ length: 17 }, (_, i) => i + 6)
```

### Adding New Colors
Modify the `colors` array in `EventModal.vue`:
```javascript
colors: [
  '#3B82F6', // Blue
  '#10B981', // Green
  // Add your colors here
]
```

### Local Storage Key
Events are stored under the key `calendar-events`. Change in `App.vue` if needed:
```javascript
localStorage.setItem('your-custom-key', JSON.stringify(this.events))
```

## 🚀 Deployment

### Netlify
1. Build the project: `npm run build`
2. Deploy the `dist/` folder to Netlify

### Vercel
1. Connect your GitHub repository
2. Vercel will automatically detect it's a Vite project
3. Deploy with default settings

### GitHub Pages
1. Install gh-pages: `npm install --save-dev gh-pages`
2. Add to package.json:
   ```json
   {
     "scripts": {
       "deploy": "gh-pages -d dist"
     },
     "homepage": "https://yourusername.github.io/vue-calendar-app"
   }
   ```
3. Build and deploy: `npm run build && npm run deploy`

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Make your changes**
4. **Commit your changes**
   ```bash
   git commit -m 'Add some amazing feature'
   ```
5. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
6. **Open a Pull Request**

### Development Guidelines
- Follow Vue.js style guide
- Use descriptive commit messages
- Add comments for complex logic
- Test your changes thoroughly

## 📋 Roadmap

### Upcoming Features
- [ ] **Month View** - Traditional monthly calendar layout
- [ ] **Event Duration** - Support for multi-hour events
- [ ] **Drag & Drop** - Move events by dragging
- [ ] **Recurring Events** - Daily, weekly, monthly repeats
- [ ] **Dark Mode** - Toggle between light and dark themes
- [ ] **Export/Import** - Calendar file (.ics) support
- [ ] **Event Reminders** - Browser notifications
- [ ] **Search & Filter** - Find events quickly
- [ ] **Event Categories** - Organize events by type

### Technical Improvements
- [ ] **TypeScript** - Add type safety
- [ ] **Unit Tests** - Comprehensive test coverage
- [ ] **PWA Support** - Offline functionality
- [ ] **Performance** - Virtual scrolling for large datasets

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Josiane Defo** - [@josiedefo](https://github.com/josiedefo)

## 🙏 Acknowledgments

- Vue.js team for the amazing framework
- Vite for the lightning-fast build tool
- The open-source community for inspiration

---

⭐ **Star this repository if you found it helpful!**

🤖 *Generated with [Claude Code](https://claude.ai/code)*