<template>
  <div>
    <main-page-hero>
      <slot name="title"></slot>
    </main-page-hero>
    <slot name="default"></slot>
  </div>
</template>

<script>
import MainPageHero from '../components/MainPageHero'

export default {
  components: { MainPageHero }
}
</script>
