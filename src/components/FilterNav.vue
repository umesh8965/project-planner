<template>
    <nav class="filter-nav">
        <button 
        @click="updateFilter('all')"
        :class="{ active : currentstate === 'all'}">
            View All
        </button>
        <button 
        @click="updateFilter('completed')"
        :class="{ active : currentstate === 'completed'}">
            Completed
        </button>
        <button 
        @click="updateFilter('ongoing')"
        :class="{ active : currentstate === 'ongoing'}">
            Ongoing
        </button>
    </nav>
</template>

<script>
export default {
    props :[ 'currentstate' ],
    methods : {
        updateFilter(selectfilter){
            this.$emit("filterChange", selectfilter)
        }
    }
}
</script>

<style>
 .filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
  }
  .filter-nav button.active {
    color: #555;
  }
</style>