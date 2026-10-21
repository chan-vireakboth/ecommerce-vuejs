<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import { LogOut, Menu, Package, ShoppingBag, User, X } from '@lucide/vue'
import { Avatar, AvatarFallback, AvatarImage } from '@/components/ui/avatar'
import { Button } from '@/components/ui/button'
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from '@/components/ui/dropdown-menu'

// TODO: replace with your own auth state (e.g. a Pinia store or composable).
const isAuthenticated = ref(false)
const user = ref({
  name: 'Sokha Chan',
  email: 'sokha@example.com',
  avatar: 'https://randomuser.me/api/portraits/women/65.jpg',
})

const menu = [
  { label: 'Products', to: '/products' },
  { label: 'Business', to: '/business' },
  { label: 'About Us', to: '/about' },
  { label: 'Contact Us', to: '/contact' },
]

const mobileOpen = ref(false)

function login() {
  // TODO: hook up your login flow.
}

function logout() {
  // TODO: hook up your logout flow.
}
</script>

<template>
  <header class="bg-background/80 sticky top-0 z-40 border-b backdrop-blur">
    <nav class="mx-auto flex h-16 max-w-7xl items-center gap-6 px-4 sm:px-6">
      <RouterLink to="/" class="flex items-center gap-2 text-lg font-semibold">
        <span class="bg-primary text-primary-foreground grid size-8 place-items-center rounded-lg">
          <ShoppingBag class="size-4" />
        </span>
        Ecommerce
      </RouterLink>

      <ul class="hidden items-center gap-1 md:flex">
        <li v-for="item in menu" :key="item.to">
          <RouterLink
            :to="item.to"
            class="text-muted-foreground hover:text-foreground rounded-md px-3 py-2 text-sm font-medium transition"
            active-class="!text-foreground"
          >
            {{ item.label }}
          </RouterLink>
        </li>
      </ul>

      <div class="ml-auto flex items-center gap-2">
        <DropdownMenu v-if="isAuthenticated">
          <DropdownMenuTrigger as-child>
            <button class="rounded-full" aria-label="Account menu">
              <Avatar>
                <AvatarImage v-if="user.avatar" :src="user.avatar" :alt="user.name" />
                <AvatarFallback>{{ user.name.slice(0, 2).toUpperCase() }}</AvatarFallback>
              </Avatar>
            </button>
          </DropdownMenuTrigger>
          <DropdownMenuContent align="end" class="w-56">
            <DropdownMenuLabel>
              <p class="font-medium">{{ user.name }}</p>
              <p class="text-muted-foreground text-xs font-normal">{{ user.email }}</p>
            </DropdownMenuLabel>
            <DropdownMenuSeparator />
            <DropdownMenuItem as-child>
              <RouterLink to="/profile"><User /> Profile</RouterLink>
            </DropdownMenuItem>
            <DropdownMenuItem as-child>
              <RouterLink to="/profile"><Package /> My orders</RouterLink>
            </DropdownMenuItem>
            <DropdownMenuSeparator />
            <DropdownMenuItem @click="logout"><LogOut /> Log out</DropdownMenuItem>
          </DropdownMenuContent>
        </DropdownMenu>
        <Button v-else @click="login">Log in</Button>

        <Button
          variant="ghost"
          size="icon"
          class="md:hidden"
          :aria-label="mobileOpen ? 'Close menu' : 'Open menu'"
          @click="mobileOpen = !mobileOpen"
        >
          <X v-if="mobileOpen" /><Menu v-else />
        </Button>
      </div>
    </nav>

    <ul v-if="mobileOpen" class="border-t px-4 py-2 md:hidden">
      <li v-for="item in menu" :key="item.to">
        <RouterLink
          :to="item.to"
          class="block rounded-md px-3 py-2 text-sm font-medium"
          active-class="bg-muted"
          @click="mobileOpen = false"
        >
          {{ item.label }}
        </RouterLink>
      </li>
    </ul>
  </header>
</template>
