<template>
  <section class="about">
    <div class="parallax-bg" ref="parallaxBg"></div>
    <div class="overlay"></div>

    <div class="hero-content">
      <span class="badge">About Us</span>
      <h2 class="hero-title">Explore the Beauty of<br>Indonesia With Us</h2>
      <p class="hero-desc">
        This website is an Indonesian travel guide platform that provides information 
        on the best destinations, travel packages, and vacation inspiration. 
        From Sabang to Merauke, 
        we're here to help you discover unforgettable experiences in every corner of the archipelago.

      </p>
    </div>

    <div class="stats-section">
      <div class="stats-left">
        <span class="stats-badge">Our Reach</span>
        <h3 class="stats-title">Most Visited<br>Destinations</h3>
        <p class="stats-desc">
          These are the top destinations that travelers love the most. From ancient temples 
          to tropical paradises, each location offers a unique experience that keeps visitors 
          coming back year after year.
        </p>
        <div class="stats-total">
          <span class="total-number">10.8M+</span>
          <span class="total-label">Total Visitors</span>
        </div>
      </div>
      <div class="stats-right">
        <div class="cards-stack">
          <div
            v-for="(item, index) in stats"
            :key="index"
            class="stack-card"
            :class="{ 'stack-active': activeCard === index }"
            :style="getCardStyle(index)"
            @mouseenter="activeCard = index"
            @mouseleave="activeCard = null"
          >
            <div class="stack-card-shine"></div>
            <div class="stack-card-content">
              <div class="stack-card-icon">{{ item.icon }}</div>
              <div class="stack-card-info">
                <div class="stack-card-name">{{ item.name }}</div>
                <div class="stack-card-location">{{ item.location }}</div>
              </div>
              <div class="stack-card-visitors">
                <span class="stack-card-number">{{ item.visitors }}</span>
                <span class="stack-card-label">visitors</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from "vue";

const activeCard = ref(null)

const offsets = [
  { rotate: -2, translateX: 0, translateY: 0 },
  { rotate: 3, translateX: 18, translateY: -6 },
  { rotate: -1, translateX: 36, translateY: -12 },
  { rotate: 4, translateX: 54, translateY: -18 },
]

function getCardStyle(index) {
  const o = offsets[index]
  const isActive = activeCard.value === index
  const scale = isActive ? 1 : 0.95 - index * 0.02
  return {
    zIndex: 10 - index,
    transform: `rotate(${o.rotate}deg) translateX(${o.translateX}px) translateY(${o.translateY}px) scale(${isActive ? 1.05 : scale})`,
    marginTop: index > 0 ? '-20px' : '0',
  }
}

const parallaxBg = ref(null)

const stats = [
  {
    icon: '🛕',
    name: 'Borobudur',
    location: 'Magelang, Jawa Tengah',
    visitors: '2.5M'
  },
  {
    icon: '🏝️',
    name: 'Bali',
    location: 'Kepulauan Sunda Kecil',
    visitors: '6.3M'
  },
  {
    icon: '🌋',
    name: 'Bromo',
    location: 'Probolinggo, Jawa Timur',
    visitors: '1.2M'
  },
  {
    icon: '🏖️',
    name: 'Raja Ampat',
    location: 'Papua Barat',
    visitors: '850K'
  }
]

let handleScroll

onMounted(() => {
  handleScroll = () => {
    if (parallaxBg.value) {
      const rect = parallaxBg.value.getBoundingClientRect()
      const speed = 0.3
      parallaxBg.value.style.transform = `translateY(${rect.top * speed}px)`
    }
  }
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.about {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  padding: 140px 20px 100px;
}

.parallax-bg {
  position: absolute;
  inset: -20% 0;
  background:
    linear-gradient(135deg, rgba(10, 10, 20, 0.5) 0%, rgba(20, 15, 40, 0.7) 100%),
    url('https://images.unsplash.com/photo-1615104168825-3d6391ccc228?q=80&w=870') center / cover no-repeat;
  will-change: transform;
  z-index: 0;
}

.overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom, rgba(13, 13, 18, 0.4) 0%, rgba(13, 13, 18, 0.92) 100%);
  z-index: 1;
}

.hero-content {
  position: relative;
  z-index: 2;
  text-align: center;
  max-width: 700px;
  margin-bottom: 80px;
}

.badge {
  display: inline-block;
  font-size: 0.85em;
  color: #a78bfa;
  text-transform: uppercase;
  letter-spacing: 3px;
  font-weight: 500;
  margin-bottom: 20px;
  background: rgba(167, 139, 250, 0.12);
  padding: 6px 18px;
  border-radius: 20px;
  border: 1px solid rgba(167, 139, 250, 0.2);
}

.hero-title {
  font-size: 3.5em;
  font-weight: 700;
  color: #ffffff;
  line-height: 1.15;
  margin-bottom: 24px;
  letter-spacing: -1.5px;
}

.hero-desc {
  font-size: 1.05em;
  color: #a1a1aa;
  line-height: 1.8;
  max-width: 580px;
  margin: 0 auto;
}

.stats-section {
  position: relative;
  z-index: 2;
  width: 100%;
  max-width: 1100px;
  display: flex;
  gap: 40px;
  align-items: center;
}

.stats-left {
  flex: 0 0 380px;
}

.stats-badge {
  display: inline-block;
  font-size: 0.78em;
  color: #a78bfa;
  text-transform: uppercase;
  letter-spacing: 3px;
  font-weight: 500;
  margin-bottom: 14px;
  background: rgba(167, 139, 250, 0.1);
  padding: 5px 14px;
  border-radius: 20px;
  border: 1px solid rgba(167, 139, 250, 0.15);
}

.stats-title {
  font-size: 2.2em;
  font-weight: 700;
  color: #ffffff;
  line-height: 1.2;
  margin-bottom: 18px;
  letter-spacing: -1px;
}

.stats-desc {
  font-size: 0.92em;
  color: #a1a1aa;
  line-height: 1.8;
  margin-bottom: 28px;
}

.stats-total {
  display: inline-flex;
  align-items: center;
  gap: 14px;
  background: rgba(167, 139, 250, 0.06);
  border: 1px solid rgba(167, 139, 250, 0.12);
  border-radius: 14px;
  padding: 14px 24px;
}

.total-number {
  font-size: 1.8em;
  font-weight: 700;
  color: #a78bfa;
  line-height: 1;
}

.total-label {
  font-size: 0.85em;
  color: #71717a;
  font-weight: 400;
}

.stats-right {
  flex: 1;
  display: flex;
  justify-content: center;
}

.cards-stack {
  position: relative;
  width: 100%;
  max-width: 440px;
  min-height: 300px;
  padding: 40px 0;
}

.stack-card {
  position: absolute;
  top: 0;
  right: 0;
  width: 85%;
  background: linear-gradient(145deg, rgba(30, 30, 35, 0.9), rgba(22, 22, 28, 0.95));
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 18px;
  padding: 22px 26px;
  transition: all 0.45s cubic-bezier(0.34, 1.56, 0.64, 1);
  cursor: pointer;
  overflow: hidden;
  box-shadow:
    0 4px 20px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.04);
}

.stack-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(167, 139, 250, 0.2), transparent);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.stack-card:hover::before {
  opacity: 1;
}

.stack-card-shine {
  position: absolute;
  inset: 0;
  border-radius: 18px;
  background: linear-gradient(135deg, rgba(167, 139, 250, 0.08) 0%, transparent 50%, rgba(255, 255, 255, 0.02) 100%);
  opacity: 0;
  transition: opacity 0.4s ease;
  pointer-events: none;
}

.stack-card:hover .stack-card-shine {
  opacity: 1;
}

.stack-active {
  border-color: rgba(167, 139, 250, 0.3) !important;
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.5),
    0 0 40px rgba(167, 139, 250, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.06) !important;
}

.stack-card-content {
  position: relative;
  z-index: 1;
  display: flex;
  align-items: center;
  gap: 14px;
}

.stack-card-icon {
  font-size: 1.6em;
  flex-shrink: 0;
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, rgba(167, 139, 250, 0.12), rgba(167, 139, 250, 0.04));
  border: 1px solid rgba(167, 139, 250, 0.1);
  border-radius: 12px;
}

.stack-card-info {
  flex: 1;
  min-width: 0;
}

.stack-card-name {
  font-size: 0.95em;
  font-weight: 600;
  color: #ffffff;
  margin-bottom: 3px;
  letter-spacing: 0.3px;
}

.stack-card-location {
  font-size: 0.75em;
  color: #63636e;
  letter-spacing: 0.2px;
}

.stack-card-visitors {
  text-align: right;
  flex-shrink: 0;
}

.stack-card-number {
  display: block;
  font-size: 1.3em;
  font-weight: 700;
  background: linear-gradient(135deg, #a78bfa, #c4b5fd);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  line-height: 1;
  margin-bottom: 2px;
}

.stack-card-label {
  font-size: 0.65em;
  color: #52525b;
  text-transform: uppercase;
  letter-spacing: 1.2px;
}

@media (max-width: 900px) {
  .hero-title {
    font-size: 2.4em;
  }

  .about {
    padding: 100px 16px 60px;
  }

  .hero-content {
    margin-bottom: 60px;
  }

  .stats-section {
    flex-direction: column;
    gap: 50px;
  }

  .stats-left {
    flex: none;
    width: 100%;
    text-align: center;
  }

  .stats-desc {
    max-width: 500px;
    margin: 0 auto 28px;
  }

  .stats-right {
    width: 100%;
  }

  .cards-stack {
    max-width: 400px;
    margin: 0 auto;
    min-height: 260px;
  }

  .stack-card {
    width: 90%;
  }
}

@media (max-width: 500px) {
  .hero-title {
    font-size: 1.8em;
  }

  .stats-title {
    font-size: 1.6em;
  }

  .stats-left {
    flex: none;
    width: 100%;
  }

  .cards-stack {
    min-height: 240px;
    padding: 30px 0;
  }

  .stack-card {
    padding: 16px 18px;
    width: 95%;
  }

  .stack-card-content {
    gap: 10px;
    flex-wrap: wrap;
  }

  .stack-card-icon {
    width: 38px;
    height: 38px;
    font-size: 1.3em;
  }

  .stack-card-number {
    font-size: 1.1em;
  }
}
</style>
