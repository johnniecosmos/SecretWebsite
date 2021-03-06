<template>
  <div class="media-card" :color="color">
    <div class="media-card__tag" :style="{ color: `var(--${color}-color)` }">
      <slot>{{ tag }}</slot>
    </div>
    <h4>{{ title }}</h4>
    <separator small space-small></separator>
    <div class="media-card__image">
      <g-image :src="require(`!!assets-loader!@images/${src}`)"></g-image>
    </div>
    <div class="media-card__footer">
      <g-link :to="to" class="media-card__footer__cta-btn">{{ cta }}</g-link>
    </div>
  </div>
</template>

<script>
import BlogAuthor from '@/components/blog/BlogAuthor'

const colors = {
  "dev": "purple",
  "nodes": "yellow",
  "announcement": "green",
  "blockchain": "peach",
  "community": "turquoise",
  "cosmos": "pink",
  "design": "red",
  "governance": "orange",
  "introduction": "blue",
  "privacy": "purple",
  "secret apps": "green",
  "solutions": "green",
  "": "blue",
  "podcast": "red",
  "video": "turquoise",
  "blog post": "yellow"
}

export default {
  components: { BlogAuthor },
  props: {
    tag: {
      type: String,
      required: false,
      default: ''
    }, 
    title: {
      type: String,
      required: false
    },
    src: {
      type: String,
      required: false
    },
    to: {
      type: String,
      required: false
    },
    cta: {
      type: String,
      required: false,
      default: 'Open the Secret'
    }
  },
  data() {
    return {
      color: ''
    }
  },
  created() {
    this.color = this.getColor()
  },
  methods: {
    getColor() {
      return colors[this.tag.toLowerCase()]
    }
  }
}
</script>

<style lang="scss" scoped>
$-heading-height: 85px;
$-badge-height: 59px;
$-card-min-height: 415px;

.media-card {
  $root: &;
  display: grid;
  grid-template-rows: 26px 1fr 22px 185px 62px;
  position: relative;
  border: 3px solid;
  border-color: var(--theme-fg);
  border-radius: $gutter;
  height: 100%;
  min-height: rem($-card-min-height);
  padding: $gutter;
  transition: 0.5s ease;
  -webkit-transition: 0.5s ease;
  @each $name, $color in $secondary-colors {
    &[color=#{$name}] a:hover {
      color: var(--#{$name}-color);
    }
  }
  a {
    text-decoration: none;
  }

  &__tag {
    text-transform: uppercase;
    line-height: 26px;
  }

  &__heading {
    width: 100%;
    height: rem($-heading-height);
  }

  &__badge {
    position: absolute;
    top: $-heading-height - ($-badge-height / 2);
    right: $gutter;
  }

  &__body {
    padding: $gutter;
  }

  &__footer {
    padding-top: $gutter;
    a:not([aria-hidden=true]) {
      display: block;
      width: 100%;
      border-radius: 10px;
      padding: 13px;
      text-align: center;
      color: var(--theme-bg);
      background-color: var(--theme-fg);
      font-weight: bold;
      text-decoration: none;
      font-size: $secondary-font-size;
    }
  }
  &:hover {
    transform: scale(1.05);
    -webkit-transform: scale(1.05);
  }
  @media (min-width: 768px) and (max-width: 1007px) {
    //min-height: rem(360px);
    grid-template-rows: 26px 96px 22px 1fr 62px;
    &__header {
      //margin-bottom: $gutter;
      min-height: rem(104px);
    }
  } 
  @media (min-width: 1008px) and (max-width: 1199px) {
    min-height: rem(360px);
    grid-template-rows: 26px 1fr 22px 149px 62px;
  } 
  @include respond-to("small and down") {
    width: 100%;
    grid-template-rows: auto;
    &__image {
      img {
        width: 100%;
      }
    }
  }
}
</style>
