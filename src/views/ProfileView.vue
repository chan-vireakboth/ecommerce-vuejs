<script setup>
import { reactive } from 'vue'
import { Heart, MapPin, Package, Settings } from '@lucide/vue'
import { Avatar, AvatarFallback, AvatarImage } from '@/components/ui/avatar'
import { Badge } from '@/components/ui/badge'
import { Button } from '@/components/ui/button'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card'
import { Input } from '@/components/ui/input'
import { Label } from '@/components/ui/label'
import { Separator } from '@/components/ui/separator'

// TODO: load the signed-in user from your auth/API.
const user = reactive({
  name: 'Sokha Chan',
  email: 'sokha@example.com',
  phone: '+855 12 345 678',
  address: 'Street 271, Phnom Penh',
  avatar: 'https://randomuser.me/api/portraits/women/65.jpg',
  memberSince: 'March 2024',
})

const stats = [
  { icon: Package, label: 'Orders', value: 18 },
  { icon: Heart, label: 'Wishlist', value: 7 },
  { icon: MapPin, label: 'Addresses', value: 2 },
]

const orders = [
  { id: '#10234', date: 'Oct 12, 2026', total: 129, status: 'Delivered' },
  { id: '#10211', date: 'Sep 28, 2026', total: 74, status: 'Shipped' },
  { id: '#10187', date: 'Sep 03, 2026', total: 45, status: 'Processing' },
]

const statusVariant = { Delivered: 'default', Shipped: 'secondary', Processing: 'outline' }

function save() {
  // TODO: send the updated profile to your API.
}
</script>

<template>
  <div class="mx-auto max-w-7xl px-4 py-12 sm:px-6">
    <div class="grid gap-6 lg:grid-cols-3">
      <Card>
        <CardContent class="flex flex-col items-center text-center">
          <Avatar class="size-24">
            <AvatarImage v-if="user.avatar" :src="user.avatar" :alt="user.name" />
            <AvatarFallback class="text-2xl">{{
              user.name.slice(0, 2).toUpperCase()
            }}</AvatarFallback>
          </Avatar>
          <h1 class="mt-4 text-xl font-semibold">{{ user.name }}</h1>
          <p class="text-muted-foreground text-sm">{{ user.email }}</p>
          <p class="text-muted-foreground mt-1 text-xs">Member since {{ user.memberSince }}</p>
          <Separator class="my-6" />
          <div class="grid w-full grid-cols-3 gap-2">
            <div v-for="s in stats" :key="s.label">
              <component :is="s.icon" class="text-muted-foreground mx-auto size-5" />
              <p class="mt-1 text-lg font-semibold">{{ s.value }}</p>
              <p class="text-muted-foreground text-xs">{{ s.label }}</p>
            </div>
          </div>
        </CardContent>
      </Card>

      <div class="space-y-6 lg:col-span-2">
        <Card>
          <CardHeader>
            <CardTitle class="flex items-center gap-2"
              ><Settings class="size-5" /> Account details</CardTitle
            >
            <CardDescription>Update your personal information.</CardDescription>
          </CardHeader>
          <CardContent>
            <form class="grid gap-4 sm:grid-cols-2" @submit.prevent="save">
              <div class="space-y-2">
                <Label for="p-name">Full name</Label>
                <Input id="p-name" v-model="user.name" />
              </div>
              <div class="space-y-2">
                <Label for="p-email">Email</Label>
                <Input id="p-email" v-model="user.email" type="email" />
              </div>
              <div class="space-y-2">
                <Label for="p-phone">Phone</Label>
                <Input id="p-phone" v-model="user.phone" />
              </div>
              <div class="space-y-2">
                <Label for="p-address">Address</Label>
                <Input id="p-address" v-model="user.address" />
              </div>
              <Button type="submit" class="sm:col-span-2 sm:justify-self-start"
                >Save changes</Button
              >
            </form>
          </CardContent>
        </Card>

        <Card>
          <CardHeader>
            <CardTitle>Recent orders</CardTitle>
          </CardHeader>
          <CardContent class="overflow-x-auto">
            <table class="w-full text-sm">
              <thead class="text-muted-foreground text-left">
                <tr>
                  <th class="pb-3 font-medium">Order</th>
                  <th class="pb-3 font-medium">Date</th>
                  <th class="pb-3 font-medium">Total</th>
                  <th class="pb-3 font-medium">Status</th>
                </tr>
              </thead>
              <tbody class="divide-y">
                <tr v-for="o in orders" :key="o.id">
                  <td class="py-3 font-medium">{{ o.id }}</td>
                  <td class="py-3">{{ o.date }}</td>
                  <td class="py-3">${{ o.total }}</td>
                  <td class="py-3">
                    <Badge :variant="statusVariant[o.status]">{{ o.status }}</Badge>
                  </td>
                </tr>
              </tbody>
            </table>
          </CardContent>
        </Card>
      </div>
    </div>
  </div>
</template>
