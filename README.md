# Sycamore UI Test: Staco Finance - Nuxt 4 Landing Page

A high-performance, pixel-perfect recreation of the Staco Finance landing page. Built with the cutting-edge **Nuxt 4** ecosystem, focusing on smooth animations, scroll-driven interactions, and modern design principles.

## 🌐 Live Demo

Check out the live deployment: [https://sycamore-test-landing-page.vercel.app/](https://sycamore-test-landing-page.vercel.app/)

---

## ⚡ Tech Stack

- **Framework:** [Nuxt 4](https://nuxt.com) (Vue 3)
- **UI Library:** [Nuxt UI](https://ui.nuxt.com)
- **Styling:** [Tailwind CSS 4](https://tailwindcss.com) (via `@nuxt/ui`)
- **Animations:**
  - `@vueuse/motion` (Element transitions, slide-ins)
  - `@vueuse/core` (Parallax, scroll detection, counters)
- **Icons:** Lucide & Heroicons (via Nuxt UI)

## ✨ Key Features

- **Smart Navigation:**
  - "Motion Pill" active state indicator.
  - Glassmorphism effect on scroll.
  - Auto-hide on scroll down, reveal on scroll up.
- **Interactive Hero:**
  - Rotating text typewriter effect.
  - Video modal/playback integration.
- **Scroll Animations:**
  - **Parallax Illustration:** The CTA illustration rises/sinks based on scroll direction.
  - **Animated Counters:** Statistics count up smoothly when entering the viewport.
  - **Section Transitions:** Elements slide in using spring physics.
- **Fully Responsive:** Mobile-first design with a custom slide-over menu for smaller screens.

## 🚀 Getting Started

> **Important:** This project uses **npm**. Do not mix package managers (pnpm/yarn) to avoid dependency conflicts with Vue instances.

### 1. Clone the repository

```bash
git clone <repository-url>
cd staco-finance
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Run Development Server

```bash
npm run dev
```

Access the app at `http://localhost:3000`.

### 4. Build for Production

```bash
npm run build
```

## 📂 Project Structure

```
├── app/
│   └── assets/
│       └── css/
│           └── main.css        # Tailwind 4 theme configuration
│   ├── components/
│   │   ├── TheNavbar.vue       # Smart header with scroll logic
│   │   ├── TheFooter.vue       # Static footer with links
│   │   └── AppLogo.vue         # Brand assets
│   ├── layouts/
│   │   └── default.vue         # Global wrapper (Navbar + Slot + Footer)
│   ├── pages/
│   │   └── index.vue           # Main landing page (Hero, Features, CTA)
├── public/                     # Static assets (Videos, SVGs)
├── nuxt.config.ts              # Nuxt 4 configuration
└── package.json
```

## 🎨 Design Notes

- **Theme:** The project uses a custom Tailwind theme defined in `main.css` to match Staco's brand colors (`--color-staco-green`, `--color-staco-dark`, etc.).
- **Performance:** Uses `v-motion` directives for performant, hardware-accelerated animations instead of heavy JavaScript scroll listeners where possible.
