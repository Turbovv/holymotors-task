<script setup lang="ts">
import { Accordion, AccordionContent, AccordionItem, AccordionTrigger } from '../shared/components/ui/accordion'

const accordionItems = [
  { value: 'item-1', title: 'Projects', content: 'Content1' },
  { value: 'item-2', title: 'Works', content: 'Yes. It\'s unstyled by default, giving you freedom over the look and feel.' },
  { value: 'item-3', title: 'Clients', content: 'Yes! You can use the transition prop to configure the animation.' },
  { value: 'item-4', title: 'Story', content: 'Yes! You can use the transition prop to configure the animation.' },
]
</script>

<template>
  <Accordion type="single" class="w-full" collapsible>
    <AccordionItem v-for="item in accordionItems" :key="item.value" :value="item.value">
      <AccordionTrigger class="uppercase"><h1 class="text-3xl">Our <span class="text-red-500">{{item.title}}</span></h1></AccordionTrigger>
      <AccordionContent>
        {{ item.content }}
       <!-- <component :is="item.content" /> -->
      </AccordionContent>
    </AccordionItem>
  </Accordion>
</template>