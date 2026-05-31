<template>
  <section id="features" class="features-section">
    <div class="container reveal">
      <h2>Nuestras <span class="gradient-text">Colecciones</span></h2>
      <div class="features-grid">
        <div v-for="(category, index) in categories" :key="index" class="feature-card">
          <div class="feature-icon" v-html="category.icon"></div>
          <h3>{{ category.title }}</h3>
          <p>{{ category.description }}</p>
        </div>
      </div>
    </div>
  </section>
  </template>

  <script setup>
  const categories = [
  { 
    title: 'Colección Mujer', 
    description: 'Encuentra la combinación perfecta de tendencia y sofisticación. Vestidos, blusas y más para cada ocasión.',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 21a9 9 0 1 0 0-18 9 9 0 0 0 0 18z"/><path d="M12 13V7"/><path d="M15 10l-3 3-3-3"/></svg>`
  },
  { 
    title: 'Colección Hombre', 
    description: 'Estilo clásico con un giro moderno. Trajes, camisas y calzado diseñados para el hombre contemporáneo.',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>`
  },
  { 
    title: 'Accesorios Premium', 
    description: 'Los detalles marcan la diferencia. Bolsos, cinturones y joyería fina para completar tu look.',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z"/><path d="M3 6h18"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>`
  }
  ];
  </script>
