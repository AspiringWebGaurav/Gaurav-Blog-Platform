# Gaurav Blog Platform (GBP)

A modern blogging platform with **real-time template switching**, dynamic content management, and 10 beautiful design templates. Built with Next.js 15, Firebase, and Tailwind CSS.

![GBP Platform](https://img.shields.io/badge/GBP-Blog%20Platform-blue) ![Next.js](https://img.shields.io/badge/Next.js-15-black) ![Firebase](https://img.shields.io/badge/Firebase-v9+-orange) ![Tailwind](https://img.shields.io/badge/Tailwind-v4-blue)

## ✨ Features

### 🎨 **10 Dynamic Templates**
- **Magazine**: Editorial multi-column with typography hierarchy
- **Newspaper**: Classic column layout with traditional typography  
- **Notebook**: Journal style with margins and handwritten fonts
- **Gallery**: Image-focused masonry layouts
- **Zen**: Ultra-minimal with maximum whitespace
- **Cards**: Material Design inspired with shadows
- **Gridline**: Technical documentation with grid overlay
- **Sidebar**: Traditional blog layout (2/3 + 1/3)
- **Monochrome**: High contrast black/white design
- **Flux**: Motion-heavy showcase with animations & gradients ⚡

### ⚡ **Real-time Features**
- **Live Template Switching**: Watch templates change instantly with progress indicators
- **Real-time Comments**: Live commenting system with moderation
- **Dynamic Content**: Content updates without page refresh
- **Progress Tracking**: Visual feedback for all operations

### 🔧 **Admin Control Panel**
- **Posts Management**: Create, edit, delete with live preview
- **Template Gallery**: Browse and preview all templates
- **Comment Moderation**: Approve, flag, delete with bulk actions
- **User Management**: Ban/unban system with reason tracking
- **Asset Upload**: Firebase Storage integration with URL generation

### 🛡️ **Security & Moderation**
- **Ban System**: Client-side enforcement for development
- **Comment Moderation**: All comments require approval
- **Anti-spam Protection**: Length limits and submission debouncing
- **Route Guards**: Protected admin areas

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ 
- Firebase project with Firestore and Storage enabled
- Git

### Installation

1. **Clone and install dependencies**
```bash
git clone <repository-url>
cd gaurav-blog-platform
npm install
```

2. **Set up environment variables**
Create `.env.local` in the root directory:
```env
# Firebase Configuration - GBP
NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_auth_domain
NEXT_PUBLIC_FIREBASE_DATABASE_URL=your_database_url
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_storage_bucket
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id
NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID=your_measurement_id
```

3. **Configure Firebase Rules (DEVELOPMENT ONLY)**

Deploy the included test rules to Firebase:

**Firestore Rules:**
```bash
firebase deploy --only firestore:rules
```

**Storage Rules:**
```bash
firebase deploy --only storage
```

⚠️ **WARNING**: The included rules provide OPEN READ/WRITE access for development. DO NOT use in production!

4. **Seed the database**
```bash
npm run seed
```

5. **Start development server**
```bash
npm run dev
```

6. **Visit the application**
- Homepage: http://localhost:3000
- Admin Panel: http://localhost:3000/admin
- Login: http://localhost:3000/login

## 📖 Usage Guide

### Getting Started

1. **Create an Account**: Visit `/login` and create an account
2. **Access Admin**: Navigate to `/admin` (any authenticated user has admin access in dev mode)
3. **Create Posts**: Use the Posts tab to create and manage content
4. **Switch Templates**: Edit posts and change templates to see live switching
5. **Moderate Comments**: Use the Comments tab to manage user interactions

### Template Switching

1. Go to Admin → Posts
2. Edit any post
3. Change the template dropdown
4. Watch the live page update with progress bar!

### Ban System

The ban system provides client-side enforcement:

1. **Ban Users**: Admin → Users → Enter UID and reason → Ban
2. **Enforcement**: Banned users cannot comment or post
3. **Unban**: Remove bans instantly from the admin panel

## 🏗️ Technical Architecture

### Stack
- **Frontend**: Next.js 15 App Router (JavaScript only)
- **Database**: Firebase Firestore with real-time subscriptions
- **Authentication**: Firebase Auth (email/password)
- **Storage**: Firebase Storage for assets and theme files
- **Styling**: Tailwind CSS v4 with custom GBP design system
- **Notifications**: React Hot Toast

### Project Structure
```
src/
├── app/                    # Next.js App Router
│   ├── (admin)/           # Admin pages
│   ├── (auth)/            # Authentication pages  
│   ├── (public)/          # Public pages
│   └── layout.js          # Root layout
├── components/            # Reusable components
│   ├── Admin*.js         # Admin panel components
│   ├── Comments.js       # Real-time comments
│   ├── Nav.js            # Navigation
│   └── ProgressBar.js    # Progress indicators
├── lib/                   # Core utilities
│   ├── firebase.js       # Firebase configuration
│   ├── auth.js           # Authentication helpers
│   ├── firestore.js      # Database operations
│   ├── ban.js            # Ban system
│   └── schema.js         # Data model definitions
└── templates/            # 10 unique templates
    ├── Magazine.js
    ├── Zen.js
    ├── Flux.js
    └── ...
```

### Data Model

**Collections:**
- `posts`: Post metadata (title, slug, status, templateId, themeVars)
- `postContent`: Post body content (postId, format, body)
- `comments`: User comments (postId, userId, body, status)
- `templates`: Template definitions (id, name, description, defaultThemeVars)
- `bannedUsers`: Ban records (uid, reason, createdAt)

## 📝 Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production  
- `npm run start` - Start production server
- `npm run seed` - Seed database with templates and demo posts

## 🔒 Security Notes

### Development Mode (Current)
- **Firestore Rules**: Open read/write access for all collections
- **Storage Rules**: Open read/write access for all paths
- **Ban Enforcement**: Client-side only
- **Admin Access**: Any authenticated user

### Production Recommendations
- Implement server-side security rules
- Add role-based access control
- Enable ban enforcement at database level
- Add content validation and sanitization
- Implement rate limiting
- Add file upload restrictions and virus scanning

## 🎯 Template System

### Template Structure
Each template accepts these props:
```javascript
{
  themeVars: {},      // Customization variables
  content: {},        // Post content and metadata
  title: "string",    // Post title
  summary: "string",  // Post summary
  templateId: "string" // Template identifier
}
```

### Theme Variables
Templates support customization through theme variables:
```javascript
{
  primaryColor: "#000000",
  secondaryColor: "#666666", 
  backgroundColor: "#ffffff",
  accentColor: "#007bff",
  fontFamily: "Inter, sans-serif",
  fontSize: "16px",
  lineHeight: "1.6",
  borderRadius: "8px"
}
```

### Adding New Templates
1. Create template component in `/src/templates/`
2. Add import to `TemplateClient.js`
3. Add template definition to seed script
4. Run `npm run seed` to update database

## 🎮 Live Demo Features

1. **Template Showcase**: Visit demo posts to see different templates
2. **Real-time Switching**: Change templates in admin and watch live updates
3. **Comment System**: Sign in and leave comments (moderation required)
4. **Search & Filter**: Use homepage search to find posts
5. **Admin Panel**: Full CRUD operations for posts, comments, users

## 🐛 Troubleshooting

### Common Issues

**"Firebase environment variables not found"**
- Ensure `.env.local` exists with all `NEXT_PUBLIC_*` variables
- Restart development server after adding environment variables

**"Template not found, using fallback"**
- Check template imports in `TemplateClient.js`
- Verify template component exports default function

**"Failed to load published posts"**
- Ensure Firebase rules are deployed
- Check Firestore collections exist (run `npm run seed`)
- Verify network connectivity to Firebase

**Blank page or loading issues**
- Check browser console for JavaScript errors
- Verify all component imports are correct
- Restart development server

### Debug Mode
In development, several debugging tools are available:
- Browser console: `window.gbpAuth` - Authentication helpers
- Browser console: `window.gbpFirestore` - Database helpers  
- Browser console: `window.gbpBan` - Ban system helpers

## 🚀 Deployment

### Vercel (Recommended)
1. Push code to GitHub
2. Connect repository to Vercel
3. Add environment variables in Vercel dashboard
4. Deploy Firebase rules to production project
5. Update domain in `robots.txt` and `sitemap.xml`

### Manual Deployment
1. Run `npm run build`
2. Deploy `out/` directory to your hosting platform
3. Configure environment variables
4. Update Firebase security rules for production

## 📄 License

This project is licensed under the MIT License. See LICENSE file for details.

## 👨‍💻 Author

**Gaurav Patil**
- Platform Creator & Developer
- Built with ❤️ using modern web technologies

---

**Gaurav Blog Platform** - Revolutionizing blogging with real-time template switching and beautiful design.

*For support and questions, please open an issue in the repository.*
