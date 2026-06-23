<template>
  <main class="product-page" v-if="product">
    <div class="container">
      <!-- Breadcrumb -->
      <nav class="breadcrumb">
        <router-link to="/">Ana Sayfa</router-link>
        <span class="breadcrumb-sep">›</span>
        <router-link :to="`/kategori/${product.category}`">{{ categoryName }}</router-link>
        <span class="breadcrumb-sep">›</span>
        <span>{{ product.name }}</span>
      </nav>

      <!-- Product Detail -->
      <div class="product-detail">
        <div class="product-gallery">
          <div class="gallery-main">
            <span v-if="product.badge" class="detail-badge" :class="badgeClass">{{ product.badge }}</span>
            <img :src="product.image" :alt="product.name" class="gallery-image" />
            <div class="gallery-glow"></div>
          </div>
        </div>

        <div class="product-info">
          <span class="product-category">{{ categoryName }}</span>
          <h1 class="product-name">{{ product.name }}</h1>
          
          <div class="product-rating">
            <span v-for="s in 5" :key="s" class="star">★</span>
            <span class="rating-count">(48 değerlendirme)</span>
          </div>

          <div class="product-pricing">
            <span class="product-price">₺{{ product.price }}</span>
            <span v-if="product.oldPrice" class="product-old-price">₺{{ product.oldPrice }}</span>
            <span v-if="discount" class="product-discount">%{{ discount }} İndirim</span>
          </div>

          <p class="product-description">{{ product.description }}</p>

          <div class="product-features">
            <h3 class="features-label">Özellikler</h3>
            <div class="features-list">
              <span v-for="feat in product.features" :key="feat" class="feature-badge">
                <span class="feature-check">✓</span>
                {{ feat }}
              </span>
            </div>
          </div>

          <div class="product-actions">
            <div class="quantity-selector">
              <button class="qty-btn" @click="qty > 1 && qty--">−</button>
              <span class="qty-value">{{ qty }}</span>
              <button class="qty-btn" @click="qty++">+</button>
            </div>
            <button class="btn btn-primary btn-lg">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/>
                <line x1="3" y1="6" x2="21" y2="6"/>
                <path d="M16 10a4 4 0 0 1-8 0"/>
              </svg>
              Sepete Ekle
            </button>
            <button class="btn btn-outline wishlist-action">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M20.8 4.6a5.5 5.5 0 0 0-7.8 0L12 5.7l-1-1.1a5.5 5.5 0 0 0-7.8 7.8l1 1.1L12 21.3l7.8-7.8 1-1.1a5.5 5.5 0 0 0 0-7.8z"/>
              </svg>
            </button>
          </div>

          <div class="product-guarantees">
            <div class="guarantee">
              <span class="guarantee-icon">🚚</span>
              <span>Ücretsiz Kargo</span>
            </div>
            <div class="guarantee">
              <span class="guarantee-icon">↩️</span>
              <span>14 Gün İade</span>
            </div>
            <div class="guarantee">
              <span class="guarantee-icon">🛡️</span>
              <span>Kararmaz Garanti</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { computed, ref } from 'vue'
import { useRoute } from 'vue-router'
import { products, categories } from '../data/products.js'

const route = useRoute()
const qty = ref(1)

const product = computed(() => {
  return products.find(p => p.id === Number(route.params.id))
})

const categoryName = computed(() => {
  if (!product.value) return ''
  const cat = categories.find(c => c.slug === product.value.category)
  return cat ? cat.name : ''
})

const discount = computed(() => {
  if (!product.value?.oldPrice) return 0
  return Math.round((1 - product.value.price / product.value.oldPrice) * 100)
})

const badgeClass = computed(() => {
  const badge = product.value?.badge?.toLowerCase()
  if (badge === 'yeni') return 'badge-new'
  if (badge === 'çok satan') return 'badge-hot'
  if (badge === 'trend') return 'badge-trend'
  return ''
})
</script>

<style scoped>
.product-page {
  padding-top: 100px;
  padding-bottom: var(--space-4xl);
}

.breadcrumb {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
  font-size: 0.8rem;
  color: var(--color-gray);
  margin-bottom: var(--space-2xl);
  flex-wrap: wrap;
}

.breadcrumb a {
  color: var(--color-gray);
  transition: color var(--transition-fast);
}

.breadcrumb a:hover {
  color: var(--color-gold);
}

.breadcrumb-sep {
  color: var(--color-gold);
}

.product-detail {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-4xl);
  align-items: start;
}

/* Gallery */
.gallery-main {
  position: relative;
  border-radius: var(--radius-xl);
  overflow: hidden;
  background: var(--color-bg-card);
  border: 1px solid rgba(201, 168, 76, 0.1);
  aspect-ratio: 1;
}

.gallery-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.gallery-glow {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 30% 70%, rgba(201, 168, 76, 0.1) 0%, transparent 60%);
  pointer-events: none;
}

.detail-badge {
  position: absolute;
  top: var(--space-lg);
  left: var(--space-lg);
  padding: 6px 16px;
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  border-radius: var(--radius-full);
  z-index: 2;
}

.badge-new {
  background: linear-gradient(135deg, var(--color-gold), var(--color-gold-dark));
  color: var(--color-black);
}

.badge-hot {
  background: linear-gradient(135deg, #E74C3C, #C0392B);
  color: var(--color-white);
}

.badge-trend {
  background: linear-gradient(135deg, #8E44AD, #6C3483);
  color: var(--color-white);
}

/* Info */
.product-category {
  font-size: 0.75rem;
  font-weight: 500;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-gold);
  display: block;
  margin-bottom: var(--space-md);
}

.product-name {
  font-family: var(--font-display);
  font-size: clamp(1.8rem, 3vw, 2.5rem);
  font-weight: 500;
  color: var(--color-white);
  margin-bottom: var(--space-lg);
}

.product-rating {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
  margin-bottom: var(--space-xl);
}

.star {
  color: var(--color-gold);
  font-size: 0.9rem;
}

.rating-count {
  font-size: 0.8rem;
  color: var(--color-gray);
}

.product-pricing {
  display: flex;
  align-items: baseline;
  gap: var(--space-md);
  margin-bottom: var(--space-xl);
  padding-bottom: var(--space-xl);
  border-bottom: 1px solid rgba(201, 168, 76, 0.1);
}

.product-price {
  font-size: 2rem;
  font-weight: 700;
  color: var(--color-gold);
}

.product-old-price {
  font-size: 1.2rem;
  color: var(--color-gray);
  text-decoration: line-through;
}

.product-discount {
  font-size: 0.8rem;
  font-weight: 600;
  color: #E74C3C;
  background: rgba(231, 76, 60, 0.1);
  padding: 4px 12px;
  border-radius: var(--radius-full);
}

.product-description {
  font-size: 1rem;
  color: var(--color-gray-light);
  line-height: 1.7;
  margin-bottom: var(--space-xl);
}

/* Features */
.features-label {
  font-size: 0.8rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-gray);
  margin-bottom: var(--space-md);
}

.features-list {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-sm);
  margin-bottom: var(--space-xl);
}

.feature-badge {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
  padding: 6px 14px;
  font-size: 0.8rem;
  background: rgba(201, 168, 76, 0.08);
  border: 1px solid rgba(201, 168, 76, 0.15);
  border-radius: var(--radius-full);
  color: var(--color-gold-light);
}

.feature-check {
  color: var(--color-gold);
  font-weight: 700;
}

/* Actions */
.product-actions {
  display: flex;
  align-items: center;
  gap: var(--space-md);
  margin-bottom: var(--space-xl);
  flex-wrap: wrap;
}

.quantity-selector {
  display: flex;
  align-items: center;
  border: 1px solid rgba(201, 168, 76, 0.2);
  border-radius: var(--radius-full);
  overflow: hidden;
}

.qty-btn {
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.1rem;
  color: var(--color-gray-light);
  transition: all var(--transition-fast);
}

.qty-btn:hover {
  background: rgba(201, 168, 76, 0.1);
  color: var(--color-gold);
}

.qty-value {
  width: 40px;
  text-align: center;
  font-weight: 600;
  color: var(--color-white);
}

.btn-lg {
  padding: var(--space-md) var(--space-2xl);
  font-size: 0.9rem;
}

.wishlist-action {
  width: 48px;
  height: 48px;
  padding: 0;
  border-radius: var(--radius-full);
}

/* Guarantees */
.product-guarantees {
  display: flex;
  gap: var(--space-xl);
  padding-top: var(--space-xl);
  border-top: 1px solid rgba(201, 168, 76, 0.1);
  flex-wrap: wrap;
}

.guarantee {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
  font-size: 0.8rem;
  color: var(--color-gray);
}

.guarantee-icon {
  font-size: 1.2rem;
}

/* Responsive */
@media (max-width: 768px) {
  .product-detail {
    grid-template-columns: 1fr;
    gap: var(--space-2xl);
  }
}
</style>
