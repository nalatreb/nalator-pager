<template>
  <div id="app">
    <ul>
      <li v-for="(text, index) in paginated" :key="index">{{ text }}</li>
    </ul>
    <br>
    <NalatorPager :page="page" :listCount="list.length" :offset="offset" @pageClicked="setPage" />
  </div>
</template>

<script>

export default {
  name: 'app',
  components: {
    NalatorPager: require('./components/NalatorPager.vue').default
  },
  data: function () {
    return {
      list: [],
      page: 1,
      offset: 10
    }
  },
  methods: {
    setPage (payload) {
      this.page = payload.page
    }
  },
  computed: {
    paginated: function () {
      return this.list.slice((this.page - 1) * this.offset, this.page * this.offset)
    }
  },
  created () {
    for (let i = 1; i < 1368; i++) {
      this.list.push(`${i} number`)
    }
  }
}
</script>

<style lang="scss">

</style>
