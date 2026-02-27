---
## package.json
```json
{
  "name": "jarvis-ai",
  "version": "6.0.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "next": "15.0.0",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "framer-motion": "^11.0.0",
    "lucide-react": "^0.400.0",
    "fuse.js": "^7.0.0",
    "@tsparticles/react": "^3.0.0",
    "@tsparticles/slim": "^3.0.0",
    "vanilla-tilt": "^1.8.1",
    "canvas-confetti": "^1.9.2",
    "jspdf": "^2.5.1",
    "pdf-lib": "^1.17.1",
    "react-swipeable": "^7.0.1",
    "countup.js": "^2.8.0",
    "dexie": "^4.0.8",
    "compromise": "^14.10.0",
    "next-pwa": "^5.6.0"
  },
  "devDependencies": {
    "typescript": "^5.4.5",
    "@types/node": "^20",
    "@types/react": "18.2.55",
    "@types/react-dom": "18.2.19",
    "@types/canvas-confetti": "^1.6.0",
    "tailwindcss": "^3.4.0",
    "autoprefixer": "^10.0.0",
    "postcss": "^8"
  }
}
```

## tsconfig.json
```json
{
  "compilerOptions": {
    "target": "es5",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [{"name": "next"}],
    "paths": {"@/*": ["./*"]}
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

## next.config.js
```js
const withPWA = require('next-pwa')({
  dest: 'public',
  register: true,
  skipWaiting: true,
  disable: process.env.NODE_ENV === 'development',
})

const nextConfig = {
  async headers() {
    return [
      {
        source: '/(.*)',
        headers: [
          {
            key: 'X-Frame-Options',
            value: 'DENY',
          },
          {
            key: 'X-Content-Type-Options',
            value: 'nosniff',
          },
        ],
      },
    ]
  },
}

module.exports = withPWA(nextConfig)
```

Fill in:
- `GEMINI_API_KEY` → https://aistudio.google.com/apikey (FREE)
- `GROQ_API_KEY` → https://console.groq.com (FREE)

### Step 3 — Run locally
```bash
npm run dev
# Open http://localhost:3000
```

### Step 4 — Deploy to Vercel (FREE)
1. GitHub pe push karo
2. vercel.com → Import repo
3. Environment variables add karo
4. Deploy!

---

## ✅ BUG FIX SUMMARY (v5 + v6 se kya theek kiya)

| Bug | v5/v6 mein kya tha | Fix |
|-----|---------------------|-----|
| ERESOLVE npm error | `react: "^19.0.0"` | `react: "18.2.0"` |
| @types mismatch | `@types/react: "^19"` | `@types/react: "18.2.55"` |
| SSR crash (Dexie) | `const db = new JarvisDB()` module level | Lazy async `getDB()` with window check |
| SSR crash (localStorage) | Direct `localStorage.getItem` | `typeof window === 'undefined'` guard |
| workbox conflict | `workbox-webpack-plugin: "^7"` | Replaced with `next-pwa: "^5.6.0"` |
| Unused `ai` package | `"ai": "^3.0.0"` | Removed completely |
| Duplicate useEffect | 2 chat-loading effects | Single effect |
| `let c = import(...)` | Unused variable | Fixed |
| Settings/History as alert/confirm | `alert()` / `confirm()` | SmartSettings + SmartHistory modals |

---

## 💰 COST — ₹0 FOREVER

| Service | Free Limit | Usage |
|---------|-----------|-------|
| Vercel Hosting | 100GB/month | ~1GB/month |
| Gemini Flash | 1500 req/day | Primary AI |
| Groq Llama3 | 14,400 req/day | Fallback 1 |
| OpenRouter | Free tier | Fallback 2 |
| AIMLAPI | Free tier | Fallback 3 |
| Web Speech API | Browser built-in | Unlimited |

---

## 🔒 GOLDEN RULES (Kabhi mat todna)

1. localStorage keys kabhi rename mat karo
2. Server (API routes) mein Dexie/localStorage import mat karo
3. API keys sirf `.env.local` mein — client mein never
4. Mobile first — 48px tap targets
5. Error chain: Gemini → Groq → OpenRouter → AIMLAPI → Keyword fallback

---

*JARVIS v6.0 — v5 + v6 Merged — Fully Fixed — ₹0 Forever*
