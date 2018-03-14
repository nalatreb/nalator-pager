<template>
  <nav class="pagination" role="navigation" aria-label="pagination">
    <ul class="pagination-list">
      <li>
        <a class="pagination-link" @click="onPageClicked(1)">First</a>
      </li>
      <li v-if="pageCount < 6 || page < 4" v-for="n in 5" :key="n">
        <a class="pagination-link" :class="{ 'is-current': n === page }" @click="onPageClicked(n)">{{ n }}</a>
      </li>
      <li v-if="page >= 4 && page + 2 <= pageCount" v-for="n in range(page - 2, page + 2)" :key="n">
        <a class="pagination-link" :class="{ 'is-current': n === page }" @click="onPageClicked(n)">{{ n }}</a>
      </li>
      <li v-if="page > pageCount - 2" v-for="n in range(pageCount - 4, pageCount)" :key="n">
        <a class="pagination-link" :class="{ 'is-current': n === page }" @click="onPageClicked(n)">{{ n }}</a>
      </li>
      <li>
        <a class="pagination-link" @click="onPageClicked(pageCount)">Last</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'NalatorPaginator',
  props: {
    listCount: Number,
    page: Number,
    offset: Number
  },
  computed: {
    pageCount () {
      return Math.ceil(this.listCount / this.offset)
    }
  },
  methods: {
    onPageClicked (page) {
      if (this.page === page) {
        return
      }
      this.$emit('pageClicked', { page })
    },
    range: function (min, max) {
      let array = []
      let j = 0
      for (let i = min; i <= max; i++) {
        array[j] = i
        j++
      }
      return array
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
