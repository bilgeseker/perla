<template>
  <main class="category-page">
    <!-- Header -->
    <section class="category-header">
      <div class="category-header-bg"></div>
      <div class="container category-header-content">
        <nav class="breadcrumb">
          <router-link to="/">Ana Sayfa</router-link>
          <span class="breadcrumb-sep">›</span>
          <span>{{ currentCategory?.name || 'Kategori' }}</span>
        </nav>
        <h1 class="category-title">
          <span class="cat-icon-lg">{{ currentCategory?.icon }}</span>
          {{ currentCategory?.name }} <span>Koleksiyonu</span>
        </h1>
        <p class="category-desc">
          {{ categoryProducts.length }} ürün bulundu
        </p>
      </div>
    </section>

    <!-- Products -->
    <section class="section">
      <div class="container">
        <div v-if="categoryProducts.length" class="products-grid">
          <ProductCard v-for="product in categoryProducts" :key="product.id" :product="product" />
        </div>
        <div v-else class="empty-state">
          <span class="empty-icon">✦</span>
          <h2 class="empty-title">Bu kategoride henüz ürün yok</h2>
          <p class="empty-desc">Yakında yeni ürünler eklenecek.</p>
          <router-link to="/" class="btn btn-primary">Ana Sayfaya Dön</router-link>
        </div>
      </div>
    </section>
  </main>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import { products, categories } from '../data/products.js'
import ProductCard from '../components/ProductCard.vue'

const route = useRoute()

const currentCategory = computed(() => {
  return categories.find(c => c.slug === route.params.slug)
})

const categoryProducts = computed(() => {
  return products.filter(p => p.category === route.params.slug)
})
</script>

<style scoped>
.category-header {
  position: relative;
  padding: 140px 0 60px;
  overflow: hidden;
}

.category-header-bg {
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, var(--color-bg-elevated) 0%, var(--color-bg) 100%);
}

.category-header-bg::before {
  content: '';
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 800px;
  height: 400px;
  background: radial-gradient(ellipse, rgba(201, 168, 76, 0.08) 0%, transparent 70%);
}

.category-header-content {
  position: relative;
}

.breadcrumb {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
  font-size: 0.8rem;
  color: var(--color-text-main);
  margin-bottom: var(--space-xl);
}

.breadcrumb a {
  color: var(--color-text-main);
  transition: color var(--transition-fast);
}

.breadcrumb a:hover {
  color: var(--color-gold);
}

.breadcrumb-sep {
  color: var(--color-gold);
}

.category-title {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 400;
  color: var(--color-text-main);
  margin-bottom: var(--space-md);
  display: flex;
  align-items: center;
  gap: var(--space-lg);
  flex-wrap: wrap;
}

.category-title span {
  color: var(--color-gold);
  font-style: italic;
}

.cat-icon-lg {
  font-size: 2.5rem;
}

.category-desc {
  font-size: 1rem;
  color: var(--color-text-main);
}

.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: var(--space-xl);
}

/* Empty State */
.empty-state {
  text-align: center;
  padding: var(--space-4xl) 0;
}

.empty-icon {
  font-size: 3rem;
  color: var(--color-gold);
  display: block;
  margin-bottom: var(--space-xl);
}

.empty-title {
  font-family: var(--font-display);
  font-size: 1.8rem;
  color: var(--color-text-main);
  margin-bottom: var(--space-md);
}

.empty-desc {
  color: var(--color-text-main);
  margin-bottom: var(--space-xl);
}

@media (max-width: 768px) {
  .products-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: var(--space-md);
  }
}

@media (max-width: 480px) {
  .products-grid {
    grid-template-columns: 1fr;
  }
}
</style>
