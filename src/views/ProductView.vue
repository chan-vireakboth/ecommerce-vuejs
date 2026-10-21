<script setup>
import { computed, ref, watch } from 'vue'
import { useRoute } from 'vue-router'
import { Search } from '@lucide/vue'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import ProductCard from '@/components/ProductCard.vue'
import { categories, products } from '@/data/products'

const route = useRoute()
const search = ref('')
const category = ref(route.query.category || 'All')
const sort = ref('featured')

watch(
  () => route.query.category,
  (value) => (category.value = value || 'All'),
)

const filtered = computed(() => {
  const term = search.value.trim().toLowerCase()
  const list = products.filter(
    (p) =>
      (category.value === 'All' || p.category === category.value) &&
      p.name.toLowerCase().includes(term),
  )
  if (sort.value === 'price-asc') return [...list].sort((a, b) => a.price - b.price)
  if (sort.value === 'price-desc') return [...list].sort((a, b) => b.price - a.price)
  if (sort.value === 'rating') return [...list].sort((a, b) => b.rating - a.rating)
  return list
})
</script>

<template>
  <div class="mx-auto max-w-7xl px-4 py-12 sm:px-6">
    <div class="mb-8">
      <h1 class="text-3xl font-bold tracking-tight">Products</h1>
      <p class="text-muted-foreground mt-1">Browse our full catalog.</p>
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
          <Input v-model="search" placeholder="Search products" class="w-56 pl-9" />
        </div>
        <select
          v-model="sort"
          class="border-input bg-background h-9 rounded-md border px-3 text-sm"
          aria-label="Sort by"
        >
          <option value="featured">Featured</option>
          <option value="price-asc">Price: low to high</option>
          <option value="price-desc">Price: high to low</option>
          <option value="rating">Top rated</option>
        </select>
      </div>
    </div>

    <div v-if="filtered.length" class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-4">
      <ProductCard v-for="product in filtered" :key="product.id" :product="product" />
    </div>
    <p v-else class="text-muted-foreground py-20 text-center">No products match your search.</p>
  </div>
</template>
