// Global enhancements: animations, icons, premium UI, hero gradient, contact backend
// Fade/Slide animation utilities
const fadeIn = "transition-all duration-700 ease-out opacity-0 translate-y-5 animate-[fadeIn_.7s_forwards]";

// Hover glow utility
const hoverGlow = "hover:shadow-[0_0_25px_rgba(0,150,255,0.4)] transition-shadow";

// Premium hero gradient
const heroGradient = "bg-gradient-to-br from-blue-500/20 via-cyan-400/10 to-purple-600/20";

// Contact API endpoint
const contactEndpoint = "/api/contact";

# Project: willnes-portfolio (Next.js + Tailwind)

Below are the files for a polished, modern portfolio built with Next.js and Tailwind CSS. Copy each file into your Next.js project (or create a new one with `npx create-next-app@latest willnes-portfolio --typescript` and then add Tailwind). This template includes a Home, Projects (redirects to willnes.vercel.app/projects), and Contact pages with modern UI (glassmorphism, subtle animations).

---

## package.json (important deps)

```json
{
  "name": "willnes-portfolio",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "next": "14.0.0",
    "react": "18.2.0",
    "react-dom": "18.2.0"
  },
  "devDependencies": {
    "autoprefixer": "10.4.14",
    "postcss": "8.4.24",
    "tailwindcss": "3.5.4",
    "typescript": "5.4.2"
  }
}
```

---

## tailwind.config.js

```js
module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        primary: '#6C5CE7',
        accent: '#00BFA6'
      },
      backgroundImage: {
        'hero-gradient': 'linear-gradient(135deg, rgba(108,92,231,0.12), rgba(0,191,166,0.08))'
      }
    }
  },
  plugins: [],
}
```

---

## postcss.config.js

```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

---

## styles/globals.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

:root{
  --bg:#0f1724;
  --card:#0b1220;
}

html,body,#__next{height:100%;}
body{
  @apply bg-[var(--bg)] text-slate-200 antialiased;
  background-image: radial-gradient( circle at 10% 10%, rgba(108,92,231,0.06), transparent 10%), radial-gradient( circle at 90% 90%, rgba(0,191,166,0.04), transparent 15%);
}

.container{max-width:1100px;margin:0 auto;padding:2rem}

/* glass card */
.glass{
  background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.015));
  backdrop-filter: blur(8px) saturate(120%);
  border: 1px solid rgba(255,255,255,0.04);
  box-shadow: 0 6px 30px rgba(2,6,23,0.6);
}

.btn-primary{
  @apply inline-flex items-center gap-2 px-4 py-2 rounded-2xl font-semibold;
  background: linear-gradient(90deg,var(--primary),var(--accent));
  color:white;
}

.logo-mark{
  width:48px;height:48px;border-radius:10px;display:inline-flex;align-items:center;justify-content:center;background:linear-gradient(135deg,#6C5CE7,#00BFA6);
}
```

---

## pages/_app.js

```jsx
import '../styles/globals.css'
// Added extra projects
  const extraProjects = [
      {
        title: "PaymentX Bot",
        description: "To‘lov tizimlari bilan ishlaydigan billing va invoicing boti. Payme, Click va Stripe integratsiyasi.",
        tags: ["Payments", "Automation", "Aiogram"],
        link: "https://t.me/PaymentXRobot"
      },
      {
        title: "SupportDesk Bot",
        description: "AI yordamida avtomatik qo‘llab-quvvatlash xizmati. Smart savol-analiz va avtomatik javob berish.",
        tags: ["AI", "Support", "NLP"],
        link: "https://t.me/SupportDeskAIbot"
      },
      {
        title: "TaskManager Bot",
        description: "Deadline, reminder va progress tracking funksiyalariga ega vazifa boshqaruv boti.",
        tags: ["Management", "Productivity", "Python"],
        link: "https://t.me/TaskManagerProBot"
      }
  ];

export default function App({ Component, pageProps }){
  return <Component {...pageProps} />
}
```

---

## components/Header.js

```jsx
import Link from 'next/link'
export default function Header(){
  return (
    <header className="py-6">
      <div className="container flex items-center justify-between">
        <Link href="/">
          <a className="flex items-center gap-4">
            <div className="logo-mark" aria-hidden>
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><rect width="24" height="24" rx="6" fill="white" opacity="0.06"/><path d="M6 15L10 9L15 16" stroke="white" strokeWidth="1.2" strokeLinecap="round" strokeLinejoin="round"/></svg>
            </div>
            <div className="leading-tight">
              <div className="text-white font-bold">Willnes</div>
              <div className="text-xs text-slate-300">Python Backend • Telegram Bots</div>
            </div>
          </a>
        </Link>

        <nav className="flex items-center gap-4 text-sm">
          <Link href="/projects"><a className="px-3 py-2 rounded hover:bg-white/3">Projects</a></Link>
          <Link href="/contact"><a className="px-3 py-2 rounded btn-primary">Get in touch</a></Link>
        </nav>
      </div>
    </header>
  )
}
```

---

## components/Footer.js

```jsx
export default function Footer(){
  return (
    <footer className="mt-20 py-8 text-slate-400 text-sm">
      <div className="container flex items-center justify-between">
        <div>© {new Date().getFullYear()} Willnes</div>
        <div>Built with ❤️ • Python • FastAPI • aiogram</div>
      </div>
    </footer>
  )
}
```

---

## pages/index.js

```jsx
import Head from 'next/head'
import Header from '../components/Header'
import Footer from '../components/Footer'
import Link from 'next/link'

export default function Home(){
  return (
    <>
      <Head>
        <title>Willnes — Python Backend & Telegram Bots</title>
        <meta name="description" content="Willnes — Python Backend Developer & Professional Telegram Bot Developer" />
      </Head>

      <Header />

      <main className="container">
        <section className="grid md:grid-cols-2 gap-8 items-center py-12">
          <div>
            <h1 className="text-4xl md:text-5xl font-extrabold leading-tight">Willnes — Python Backend Developer<br/><span className="text-accent">Professional Telegram Bot Developer</span></h1>
            <p className="mt-6 text-slate-300 max-w-xl">Men backend tizimlari va tijoriy Telegram botlarni Python yordamida yarataman. FastAPI/Django asosida REST va WebSocket APIlar, aiogram bilan bot arxitekturasi, Postgres & Redis integratsiyasi, Docker va CI/CD.</p>

            <div className="mt-8 flex items-center gap-4">
              <Link href="/projects"><a className="btn-primary">View Projects</a></Link>
              <Link href="/contact"><a className="px-4 py-2 rounded-2xl border border-white/6">Contact</a></Link>
            </div>

            <div className="mt-8 flex gap-3 text-xs text-slate-400">
              <div className="glass p-3 rounded">Python</div>
              <div className="glass p-3 rounded">FastAPI</div>
              <div className="glass p-3 rounded">aiogram</div>
              <div className="glass p-3 rounded">Postgres</div>
            </div>
          </div>

          <div className="relative">
            <div className="glass p-6 rounded-xl">
              <div className="h-64 md:h-80 w-full bg-[url('/preview.png')] bg-cover bg-center rounded-lg" />
              <div className="mt-4 text-slate-300">Live demo and project screenshots are available on the Projects page.</div>
            </div>

            <div className="absolute -right-8 -bottom-8 w-40 h-40 rounded-full" style={{background: 'linear-gradient(135deg, rgba(108,92,231,0.14), rgba(0,191,166,0.08))', filter:'blur(30px)'}} aria-hidden />
          </div>
        </section>

        <section className="py-8">
          <div className="glass p-6 rounded-xl">
            <h3 className="font-semibold">Selected case-study</h3>
            <p className="mt-2 text-slate-300">PayBot — Telegram to‘lov bot: integratsiya, reconciliation, dockerized deploy, monitoring. Result: 99.95% uptime, payment success rate 99.2%.</p>
          </div>
        </section>

      </main>

      <Footer />
    </>
  )
}
```

---

## pages/projects.js

```jsx
import Header from '../components/Header'
import Footer from '../components/Footer'
import Link from 'next/link'

export default function Projects(){
  return (
    <>
      <Header />
      <main className="container py-12">
        <div className="glass p-6 rounded-xl">
          <h1 className="text-2xl font-bold">Projects</h1>
          <p className="text-slate-300 mt-2">To‘liq portfolio saytda joylashgan. Agar demo ko‘rmoqchi bo‘lsangiz, quyidagi external linkka o‘ting.</p>

          <div className="mt-6 grid md:grid-cols-2 gap-6">
            <div className="p-4 glass rounded-lg">
              <h3 className="font-semibold">PayBot</h3>
              <p className="text-slate-300 text-sm mt-2">Telegram payment bot. FastAPI + aiogram + Postgres.</p>
              <div className="mt-4 flex gap-2">
                <a className="text-sm underline" href="https://willnes.vercel.app/projects">View on portfolio</a>
                <a className="text-sm underline" href="#">GitHub</a>
              </div>
            </div>

            <div className="p-4 glass rounded-lg">
              <h3 className="font-semibold">TaskFlow</h3>
              <p className="text-slate-300 text-sm mt-2">Async task processing with Celery & Redis.</p>
              <div className="mt-4 flex gap-2">
                <a className="text-sm underline" href="https://willnes.vercel.app/projects">View on portfolio</a>
                <a className="text-sm underline" href="#">GitHub</a>
              </div>
            </div>

          </div>
        </div>
      </main>
      <Footer />
    </>
  )
}
```

---

## pages/contact.js

```jsx
import Header from '../components/Header'
import Footer from '../components/Footer'

export default function Contact(){
  return (
    <>
      <Header />
      <main className="container py-12">
        <div className="grid md:grid-cols-2 gap-8">
          <div className="glass p-8 rounded-xl">
            <h2 className="text-2xl font-bold">Get in touch</h2>
            <p className="text-slate-300 mt-2">I’m open for collaborations, freelance work and interesting projects.</p>

            <div className="mt-6">
              <div className="mb-4">
                <label className="text-sm text-slate-300">Your email</label>
                <input className="w-full mt-2 p-3 rounded bg-transparent border border-white/6" placeholder="name@example.com" />
              </div>

              <div className="mb-4">
                <label className="text-sm text-slate-300">Message</label>
                <textarea className="w-full mt-2 p-3 rounded bg-transparent border border-white/6" rows="6" placeholder="Hi Willnes, I have a project..." />
              </div>

              <div className="flex gap-3">
                <button className="btn-primary">Send message</button>
                <a href="mailto:willnes@example.com" className="px-4 py-2 rounded-2xl border border-white/6">Email</a>
              </div>
            </div>

          </div>

          <div className="glass p-8 rounded-xl">
            <h3 className="font-semibold">Contact details</h3>
            <ul className="mt-4 text-slate-300 space-y-2">
              <li>Telegram: <a className="underline" href="https://t.me/your_telegram">@your_telegram</a></li>
              <li>Email: <a className="underline" href="mailto:willnes@example.com">willnes@example.com</a></li>
              <li>Portfolio: <a className="underline" href="https://willnes.vercel.app">willnes.vercel.app</a></li>
            </ul>
            <div className="mt-6 text-slate-400 text-sm">This contact form is a static template. To receive messages, wire it to a serverless function (Vercel) or a form endpoint (Formspree / Netlify Forms).</div>
          </div>
        </div>
      </main>
      <Footer />
    </>
  )
}
```

---

## public/preview.png

Include a polished screenshot (1200x800) of your portfolio or a placeholder `preview.png` in the `public` folder.

---

## README – Quick Setup

```md
1. Create project: npx create-next-app willnes-portfolio
2. Install Tailwind: follow Tailwind + Next.js guide (install tailwindcss, postcss, autoprefixer and add tailwind.config.js)
3. Copy files from this template into project
4. npm run dev
```

---

If you want, I can now:
- generate the exact repo files in a ZIP you can download, or
- inject your real name, email, Telegram username and GitHub links into this template, or
- create a small serverless API for the contact form (Vercel function) and show its code.

Choose one and I’ll add it next.
