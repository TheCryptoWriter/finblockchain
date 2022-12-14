<template>
  <section :class="`hero is-medium hero-theme-${computedTheme}`">
    <img
      class="hero-bg-img"
      :src="responsiveImage.src"
      :lazy="false"
      :srcset="responsiveImage.srcSet"
    />
    <div class="hero-body">
      <div class="container">
        <h1 class="title animated fadeInUp">
          {{ title }}
        </h1>
        <h2 class="subtitle animated fadeInUp slower">
          {{ subtitle }}
        </h2>
        <h2 class="lead animated fadeInDown">
          {{ lead }}
        </h2>
        <br />
        <div
          v-if="$slots.default"
          class="under-subtitle animated fadeInDown slower"
        >
          <slot />
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: 'SiteHero',
  props: {
    title: { type: String, default: '' },
    subtitle: { type: String, default: '' },
    lead: { type: String, default: '' },
    image: { type: String, default: '' },
    color: { type: String, default: '#469af0' },
    theme: { type: String, default: '' }
  },
  computed: {
    responsiveImage() {
      if (this.image.indexOf('/uploads') === 0) {
        return require(`~/assets${this.image}`)
      }
      return { src: this.image, srcSet: '' }
    },
    computedTheme() {
      if (this.theme === '' && this.$siteConfig.hero.theme) {
        return this.$siteConfig.hero.theme
      }
      return this.theme || 'mist'
    }
  }
}
</script>

<style lang="scss" scoped>
.hero {
  margin-top: 52px;
  background-size: cover !important;
  background-position: center;
  text-align: center;
  overflow: hidden;
  position: relative;
}

.title {
  margin-bottom: 0 !important;
  @media (max-width: 768px) {
    font-weight: bold;
    font-size: 34px;
    line-height: 40px;
    padding-bottom: 20px;
  }

  @media (min-width: 768px) {
    font-size: 3.2rem;
    font-size: 46px;
    line-height: 54px;
    padding-bottom: 30px;
  }
}

.subtitle,
.lead,
.under-subtitle {
  padding: 0;
  margin: 0;
}

.subtitle {
  margin-bottom: 0 !important;
  @media (max-width: 768px) {
    font-size: 1.5rem;
    padding-bottom: 10px;
  }

  @media (min-width: 768px) {
    font-size: 2rem;
    padding-bottom: 20px;
  }
}

.lead {
  margin-bottom: 0 !important;
  @media (max-width: 768px) {
    font-size: 0.75rem;
    padding-bottom: 0px;
  }
  @media (min-width: 768px) {
    font-size: 1rem;
    padding-bottom: 10px;
  }
}

.under-subtitle {
  display: inline-block;
  font-size: 0.8rem;
  border-top: 2px solid $primary;
  padding-top: 5px;
}

.opti-image {
  opacity: 0;
}

.opti-image-loaded {
  opacity: 0.12;
  animation: blurIn 4.5s ease;
}
</style>
<style lang="scss">
.hero {
  .hero-bg-img {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    object-fit: cover;
    width: 100%;
    height: 100%;
  }

  .opti-image {
    opacity: 0;
  }

  .opti-image-loaded {
    opacity: 1;
  }
}

.hero-theme-mist {
  .hero-bg-img {
    filter: grayscale(1);
  }

  .opti-image-loaded {
    opacity: 0.12;
    animation: blurInGrayscale 4.5s ease;
  }
}

.hero-theme-dark,
.hero-theme-light {
  &.hero:after {
    content: '';
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.25);
    position: absolute;
  }

  .hero-body {
    position: relative;
    z-index: 2;
  }
}

.hero-theme-dark {
  .title,
  .subtitle,
  .lead,
  .under-subtitle,
  .under-subtitle strong {
    color: white;
  }
}

.hero-theme-light.hero {
  &:after {
    background: rgba(255, 255, 255, 0.6);
  }

  .title,
  .subtitle,
  .lead,
  .under-subtitle,
  .under-subtitle strong {
    text-shadow: 1px 1px 2px white;
  }
}
</style>
