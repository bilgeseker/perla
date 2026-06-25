<template>
  <main class="home">
    <!-- ===== HERO SECTION ===== -->
    <section class="hero">
      <div class="hero-bg">
        <img src="/images/hero_jewelry.png" alt="Perla Aksesuar" class="hero-bg-img" />
        <div class="hero-overlay"></div>
        <div class="hero-particles">
          <span v-for="i in 20" :key="i" class="particle" :style="particleStyle(i)"></span>
        </div>
      </div>
      <div class="hero-content container">
        <div class="hero-text" ref="heroText">
          <span class="hero-tag">✦ XUPING KALİTESİNDE TAKILAR</span>
          <h1 class="hero-title">
            Zarafetinizi<br />
            <span class="hero-title-accent">Tamamlayın</span>
          </h1>
          <p class="hero-desc">
            Kararmayan, alerji yapmayan premium kalite takılar.
            Her parça, tarzınızı yansıtan özenle seçilmiş tasarımlar.
          </p>
          <div class="hero-actions">
            <router-link to="/kategori/kolye" class="btn btn-primary">
              Koleksiyonu Keşfet
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M5 12h14M12 5l7 7-7 7" />
              </svg>
            </router-link>
            <a href="#ozellikler" class="btn btn-outline" @click.prevent="scrollTo('ozellikler')">Neden Perla?</a>
          </div>
          <!-- <div class="hero-stats">
            <div class="stat">
              <span class="stat-number">5000+</span>
              <span class="stat-label">Mutlu Müşteri</span>
            </div>
            <div class="stat-divider"></div>
            <div class="stat">
              <span class="stat-number">300+</span>
              <span class="stat-label">Ürün Çeşidi</span>
            </div>
            <div class="stat-divider"></div>
            <div class="stat">
              <span class="stat-number">%100</span>
              <span class="stat-label">Kararmaz Garanti</span>
            </div>
          </div> -->
        </div>
      </div>
      <div class="hero-scroll-indicator" @click="scrollTo('kategoriler')">
        <span class="scroll-text">Keşfet</span>
        <div class="scroll-line"></div>
      </div>
    </section>

    <!-- ===== CATEGORIES SECTION ===== -->
    <section id="kategoriler" class="section categories-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Koleksiyon <span>Kategorileri</span></h2>
          <p class="section-subtitle">Her tarza uygun, özenle seçilmiş takı koleksiyonumuz</p>
        </div>
        <div class="categories-grid">
          <router-link v-for="cat in categories" :key="cat.id" :to="`/kategori/${cat.slug}`" class="category-card">
            <div class="cat-icon-wrapper">
              <span class="cat-icon">{{ cat.icon }}</span>
            </div>
            <span class="cat-name">{{ cat.name }}</span>
            <span class="cat-arrow">→</span>
          </router-link>
        </div>
      </div>
    </section>

    <!-- ===== FEATURED PRODUCTS ===== -->
    <section class="section products-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Öne Çıkan <span>Ürünler</span></h2>
          <p class="section-subtitle">En çok tercih edilen ve trend olan parçalar</p>
        </div>

        <!-- Filter Tabs -->
        <div class="filter-tabs">
          <button class="filter-tab" :class="{ active: activeFilter === 'all' }"
            @click="activeFilter = 'all'">Tümü</button>
          <button v-for="cat in categories.slice(0, 5)" :key="cat.id" class="filter-tab"
            :class="{ active: activeFilter === cat.slug }" @click="activeFilter = cat.slug">{{ cat.name }}</button>
        </div>

        <!-- Product Grid -->
        <transition-group name="product-grid" tag="div" class="products-grid">
          <ProductCard v-for="product in filteredProducts" :key="product.id" :product="product" />
        </transition-group>

        <div class="products-cta">
          <router-link to="/kategori/kolye" class="btn btn-outline">
            Tüm Ürünleri Gör
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M5 12h14M12 5l7 7-7 7" />
            </svg>
          </router-link>
        </div>
      </div>
    </section>

    <!-- ===== PROMOTIONAL BANNER ===== -->
    <section class="promo-section">
      <div class="promo-bg"></div>
      <!-- <div class="container promo-content">
        <div class="promo-text">
          <span class="promo-tag">✦ ÖZEL FIRSAT</span>
          <h2 class="promo-title">İlk Siparişinize<br /><span class="gold-text">%15 İndirim</span></h2>
          <p class="promo-desc">Bültenimize abone olun ve ilk alışverişinizde geçerli özel indirim kodunuzu alın.</p>
          <div class="promo-form">
            <input type="email" placeholder="E-posta adresiniz" class="promo-input" />
            <button class="btn btn-primary">Abone Ol</button>
          </div>
        </div>
        <div class="promo-visual">
          <div class="promo-ring promo-ring-1"></div>
          <div class="promo-ring promo-ring-2"></div>
          <div class="promo-ring promo-ring-3"></div>
          <span class="promo-percent">%15</span>
        </div>
      </div> -->
      <div class="container promo-content">
        <div class="promo-text">
          <span class="promo-tag">✦ PERLA FARKI</span>
          <h2 class="promo-title">Stilinizin<br /><span class="gold-text">günlük tamamlayıcısı</span></h2>
          <p class="promo-desc">
            Kararmayan, alerji yapmayan ve uzun ömürlü parlaklık sunan takılarımızla her anı şık ve güvenli kılın.
          </p>
          <router-link to="/kategori/kolye" class="btn btn-primary">Koleksiyonu İncele</router-link>
        </div>
        <div class="promo-visual">
          <div class="promo-ring promo-ring-1"></div>
          <div class="promo-ring promo-ring-2"></div>
          <div class="promo-ring promo-ring-3"></div>
          <div class="promo-badge">
            <span>✦</span>
            <small>Premium kalite</small>
          </div>
        </div>
      </div>
    </section>

    <!-- ===== FEATURES SECTION ===== -->
    <section id="ozellikler" class="section features-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Neden <span>Perla?</span></h2>
          <p class="section-subtitle">Xuping kalitesinde takılar ile fark yaratın</p>
        </div>
        <div class="features-grid">
          <div v-for="(feature, i) in features" :key="i" class="feature-card">
            <div class="feature-icon-wrapper">
              <span class="feature-icon">{{ feature.icon }}</span>
            </div>
            <h3 class="feature-title">{{ feature.title }}</h3>
            <p class="feature-desc">{{ feature.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ===== TRUST / QUALITY SECTION ===== -->
    <section class="section quality-section">
      <div class="container">
        <div class="quality-content">
          <div class="quality-text">
            <span class="quality-tag">✦ XUPİNG TEKNOLOJİSİ</span>
            <h2 class="quality-title">
              Kararmayan Takıların<br />
              <span class="gold-text">Sırrı</span>
            </h2>
            <p class="quality-desc">
              Xuping teknolojisi ile üretilen takılarımız, özel alaşım kaplama sayesinde
              uzun süre ilk günkü parlaklığını korur. Suya, tere ve parfüme dayanıklı
              yapısıyla günlük kullanım için idealdir.
            </p>
            <ul class="quality-list">
              <li>
                <span class="quality-check">✓</span>
                18K altın kaplama kalitesi
              </li>
              <li>
                <span class="quality-check">✓</span>
                Nikel içermez, alerji yapmaz
              </li>
              <li>
                <span class="quality-check">✓</span>
                Suya ve tere dayanıklı
              </li>
              <li>
                <span class="quality-check">✓</span>
                Uzun ömürlü parlaklık garantisi
              </li>
            </ul>
          </div>
          <div class="quality-visual">
            <div class="quality-img-wrapper">
              <img src="/images/bracelet_gold.png" alt="Xuping kalite" class="quality-img" />
              <div class="quality-glow"></div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ===== TESTIMONIALS ===== -->
    <section class="section testimonials-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Müşterilerimiz <span>Ne Diyor?</span></h2>
          <p class="section-subtitle">Binlerce mutlu müşterimizden bazıları</p>
        </div>
        <div class="testimonials-grid">
          <div v-for="(testimonial, i) in testimonials" :key="i" class="testimonial-card">
            <div class="testimonial-stars">
              <span v-for="s in 5" :key="s" class="star">★</span>
            </div>
            <p class="testimonial-text">"{{ testimonial.text }}"</p>
            <div class="testimonial-author">
              <div class="author-avatar">{{ testimonial.initials }}</div>
              <div class="author-info">
                <span class="author-name">{{ testimonial.name }}</span>
                <span class="author-product">{{ testimonial.product }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script setup>
import { ref, computed } from 'vue'
import { products, categories, features } from '../data/products.js'
import ProductCard from '../components/ProductCard.vue'

const activeFilter = ref('all')

const filteredProducts = computed(() => {
  if (activeFilter.value === 'all') return products
  return products.filter(p => p.category === activeFilter.value)
})

const testimonials = [
  {
    name: 'Ayşe K.',
    initials: 'AK',
    product: 'Altın Zincir Kolye',
    text: 'Kolye gerçekten çok kaliteli, 6 aydır kullanıyorum ve hâlâ ilk günkü gibi parlıyor. Xuping kalitesi gerçekten fark yaratıyor!'
  },
  {
    name: 'Merve T.',
    initials: 'MT',
    product: 'Zarif Halka Küpe',
    text: 'Normalde takılara alerjim var ama Perla ürünlerinde hiçbir sorun yaşamadım. Hem şık hem de sağlıklı. Kesinlikle tavsiye ederim.'
  },
  {
    name: 'Elif S.',
    initials: 'ES',
    product: 'İnce Zincir Bileklik',
    text: 'Arkadaşıma hediye aldım, bayıldı! Kutusu bile çok şıktı. Fiyat-performans olarak harika bir marka.'
  }
]

function particleStyle(i) {
  const size = Math.random() * 4 + 2
  return {
    left: `${Math.random() * 100}%`,
    top: `${Math.random() * 100}%`,
    width: `${size}px`,
    height: `${size}px`,
    animationDelay: `${Math.random() * 5}s`,
    animationDuration: `${3 + Math.random() * 4}s`
  }
}

function scrollTo(id) {
  const el = document.getElementById(id)
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style scoped>
/* ===== HERO ===== */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
}

.hero-bg-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg,
      rgba(10, 10, 10, 0.92) 0%,
      rgba(10, 10, 10, 0.7) 50%,
      rgba(10, 10, 10, 0.85) 100%);
}

.hero-particles {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.particle {
  position: absolute;
  border-radius: 50%;
  background: var(--color-gold);
  opacity: 0.3;
  animation: float var(--transition-slow) ease-in-out infinite;
}

.hero-content {
  position: relative;
  z-index: 2;
  padding-top: 120px;
  padding-bottom: 80px;
}

.hero-text {
  max-width: 650px;
}

.hero-tag {
  display: inline-block;
  font-size: 0.75rem;
  font-weight: 500;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold);
  margin-bottom: var(--space-xl);
  padding: var(--space-sm) var(--space-lg);
  border: 1px solid rgba(201, 168, 76, 0.3);
  border-radius: var(--radius-full);
  animation: fadeInUp 0.6s ease forwards;
}

.hero-title {
  font-family: var(--font-display);
  font-size: clamp(3rem, 7vw, 5.5rem);
  font-weight: 400;
  line-height: 1.1;
  /* color: var(--color-text-main); */
  color: var(--color-white);
  margin-bottom: var(--space-xl);
  animation: fadeInUp 0.6s ease 0.15s forwards;
  opacity: 0;
}

.hero-title-accent {
  font-style: italic;
  background: linear-gradient(135deg, var(--color-gold-light), var(--color-gold), var(--color-gold-dark));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-desc {
  font-size: 1.1rem;
  color: var(--color-white);
  line-height: 1.7;
  margin-bottom: var(--space-2xl);
  max-width: 480px;
  animation: fadeInUp 0.6s ease 0.3s forwards;
  opacity: 0;
}

.hero-actions {
  display: flex;
  gap: var(--space-md);
  margin-bottom: var(--space-3xl);
  animation: fadeInUp 0.6s ease 0.45s forwards;
  opacity: 0;
  flex-wrap: wrap;
}

.hero-stats {
  display: flex;
  align-items: center;
  gap: var(--space-xl);
  animation: fadeInUp 0.6s ease 0.6s forwards;
  opacity: 0;
}

.stat {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.stat-number {
  font-family: var(--font-display);
  font-size: 1.8rem;
  font-weight: 600;
  color: var(--color-gold);
}

.stat-label {
  font-size: 0.75rem;
  color: var(--color-gray);
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.stat-divider {
  width: 1px;
  height: 40px;
  background: rgba(201, 168, 76, 0.2);
}

/* Scroll Indicator */
.hero-scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-sm);
  cursor: pointer;
  z-index: 2;
  animation: fadeIn 1s ease 1s forwards;
  opacity: 0;
}

.scroll-text {
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold);
}

.scroll-line {
  width: 1px;
  height: 40px;
  background: linear-gradient(to bottom, var(--color-gold), transparent);
  animation: scrollPulse 2s ease infinite;
}

@keyframes scrollPulse {

  0%,
  100% {
    opacity: 1;
    height: 40px;
  }

  50% {
    opacity: 0.5;
    height: 20px;
  }
}

/* ===== CATEGORIES ===== */
.categories-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: var(--space-lg);
}

.category-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-md);
  padding: var(--space-2xl) var(--space-lg);
  background: var(--color-bg-card);
  border: 1px solid rgba(201, 168, 76, 0.08);
  border-radius: var(--radius-lg);
  transition: all var(--transition-normal);
  text-decoration: none;
  position: relative;
  overflow: hidden;
}

.category-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 50% 0%, rgba(201, 168, 76, 0.08) 0%, transparent 70%);
  opacity: 0;
  transition: opacity var(--transition-normal);
}

.category-card:hover::before {
  opacity: 1;
}

.category-card:hover {
  border-color: rgba(201, 168, 76, 0.3);
  transform: translateY(-4px);
  box-shadow: var(--shadow-gold);
}

.cat-icon-wrapper {
  width: 56px;
  height: 56px;
  border-radius: var(--radius-full);
  background: rgba(201, 168, 76, 0.1);
  border: 1px solid rgba(201, 168, 76, 0.15);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all var(--transition-normal);
}

.category-card:hover .cat-icon-wrapper {
  background: rgba(201, 168, 76, 0.2);
  transform: scale(1.1);
}

.cat-icon {
  font-size: 1.5rem;
}

.cat-name {
  font-size: 0.85rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--color-text-main);
  transition: color var(--transition-fast);
}

.category-card:hover .cat-name {
  color: var(--color-gold);
}

.cat-arrow {
  font-size: 1.2rem;
  color: var(--color-gold);
  opacity: 0;
  transform: translateY(5px);
  transition: all var(--transition-normal);
}

.category-card:hover .cat-arrow {
  opacity: 1;
  transform: translateY(0);
}

/* ===== PRODUCTS ===== */
.filter-tabs {
  display: flex;
  justify-content: center;
  gap: var(--space-sm);
  margin-bottom: var(--space-3xl);
  flex-wrap: wrap;
}

.filter-tab {
  padding: var(--space-sm) var(--space-lg);
  font-size: 0.8rem;
  font-weight: 500;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: var(--color-gray);
  border: 1px solid rgba(201, 168, 76, 0.1);
  border-radius: var(--radius-full);
  transition: all var(--transition-normal);
}

.filter-tab:hover {
  border-color: rgba(201, 168, 76, 0.3);
  color: var(--color-gold);
}

.filter-tab.active {
  background: var(--color-gold);
  color: var(--color-black);
  border-color: var(--color-gold);
}

.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: var(--space-xl);
}

.products-cta {
  display: flex;
  justify-content: center;
  margin-top: var(--space-3xl);
}

/* Product grid transitions */
.product-grid-enter-active {
  transition: all 0.4s ease;
}

.product-grid-leave-active {
  transition: all 0.3s ease;
  position: absolute;
}

.product-grid-enter-from {
  opacity: 0;
  transform: scale(0.9);
}

.product-grid-leave-to {
  opacity: 0;
  transform: scale(0.9);
}

/* ===== PROMO SECTION ===== */
.promo-section {
  position: relative;
  padding: var(--space-4xl) 0;
  overflow: hidden;
}

.promo-bg {
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, var(--color-black-light) 0%, var(--color-gray) 50%, var(--color-black-light) 100%);
  border-top: 1px solid rgba(201, 168, 76, 0.1);
  border-bottom: 1px solid rgba(201, 168, 76, 0.1);
}

.promo-content {
  position: relative;
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  align-items: center;
  gap: var(--space-3xl);
}

.promo-tag {
  display: inline-block;
  font-size: 0.75rem;
  font-weight: 500;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold);
  margin-bottom: var(--space-lg);
}

.promo-title {
  font-family: var(--font-display);
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 400;
  line-height: 1.2;
  color: var(--color-white);
  margin-bottom: var(--space-lg);
}

.promo-desc {
  font-size: 1rem;
  color: var(--color-white);
  line-height: 1.6;
  margin-bottom: var(--space-xl);
  max-width: 450px;
}

.promo-form {
  display: flex;
  gap: var(--space-md);
  max-width: 450px;
}

.promo-input {
  flex: 1;
  padding: var(--space-md) var(--space-lg);
  background: var(--color-bg-elevated);
  border: 1px solid rgba(201, 168, 76, 0.2);
  border-radius: var(--radius-full);
  color: var(--color-white);
  font-size: 0.9rem;
  font-family: var(--font-body);
  outline: none;
  transition: border-color var(--transition-fast);
}


.promo-input::placeholder {
  color: var(--color-gold-shimmer);
}

.promo-input:focus {
  border-color: var(--color-gold);
}

/* Promo Visual */
.promo-visual {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  height: 250px;
}

.promo-ring {
  position: absolute;
  border-radius: 50%;
  border: 1px solid rgba(201, 168, 76, 0.2);
}

.promo-ring-1 {
  width: 200px;
  height: 200px;
  animation: float 6s ease-in-out infinite;
}

.promo-ring-2 {
  width: 150px;
  height: 150px;
  border-color: rgba(201, 168, 76, 0.3);
  animation: float 4s ease-in-out infinite reverse;
}

.promo-ring-3 {
  width: 100px;
  height: 100px;
  border-color: rgba(201, 168, 76, 0.15);
  animation: float 5s ease-in-out infinite;
}

.promo-percent {
  font-family: var(--font-display);
  font-size: 3.5rem;
  font-weight: 700;
  color: var(--color-gold);
  z-index: 1;
}

/* ===== FEATURES ===== */
.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: var(--space-xl);
}

.feature-card {
  text-align: center;
  padding: var(--space-2xl);
  background: var(--color-bg-card);
  border: 1px solid rgba(201, 168, 76, 0.08);
  border-radius: var(--radius-lg);
  transition: all var(--transition-normal);
}

.feature-card:hover {
  border-color: rgba(201, 168, 76, 0.2);
  transform: translateY(-4px);
}

.feature-icon-wrapper {
  width: 64px;
  height: 64px;
  margin: 0 auto var(--space-lg);
  border-radius: var(--radius-full);
  background: rgba(201, 168, 76, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
}

.feature-icon {
  font-size: 1.8rem;
}

.feature-title {
  font-family: var(--font-display);
  font-size: 1.2rem;
  font-weight: 500;
  color: var(--color-gold);
  margin-bottom: var(--space-md);
}

.feature-desc {
  font-size: 0.875rem;
  color: var(--color-text-main);
  line-height: 1.6;
}

/* ===== QUALITY ===== */
.quality-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-4xl);
  align-items: center;
}

.quality-tag {
  display: inline-block;
  font-size: 0.75rem;
  font-weight: 500;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold);
  margin-bottom: var(--space-lg);
}

.quality-title {
  font-family: var(--font-display);
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 400;
  line-height: 1.2;
  color: var(--color-text-main);
  margin-bottom: var(--space-xl);
}

.quality-desc {
  font-size: 1rem;
  color: var(--color-text-main);
  line-height: 1.7;
  margin-bottom: var(--space-xl);
}

.quality-list {
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
}

.quality-list li {
  display: flex;
  align-items: center;
  gap: var(--space-md);
  font-size: 0.95rem;
  color: var(--color-text-main);
}

.quality-check {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 24px;
  height: 24px;
  border-radius: var(--radius-full);
  background: rgba(201, 168, 76, 0.15);
  color: var(--color-gold);
  font-size: 0.8rem;
  flex-shrink: 0;
}

.quality-visual {
  display: flex;
  align-items: center;
  justify-content: center;
}

.quality-img-wrapper {
  position: relative;
  border-radius: var(--radius-xl);
  overflow: hidden;
  border: 1px solid rgba(201, 168, 76, 0.15);
}

.quality-img {
  width: 100%;
  max-width: 450px;
  aspect-ratio: 1;
  object-fit: cover;
}

.quality-glow {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 30% 70%, rgba(201, 168, 76, 0.15) 0%, transparent 60%);
  pointer-events: none;
}

/* ===== TESTIMONIALS ===== */
.testimonials-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--space-xl);
}

.testimonial-card {
  padding: var(--space-2xl);
  background: var(--color-bg-card);
  border: 1px solid rgba(201, 168, 76, 0.08);
  border-radius: var(--radius-lg);
  transition: all var(--transition-normal);
}

.testimonial-card:hover {
  border-color: rgba(201, 168, 76, 0.2);
  transform: translateY(-4px);
}

.testimonial-stars {
  display: flex;
  gap: 2px;
  margin-bottom: var(--space-lg);
}

.star {
  color: var(--color-gold);
  font-size: 1rem;
}

.testimonial-text {
  font-size: 0.95rem;
  color: var(--color-text-main);
  line-height: 1.7;
  font-style: italic;
  margin-bottom: var(--space-xl);
}

.testimonial-author {
  display: flex;
  align-items: center;
  gap: var(--space-md);
}

.author-avatar {
  width: 44px;
  height: 44px;
  border-radius: var(--radius-full);
  background: linear-gradient(135deg, var(--color-gold), var(--color-gold-dark));
  color: var(--color-black);
  font-size: 0.8rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
}

.author-info {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.author-name {
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--color-text-main);
}

.author-product {
  font-size: 0.75rem;
  color: var(--color-text-main);
}

.promo-highlights {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-sm);
  margin-bottom: var(--space-xl);
}

.promo-highlight-item {
  padding: 0.7rem 1rem;
  border: 1px solid rgba(201, 168, 76, 0.2);
  border-radius: var(--radius-full);
  background: rgba(255, 255, 255, 0.05);
  color: var(--color-gold-shimmer);
  font-size: 0.9rem;
}

.promo-badge {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 120px;
  height: 120px;
  border-radius: 50%;
  background: rgba(201, 168, 76, 0.12);
  border: 1px solid rgba(201, 168, 76, 0.25);
  box-shadow: 0 0 0 12px rgba(201, 168, 76, 0.05);
  color: var(--color-gold);
  text-align: center;
}

.promo-badge span {
  font-size: 2rem;
  line-height: 1;
}

.promo-badge small {
  margin-top: 0.35rem;
  font-size: 0.75rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--color-gold-shimmer);
}

/* ===== RESPONSIVE ===== */
@media (max-width: 768px) {
  .hero-content {
    padding-top: 100px;
    padding-bottom: 60px;
  }

  .hero-stats {
    flex-direction: column;
    align-items: flex-start;
    gap: var(--space-lg);
  }

  .stat-divider {
    width: 40px;
    height: 1px;
    display: none;
  }

  .hero-scroll-indicator {
    display: none;
  }

  .promo-content {
    grid-template-columns: 1fr;
  }

  .promo-visual {
    display: none;
  }

  .promo-form {
    flex-direction: column;
  }

  .quality-content {
    grid-template-columns: 1fr;
    gap: var(--space-2xl);
  }

  .quality-visual {
    order: -1;
  }

  .categories-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: var(--space-md);
  }

  .category-card {
    padding: var(--space-lg) var(--space-md);
  }

  .products-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: var(--space-md);
  }
}

@media (max-width: 480px) {
  .categories-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .products-grid {
    grid-template-columns: 1fr;
  }
}
</style>
