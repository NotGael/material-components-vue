<template>
  <aside
    class="mdc-drawer mdc-drawer--persistent"
    @MDCPersistentDrawer:close="model = false">
    <nav class="mdc-drawer__drawer">
      <slot name="toolbarSpacer" />
      <slot name="header" />
      <slot />
    </nav>
  </aside>
</template>

<script>
import { MDCPersistentDrawer } from '@material/drawer'

import { baseComponentMixin, themeClassMixin } from '../../base'

export default {
  mixins: [baseComponentMixin, themeClassMixin],
  model: {
    prop: 'open',
    event: 'change'
  },
  props: {
    open: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      mdcPersistentDrawer: undefined
    }
  },
  computed: {
    model: {
      get () {
        return this.open
      },
      set (value) {
        this.$emit('change', value)
      }
    }
  },
  watch: {
    open () {
      this.mdcPersistentDrawer.open = this.open
    }
  },
  mounted () {
    this.mdcPersistentDrawer = MDCPersistentDrawer.attachTo(this.$el)
    this.mdcPersistentDrawer.open = this.open
  },
  beforeDestroy () {
    this.mdcPersistentDrawer.destroy()
  }
}
</script>
