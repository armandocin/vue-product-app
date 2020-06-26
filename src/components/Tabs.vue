<template>
    <div>
        <span class="tab"
              :class="{activeTab: selectedTab === tab}"
              v-on:click="selectedTab = tab"
              v-for="(tab, index) in tabs"
              :key="index"
          >
            {{ tab }}
        </span>
    </div>
</template>

<script>
  export default {
    name: 'Tabs',
    props: {
      tabs: {type: Array}
    },
    data() {
      return {
        selectedTab: this.tabs[0]
      }
    }
  }
</script>

<style scoped>
    .tab {
        margin-left: 20px;
        cursor: pointer;
    }

    .activeTab {
        color: #16C0B0;
        text-decoration: underline;
    }
</style>
