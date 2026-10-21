<script setup>
import { HeartHandshake, Leaf, Sparkles } from '@lucide/vue'
import { Avatar, AvatarFallback, AvatarImage } from '@/components/ui/avatar'

const values = [
  {
    icon: HeartHandshake,
    title: 'Customer first',
    text: 'Every decision starts with what is best for our shoppers.',
  },
  {
    icon: Sparkles,
    title: 'Quality matters',
    text: 'We work only with sellers who meet our standards.',
  },
  { icon: Leaf, title: 'Sustainable', text: 'Plastic-free packaging and carbon-neutral delivery.' },
]

const team = [
  {
    name: 'Dara Kim',
    role: 'Founder & CEO',
    photo: 'https://randomuser.me/api/portraits/men/32.jpg',
  },
  {
    name: 'Srey Mao',
    role: 'Head of Product',
    photo: 'https://randomuser.me/api/portraits/women/44.jpg',
  },
  {
    name: 'Vibol Heng',
    role: 'Head of Engineering',
    photo: 'https://randomuser.me/api/portraits/men/75.jpg',
  },
  {
    name: 'Lina Sok',
    role: 'Customer Success',
    photo: 'https://randomuser.me/api/portraits/women/68.jpg',
  },
]
</script>

<template>
  <section class="mx-auto max-w-3xl px-4 py-16 text-center sm:px-6 lg:py-24">
    <p class="text-primary text-sm font-semibold">About us</p>
    <h1 class="mt-2 text-4xl font-bold tracking-tight sm:text-5xl">
      Making shopping simple since 2020
    </h1>
    <p class="text-muted-foreground mt-6 text-lg">
      Ecommerce started as a small marketplace for local makers. Today we connect millions of
      shoppers with thousands of sellers, while keeping the same goal: great products, fair prices
      and friendly service.
    </p>
  </section>

  <section class="mx-auto grid max-w-7xl gap-6 px-4 pb-16 sm:px-6 md:grid-cols-3">
    <div v-for="v in values" :key="v.title" class="rounded-xl border p-6">
      <component :is="v.icon" class="text-primary mb-4 size-8" />
      <h3 class="font-semibold">{{ v.title }}</h3>
      <p class="text-muted-foreground mt-1 text-sm">{{ v.text }}</p>
    </div>
  </section>

  <section class="bg-muted/50 py-16">
    <div class="mx-auto max-w-7xl px-4 sm:px-6">
      <h2 class="mb-10 text-center text-3xl font-bold">Meet the team</h2>
      <div class="grid grid-cols-2 gap-8 md:grid-cols-4">
        <div v-for="m in team" :key="m.name" class="text-center">
          <Avatar class="mx-auto size-20">
            <AvatarImage :src="m.photo" :alt="m.name" />
            <AvatarFallback class="text-lg">{{
              m.name
                .split(' ')
                .map((n) => n[0])
                .join('')
            }}</AvatarFallback>
          </Avatar>
          <p class="mt-3 font-medium">{{ m.name }}</p>
          <p class="text-muted-foreground text-sm">{{ m.role }}</p>
        </div>
      </div>
    </div>
  </section>
</template>
