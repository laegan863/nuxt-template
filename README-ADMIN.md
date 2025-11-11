# Modern Admin Dashboard

A modern, responsive admin dashboard built with Nuxt 3, Tailwind CSS, and FontAwesome icons. Features light and dark mode with smooth transitions.

## Features

✨ **Modern Design**
- Clean and minimalist interface
- Glassmorphism effects
- Gradient accents
- Smooth animations and transitions

🌗 **Dark Mode**
- Toggle between light and dark themes
- Automatic theme persistence
- Smooth theme transitions

📱 **Responsive**
- Mobile-first design
- Collapsible sidebar
- Optimized for all screen sizes

🎨 **Built With**
- **Nuxt 3** - The Intuitive Vue Framework
- **Tailwind CSS** - Utility-first CSS framework
- **@nuxtjs/color-mode** - Dark mode support
- **FontAwesome** - Beautiful icons

## Getting Started

### Install Dependencies

\`\`\`bash
npm install
\`\`\`

### Development Server

\`\`\`bash
npm run dev
\`\`\`

Visit http://localhost:3000 to see your dashboard.

### Build for Production

\`\`\`bash
npm run build
npm run preview
\`\`\`

## Project Structure

\`\`\`
app/
├── assets/
│   └── css/
│       └── main.css          # Global styles with Tailwind directives
├── components/
│   ├── Navbar.vue            # Top navigation with theme toggle
│   └── Sidebar.vue           # Collapsible sidebar with dropdown
├── layouts/
│   └── admin.vue             # Admin layout wrapper
├── pages/
│   ├── index.vue             # Redirects to dashboard
│   ├── dashboard.vue         # Main dashboard page
│   └── empty.vue             # Empty page template
└── plugins/
    └── fontawesome.ts        # FontAwesome configuration
\`\`\`

## Features Overview

### Dashboard Page
- Statistics cards with gradients
- Recent activity feed
- Quick action buttons
- Responsive grid layout

### Sidebar
- Collapsible navigation
- Dropdown menu support
- Active route highlighting
- FontAwesome icons

### Theme Toggle
- Light/Dark mode switch
- Persistent preference
- Smooth transitions
- Automatic system detection

## Customization

### Colors
Edit `tailwind.config.js` to customize the color palette:

\`\`\`js
theme: {
  extend: {
    colors: {
      primary: {
        // Your custom colors
      }
    }
  }
}
\`\`\`

### Adding New Pages
1. Create a new file in `app/pages/`
2. Add route link in `Sidebar.vue`
3. Use the admin layout: `<NuxtLayout name="admin">`

## License

MIT
