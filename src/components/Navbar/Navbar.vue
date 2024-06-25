<script setup lang="ts">
import { Accordion, AccordionContent, AccordionItem, AccordionTrigger } from '../ui/accordion'

const accordionItems = [
  { value: 'item-1', title: 'Projects', content: 'Content 1' },
  { value: 'item-2', title: 'Works', content: 'Content 2' },
  { value: 'item-3', title: 'Clients', content: 'Content 3' },
  { value: 'item-4', title: 'Story', content: 'Content 4' },
]
</script>

<template>
  <Accordion type="single" class="w-full" collapsible>
    <AccordionItem v-for="item in accordionItems" :key="item.value" :value="item.value">
      <AccordionTrigger class="uppercase">
        <h1>Our 
          <span class="text-red-500">{{item.title}}</span>
        </h1>
      </AccordionTrigger>
      <AccordionContent>
        {{ item.content }}
      </AccordionContent>
    </AccordionItem>
  </Accordion>
</template>

