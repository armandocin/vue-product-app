<template>
    <div class="tab"
         :id="`p-${this.tabId}`"
         :aria-labelledby="`t-${this.tabId}`"
         role="tabpanel"
         v-show="active"
    >
        <slot></slot>
    </div>
</template>

<script>
  export default {
    name: 'Tab',
    props: {
      title: {
        type: String,
        default: ''
      },
      id: String
    },
    mounted () {
      this.$parent.addTab(this)
    },
    data () {
      return {
        active: false
      }
    },
    computed: {
      isValidParent() {
        return this.$parent.$options.name === 'Tabs'
      },
      tabId () {
        return this.id ? this.id : this.title
      }
    }
  }
</script>

<style scoped>
.tab {
    border: 1px solid #ccc;
    padding: 10px;
}
</style>
