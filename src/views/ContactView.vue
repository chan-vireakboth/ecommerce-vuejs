<script setup>
import { reactive } from 'vue'
import { Clock, Mail, MapPin, Phone } from '@lucide/vue'
import { Button } from '@/components/ui/button'
import { Card, CardContent } from '@/components/ui/card'
import { Input } from '@/components/ui/input'
import { Label } from '@/components/ui/label'
import { Textarea } from '@/components/ui/textarea'

const form = reactive({ name: '', email: '', subject: '', message: '' })

const info = [
  { icon: Mail, label: 'Email', value: 'support@shopnest.com' },
  { icon: Phone, label: 'Phone', value: '+855 23 000 000' },
  { icon: MapPin, label: 'Office', value: 'Phnom Penh, Cambodia' },
  { icon: Clock, label: 'Hours', value: 'Mon–Fri, 8:00–17:00' },
]

function submit() {
  // TODO: send the form to your API.
  console.log('Contact form', { ...form })
}
</script>

<template>
  <div class="mx-auto max-w-7xl px-4 py-16 sm:px-6">
    <div class="mb-12 max-w-2xl">
      <h1 class="text-4xl font-bold tracking-tight">Contact us</h1>
      <p class="text-muted-foreground mt-3 text-lg">
        Questions about an order, or want to partner with us? Send a message and we will reply
        within one business day.
      </p>
    </div>

    <div class="grid gap-10 lg:grid-cols-3">
      <ul class="space-y-6">
        <li v-for="item in info" :key="item.label" class="flex gap-4">
          <span class="bg-muted grid size-10 shrink-0 place-items-center rounded-lg">
            <component :is="item.icon" class="size-5" />
          </span>
          <div>
            <p class="text-muted-foreground text-sm">{{ item.label }}</p>
            <p class="font-medium">{{ item.value }}</p>
          </div>
        </li>
      </ul>

      <Card class="lg:col-span-2">
        <CardContent>
          <form class="grid gap-4 sm:grid-cols-2" @submit.prevent="submit">
            <div class="space-y-2">
              <Label for="name">Name</Label>
              <Input id="name" v-model="form.name" required />
            </div>
            <div class="space-y-2">
              <Label for="email">Email</Label>
              <Input id="email" v-model="form.email" type="email" required />
            </div>
            <div class="space-y-2 sm:col-span-2">
              <Label for="subject">Subject</Label>
              <Input id="subject" v-model="form.subject" />
            </div>
            <div class="space-y-2 sm:col-span-2">
              <Label for="message">Message</Label>
              <Textarea id="message" v-model="form.message" rows="5" required />
            </div>
            <Button type="submit" class="sm:col-span-2 sm:justify-self-start">Send message</Button>
          </form>
        </CardContent>
      </Card>
    </div>
  </div>
</template>
