<template>
  <button
    class="mr10 mb5 bg-transparent brdr-1 brdr-circle brdr-c-transparent relative inline-flex pointer color"
    @click="switchFilter(id, label)"
    :class="{ active: active }"
    :aria-label="$t('Select color ') + label"
  >
    <div
      class="absolute brdr-circle brdr-1 brdr-c-alto block color-inside"
      :style="colorFrom(label)"
    />
  </button>
</template>

<script>
import { coreComponent } from 'lib/themes'

export default {
  data () {
    return {
      active: false
    }
  },
  beforeMount () {
    if (this.$route.name !== 'product') {
      this.$bus.$on('filter-changed-' + this.context, (filterOption) => {
        if (filterOption.attribute_code === this.code) {
          if (filterOption.id === this.id) {
            if (this.active) {
              this.active = false
            } else {
              this.active = true
            }
          } else {
            this.active = false
          }
          // filterOption.id === this.id ? this.active = true : this.active = false
        }
      })
    }
  },
  methods: {
    colorFrom (label) {
      if (label.indexOf(',') >= 0) {
        return 'background: linear-gradient(' + label + ')'
      } else {
        return 'background-color: ' + label
      }
    },
    switchFilter (id, label) {
      this.$bus.$emit('filter-changed-' + this.context, { attribute_code: this.code, id: id, label: label })
    }
  },
  mixins: [coreComponent('core/ColorButton')]
}
</script>

<style lang="scss" scoped>
  @import '~theme/css/base/global_vars';
  $lightgray-secondary: map-get($colors, lightgray-secondary);
  $emperor: map-get($colors, emperor);

  .color {
    width: 40px;
    height: 40px;

    &:hover,
    &:focus {
      border-color: $lightgray-secondary;
    }

    &.active {
      border-color: $emperor;
    }
  }

  .color-inside {
    width: 34px;
    height: 34px;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%)
  }
</style>
