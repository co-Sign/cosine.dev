# 🚀 Co-Sign Landing Page - Complete Implementation Plan

## 📋 Project Overview

**Goal**: Create a clean, modern landing page that matches the main Co-Sign app aesthetic with:
- ✅ **Unified Design Language**: Match the video calling app's clean UI
- ✅ **Light/Dark Theme Support**: Seamless theme switching
- ✅ **Futuristic Typography**: Custom font integration 
- ✅ **Minimal Glass Effects**: Subtle, not overwhelming
- ✅ **shadcn/ui Components**: Consistent component library
- ✅ **Mobile-First Design**: Perfect responsive experience

---

## 🎨 Design System Alignment

### Color Palette (From Main App)
```css
/* Light Theme */
--bg-light: #E8F4FD;
--text-light: #1C1F2E;
--glass-light: rgba(255, 255, 255, 0.8);

/* Dark Theme */  
--bg-dark: #1C1F2E;
--text-dark: #ffffff;
--glass-dark: rgba(255, 255, 255, 0.05);

/* Brand Colors */
--primary: #0E78F9;
--secondary: #252A41;
--border: rgba(255, 255, 255, 0.08);
```

### Typography
- **Primary Font**: Geist Sans (same as main app)
- **Futuristic Elements**: Maintained but subtle
- **Hierarchy**: Clear heading scales

### Component Style
- **Minimal Glass**: Subtle backdrop-blur effects
- **Clean Cards**: Simple borders, soft shadows
- **Button Styles**: Match main app button designs
- **Form Elements**: Consistent input styling

---

## 🏗️ Component Architecture

### Core Components
```
src/
├── components/
│   ├── ui/                    # shadcn/ui components
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   ├── input.tsx
│   │   └── theme-toggle.tsx
│   ├── layout/
│   │   ├── Navbar.tsx         # Clean navigation
│   │   ├── Footer.tsx         # Simple footer
│   │   └── ThemeProvider.tsx  # Theme context
│   ├── sections/
│   │   ├── Hero.tsx           # Hero with clean design
│   │   ├── Features.tsx       # Feature showcase
│   │   ├── Demo.tsx           # Demo section
│   │   ├── Pricing.tsx        # Pricing cards
│   │   └── Contact.tsx        # Contact form
│   └── effects/
│       ├── AnimatedBackground.tsx
│       └── ScrollAnimations.tsx
```

---

## 🔧 STEP 1: Dependencies Installation

```bash
# Install required dependencies
bun add class-variance-authority clsx tailwind-merge lucide-react next-themes
bun add @radix-ui/react-slot
bun add -D tailwindcss @tailwindcss/typography autoprefixer postcss
```

---

## 🔧 STEP 2: Configuration Files

### tailwind.config.js
```javascript
/** @type {import('tailwindcss').Config} */
export default {
  darkMode: ["class"],
  content: [
    './pages/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './app/**/*.{ts,tsx}',
    './src/**/*.{ts,tsx}',
    './index.html',
  ],
  prefix: "",
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      fontFamily: {
        sans: ["Geist Sans", "system-ui", "sans-serif"],
        mono: ["Geist Mono", "monospace"],
      },
      keyframes: {
        "accordion-down": {
          from: { height: "0" },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: "0" },
        },
        "fade-in": {
          "0%": { opacity: "0", transform: "translateY(10px)" },
          "100%": { opacity: "1", transform: "translateY(0)" },
        },
        "fade-in-delayed": {
          "0%": { opacity: "0", transform: "translateY(20px)" },
          "100%": { opacity: "1", transform: "translateY(0)" },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
        "fade-in": "fade-in 0.6s ease-out",
        "fade-in-delayed": "fade-in-delayed 0.8s ease-out 0.2s both",
      },
      backdropBlur: {
        xs: '2px',
      },
      boxShadow: {
        'glass': '0 8px 32px 0 rgba(14, 120, 249, 0.1)',
        'glass-strong': '0 8px 32px 0 rgba(14, 120, 249, 0.2)',
      },
    },
  },
  plugins: [require("@tailwindcss/typography")],
}
```

### postcss.config.js
```javascript
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

---

## 🔧 STEP 3: Core Utilities

### src/lib/utils.ts
```typescript
import { type ClassValue, clsx } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}
```

---

## 🔧 STEP 4: Updated Design Tokens (Replace existing design-tokens.css)

### src/design-tokens.css
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Co-Sign Design System - Clean & Modern */
@layer base {
  :root {
    /* Light theme variables */
    --background: 232 244 253;  /* #E8F4FD */
    --foreground: 28 31 46;     /* #1C1F2E */
    --card: 255 255 255;
    --card-foreground: 28 31 46;
    --popover: 255 255 255;
    --popover-foreground: 28 31 46;
    --primary: 14 120 249;      /* #0E78F9 */
    --primary-foreground: 255 255 255;
    --secondary: 245 245 245;
    --secondary-foreground: 28 31 46;
    --muted: 245 245 245;
    --muted-foreground: 107 114 128;
    --accent: 245 245 245;
    --accent-foreground: 28 31 46;
    --destructive: 239 68 68;
    --destructive-foreground: 255 255 255;
    --border: 229 231 235;
    --input: 229 231 235;
    --ring: 14 120 249;
    --radius: 0.5rem;
  }

  .dark {
    /* Dark theme variables */
    --background: 28 31 46;     /* #1C1F2E */
    --foreground: 255 255 255;
    --card: 37 42 65;          /* #252A41 */
    --card-foreground: 255 255 255;
    --popover: 37 42 65;
    --popover-foreground: 255 255 255;
    --primary: 14 120 249;      /* #0E78F9 */
    --primary-foreground: 255 255 255;
    --secondary: 37 42 65;      /* #252A41 */
    --secondary-foreground: 255 255 255;
    --muted: 37 42 65;
    --muted-foreground: 156 163 175;
    --accent: 37 42 65;
    --accent-foreground: 255 255 255;
    --destructive: 239 68 68;
    --destructive-foreground: 255 255 255;
    --border: 255 255 255 / 0.08;
    --input: 37 42 65;
    --ring: 14 120 249;
  }
}

@layer base {
  * {
    @apply border-border;
  }
  body {
    @apply bg-background text-foreground;
    font-feature-settings: "rlig" 1, "calt" 1;
  }
}

@layer components {
  .glass-card {
    @apply backdrop-blur-sm bg-card/50 border border-border/50 rounded-lg;
  }
  
  .glass-button {
    @apply backdrop-blur-sm bg-white/5 border border-white/10 hover:bg-white/10 
           text-white transition-all duration-300 rounded-md px-4 py-2;
  }
  
  .gradient-text {
    @apply bg-gradient-to-r from-primary to-blue-400 bg-clip-text text-transparent;
  }
  
  .hero-gradient {
    background: radial-gradient(circle at 50% 50%, hsl(var(--primary) / 0.1) 0%, transparent 50%);
  }
}

/* Geist Font Integration */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');

body {
  font-family: 'Inter', 'Geist Sans', system-ui, sans-serif;
  font-optical-sizing: auto;
  font-variation-settings: "slnt" 0;
}

h1, h2, h3, h4, h5, h6 {
  font-family: 'Inter', 'Geist Sans', system-ui, sans-serif;
  font-weight: 600;
  letter-spacing: -0.025em;
}
```

---

## 🔧 STEP 5: shadcn/ui Components

### src/components/ui/button.tsx
```typescript
import * as React from "react"
import { Slot } from "@radix-ui/react-slot"
import { cva, type VariantProps } from "class-variance-authority"

import { cn } from "@/lib/utils"

const buttonVariants = cva(
  "inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-md text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground hover:bg-primary/90",
        destructive:
          "bg-destructive text-destructive-foreground hover:bg-destructive/90",
        outline:
          "border border-input bg-background hover:bg-accent hover:text-accent-foreground",
        secondary:
          "bg-secondary text-secondary-foreground hover:bg-secondary/80",
        ghost: "hover:bg-accent hover:text-accent-foreground",
        glass: "backdrop-blur-sm bg-white/5 border border-white/10 hover:bg-white/10 text-white",
        "glass-primary": "backdrop-blur-sm bg-primary/20 border border-primary/30 hover:bg-primary/30 text-white",
      },
      size: {
        default: "h-10 px-4 py-2",
        sm: "h-9 rounded-md px-3",
        lg: "h-11 rounded-md px-8",
        icon: "h-10 w-10",
      },
    },
    defaultVariants: {
      variant: "default",
      size: "default",
    },
  }
)

export interface ButtonProps
  extends React.ButtonHTMLAttributes<HTMLButtonElement>,
    VariantProps<typeof buttonVariants> {
  asChild?: boolean
}

const Button = React.forwardRef<HTMLButtonElement, ButtonProps>(
  ({ className, variant, size, asChild = false, ...props }, ref) => {
    const Comp = asChild ? Slot : "button"
    return (
      <Comp
        className={cn(buttonVariants({ variant, size, className }))}
        ref={ref}
        {...props}
      />
    )
  }
)
Button.displayName = "Button"

export { Button, buttonVariants }
```

### src/components/ui/card.tsx
```typescript
import * as React from "react"

import { cn } from "@/lib/utils"

const Card = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div
    ref={ref}
    className={cn(
      "rounded-lg border bg-card text-card-foreground shadow-sm",
      className
    )}
    {...props}
  />
))
Card.displayName = "Card"

const CardHeader = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div ref={ref} className={cn("flex flex-col space-y-1.5 p-6", className)} {...props} />
))
CardHeader.displayName = "CardHeader"

const CardTitle = React.forwardRef<
  HTMLParagraphElement,
  React.HTMLAttributes<HTMLHeadingElement>
>(({ className, ...props }, ref) => (
  <h3
    ref={ref}
    className={cn(
      "text-2xl font-semibold leading-none tracking-tight",
      className
    )}
    {...props}
  />
))
CardTitle.displayName = "CardTitle"

const CardDescription = React.forwardRef<
  HTMLParagraphElement,
  React.HTMLAttributes<HTMLParagraphElement>
>(({ className, ...props }, ref) => (
  <p
    ref={ref}
    className={cn("text-sm text-muted-foreground", className)}
    {...props}
  />
))
CardDescription.displayName = "CardDescription"

const CardContent = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div ref={ref} className={cn("p-6 pt-0", className)} {...props} />
))
CardContent.displayName = "CardContent"

const CardFooter = React.forwardRef<
  HTMLDivElement,
  React.HTMLAttributes<HTMLDivElement>
>(({ className, ...props }, ref) => (
  <div
    ref={ref}
    className={cn("flex items-center p-6 pt-0", className)}
    {...props}
  />
))
CardFooter.displayName = "CardFooter"

export { Card, CardHeader, CardFooter, CardTitle, CardDescription, CardContent }
```

### src/components/ui/theme-toggle.tsx
```typescript
import * as React from "react"
import { Moon, Sun } from "lucide-react"
import { useTheme } from "next-themes"

import { Button } from "@/components/ui/button"

export function ThemeToggle() {
  const { setTheme, theme } = useTheme()

  return (
    <Button
      variant="ghost"
      size="icon"
      onClick={() => setTheme(theme === "light" ? "dark" : "light")}
      className="h-9 w-9"
    >
      <Sun className="h-4 w-4 rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0" />
      <Moon className="absolute h-4 w-4 rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100" />
      <span className="sr-only">Toggle theme</span>
    </Button>
  )
}
```

---

## 🔧 STEP 6: Theme Provider

### src/components/theme-provider.tsx
```typescript
import * as React from "react"
import { ThemeProvider as NextThemesProvider } from "next-themes"
import { type ThemeProviderProps } from "next-themes/dist/types"

export function ThemeProvider({ children, ...props }: ThemeProviderProps) {
  return <NextThemesProvider {...props}>{children}</NextThemesProvider>
}
```

---

## 🔧 STEP 7: Clean Component Implementations

### src/components/Navbar.tsx
```typescript
import { useState } from 'react'
import { motion } from 'framer-motion'
import { Menu, X } from 'lucide-react'
import { Button } from '@/components/ui/button'
import { ThemeToggle } from '@/components/ui/theme-toggle'
import { cn } from '@/lib/utils'

export default function Navbar() {
  const [isOpen, setIsOpen] = useState(false)

  const navItems = [
    { name: 'Features', href: '#features' },
    { name: 'Demo', href: '#demo' },
    { name: 'Pricing', href: '#pricing' },
    { name: 'Contact', href: '#contact' },
  ]

  return (
    <nav className="fixed top-0 w-full z-50 bg-background/80 backdrop-blur-md border-b border-border">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex justify-between h-16">
          {/* Logo */}
          <div className="flex items-center">
            <motion.div
              initial={{ opacity: 0, x: -20 }}
              animate={{ opacity: 1, x: 0 }}
              transition={{ duration: 0.5 }}
              className="flex items-center space-x-2"
            >
              <div className="w-8 h-8 bg-primary rounded-lg flex items-center justify-center">
                <span className="text-white font-bold text-lg">C</span>
              </div>
              <span className="text-xl font-bold gradient-text">Co-Sign</span>
            </motion.div>
          </div>

          {/* Desktop Navigation */}
          <div className="hidden md:flex items-center space-x-8">
            {navItems.map((item) => (
              <a
                key={item.name}
                href={item.href}
                className="text-foreground/80 hover:text-foreground transition-colors duration-200"
              >
                {item.name}
              </a>
            ))}
            <ThemeToggle />
            <div className="flex items-center space-x-3">
              <Button variant="ghost" asChild>
                <a href="https://app.co-sign.dev/sign-in">Sign In</a>
              </Button>
              <Button asChild>
                <a href="https://app.co-sign.dev/sign-up">Get Started</a>
              </Button>
            </div>
          </div>

          {/* Mobile menu button */}
          <div className="md:hidden flex items-center space-x-2">
            <ThemeToggle />
            <Button
              variant="ghost"
              size="icon"
              onClick={() => setIsOpen(!isOpen)}
            >
              {isOpen ? <X className="h-5 w-5" /> : <Menu className="h-5 w-5" />}
            </Button>
          </div>
        </div>

        {/* Mobile Navigation */}
        {isOpen && (
          <motion.div
            initial={{ opacity: 0, y: -10 }}
            animate={{ opacity: 1, y: 0 }}
            exit={{ opacity: 0, y: -10 }}
            className="md:hidden py-4 border-t border-border"
          >
            <div className="flex flex-col space-y-3">
              {navItems.map((item) => (
                <a
                  key={item.name}
                  href={item.href}
                  className="text-foreground/80 hover:text-foreground transition-colors duration-200 py-2"
                  onClick={() => setIsOpen(false)}
                >
                  {item.name}
                </a>
              ))}
              <div className="flex flex-col space-y-2 pt-4">
                <Button variant="ghost" asChild>
                  <a href="https://app.co-sign.dev/sign-in">Sign In</a>
                </Button>
                <Button asChild>
                  <a href="https://app.co-sign.dev/sign-up">Get Started</a>
                </Button>
              </div>
            </div>
          </motion.div>
        )}
      </div>
    </nav>
  )
}
```

### src/components/Hero.tsx
```typescript
import { motion } from 'framer-motion'
import { Play } from 'lucide-react'
import { Button } from '@/components/ui/button'

export default function Hero() {
  return (
    <section className="relative min-h-screen flex items-center justify-center overflow-hidden">
      {/* Background */}
      <div className="absolute inset-0 hero-gradient" />
      
      {/* Content */}
      <div className="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
        <motion.div
          initial={{ opacity: 0, y: 30 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.8 }}
          className="space-y-8"
        >
          {/* Badge */}
          <motion.div
            initial={{ opacity: 0, scale: 0.9 }}
            animate={{ opacity: 1, scale: 1 }}
            transition={{ duration: 0.6, delay: 0.2 }}
            className="inline-flex items-center gap-2 glass-card px-4 py-2"
          >
            <div className="w-2 h-2 bg-primary rounded-full animate-pulse" />
            <span className="text-sm font-medium text-muted-foreground">
              Revolutionary Sign Language Translation
            </span>
          </motion.div>

          {/* Heading */}
          <div className="space-y-4">
            <h1 className="text-4xl md:text-6xl lg:text-7xl font-bold">
              <span className="gradient-text">Break Communication</span>
              <br />
              <span className="text-foreground">Barriers with AI</span>
            </h1>
            <p className="text-xl md:text-2xl text-muted-foreground max-w-3xl mx-auto">
              Real-time sign language translation in video calls. 
              Connect with anyone, anywhere, in any language.
            </p>
          </div>

          {/* CTAs */}
          <motion.div
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.6, delay: 0.6 }}
            className="flex flex-col sm:flex-row gap-4 justify-center items-center"
          >
            <Button size="lg" asChild>
              <a href="https://app.co-sign.dev/sign-up">
                Start Free Trial
              </a>
            </Button>
            <Button variant="outline" size="lg" asChild>
              <a href="https://app.co-sign.dev/demo" className="flex items-center gap-2">
                <Play className="h-4 w-4" />
                Watch Demo
              </a>
            </Button>
          </motion.div>

          {/* Stats */}
          <motion.div
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.6, delay: 0.8 }}
            className="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-2xl mx-auto pt-16"
          >
            <div className="text-center">
              <div className="text-3xl font-bold gradient-text">99%</div>
              <div className="text-sm text-muted-foreground">Translation Accuracy</div>
            </div>
            <div className="text-center">
              <div className="text-3xl font-bold gradient-text">50ms</div>
              <div className="text-sm text-muted-foreground">Real-time Latency</div>
            </div>
            <div className="text-center">
              <div className="text-3xl font-bold gradient-text">24/7</div>
              <div className="text-sm text-muted-foreground">Available Support</div>
            </div>
          </motion.div>
        </motion.div>
      </div>
    </section>
  )
}
```

### src/components/Features.tsx
```typescript
import { motion } from 'framer-motion'
import { 
  Video, 
  MessageCircle, 
  Globe, 
  Shield, 
  Zap, 
  Users 
} from 'lucide-react'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card'

export default function Features() {
  const features = [
    {
      icon: MessageCircle,
      title: "Real-time Translation",
      description: "Instant sign language to text and speech translation with 99% accuracy using advanced AI.",
      color: "text-blue-500"
    },
    {
      icon: Video,
      title: "HD Video Quality",
      description: "Crystal clear 4K video calls optimized for sign language visibility and gesture recognition.",
      color: "text-green-500"
    },
    {
      icon: Globe,
      title: "Multi-language Support",
      description: "Support for ASL, BSL, and 50+ international sign languages with regional dialects.",
      color: "text-purple-500"
    },
    {
      icon: Shield,
      title: "Enterprise Security",
      description: "End-to-end encryption with HIPAA compliance for healthcare and education sectors.",
      color: "text-red-500"
    },
    {
      icon: Zap,
      title: "Lightning Fast",
      description: "Sub-50ms latency for real-time communication without delays or interruptions.",
      color: "text-yellow-500"
    },
    {
      icon: Users,
      title: "Team Collaboration",
      description: "Support up to 100 participants with breakout rooms and collaborative features.",
      color: "text-indigo-500"
    }
  ]

  return (
    <section id="features" className="py-24 px-4 sm:px-6 lg:px-8">
      <div className="max-w-7xl mx-auto">
        <motion.div
          initial={{ opacity: 0, y: 30 }}
          whileInView={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.8 }}
          viewport={{ once: true }}
          className="text-center mb-16"
        >
          <h2 className="text-3xl md:text-4xl font-bold mb-4">
            <span className="gradient-text">Powerful Features</span>
            <br />
            <span className="text-foreground">Built for Everyone</span>
          </h2>
          <p className="text-xl text-muted-foreground max-w-3xl mx-auto">
            Experience seamless communication with cutting-edge technology 
            designed to bridge language barriers.
          </p>
        </motion.div>

        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          {features.map((feature, index) => (
            <motion.div
              key={feature.title}
              initial={{ opacity: 0, y: 30 }}
              whileInView={{ opacity: 1, y: 0 }}
              transition={{ duration: 0.6, delay: index * 0.1 }}
              viewport={{ once: true }}
            >
              <Card className="h-full hover:shadow-lg transition-shadow duration-300">
                <CardHeader>
                  <div className={`w-12 h-12 rounded-lg bg-${feature.color.split('-')[1]}-100 dark:bg-${feature.color.split('-')[1]}-900/20 flex items-center justify-center mb-4`}>
                    <feature.icon className={`h-6 w-6 ${feature.color}`} />
                  </div>
                  <CardTitle className="text-xl">{feature.title}</CardTitle>
                </CardHeader>
                <CardContent>
                  <CardDescription className="text-base">
                    {feature.description}
                  </CardDescription>
                </CardContent>
              </Card>
            </motion.div>
          ))}
        </div>
      </div>
    </section>
  )
}
```

---

## 🔧 STEP 8: Update Main App.tsx

### src/App.tsx
```typescript
import { useEffect } from 'react'
import { ThemeProvider } from '@/components/theme-provider'
import Navbar from '@/components/Navbar'
import Hero from '@/components/Hero'
import Features from '@/components/Features'
import '@/design-tokens.css'
import Lenis from 'lenis'

function App() {
  useEffect(() => {
    const lenis = new Lenis({
      duration: 1.2,
      easing: (t: number) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
    })

    function raf(time: number) {
      lenis.raf(time)
      requestAnimationFrame(raf)
    }

    requestAnimationFrame(raf)

    return () => {
      lenis.destroy()
    }
  }, [])

  return (
    <ThemeProvider attribute="class" defaultTheme="system" enableSystem>
      <div className="min-h-screen bg-background text-foreground">
        <Navbar />
        <main>
          <Hero />
          <Features />
          {/* Add more sections as needed */}
        </main>
      </div>
    </ThemeProvider>
  )
}

export default App
```

---

## 🔧 STEP 9: Update main.tsx

### src/main.tsx
```typescript
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.tsx'

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

---

## 🎯 Key Improvements Over Current

### What We're Removing
- ❌ **Excessive Glow Effects**: Too flashy
- ❌ **Heavy 3D Elements**: Not matching main app
- ❌ **Over-animated Background**: Distracting
- ❌ **Complex Glass Morphism**: Simplified approach

### What We're Adding
- ✅ **Theme Toggle**: Light/dark mode
- ✅ **Clean Typography**: Better readability
- ✅ **shadcn/ui Components**: Consistent with modern apps
- ✅ **Responsive Design**: Perfect mobile experience
- ✅ **Performance**: Faster loading times

---

## 📱 Mobile-First Approach

### Breakpoints
```css
/* Mobile: 375px+ */
/* Tablet: 768px+ */  
/* Desktop: 1024px+ */
/* Large: 1280px+ */
```

### Mobile Optimizations
- **Navigation**: Hamburger menu
- **Hero**: Stacked layout
- **Features**: Single column grid
- **Pricing**: Stacked cards
- **Touch Targets**: 44px minimum

---

## 🚀 Performance Targets

### Core Web Vitals
- **LCP**: < 2.5s (Hero loads fast)
- **FID**: < 100ms (Interactive quickly)
- **CLS**: < 0.1 (No layout shifts)

### Bundle Size
- **Total JS**: < 200KB gzipped
- **CSS**: < 50KB gzipped
- **Images**: WebP format, optimized

---

## 🔗 Integration Points

### Main App Links
```tsx
// Navigation
<Link href="https://app.co-sign.dev/sign-in">Sign In</Link>
<Link href="https://app.co-sign.dev/sign-up">Get Started</Link>

// Demo Section
<Link href="https://app.co-sign.dev/demo">Try Demo</Link>

// Pricing CTAs
<Link href="https://app.co-sign.dev/sign-up?plan=free">Start Free</Link>
<Link href="https://app.co-sign.dev/sign-up?plan=pro">Start Pro</Link>
```

### Analytics Tracking
```tsx
// Track user interactions
const trackCTA = (action: string, plan?: string) => {
  // Analytics implementation
  gtag('event', 'click', {
    event_category: 'cta',
    event_label: action,
    value: plan
  });
};
```

---

## ✅ Success Metrics

### User Experience
- [ ] Theme switching works seamlessly
- [ ] Mobile experience is excellent
- [ ] Page loads under 3 seconds
- [ ] All CTA buttons lead to correct pages

### Design Consistency
- [ ] Matches main app's visual language
- [ ] Typography is consistent
- [ ] Color palette aligns
- [ ] Component styles match

### Technical
- [ ] Lighthouse score > 90
- [ ] No accessibility violations
- [ ] Cross-browser compatibility
- [ ] SEO optimized

---

## 🎉 Launch Checklist

### Pre-Launch
- [ ] All components implemented
- [ ] Theme switching tested
- [ ] Mobile responsive verified
- [ ] Performance optimized
- [ ] Analytics configured

### Launch
- [ ] Deploy to production
- [ ] DNS configured for co-sign.dev
- [ ] SSL certificate active
- [ ] CDN configured

### Post-Launch
- [ ] Monitor analytics
- [ ] Gather user feedback
- [ ] Performance monitoring
- [ ] A/B testing setup

---

**Next Steps**: Use the prompt below to implement this complete design system.

**Timeline**: 2-3 days for complete implementation
**Priority**: Clean, consistent design that matches the main app

---

# 🤖 IMPLEMENTATION PROMPT

Use this prompt in your other IDE to implement the Co-Sign landing page:

```
I need to completely redesign my Co-Sign landing page to match our main video calling app's clean aesthetic. 

CURRENT PROJECT: Bun + Vite + React + TypeScript setup

GOAL: Transform the existing landing page into a clean, modern design with:
- Light/Dark theme support with seamless switching
- shadcn/ui components for consistency
- Minimal glass effects (not overwhelming)
- Clean typography using Geist Sans/Inter
- Mobile-first responsive design
- Matches the main app's color scheme (#E8F4FD light, #1C1F2E dark, #0E78F9 primary)

TASKS:
1. Install dependencies: class-variance-authority, clsx, tailwind-merge, lucide-react, next-themes, @radix-ui/react-slot, tailwindcss, @tailwindcss/typography, autoprefixer, postcss

2. Replace the existing design-tokens.css with the new clean design system

3. Set up Tailwind config with shadcn/ui compatibility

4. Create utility functions and core UI components (Button, Card, ThemeToggle)

5. Build clean components:
   - Navbar with theme toggle and mobile menu
   - Hero section with subtle animations
   - Features section with 6 feature cards
   - Pricing section (Free, Pro $29/month, Enterprise)
   - Demo section linking to app.co-sign.dev/demo

6. Implement ThemeProvider for light/dark mode

7. Remove excessive glow effects and heavy 3D elements

8. Ensure all CTAs link to: app.co-sign.dev/sign-up and app.co-sign.dev/sign-in

9. Make it mobile-responsive and performance optimized

DESIGN REQUIREMENTS:
- Clean, minimal aesthetic matching the main app
- Professional look, not overly futuristic
- Readable typography with proper contrast
- Subtle hover effects and animations
- Glass morphism used sparingly
- Primary color: #0E78F9
- Light background: #E8F4FD
- Dark background: #1C1F2E

Please implement this step by step, starting with the configuration files, then the design system, then the components. Focus on creating a cohesive design that feels like part of the main Co-Sign application ecosystem.