<template>
  <nav class="filter-nav">
    <button 
      @click="updateFilter('all')"
      :class="{ active: current === 'all' }"
    >View all
    </button>

    <button 
      @click="updateFilter('completed')"
      :class="{ active: current === 'completed' }"
    >Completed
    </button>

    <button 
      @click="updateFilter('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: [ 'current' ],

  methods: {
    updateFilter(by) {
      this.$emit('filterChange', by)
    }
  }
}
</script>

<style>
  .filter-nav button {
    background: none;
    border: 0;
    color: #808080;
    cursor: pointer;
    outline: none;
    padding: 5px 0;
    margin-left: 15px;
  }

  .filter-nav button:first-child {
    margin-left: 10px;
  }

  .filter-nav button.active {
    color: #000;
    /* text-decoration: underline; */
    border-bottom: 2px solid #00ce89;
  }
</style>