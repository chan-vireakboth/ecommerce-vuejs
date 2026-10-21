<script setup>
import { ShoppingCart, Star } from '@lucide/vue'
import { Badge } from '@/components/ui/badge'
import { Button } from '@/components/ui/button'
import { Card, CardContent, CardFooter } from '@/components/ui/card'

defineProps({
  product: { type: Object, required: true },
})
</script>

<template>
  <Card class="overflow-hidden pt-0 transition hover:shadow-md">
    <div class="bg-muted relative aspect-square">
      <img :src="product.image" :alt="product.name" loading="lazy" class="absolute inset-0 size-full object-cover" />
      <Badge v-if="product.badge" class="absolute top-3 left-3">{{ product.badge }}</Badge>
    </div>
    <CardContent class="space-y-1">
      <p class="text-muted-foreground text-xs">{{ product.category }}</p>
      <h3 class="font-medium">{{ product.name }}</h3>
      <div class="flex items-center gap-1 text-sm">
        <Star class="size-4 fill-amber-400 text-amber-400" />
        {{ product.rating }}
      </div>
    </CardContent>
    <CardFooter class="flex items-center justify-between">
      <div>
        <span class="text-lg font-semibold">${{ product.price }}</span>
        <span v-if="product.oldPrice" class="text-muted-foreground ml-2 text-sm line-through"
          >${{ product.oldPrice }}</span
        >
      </div>
      <Button size="icon" aria-label="Add to cart"><ShoppingCart /></Button>
    </CardFooter>
  </Card>
</template>
