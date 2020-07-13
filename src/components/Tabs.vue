<template>
    <div class="tabs-control">
        <ul class="tab-buttons">
            <li
                class="tab-button"
                :class="{'tab-button--active': tab.active}"
                v-for="(tab, index) in tabs"
                :key="tab.tabId"
                v-on:click="selectTab(index)"
            >
                {{ tab.title }}
            </li>
        </ul>
        <div class="tabs">
            <slot></slot>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'Tabs',
    props: {
      defaultActiveTab: [String, Number, Object]
    },
    data () {
      return {
        activeTabIndex: 0,
        tabs: []
      }
    },
    methods: {
      addTab (item) {
        const index = this.$slots.default.indexOf(item.$vnode);
        this.tabs.splice(index, 0, item);
      },
      selectTab (index) {
        this.changeTab(this.activeTabIndex, index)
      },
      activateTab (index) {
        this.activeTabIndex = index
        let tab = this.tabs[index]
        tab.active = true
        this.$emit('input', tab.title)
      },
      changeTab (oldIndex, newIndex) {
        let oldTab = this.tabs[oldIndex] || {}
        let newTab = this.tabs[newIndex]

        if (newTab.disabled) return

        this.activeTabIndex = newIndex
        oldTab.active = false
        newTab.active = true
      },
      findTabAndActivate (tabNameOrIndex) {
        let indexToActivate = this.tabs.findIndex((tab, index) => tab.title === tabNameOrIndex || index === tabNameOrIndex)
          // if somehow activeTabIndex is not reflected in the actual vue-tab instance, set it.
          if (indexToActivate === this.activeTabIndex && !this.tabs[this.activeTabIndex].active) {
            this.tabs[this.activeTabIndex].active = true
          }
        if (indexToActivate !== -1) {
          this.changeTab(this.activeTabIndex, indexToActivate)
        } else {
          this.changeTab(this.activeTabIndex, 0)
        }
      }
    },
    watch: {
      tabs (newList) {
        if (newList.length > 0 && !this.defaultActiveTab) {
          if (newList.length <= this.activeTabIndex) {
            this.activateTab(this.activeTabIndex - 1);
          } else {
            this.activateTab(this.activeTabIndex);
          }
        }
        if (newList.length > 0 && this.defaultActiveTab) {
          this.findTabAndActivate(this.defaultActiveTab)
        }
      },
      defaultActiveTab (newVal) {
        this.findTabAndActivate(newVal)
      }
    }
  }
</script>

<style scoped>
    .tab-buttons {
        display: flex;
        list-style: none;
        padding: 0;
        margin: 0;
    }

    .tab-button {
        padding: 6px 10px;
        border-top-left-radius: 3px;
        border-top-right-radius: 3px;
        border: 1px solid #ccc;
        cursor: pointer;
        background: #f0f0f0;
        margin-bottom: -1px;
        margin-right: -1px;
    }
    .tab-button:hover {
        background: #e0e0e0;
    }
    .tab-button--active {
        background: #e0e0e0;
    }
</style>
