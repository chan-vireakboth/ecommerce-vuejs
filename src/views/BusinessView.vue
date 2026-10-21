<script setup>
import { computed, ref } from 'vue'
import { BadgeCheck, MapPin, Package, Search, Star } from '@lucide/vue'
import { Avatar, AvatarFallback } from '@/components/ui/avatar'
import { Badge } from '@/components/ui/badge'
import { Button } from '@/components/ui/button'
import { Card, CardContent, CardFooter } from '@/components/ui/card'
import { Input } from '@/components/ui/input'
import { categories, shops } from '@/data/products'

const search = ref('')
const category = ref('All')
const sort = ref('rating')

const filtered = computed(() => {
  const term = search.value.trim().toLowerCase()
  const list = shops.filter(
    (s) =>
      (category.value === 'All' || s.category === category.value) &&
      (s.name.toLowerCase().includes(term) || s.location.toLowerCase().includes(term)),
  )
  if (sort.value === 'rating') return [...list].sort((a, b) => b.rating - a.rating)
  if (sort.value === 'products') return [...list].sort((a, b) => b.products - a.products)
  if (sort.value === 'name') return [...list].sort((a, b) => a.name.localeCompare(b.name))
  return list
})

const initials = (name) =>
  name
    .split(' ')
    .map((n) => n[0])
    .join('')
    .slice(0, 2)
</script>

<template>
  <div class="mx-auto max-w-7xl px-4 py-12 sm:px-6">
    <div class="mb-8">
      <h1 class="text-3xl font-bold tracking-tight">Shops</h1>
      <p class="text-muted-foreground mt-1">Discover businesses and shops selling on Ecommerce.</p>
    </div>

    <div class="mb-8 flex flex-col gap-4 lg:flex-row lg:items-center lg:justify-between">
      <div class="flex flex-wrap gap-2">
        <Button
          v-for="c in categories"
          :key="c"
          size="sm"
          :variant="category === c ? 'default' : 'outline'"
          @click="category = c"
        >
          {{ c }}
        </Button>
      </div>
      <div class="flex gap-2">
        <div class="relative">
          <Search class="text-muted-foreground absolute top-1/2 left-3 size-4 -translate-y-1/2" />
          <Input v-model="search" placeholder="Search shop or city" class="w-56 pl-9" />
        </div>
        <select
          v-model="sort"
          class="border-input bg-background h-9 rounded-md border px-3 text-sm"
          aria-label="Sort by"
        >
          <option value="rating">Top rated</option>
          <option value="products">Most products</option>
          <option value="name">Name A–Z</option>
        </select>
      </div>
    </div>

    <div v-if="filtered.length" class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-4">
      <Card
        v-for="shop in filtered"
        :key="shop.id"
        class="overflow-hidden pt-0 transition hover:shadow-md"
      >
        <div class="bg-muted relative aspect-[16/10]">
          <img :src="shop.cover" :alt="shop.name" loading="lazy" class="absolute inset-0 size-full object-cover" />
          <Badge variant="secondary" class="absolute top-3 left-3">{{ shop.category }}</Badge>
        </div>
        <CardContent class="relative space-y-2">
          <Avatar class="border-background -mt-10 size-12 border-4">
            <AvatarFallback class="bg-primary text-primary-foreground text-sm font-semibold">
              {{ initials(shop.name) }}
            </AvatarFallback>
          </Avatar>
          <h3 class="flex items-center gap-1 font-semibold">
            {{ shop.name }}
            <BadgeCheck v-if="shop.verified" class="size-4 text-sky-500" aria-label="Verified" />
          </h3>
          <div class="text-muted-foreground space-y-1 text-sm">
            <p class="flex items-center gap-1.5"><MapPin class="size-4" /> {{ shop.location }}</p>
            <p class="flex items-center gap-1.5">
              <Package class="size-4" /> {{ shop.products }} products
            </p>
            <p class="flex items-center gap-1.5">
              <Star class="size-4 fill-amber-400 text-amber-400" />
              <span class="text-foreground font-medium">{{ shop.rating }}</span>
              ({{ shop.reviews.toLocaleString() }} reviews)
            </p>
          </div>
        </CardContent>
        <CardFooter class="gap-2">
          <Button class="flex-1">Visit shop</Button>
          <Button variant="outline">Follow</Button>
        </CardFooter>
      </Card>
    </div>
    <p v-else class="text-muted-foreground py-20 text-center">No shops match your search.</p>
  </div>
</template>
