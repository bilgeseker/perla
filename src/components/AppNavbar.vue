<template>
  <header class="navbar" :class="{ scrolled: isScrolled, 'menu-open': isMobileMenuOpen, 'navbar-home': isHomePage }">
    <div class="navbar-inner container">
      <!-- Logo -->
      <router-link to="/" class="navbar-logo" @click="closeMobileMenu">
        <span class="logo-icon">✦</span>
        <span class="logo-text">PERLA</span>
        <span class="logo-tagline">AKSESUAR</span>
      </router-link>

      <!-- Desktop Navigation -->
      <nav class="navbar-nav">
        <router-link to="/" class="nav-link" active-class="active">Ana Sayfa</router-link>
        <div class="nav-dropdown" @mouseenter="openDropdown" @mouseleave="closeDropdown">
          <span class="nav-link dropdown-trigger">
            Kategoriler
            <svg class="dropdown-arrow" width="10" height="6" viewBox="0 0 10 6" fill="none">
              <path d="M1 1L5 5L9 1" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" />
            </svg>
          </span>
          <transition name="dropdown">
            <div v-if="isDropdownOpen" class="dropdown-menu">
              <router-link v-for="cat in categories" :key="cat.id" :to="`/kategori/${cat.slug}`" class="dropdown-item">
                <span class="dropdown-icon">{{ cat.icon }}</span>
                {{ cat.name }}
              </router-link>
            </div>
          </transition>
        </div>
        <a href="#ozellikler" class="nav-link" @click.prevent="scrollToSection('ozellikler')">Neden Perla?</a>
        <a href="#iletisim" class="nav-link" @click.prevent="scrollToSection('iletisim')">İletişim</a>
      </nav>

      <!-- Actions -->
      <div class="navbar-actions">
        <button class="action-btn search-btn" aria-label="Ara">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="11" cy="11" r="8" />
            <path d="m21 21-4.3-4.3" />
          </svg>
        </button>
        <button class="action-btn wishlist-btn" aria-label="Favoriler">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path
              d="M20.8 4.6a5.5 5.5 0 0 0-7.8 0L12 5.7l-1-1.1a5.5 5.5 0 0 0-7.8 7.8l1 1.1L12 21.3l7.8-7.8 1-1.1a5.5 5.5 0 0 0 0-7.8z" />
          </svg>
        </button>
        <button class="action-btn cart-btn" aria-label="Sepet">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z" />
            <line x1="3" y1="6" x2="21" y2="6" />
            <path d="M16 10a4 4 0 0 1-8 0" />
          </svg>
          <span class="cart-count">0</span>
        </button>

        <!-- Mobile menu toggle -->
        <button class="mobile-menu-toggle" @click="toggleMobileMenu"
          :aria-label="isMobileMenuOpen ? 'Menüyü Kapat' : 'Menüyü Aç'">
          <span class="hamburger" :class="{ open: isMobileMenuOpen }">
            <span></span>
            <span></span>
            <span></span>
          </span>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <transition name="mobile-menu">
      <div v-if="isMobileMenuOpen" class="mobile-menu">
        <nav class="mobile-nav">
          <router-link to="/" class="mobile-nav-link" @click="closeMobileMenu">Ana Sayfa</router-link>
          <div class="mobile-nav-divider"></div>
          <span class="mobile-nav-label">Kategoriler</span>
          <router-link v-for="cat in categories" :key="cat.id" :to="`/kategori/${cat.slug}`"
            class="mobile-nav-link mobile-cat-link" @click="closeMobileMenu">
            <span class="mobile-cat-icon">{{ cat.icon }}</span>
            {{ cat.name }}
          </router-link>
          <div class="mobile-nav-divider"></div>
          <a href="#ozellikler" class="mobile-nav-link"
            @click.prevent="scrollToSection('ozellikler'); closeMobileMenu()">Neden Perla?</a>
          <a href="#iletisim" class="mobile-nav-link"
            @click.prevent="scrollToSection('iletisim'); closeMobileMenu()">İletişim</a>
        </nav>
      </div>
    </transition>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import { useRoute } from 'vue-router'
import { categories } from '../data/products.js'

const route = useRoute()
const isScrolled = ref(false)
const isDropdownOpen = ref(false)
const isMobileMenuOpen = ref(false)
let dropdownTimeout = null

const isHomePage = computed(() => route.path === '/')

function handleScroll() {
  isScrolled.value = window.scrollY > 50
}

function openDropdown() {
  clearTimeout(dropdownTimeout)
  isDropdownOpen.value = true
}

function closeDropdown() {
  dropdownTimeout = setTimeout(() => {
    isDropdownOpen.value = false
  }, 200)
}

function toggleMobileMenu() {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
  document.body.style.overflow = isMobileMenuOpen.value ? 'hidden' : ''
}

function closeMobileMenu() {
  isMobileMenuOpen.value = false
  document.body.style.overflow = ''
}

function scrollToSection(id) {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  transition: all var(--transition-normal);
  background: transparent;
}

.navbar.scrolled {
  background: rgba(250, 249, 246, 0.95);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(201, 168, 76, 0.12);
}

.navbar-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 64px;
  gap: var(--space-xl);
}

/* Logo */
.navbar-logo {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
  text-decoration: none;
  flex-shrink: 0;
}

.logo-icon {
  font-size: 1.2rem;
  color: var(--color-gold);
  /* animation: pulse-gold 3s ease infinite; */
}

.logo-text {
  font-family: var(--font-display);
  font-size: 1.4rem;
  font-weight: 600;
  letter-spacing: 0.2em;
  color: var(--color-gold);
}

.logo-tagline {
  font-size: 0.6rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--color-text-main);
  margin-left: -4px;
  align-self: flex-end;
  margin-bottom: 4px;
}

.navbar-home .logo-tagline {
  color: var(--color-white);
}

.navbar.scrolled .logo-tagline {
  color: var(--color-text-main);
}

/* Navigation */
.navbar-nav {
  display: flex;
  align-items: center;
  gap: var(--space-xl);
}

.nav-link {
  font-size: 0.85rem;
  font-weight: 400;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--color-text-main);
  transition: color var(--transition-fast);
  position: relative;
  padding: var(--space-sm) 0;
}

.navbar-home .nav-link {
  color: var(--color-white);
}

.navbar.scrolled .nav-link {
  color: var(--color-text-main);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 1px;
  background: var(--color-gold);
  transition: width var(--transition-normal);
}

.nav-link:hover,
.nav-link.active {
  color: var(--color-gold);
}

.nav-link:hover::after,
.nav-link.active::after {
  width: 100%;
}

/* Dropdown */
.nav-dropdown {
  position: relative;
}

.dropdown-trigger {
  display: flex;
  align-items: center;
  gap: 6px;
  cursor: pointer;
}

.dropdown-arrow {
  transition: transform var(--transition-fast);
}

.nav-dropdown:hover .dropdown-arrow {
  transform: rotate(180deg);
}

.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  min-width: 200px;
  padding: var(--space-sm);
  margin-top: var(--space-sm);
  background: var(--color-bg-elevated);
  border: 1px solid rgba(201, 168, 76, 0.15);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  backdrop-filter: blur(20px);
}

.dropdown-item {
  display: flex;
  align-items: center;
  gap: var(--space-md);
  padding: var(--space-md) var(--space-lg);
  font-size: 0.9rem;
  color: var(--color-gray-light);
  border-radius: var(--radius-md);
  transition: all var(--transition-fast);
}

.dropdown-item:hover {
  background: rgba(201, 168, 76, 0.1);
  color: var(--color-gold);
}

.dropdown-icon {
  font-size: 1.1rem;
}

/* Dropdown transitions */
.dropdown-enter-active,
.dropdown-leave-active {
  transition: all 0.2s ease;
}

.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateX(-50%) translateY(-8px);
}

/* Actions */
.navbar-actions {
  display: flex;
  align-items: center;
  gap: var(--space-md);
}

.action-btn {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: var(--radius-full);
  color: var(--color-text-main);
  transition: all var(--transition-fast);
}

.navbar-home .action-btn {
  color: var(--color-white);
}

.navbar.scrolled .action-btn {
  color: var(--color-text-main);
}

.action-btn:hover {
  color: var(--color-gold);
  background: rgba(201, 168, 76, 0.1);
}

.cart-count {
  position: absolute;
  top: 2px;
  right: 2px;
  width: 16px;
  height: 16px;
  border-radius: var(--radius-full);
  background: var(--color-gold);
  color: var(--color-black);
  font-size: 0.65rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Mobile Menu Toggle */
.mobile-menu-toggle {
  display: none;
  width: 40px;
  height: 40px;
  align-items: center;
  justify-content: center;
}

.hamburger {
  position: relative;
  width: 22px;
  height: 16px;
}

.hamburger span {
  position: absolute;
  left: 0;
  width: 100%;
  height: 2px;
  background: var(--color-text-main);
  border-radius: 2px;
  transition: all var(--transition-normal);
}

.navbar-home .hamburger span {
  background: var(--color-white);
}

.navbar.scrolled .hamburger span {
  background: var(--color-text-main);
}

.hamburger span:nth-child(1) {
  top: 0;
}

.hamburger span:nth-child(2) {
  top: 7px;
}

.hamburger span:nth-child(3) {
  top: 14px;
}

.hamburger.open span:nth-child(1) {
  top: 7px;
  transform: rotate(45deg);
  background: var(--color-gold);
}

.hamburger.open span:nth-child(2) {
  opacity: 0;
}

.hamburger.open span:nth-child(3) {
  top: 7px;
  transform: rotate(-45deg);
  background: var(--color-gold);
}

/* Mobile Menu */
.mobile-menu {
  position: fixed;
  top: 64px;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(250, 249, 246, 0.98);
  backdrop-filter: blur(20px);
  padding: var(--space-lg);
  overflow-y: auto;
}

.mobile-nav {
  display: flex;
  flex-direction: column;
  gap: var(--space-xs);
}

.mobile-nav-link {
  display: flex;
  align-items: center;
  gap: var(--space-md);
  padding: var(--space-sm) var(--space-lg);
  font-size: 0.9rem;
  color: var(--color-text-main);
  border-radius: var(--radius-md);
  transition: all var(--transition-fast);
}

.mobile-nav-link:hover {
  background: rgba(201, 168, 76, 0.1);
  color: var(--color-gold);
}

.mobile-cat-link {
  padding-left: var(--space-2xl);
}

.mobile-cat-icon {
  font-size: 1rem;
}

.mobile-nav-label {
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--color-gold);
  padding: var(--space-md) var(--space-lg);
}

.mobile-nav-divider {
  height: 1px;
  background: rgba(201, 168, 76, 0.1);
  margin: var(--space-sm) 0;
}

/* Mobile menu transitions */
.mobile-menu-enter-active,
.mobile-menu-leave-active {
  transition: all 0.3s ease;
}

.mobile-menu-enter-from,
.mobile-menu-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

/* Responsive */
@media (max-width: 900px) {
  .navbar-nav {
    display: none;
  }

  .search-btn,
  .wishlist-btn {
    display: none;
  }

  .mobile-menu-toggle {
    display: flex;
  }
}

@media (max-width: 600px) {
  .navbar-inner {
    height: 56px;
    gap: var(--space-md);
  }

  .logo-icon {
    font-size: 1rem;
  }

  .logo-text {
    font-size: 1.1rem;
    letter-spacing: 0.15em;
  }

  .logo-tagline {
    font-size: 0.5rem;
  }

  .action-btn {
    width: 36px;
    height: 36px;
  }

  .mobile-menu {
    top: 56px;
    padding: var(--space-md);
  }

  .mobile-nav-link {
    padding: var(--space-xs) var(--space-md);
    font-size: 0.85rem;
  }

  .mobile-nav-label {
    font-size: 0.7rem;
    padding: var(--space-sm) var(--space-md);
  }
}
</style>
