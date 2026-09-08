<script setup>
defineProps({
  name: { type: String, required: true },
  size: { type: [Number, String], default: 24 },
})

const paths = {
  menu: 'M4 7h16M4 12h16M4 17h16',
  close: 'M6 6l12 12M18 6L6 18',
  plus: 'M12 5v14M5 12h14',
  minus: 'M5 12h14',
  arrowRight: 'M5 12h14M13 6l6 6-6 6',
  arrowDown: 'M12 5v14M19 12l-7 7-7-7',
  arrowUpRight: 'M7 17L17 7M8 7h9v9',
  star: 'M12 3.5l2.2 6.6H21l-5.4 3.9 2.1 6.5L12 16.8 6.3 20.5l2.1-6.5L3 10.1h6.8L12 3.5z',
  heart:
    'M12 20s-7-4.4-7-10a4 4 0 0 1 7-2 4 4 0 0 1 7 2c0 5.6-7 10-7 10z',
  clock: 'M12 7v5l3 2M12 21a9 9 0 1 0 0-18 9 9 0 0 0 0 18z',
  users:
    'M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2M9 11a4 4 0 1 0 0-8 4 4 0 0 0 0 8zM22 21v-2a4 4 0 0 0-3-3.87M16 3.13a4 4 0 0 1 0 7.75',
  leaf: 'M5 19c8-1 13-8 14-15-7 1-14 6-14 15zM8 12c2 2 5 4 8 5',
  sparkle: 'M12 3l1.5 6L20 10.5 13.5 12 12 18l-1.5-6L4 10.5 10.5 9 12 3z',
  flower:
    'M12 8c-1.2-2.8-1.2-4.5 0-4.5s1.2 1.7 0 4.5zM12 16c1.2 2.8 1.2 4.5 0 4.5s-1.2-1.7 0-4.5zM8 12c-2.8-1.2-4.5-1.2-4.5 0s1.7 1.2 4.5 0zM16 12c2.8 1.2 4.5 1.2 4.5 0s-1.7-1.2-4.5 0zM12 12a1.6 1.6 0 1 0 0.01 0',
  instagram:
    'M8 4h8a4 4 0 0 1 4 4v8a4 4 0 0 1-4 4H8a4 4 0 0 1-4-4V8a4 4 0 0 1 4-4zM12 9a3 3 0 1 0 0 6 3 3 0 0 0 0-6zM17.5 7.5h.01',
  facebook: 'M15 8h-2a2 2 0 0 0-2 2v2h4l-.5 3H11v7H8v-7H6v-3h2v-2.2A3.8 3.8 0 0 1 11.8 5H15v3z',
  youtube: 'M5 8.5A2.5 2.5 0 0 1 7.5 6h9A2.5 2.5 0 0 1 19 8.5v7a2.5 2.5 0 0 1-2.5 2.5h-9A2.5 2.5 0 0 1 5 15.5v-7zM11 10l5 2.5L11 15v-5z',
  whatsapp:
    'M5 19l1.2-3.2A7.5 7.5 0 1 1 19 12a7.4 7.4 0 0 1-2.4 5.5L19 19M8.5 9.5c.3 2 2 4.2 4 4.8',
  bag: 'M6 8h12l-1 12H7L6 8zM9 8V6a3 3 0 0 1 6 0v2',
}
</script>

<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    :width="size"
    :height="size"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="1.6"
    stroke-linecap="round"
    stroke-linejoin="round"
    aria-hidden="true"
  >
    <path :d="paths[name] || paths.sparkle" />
  </svg>
</template>
