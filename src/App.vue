<template>
  <div class="container">
    <button class="btn btn-primary"
            v-for='tab in tabs'
            :key='tab'
            :class="[{active: currentTab  === tab}]"
            @click="currentTab = tab"
    >{{tab}}
    </button>
    <transition enter-active-class="animated bounceInRight"
                leave-active-class="animated bounceOutRight"
                name="component-fade" mode="out-in"><keep-alive><tab-posts class="tab" v-bind:is="currentTabComponent"></tab-posts></keep-alive></transition>
  </div>
</template>

<script>
  import tabposts from './components/tab.vue'; 
  import archive from './components/archive.vue'; 

export default {
  name: 'app',
  data () {
    return {
      currentTab: 'Posts',
      tabs: ['Posts', 'Archive']
    }
  },
  components: {
    'tab-posts': tabposts,
    'tab-archive': archive
  },
  computed: {
    currentTabComponent: function () {
      return 'tab-' + this.currentTab.toLowerCase()
    }
  }
}
</script>

<style>
/* .component-fade-enter-active, .component-fade-leave-active {
  transition: all .5s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.component-fade-enter, .component-fade-leave-to
.component-fade-leave-active до версии 2.1.8 {
  transform: translateX(10px);
  opacity: 0;
} */
</style>
