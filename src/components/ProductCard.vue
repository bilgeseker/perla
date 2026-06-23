<template>
  <router-link :to="`/urun/${product.id}`" class="product-card" @mouseenter="isHovered = true"
    @mouseleave="isHovered = false">
    <!-- Image -->
    <div class="card-image-wrapper">
      <div class="card-image-bg"></div>
      <img :src="product.image" :alt="product.name" class="card-image" loading="lazy" />
      <div class="card-overlay">
        <button class="overlay-btn" @click.prevent title="Favorilere Ekle">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path
              d="M20.8 4.6a5.5 5.5 0 0 0-7.8 0L12 5.7l-1-1.1a5.5 5.5 0 0 0-7.8 7.8l1 1.1L12 21.3l7.8-7.8 1-1.1a5.5 5.5 0 0 0 0-7.8z" />
          </svg>
        </button>
        <button class="overlay-btn" @click.prevent title="Hızlı Bakış">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z" />
            <circle cx="12" cy="12" r="3" />
          </svg>
        </button>
      </div>
      <span v-if="product.badge" class="card-badge" :class="badgeClass">{{ product.badge }}</span>
    </div>

    <!-- Info -->
    <div class="card-info">
      <span class="card-category">{{ categoryName }}</span>
      <h3 class="card-title">{{ product.name }}</h3>
      <div class="card-features">
        <span v-for="feat in product.features.slice(0, 2)" :key="feat" class="feature-tag">{{ feat }}</span>
      </div>
      <div class="card-pricing">
        <span class="card-price">₺{{ product.price }}</span>
        <span v-if="product.oldPrice" class="card-old-price">₺{{ product.oldPrice }}</span>
        <span v-if="discount" class="card-discount">%{{ discount }}</span>
      </div>
    </div>

    <!-- Add to cart -->
    <!-- <button class="card-cart-btn" @click.prevent>
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z" />
        <line x1="3" y1="6" x2="21" y2="6" />
        <path d="M16 10a4 4 0 0 1-8 0" />
      </svg>
      Sepete Ekle
    </button> -->
  </router-link>
</template>

<script setup>
import { computed, ref } from 'vue'
import { categories } from '../data/products.js'

const props = defineProps({
  product: { type: Object, required: true }
})

const isHovered = ref(false)

const categoryName = computed(() => {
  const cat = categories.find(c => c.slug === props.product.category)
  return cat ? cat.name : ''
})

const discount = computed(() => {
  if (!props.product.oldPrice) return 0
  return Math.round((1 - props.product.price / props.product.oldPrice) * 100)
})

const badgeClass = computed(() => {
  const badge = props.product.badge?.toLowerCase()
  if (badge === 'yeni') return 'badge-new'
  if (badge === 'çok satan') return 'badge-hot'
  if (badge === 'trend') return 'badge-trend'
  return ''
})
</script>

<style scoped>
.product-card {
  display: flex;
  flex-direction: column;
  background: var(--color-bg-card);
  border-radius: var(--radius-lg);
  overflow: hidden;
  border: 1px solid rgba(201, 168, 76, 0.08);
  transition: all var(--transition-normal);
  position: relative;
  text-decoration: none;
  color: inherit;
}

.product-card:hover {
  border-color: rgba(201, 168, 76, 0.25);
  transform: translateY(-6px);
  box-shadow: var(--shadow-gold);
}

/* Image */
.card-image-wrapper {
  position: relative;
  aspect-ratio: 1;
  overflow: hidden;
  background: var(--color-bg-elevated);
}

.card-image-bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 50% 50%, rgba(201, 168, 76, 0.05) 0%, transparent 70%);
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform var(--transition-slow);
}

.product-card:hover .card-image {
  transform: scale(1.08);
}

/* Overlay */
.card-overlay {
  position: absolute;
  top: var(--space-md);
  right: var(--space-md);
  display: flex;
  flex-direction: column;
  gap: var(--space-sm);
  opacity: 0;
  transform: translateX(10px);
  transition: all var(--transition-normal);
}

.product-card:hover .card-overlay {
  opacity: 1;
  transform: translateX(0);
}

.overlay-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 38px;
  height: 38px;
  border-radius: var(--radius-full);
  background: rgba(10, 10, 10, 0.8);
  backdrop-filter: blur(8px);
  color: var(--color-white);
  border: 1px solid rgba(201, 168, 76, 0.2);
  transition: all var(--transition-fast);
}

.overlay-btn:hover {
  background: var(--color-gold);
  color: var(--color-black);
  border-color: var(--color-gold);
}

/* Badge */
.card-badge {
  position: absolute;
  top: var(--space-md);
  left: var(--space-md);
  padding: 4px 12px;
  font-size: 0.7rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  border-radius: var(--radius-full);
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
.card-info {
  padding: var(--space-lg);
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: var(--space-sm);
}

.card-category {
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--color-gold);
}

.card-title {
  font-family: var(--font-display);
  font-size: 1.15rem;
  font-weight: 500;
  color: var(--color-text-main);
  line-height: 1.3;
}

.card-features {
  display: flex;
  gap: var(--space-sm);
  margin-top: var(--space-xs);
}

.feature-tag {
  font-size: 0.65rem;
  padding: 3px 8px;
  border-radius: var(--radius-full);
  background: rgba(201, 168, 76, 0.06);
  color: var(--color-gold-dark);
  border: 1px solid rgba(201, 168, 76, 0.2);
}

.card-pricing {
  display: flex;
  align-items: baseline;
  gap: var(--space-sm);
  margin-top: auto;
  padding-top: var(--space-sm);
}

.card-price {
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--color-gold);
}

.card-old-price {
  font-size: 0.85rem;
  color: var(--color-gray);
  text-decoration: line-through;
}

.card-discount {
  font-size: 0.7rem;
  font-weight: 600;
  color: #E74C3C;
  background: rgba(231, 76, 60, 0.1);
  padding: 2px 8px;
  border-radius: var(--radius-full);
}

/* Add to cart */
.card-cart-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-sm);
  padding: var(--space-md);
  background: var(--color-bg-elevated);
  border-top: 1px solid rgba(201, 168, 76, 0.08);
  color: var(--color-text-main);
  font-size: 0.8rem;
  font-weight: 500;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  transition: all var(--transition-normal);
}

.card-cart-btn:hover {
  background: var(--color-gold);
  color: var(--color-black);
}
</style>
