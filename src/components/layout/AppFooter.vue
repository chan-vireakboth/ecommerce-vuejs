<script setup>
import { RouterLink } from 'vue-router'

const year = new Date().getFullYear()
</script>

<template>
  <footer class="border-t">
    <div
      class="text-muted-foreground mx-auto flex max-w-7xl flex-col items-center justify-between gap-4 px-4 py-8 text-sm sm:flex-row sm:px-6"
    >
      <p>© {{ year }} Ecommerce. All rights reserved.</p>
      <div class="flex gap-6">
        <RouterLink to="/about" class="hover:text-foreground">About</RouterLink>
        <RouterLink to="/contact" class="hover:text-foreground">Contact</RouterLink>
        <a href="#" class="hover:text-foreground">Privacy</a>
        <a href="#" class="hover:text-foreground">Terms</a>
      </div>
    </div>
  </footer>
</template>
