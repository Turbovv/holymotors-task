<script setup>
import { defineComponent } from 'vue';
import { Accordion, AccordionContent, AccordionItem, AccordionTrigger } from '../shared/components/ui/accordion'
import OurProjects from '../OurProjects/OurProjects.vue';
import OurClients from '../OurClients/OurClients.vue';
import OurWorks from '../OurWorks/OurWorks.vue'
import Footer from '../Footer/Footer.vue';

const accordionItems = [
  { value: 'item-1', title: 'Projects', content: defineComponent(OurProjects) },
  { value: 'item-2', title: 'Works', content: defineComponent(OurWorks) },

  { value: 'item-3', title: 'Clients', content: defineComponent(OurClients) },
  { value: 'item-4', title: 'Story', content: defineComponent(Footer) },
]
</script>

<template>
  <Accordion type="single" collapsible>
    <AccordionItem v-for="item in accordionItems" :key="item.value" :value="item.value">
      <AccordionTrigger class="uppercase no-underline">
        <h1 class="text-3xl">Our <span class="text-red-500">{{ item.title }}</span></h1>
      </AccordionTrigger>
      <AccordionContent>
        <component :is="item.content" />
      </AccordionContent>
    </AccordionItem>
  </Accordion>
</template>