<template>
  <nuxt-link
    :class="{ 'bg-primaryLight': isActive, 'ml-3': index == 1 }"
    class="px-6 py-3 rounded flex items-center justify-center nav-item"
    :to="path"
  >
    <component :is="icon" />
    <span class="ml-8 font-medium text-xl">
      {{ name }}
    </span>
  </nuxt-link>
</template>

<script>
export default {
  name: 'SidebarItem',
  components: {
    Home: () => import('~/assets/svg/home.svg'),
  },
  props: {
    name: {
      type: String,
      required: true,
    },
    iconType: {
      type: String,
      required: true,
    },
    path: {
      type: String,
      required: true,
    },
    index: {
      type: Number,
      required: true
    },
  },
  data() {
    return {}
  },
  computed: {
    icon() {
      switch (this.iconType.toLowerCase()) {
        case 'home': {
          return 'Home'
        }
        case 'address': {
          return 'Address'
        }
        default: {
          return ''
        }
      }
    },
    isActive() {
      return this.$route.name;
    },
  },
}
</script>

<style lang="css" scoped>
.nav-item:not(:first-child) {
  margin-top: 0.7rem;
}
</style>
