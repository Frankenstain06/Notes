# Next.js Learning Notes

## React vs Next.js

> **Analogy:** মুড়িমাখা দোকানের মতো ভাবো

### React (CSR - Client Side Rendering)
- **খালি কাগজ আগে দেয়**, তারপর সামনে সামনে মাখে
- প্রথমে খালি HTML → JS ডাউনলোড → API fetch → UI render
- **ফলাফল:** ধীর first load, loading screen দেখা যায়

### Next.js (SSR - Server Side Rendering)
- **আগেই পুরো মুড়িমাখা রেডি** করে রাখে
- Server-এ data fetch → পূর্ণ HTML তৈরি → ব্রাউজারে পাঠায়
- **ফলাফল:** দ্রুত load, প্রায় কোনো loading নেই

| বিষয় | React | Next.js |
|------|-------|---------|
| HTML | খালি আসে | data সহ আসে |
| Data fetch | ব্রাউজারে | সার্ভারে |
| First load | ধীর | দ্রুত |
| SEO | খারাপ | অনেক ভালো |
| Routing | Manual (react-router) | Built-in |

> **Hydration:** HTML আসার পর JS ডাউনলোড হয়ে page interactive হয়

---

## Core Concepts

### Server & Client
| Term | মানে |
|------|------|
| **Server** | Request নেয়, response দেয় (রান্নাঘর) |
| **Client** | Request পাঠায় (Browser/App) |

### Localhost & Port
- **Localhost** = নিজের কম্পিউটারই server (`localhost:3000`)
- **Port** = একই PC-তে আলাদা server চেনার নম্বর

| Address | কাজ |
|---------|-----|
| `localhost:3000` | Frontend |
| `localhost:8000` | Backend |
| `localhost:5432` | Database |

---

## File-Based Routing

> **Analogy:** ফোল্ডার = রাস্তা, ফাইল = গন্তব্য

Next.js এ **folder structure** দিয়েই URL তৈরি হয়। কোনো Router config লাগে না!

### Basic Routing

```
app/
├── page.tsx          → yoursite.com/
├── about/
│   └── page.tsx      → yoursite.com/about
├── blog/
│   └── page.tsx      → yoursite.com/blog
└── contact/
    └── page.tsx      → yoursite.com/contact
```

| Folder Structure | URL |
|-----------------|-----|
| `app/page.tsx` | `/` (homepage) |
| `app/about/page.tsx` | `/about` |
| `app/blog/page.tsx` | `/blog` |

### Dynamic Routes (বদলে যায় এমন URL)

> **Analogy:** Hotel room number এর মতো - ঘর একই structure, নম্বর আলাদা

```
app/
└── blog/
    └── [slug]/
        └── page.tsx   → /blog/hello-world, /blog/my-post
```

**[slug]** = যেকোনো value হতে পারে

```tsx
// app/blog/[slug]/page.tsx
export default function BlogPost({ params }: { params: { slug: string } }) {
  return <h1>Post: {params.slug}</h1>
}
```

| URL | params.slug |
|-----|-------------|
| `/blog/hello` | `"hello"` |
| `/blog/my-first-post` | `"my-first-post"` |

### Nested Dynamic Routes

```
app/
└── shop/
    └── [category]/
        └── [productId]/
            └── page.tsx   → /shop/shoes/123
```

```tsx
// params = { category: "shoes", productId: "123" }
```

### Catch-All Routes (সব ধরো!)

```
app/
└── docs/
    └── [...slug]/
        └── page.tsx   → /docs/a/b/c/d
```

| URL | params.slug |
|-----|-------------|
| `/docs/intro` | `["intro"]` |
| `/docs/guide/install` | `["guide", "install"]` |

---

## Special Files

> Next.js এ কিছু **magic filename** আছে যেগুলো automatic কাজ করে

| File | কাজ |
|------|-----|
| `page.tsx` | Route এর main content |
| `layout.tsx` | Shared wrapper (navbar, footer) |
| `loading.tsx` | Loading state UI |
| `error.tsx` | Error handling UI |
| `not-found.tsx` | 404 page |
| `template.tsx` | Layout এর মতো, but re-renders |

### layout.tsx (গুরুত্বপূর্ণ!)

> **Analogy:** বাড়ির দেয়াল - ভিতরের জিনিস বদলালেও দেয়াল একই থাকে

```tsx
// app/layout.tsx - Root Layout
export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>
        <nav>Navigation Bar</nav>
        {children}  {/* এখানে page content আসে */}
        <footer>Footer</footer>
      </body>
    </html>
  )
}
```

**Nested Layouts:**
```
app/
├── layout.tsx           → সবার জন্য (navbar)
└── dashboard/
    ├── layout.tsx       → শুধু dashboard এর জন্য (sidebar)
    └── page.tsx
```

### loading.tsx

```tsx
// app/dashboard/loading.tsx
export default function Loading() {
  return <div>Loading...</div>
}
```

Page load হওয়ার সময় **automatic** এই UI দেখাবে!

### error.tsx

```tsx
// app/dashboard/error.tsx
'use client' // Error component must be client

export default function Error({ error, reset }: { 
  error: Error; 
  reset: () => void 
}) {
  return (
    <div>
      <h2>কিছু ভুল হয়েছে!</h2>
      <button onClick={() => reset()}>আবার চেষ্টা করো</button>
    </div>
  )
}
```

---

## Server vs Client Components

> **সবচেয়ে গুরুত্বপূর্ণ concept!**

### Server Components (Default)

> **Analogy:** রেস্টুরেন্টের রান্নাঘর - Customer দেখে না, শুধু result পায়

```tsx
// এটা Server Component (default)
async function ProductList() {
  const products = await fetch('https://api.com/products')
  return <div>{/* render products */}</div>
}
```

**সুবিধা:**
- Database সরাসরি access করা যায়
- API keys নিরাপদ থাকে
- JS bundle ছোট হয়
- SEO ভালো হয়

**সীমাবদ্ধতা:**
- useState, useEffect ব্যবহার করা যায় না
- onClick, onChange ব্যবহার করা যায় না
- Browser APIs (localStorage) ব্যবহার করা যায় না

### Client Components

> **Analogy:** Customer এর সামনে তৈরি - Interactive!

```tsx
'use client' // এই line দিলেই Client Component

import { useState } from 'react'

export default function Counter() {
  const [count, setCount] = useState(0)
  
  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  )
}
```

**কখন Client Component লাগে:**
- useState, useEffect দরকার
- Event handlers (onClick, onChange)
- Browser APIs (localStorage, window)
- Custom hooks যেগুলো state ব্যবহার করে

### কোনটা কখন ব্যবহার করবো?

| কাজ | Component Type |
|-----|---------------|
| Data fetching | Server |
| Database access | Server |
| API keys ব্যবহার | Server |
| Static content | Server |
| Form interaction | Client |
| Button clicks | Client |
| useState/useEffect | Client |
| Animations | Client |

### Best Practice: Mix করো!

```tsx
// app/products/page.tsx (Server Component)
import AddToCart from './AddToCart'

async function ProductPage() {
  const product = await getProduct() // Server এ fetch
  
  return (
    <div>
      <h1>{product.name}</h1>
      <p>{product.description}</p>
      <AddToCart productId={product.id} /> {/* Client Component */}
    </div>
  )
}
```

```tsx
// app/products/AddToCart.tsx (Client Component)
'use client'

export default function AddToCart({ productId }: { productId: string }) {
  const handleClick = () => {
    // cart এ add করো
  }
  
  return <button onClick={handleClick}>Add to Cart</button>
}
```

---

## Data Fetching

### Server Component এ Fetch (সবচেয়ে সহজ!)

```tsx
// app/users/page.tsx
async function UsersPage() {
  const res = await fetch('https://api.com/users')
  const users = await res.json()
  
  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  )
}
```

### Caching Options

```tsx
// Default: Cached forever (Static)
fetch('https://api.com/data')

// Never cache (Always fresh)
fetch('https://api.com/data', { cache: 'no-store' })

// Revalidate every 60 seconds
fetch('https://api.com/data', { next: { revalidate: 60 } })
```

| Option | বাংলায় | Use Case |
|--------|--------|----------|
| `cache: 'force-cache'` | Save করে রাখো | Blog posts, static data |
| `cache: 'no-store'` | প্রতিবার নতুন আনো | Real-time data, dashboard |
| `revalidate: 60` | ৬০ সেকেন্ড পর refresh | News, price updates |

### Direct Database Access

```tsx
// app/products/page.tsx
import { db } from '@/lib/db'

async function ProductsPage() {
  const products = await db.product.findMany() // Prisma example
  
  return <ProductList products={products} />
}
```

> **সুবিধা:** কোনো API বানাতে হবে না! সরাসরি DB থেকে নাও

---

## API Routes (Route Handlers)

> **Analogy:** নিজের backend বানাও Next.js এর ভিতরেই!

### Basic API Route

```tsx
// app/api/users/route.ts
import { NextResponse } from 'next/server'

export async function GET() {
  const users = [{ id: 1, name: 'Fahim' }]
  return NextResponse.json(users)
}

export async function POST(request: Request) {
  const body = await request.json()
  // save to database
  return NextResponse.json({ message: 'User created!' }, { status: 201 })
}
```

| HTTP Method | Function | কাজ |
|-------------|----------|-----|
| GET | `GET()` | Data নেওয়া |
| POST | `POST()` | Data তৈরি |
| PUT | `PUT()` | Data update |
| DELETE | `DELETE()` | Data মুছা |

### Dynamic API Route

```tsx
// app/api/users/[id]/route.ts
export async function GET(
  request: Request, 
  { params }: { params: { id: string } }
) {
  const user = await getUserById(params.id)
  return NextResponse.json(user)
}
```

---

## Navigation

### Link Component (Best!)

```tsx
import Link from 'next/link'

export default function Navbar() {
  return (
    <nav>
      <Link href="/">Home</Link>
      <Link href="/about">About</Link>
      <Link href="/blog/hello-world">Blog Post</Link>
    </nav>
  )
}
```

> **সুবিধা:** Page reload হয় না, Super fast!

### useRouter (Programmatic Navigation)

```tsx
'use client'
import { useRouter } from 'next/navigation'

export default function LoginButton() {
  const router = useRouter()
  
  const handleLogin = async () => {
    await login()
    router.push('/dashboard')  // Navigate করো
    // router.replace('/dashboard')  // History তে রাখবে না
    // router.back()  // পেছনে যাও
    // router.refresh()  // Page refresh
  }
  
  return <button onClick={handleLogin}>Login</button>
}
```

### usePathname & useSearchParams

```tsx
'use client'
import { usePathname, useSearchParams } from 'next/navigation'

export default function CurrentPath() {
  const pathname = usePathname()        // "/blog/hello"
  const searchParams = useSearchParams() // "?sort=asc"
  
  const sort = searchParams.get('sort')  // "asc"
  
  return <p>Current path: {pathname}</p>
}
```

---

## Metadata & SEO

### Static Metadata

```tsx
// app/page.tsx
import { Metadata } from 'next'

export const metadata: Metadata = {
  title: 'My Website',
  description: 'Welcome to my awesome website',
  keywords: ['next.js', 'react', 'web development'],
  openGraph: {
    title: 'My Website',
    description: 'Welcome!',
    images: ['/og-image.jpg'],
  },
}

export default function Home() {
  return <h1>Home</h1>
}
```

### Dynamic Metadata

```tsx
// app/blog/[slug]/page.tsx
export async function generateMetadata({ params }: { params: { slug: string } }) {
  const post = await getPost(params.slug)
  
  return {
    title: post.title,
    description: post.excerpt,
  }
}
```

---

## Image Optimization

```tsx
import Image from 'next/image'

export default function Avatar() {
  return (
    <Image
      src="/profile.jpg"      // public folder থেকে
      alt="Profile picture"
      width={200}
      height={200}
      priority              // গুরুত্বপূর্ণ image দ্রুত load
    />
  )
}
```

**সুবিধা:**
- Automatic lazy loading
- WebP format এ convert
- Responsive sizes
- Blur placeholder

### External Images

```tsx
// next.config.ts
const nextConfig = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'example.com',
      },
    ],
  },
}
```

---

## Environment Variables

### Files

| File | কাজ |
|------|-----|
| `.env.local` | Local development (Git ignore করো!) |
| `.env` | All environments |
| `.env.production` | শুধু production |

### Usage

```bash
# .env.local
DATABASE_URL="postgresql://..."
NEXT_PUBLIC_API_URL="https://api.com"  # Browser এ ব্যবহার করতে চাইলে
```

```tsx
// Server Component / API Route
const dbUrl = process.env.DATABASE_URL  // কাজ করবে

// Client Component
const apiUrl = process.env.NEXT_PUBLIC_API_URL  // NEXT_PUBLIC_ লাগবে
```

> **সাবধান:** `NEXT_PUBLIC_` ছাড়া variable browser এ যাবে না!

---

## Static vs Dynamic Rendering

### Static (Build time এ তৈরি)

> **Analogy:** রেডিমেড জামা - আগেই বানানো

```tsx
// এটা automatically static
async function BlogPage() {
  const posts = await fetch('https://api.com/posts', {
    cache: 'force-cache'  // বা কিছু না দিলেও static
  })
  return <PostList posts={posts} />
}
```

**কখন Static:**
- `fetch()` with default caching
- কোনো dynamic function নেই

### Dynamic (Request time এ তৈরি)

> **Analogy:** Order দিলে তৈরি - Fresh!

```tsx
async function DashboardPage() {
  const data = await fetch('https://api.com/data', {
    cache: 'no-store'  // প্রতিবার fresh data
  })
  return <Dashboard data={data} />
}
```

**কখন Dynamic হয়:**
- `cache: 'no-store'`
- `cookies()` বা `headers()` ব্যবহার করলে
- `searchParams` ব্যবহার করলে

| Feature | Static | Dynamic |
|---------|--------|---------|
| Speed | অনেক দ্রুত | তুলনামূলক ধীর |
| Data | পুরনো হতে পারে | সবসময় fresh |
| Use case | Blog, docs | Dashboard, real-time |

---

## Server Actions

> **New feature!** Form submit সরাসরি server function এ!

```tsx
// app/actions.ts
'use server'

export async function createPost(formData: FormData) {
  const title = formData.get('title')
  const content = formData.get('content')
  
  await db.post.create({ data: { title, content } })
  
  revalidatePath('/posts')  // Cache refresh
}
```

```tsx
// app/posts/new/page.tsx
import { createPost } from '../actions'

export default function NewPost() {
  return (
    <form action={createPost}>
      <input name="title" placeholder="Title" />
      <textarea name="content" placeholder="Content" />
      <button type="submit">Create Post</button>
    </form>
  )
}
```

> **সুবিধা:** API route বানাতে হবে না! সরাসরি function call!

---

## Middleware

> **Analogy:** দারোয়ান - প্রতিটা request check করে

```tsx
// middleware.ts (root folder এ রাখো)
import { NextResponse } from 'next/server'
import type { NextRequest } from 'next/server'

export function middleware(request: NextRequest) {
  // Check if user is logged in
  const token = request.cookies.get('token')
  
  if (!token && request.nextUrl.pathname.startsWith('/dashboard')) {
    return NextResponse.redirect(new URL('/login', request.url))
  }
  
  return NextResponse.next()
}

export const config = {
  matcher: ['/dashboard/:path*', '/admin/:path*']
}
```

**Use Cases:**
- Authentication check
- Language redirect
- Logging
- Rate limiting

---

## Parallel & Intercepting Routes

### Parallel Routes (একসাথে multiple pages)

```
app/
└── dashboard/
    ├── @analytics/
    │   └── page.tsx
    ├── @team/
    │   └── page.tsx
    ├── layout.tsx
    └── page.tsx
```

```tsx
// app/dashboard/layout.tsx
export default function Layout({
  children,
  analytics,
  team,
}: {
  children: React.ReactNode
  analytics: React.ReactNode
  team: React.ReactNode
}) {
  return (
    <div>
      {children}
      <div className="grid grid-cols-2">
        {analytics}
        {team}
      </div>
    </div>
  )
}
```

### Intercepting Routes (Modal!)

```
app/
├── @modal/
│   └── (.)photo/[id]/
│       └── page.tsx     → Modal এ দেখাবে
└── photo/[id]/
    └── page.tsx          → Full page
```

> **Example:** Instagram এর মতো - feed এ click করলে modal, direct URL এ গেলে full page

---

## Useful Hooks & Functions

| Hook/Function | কাজ | Component |
|--------------|-----|-----------|
| `useRouter()` | Navigation | Client |
| `usePathname()` | Current path | Client |
| `useSearchParams()` | Query params | Client |
| `useParams()` | Dynamic params | Client |
| `redirect()` | Redirect user | Server |
| `notFound()` | 404 trigger | Server |
| `cookies()` | Read/write cookies | Server |
| `headers()` | Read headers | Server |

---

## Project Structure (Recommended)

```
my-next-app/
├── app/
│   ├── (auth)/              # Route group (URL এ আসবে না)
│   │   ├── login/
│   │   └── register/
│   ├── (main)/
│   │   ├── dashboard/
│   │   └── profile/
│   ├── api/
│   │   └── users/
│   ├── globals.css
│   ├── layout.tsx
│   └── page.tsx
├── components/
│   ├── ui/                  # Reusable UI components
│   └── forms/               # Form components
├── lib/
│   ├── db.ts               # Database connection
│   └── utils.ts            # Helper functions
├── hooks/                   # Custom hooks
├── types/                   # TypeScript types
├── public/                  # Static files
└── middleware.ts
```

### Route Groups `(folder)`

```
app/
├── (marketing)/        # URL: /about, /contact
│   ├── about/
│   └── contact/
└── (shop)/             # URL: /products, /cart
    ├── products/
    └── cart/
```

> **Note:** `()` দিয়ে folder name URL এ আসে না, শুধু organize করার জন্য

---

## Common Patterns

### Protected Route Pattern

```tsx
// app/dashboard/layout.tsx
import { redirect } from 'next/navigation'
import { getUser } from '@/lib/auth'

export default async function DashboardLayout({
  children,
}: {
  children: React.ReactNode
}) {
  const user = await getUser()
  
  if (!user) {
    redirect('/login')
  }
  
  return <>{children}</>
}
```

### Loading Data Pattern

```tsx
// app/products/page.tsx
import { Suspense } from 'react'
import ProductList from './ProductList'
import ProductSkeleton from './ProductSkeleton'

export default function ProductsPage() {
  return (
    <Suspense fallback={<ProductSkeleton />}>
      <ProductList />
    </Suspense>
  )
}
```

---

## Deploy

**Deploy = App কে ইন্টারনেটে চালু করা যাতে সবাই access করতে পারে**

| Local | Deployed |
|-------|----------|
| শুধু তুমি দেখো | সবাই দেখতে পারে |
| Testing এর জন্য | ২৪/৭ অন থাকে |

### Deploy Platforms

| Type | Platforms |
|------|-----------|
| **Frontend** | Vercel, Netlify, Firebase |
| **Backend** | Render, Railway, Fly.io |
| **Database** | Supabase, Neon, Railway |

### Vercel Deploy (সবচেয়ে সহজ!)

```bash
# 1. Install Vercel CLI
npm i -g vercel

# 2. Login
vercel login

# 3. Deploy
vercel
```

অথবা GitHub repo connect করো Vercel dashboard এ - automatic deploy হবে!

---

## Quick Commands

```bash
# Create new project
npx create-next-app@latest my-app

# Development server
npm run dev

# Production build
npm run build

# Start production server
npm start

# Lint check
npm run lint
```

---

## Summary Cheatsheet

| Concept | মনে রাখো |
|---------|---------|
| Routing | Folder = URL path |
| `page.tsx` | Route এর content |
| `layout.tsx` | Shared wrapper |
| Server Component | Default, data fetch এখানে |
| Client Component | `'use client'` দিয়ে শুরু |
| `loading.tsx` | Auto loading UI |
| `error.tsx` | Auto error handling |
| Dynamic route | `[param]` folder |
| API route | `app/api/` folder এ |
| Metadata | SEO এর জন্য |
| Image | `next/image` ব্যবহার করো |
| Link | `next/link` ব্যবহার করো |

---

> **Happy Coding!** Next.js শিখে ফেলো, দুনিয়া জয় করো!



