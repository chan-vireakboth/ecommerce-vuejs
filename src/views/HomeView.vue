<script setup>
import { RouterLink } from 'vue-router'
import { ArrowRight, Headphones, RotateCcw, ShieldCheck, Truck } from '@lucide/vue'
import { Badge } from '@/components/ui/badge'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import ProductCard from '@/components/ProductCard.vue'
import { categories, categoryImages, heroImages, products } from '@/data/products'

const featured = products.slice(0, 4)

const perks = [
  { icon: Truck, title: 'Free shipping', text: 'On orders over $50' },
  { icon: RotateCcw, title: '30-day returns', text: 'No questions asked' },
  { icon: ShieldCheck, title: 'Secure payment', text: 'Encrypted checkout' },
  { icon: Headphones, title: '24/7 support', text: 'We are here to help' },
]
</script>

<template>
  <!-- Hero -->
  <section class="from-muted/60 bg-gradient-to-b to-transparent">
    <div
      class="mx-auto grid max-w-7xl items-center gap-10 px-4 py-16 sm:px-6 lg:grid-cols-2 lg:py-24"
    >
      <div class="space-y-6">
        <Badge variant="secondary">New season collection</Badge>
        <h1 class="text-4xl font-bold tracking-tight sm:text-5xl">
          Everything you love, delivered to your door.
        </h1>
        <p class="text-muted-foreground max-w-lg text-lg">
          Shop thousands of products from trusted brands and local sellers, with fast delivery and
          easy returns.
        </p>
        <div class="flex flex-wrap gap-3">
          <Button size="lg" as-child>
            <RouterLink to="/products">Shop now <ArrowRight /></RouterLink>
          </Button>
          <Button size="lg" variant="outline" as-child>
            <RouterLink to="/business">Browse shops</RouterLink>
          </Button>
        </div>
      </div>
      <div class="grid grid-cols-2 gap-4">
        <img
          v-for="(src, i) in heroImages"
          :key="src"
          :src="src"
          alt=""
          :class="['aspect-[4/5] w-full rounded-2xl object-cover', i === 1 && 'mt-10']"
        />
      </div>
    </div>
  </section>

  <!-- Perks -->
  <section class="mx-auto max-w-7xl px-4 sm:px-6">
    <div class="grid grid-cols-2 gap-6 rounded-2xl border p-6 lg:grid-cols-4">
      <div v-for="perk in perks" :key="perk.title" class="flex items-center gap-3">
        <component :is="perk.icon" class="text-primary size-6 shrink-0" />
        <div>
          <p class="text-sm font-medium">{{ perk.title }}</p>
          <p class="text-muted-foreground text-xs">{{ perk.text }}</p>
        </div>
      </div>
    </div>
  </section>

  <!-- Categories -->
  <section class="mx-auto max-w-7xl px-4 py-16 sm:px-6">
    <h2 class="mb-6 text-2xl font-semibold">Shop by category</h2>
    <div class="grid grid-cols-2 gap-4 sm:grid-cols-3 lg:grid-cols-5">
      <RouterLink
        v-for="category in categories.slice(1)"
        :key="category"
        :to="{ path: '/products', query: { category } }"
        class="group relative aspect-[4/3] overflow-hidden rounded-xl"
      >
        <img
          :src="categoryImages[category]"
          :alt="category"
          loading="lazy"
          class="size-full object-cover transition duration-300 group-hover:scale-105"
        />
        <span
          class="absolute inset-0 flex items-end bg-gradient-to-t from-black/60 to-transparent p-4 font-medium text-white"
        >
          {{ category }}
        </span>
      </RouterLink>
    </div>
  </section>

  <!-- Featured -->
  <section class="mx-auto max-w-7xl px-4 pb-16 sm:px-6">
    <div class="mb-6 flex items-end justify-between">
      <h2 class="text-2xl font-semibold">Featured products</h2>
      <RouterLink to="/products" class="text-sm font-medium hover:underline">View all</RouterLink>
    </div>
    <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-4">
      <ProductCard v-for="product in featured" :key="product.id" :product="product" />
    </div>
  </section>

  <!-- Newsletter -->
  <section class="mx-auto max-w-7xl px-4 pb-20 sm:px-6">
    <div class="bg-primary text-primary-foreground rounded-2xl px-6 py-12 text-center">
      <h2 class="text-2xl font-semibold">Get 10% off your first order</h2>
      <p class="mt-2 opacity-80">Subscribe for deals, new arrivals and exclusive offers.</p>
      <form class="mx-auto mt-6 flex max-w-md gap-2" @submit.prevent>
        <Input type="email" placeholder="you@example.com" class="bg-background text-foreground" />
        <Button variant="secondary" type="submit">Subscribe</Button>
      </form>
    </div>
  </section>
</template>
