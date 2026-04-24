# AI Storyteller 🎙️📚

An interactive AI-powered storytelling application that generates unique stories and narrates them with AI voices. Create personalized stories, listen to them being read aloud, and save your favorites—all powered by advanced AI.

Built with **Vite, React, TypeScript, and Supabase**.

![Vite](https://img.shields.io/badge/Vite-5.0-blue)
![React](https://img.shields.io/badge/React-18.0-blue)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue)
![Supabase](https://img.shields.io/badge/Supabase-Database-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## 🚀 Live Demo

- **🌐 Live Application:** [AI Storyteller App](https://app-axrbfd6d08ht.appmedo.com)  
- **📹 Video Walkthrough:** [YouTube Demo](https://youtu.be/OzlNdiQz5q0)

---

## ✨ Key Features

- 🎧 **Listening Mode** — AI voices narrate stories with natural text-to-speech
- ✍️ **Story Generator** — Create custom stories with AI based on your prompts
- 💾 **Save & Manage** — Store and organize your favorite stories in the cloud
- 🎨 **User-Friendly Interface** — Clean, intuitive design for seamless storytelling
- 🌐 **Cloud Storage** — All stories synced and backed up with Supabase

---

## 📂 Project Structure

```
ai-storyteller/
├── README.md                          # Documentation
├── package.json                       # Dependencies & scripts
├── vite.config.ts                     # Vite configuration
├── tsconfig.json                      # TypeScript settings
├── index.html                         # Entry HTML file
├── postcss.config.js                  # PostCSS configuration
├── components.json                    # UI component library config
│
├── public/                            # Static assets
│   ├── favicon.png
│   └── images/
│
└── src/                               # Source code
    ├── main.tsx                       # React entry point
    ├── App.tsx                        # Root component
    ├── index.css                      # Global styles
    ├── routes.tsx                     # Route definitions
    │
    ├── pages/                         # Page components
    │   ├── HomePage
    │   ├── StoryGenerator
    │   ├── ListeningMode
    │   └── SavedStories
    │
    ├── components/                    # Reusable UI components
    │   ├── StoryCard
    │   ├── AudioPlayer
    │   └── ...
    │
    ├── context/                       # React Context for state management
    │   └── StoryContext.tsx
    │
    ├── hooks/                         # Custom React hooks
    │   ├── useAudio
    │   └── useStories
    │
    ├── services/                      # API & database services
    │   ├── supabaseClient.ts
    │   ├── storyService.ts
    │   └── audioService.ts
    │
    ├── db/                            # Database configuration
    │   └── supabaseConfig.ts
    │
    ├── lib/                           # Utility functions & helpers
    │   └── utils.ts
    │
    ├── layout/                        # Layout components
    │   └── MainLayout.tsx
    │
    └── types/                         # TypeScript type definitions
        └── story.ts
```

---

## 🛠 Tech Stack

- **Frontend Framework:** React 18
- **Build Tool:** Vite 5
- **Language:** TypeScript
- **Styling:** CSS/Tailwind CSS
- **State Management:** React Context API
- **Backend & Database:** Supabase (PostgreSQL)
- **Authentication:** Supabase Auth
- **Text-to-Speech:** Web Speech API / Third-party TTS service

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** ≥ 20.x ([Download](https://nodejs.org/))
- **npm** ≥ 10.x (comes with Node.js)
- **Git** (for cloning the repository)

**Verify installation:**
```bash
node -v    # Should output v20.x.x or higher
npm -v     # Should output 10.x.x or higher
```

---

## 🚀 Getting Started

### Step 1: Clone the Repository

```bash
git clone https://github.com/khushikushwah/AI-Storyteller.git
cd AI-Storyteller
```

### Step 2: Install Dependencies

```bash
npm install
```

### Step 3: Set Up Environment Variables

Create a `.env.local` file in the root directory and add your Supabase credentials:

```env
# Supabase Configuration
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here

# Optional: Add other API keys if using external services
VITE_API_KEY=your-api-key
```

**How to get Supabase credentials:**
1. Go to [Supabase](https://supabase.com/)
2. Create a new project
3. Go to **Settings → API** to find your Project URL and Anon Key
4. Copy them into `.env.local`

### Step 4: Start Development Server

```bash
npm run dev
```

The app will be available at: `http://localhost:5173`

**Alternative command:**
```bash
npx vite --host 127.0.0.1
```

### Step 5: Build for Production

```bash
npm run build
```

This generates an optimized build in the `dist/` folder.

---

## 🗄️ Supabase Setup Guide

### Database Schema

The app uses the following main tables:

**1. stories** table:
```sql
CREATE TABLE stories (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL,
  title TEXT NOT NULL,
  content TEXT NOT NULL,
  prompt TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  FOREIGN KEY (user_id) REFERENCES auth.users(id)
);
```

**2. audio_tracks** table (optional, for audio storage):
```sql
CREATE TABLE audio_tracks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  story_id UUID NOT NULL,
  audio_url TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  FOREIGN KEY (story_id) REFERENCES stories(id)
);
```

### Setting Up Supabase Database:

1. Log into your Supabase project
2. Go to **SQL Editor**
3. Create a new query and paste the SQL schemas above
4. Execute the queries
5. Verify tables appear under **Database → Tables**

---

## 📦 Available Scripts

```bash
# Development
npm run dev              # Start dev server on localhost:5173

# Build
npm run build           # Create optimized production build

# Preview
npm run preview         # Preview the production build locally

# Type Checking
npm run type-check      # Check TypeScript types

# Linting (if configured)
npm run lint            # Run ESLint
npm run lint:fix        # Fix linting issues
```

---

## 🎯 How to Use the App

### 1. **Create a Story**
   - Click "Create Story"
   - Enter a prompt describing the story you want
   - Click "Generate" to let AI create a unique story
   - Review the generated content

### 2. **Listen to Story**
   - Select a story from the list
   - Click the play button to hear AI narration
   - Adjust playback speed and volume as needed

### 3. **Save Your Story**
   - After generating a story, click "Save"
   - Story is automatically saved to your Supabase database
   - Access saved stories anytime from "My Stories"

### 4. **Manage Stories**
   - View all your saved stories
   - Delete stories you no longer need
   - Edit story titles or descriptions

---

## 🔧 Development Setup on Your Machine

### Windows

1. **Download Node.js installer** from [nodejs.org](https://nodejs.org/)
2. **Run the installer** and follow the setup wizard
3. **Verify installation:**
   ```cmd
   node -v
   npm -v
   ```
4. **Open VS Code** and start developing

### macOS

**Using Homebrew (Recommended):**
```bash
brew install node
```

**Or download from [nodejs.org](https://nodejs.org/)**

**Verify installation:**
```bash
node -v
npm -v
```

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install nodejs npm
node -v
npm -v
```

---

## 🐛 Troubleshooting

### Issue: `npm install` fails
**Solution:**
```bash
npm cache clean --force
npm install
```

### Issue: Port 5173 already in use
**Solution:**
```bash
npm run dev -- --port 3000
```

### Issue: `.env.local` variables not loading
**Solution:**
- Ensure file name is exactly `.env.local`
- Restart dev server after adding variables
- Variables must start with `VITE_` prefix to be accessible in browser

### Issue: Supabase connection fails
**Solution:**
- Verify `.env.local` has correct Supabase URL and key
- Check Supabase project is active
- Ensure network is connected
- Check browser console for detailed error messages

---

## 📁 Key Files Explained

| File | Purpose |
|------|---------|
| `src/App.tsx` | Main React component & routing |
| `src/routes.tsx` | Route definitions |
| `src/services/supabaseClient.ts` | Supabase client configuration |
| `src/context/StoryContext.tsx` | Global story state management |
| `src/pages/*` | Page components (Home, Generator, etc.) |
| `.env.local` | Environment variables (⚠️ Never commit!) |

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. **Fork** the repository
2. **Create a feature branch:** `git checkout -b feature/your-feature`
3. **Make your changes** and commit: `git commit -m "Add your feature"`
4. **Push to your branch:** `git push origin feature/your-feature`
5. **Open a Pull Request** with description of changes

**Guidelines:**
- Follow existing code style
- Add meaningful commit messages
- Test your changes before submitting PR
- Update documentation if needed

---

## 📄 License

This project is licensed under the **MIT License** - see the LICENSE file for details.

---

## 👨‍💻 Author

**Khushi Kushwah**
- GitHub: [@khushikushwah](https://github.com/khushikushwah)
- Email: your-email@example.com

---

## 🙋 Support & Feedback

- **Report Issues:** [GitHub Issues](https://github.com/khushikushwah/AI-Storyteller/issues)
- **Request Features:** Open an issue with `[FEATURE REQUEST]` tag
- **General Questions:** Discussions section coming soon

---

## 🎓 Learn More

- [React Documentation](https://react.dev)
- [Vite Guide](https://vitejs.dev)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Supabase Docs](https://supabase.com/docs)
- [Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API)

---

**Made with ❤️ by Khushi Kushwah**
