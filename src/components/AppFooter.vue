<template>
  <footer id="iletisim" class="footer">
    <div class="footer-glow"></div>
    <div class="container">
      <!-- Upper Footer -->
      <div class="footer-upper">
        <div class="footer-brand">
          <div class="footer-logo">
            <span class="logo-icon">✦</span>
            <span class="logo-text">PERLA</span>
          </div>
          <p class="footer-description">
            Xuping kalitesinde, kararmaya dayanıklı şık takılar. 
            Zarafetinizi tamamlayacak en özel parçalar Perla'da.
          </p>
          <div class="footer-social">
            <a href="#" class="social-link" aria-label="Instagram">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <rect x="2" y="2" width="20" height="20" rx="5"/>
                <circle cx="12" cy="12" r="5"/>
                <circle cx="17.5" cy="6.5" r="1.5" fill="currentColor" stroke="none"/>
              </svg>
            </a>
            <a href="#" class="social-link" aria-label="WhatsApp">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
              </svg>
            </a>
            <a href="#" class="social-link" aria-label="TikTok">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                <path d="M19.59 6.69a4.83 4.83 0 01-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 01-2.88 2.5 2.89 2.89 0 01-2.89-2.89 2.89 2.89 0 012.89-2.89c.28 0 .54.04.79.11v-3.5a6.37 6.37 0 00-.79-.05A6.34 6.34 0 003.15 15.2a6.34 6.34 0 0010.86 4.46V13a8.15 8.15 0 005.58 2.2V11.8a4.85 4.85 0 01-3.58-1.58V6.69h3.58z"/>
              </svg>
            </a>
          </div>
        </div>

        <div class="footer-links-grid">
          <div class="footer-links-col">
            <h4 class="footer-heading">Kategoriler</h4>
            <ul class="footer-list">
              <li><router-link to="/kategori/kolye">Kolye</router-link></li>
              <li><router-link to="/kategori/kupe">Küpe</router-link></li>
              <li><router-link to="/kategori/bileklik">Bileklik</router-link></li>
              <li><router-link to="/kategori/yuzuk">Yüzük</router-link></li>
              <li><router-link to="/kategori/halhal">Halhal</router-link></li>
              <li><router-link to="/kategori/set">Set</router-link></li>
            </ul>
          </div>

          <div class="footer-links-col">
            <h4 class="footer-heading">Bilgi</h4>
            <ul class="footer-list">
              <li><a href="#">Hakkımızda</a></li>
              <li><a href="#">Kargo & Teslimat</a></li>
              <li><a href="#">İade & Değişim</a></li>
              <li><a href="#">Gizlilik Politikası</a></li>
              <li><a href="#">SSS</a></li>
            </ul>
          </div>

          <div class="footer-links-col">
            <h4 class="footer-heading">İletişim</h4>
            <ul class="footer-list contact-list">
              <li>
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0118 0z"/>
                  <circle cx="12" cy="10" r="3"/>
                </svg>
                İstanbul, Türkiye
              </li>
              <li>
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                  <polyline points="22,6 12,13 2,6"/>
                </svg>
                info@perlaaksesuar.com
              </li>
              <li>
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 19.5 19.5 0 01-6-6 19.79 19.79 0 01-3.07-8.67A2 2 0 014.11 2h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L8.09 9.91a16 16 0 006 6l1.27-1.27a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 16.92z"/>
                </svg>
                +90 (555) 123 45 67
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Divider -->
      <div class="footer-divider"></div>

      <!-- Bottom Footer -->
      <div class="footer-bottom">
        <p class="copyright">
          © {{ currentYear }} Perla Aksesuar. Tüm hakları saklıdır.
        </p>
        <div class="footer-badges">
          <span class="badge">🛡️ Güvenli Alışveriş</span>
          <span class="badge">🚚 Hızlı Kargo</span>
          <span class="badge">↩️ Kolay İade</span>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear()
</script>

<style scoped>
.footer {
  position: relative;
  background: var(--color-black-light);
  border-top: 1px solid rgba(201, 168, 76, 0.1);
  padding-top: var(--space-4xl);
  overflow: hidden;
}

.footer-glow {
  position: absolute;
  top: -200px;
  left: 50%;
  transform: translateX(-50%);
  width: 600px;
  height: 400px;
  background: radial-gradient(ellipse, rgba(201, 168, 76, 0.06) 0%, transparent 70%);
  pointer-events: none;
}

.footer-upper {
  display: grid;
  grid-template-columns: 1.2fr 2fr;
  gap: var(--space-4xl);
  padding-bottom: var(--space-3xl);
}

/* Brand */
.footer-logo {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
  margin-bottom: var(--space-lg);
}

.footer-logo .logo-icon {
  font-size: 1.3rem;
  color: var(--color-gold);
}

.footer-logo .logo-text {
  font-family: var(--font-display);
  font-size: 1.5rem;
  font-weight: 600;
  letter-spacing: 0.3em;
  color: var(--color-gold);
}

.footer-description {
  font-size: 0.9rem;
  color: var(--color-gray);
  line-height: 1.7;
  margin-bottom: var(--space-xl);
}

.footer-social {
  display: flex;
  gap: var(--space-md);
}

.social-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 42px;
  height: 42px;
  border-radius: var(--radius-full);
  border: 1px solid rgba(201, 168, 76, 0.2);
  color: var(--color-gray);
  transition: all var(--transition-normal);
}

.social-link:hover {
  border-color: var(--color-gold);
  color: var(--color-gold);
  background: rgba(201, 168, 76, 0.1);
  transform: translateY(-3px);
}

/* Links Grid */
.footer-links-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--space-xl);
}

.footer-heading {
  font-family: var(--font-display);
  font-size: 1.1rem;
  font-weight: 500;
  color: var(--color-gold);
  margin-bottom: var(--space-lg);
  letter-spacing: 0.05em;
}

.footer-list {
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
}

.footer-list a,
.footer-list li {
  font-size: 0.875rem;
  color: var(--color-gray);
  transition: color var(--transition-fast);
  display: flex;
  align-items: center;
  gap: var(--space-sm);
}

.footer-list a:hover {
  color: var(--color-gold-light);
}

.contact-list svg {
  color: var(--color-gold);
  flex-shrink: 0;
}

/* Divider */
.footer-divider {
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(201, 168, 76, 0.2), transparent);
}

/* Bottom */
.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--space-xl) 0;
  flex-wrap: wrap;
  gap: var(--space-md);
}

.copyright {
  font-size: 0.8rem;
  color: var(--color-gray);
}

.footer-badges {
  display: flex;
  gap: var(--space-lg);
}

.badge {
  font-size: 0.75rem;
  color: var(--color-gray);
  display: flex;
  align-items: center;
  gap: var(--space-xs);
}

/* Responsive */
@media (max-width: 900px) {
  .footer-upper {
    grid-template-columns: 1fr;
    gap: var(--space-3xl);
  }

  .footer-links-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .footer-links-grid {
    grid-template-columns: 1fr;
  }

  .footer-bottom {
    flex-direction: column;
    text-align: center;
  }

  .footer-badges {
    flex-wrap: wrap;
    justify-content: center;
  }
}
</style>
