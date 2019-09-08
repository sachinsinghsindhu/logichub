<template>
  <div class="table-container">
      <div class="row" v-for="(row, index) in data" @click="openTab(index)">
        <div class="col" v-for="(col, colIndx) in format">
          <div>{{row[col]}}</div>
        </div>
      </div>
  </div>
</template>

<script>
import { constants } from 'crypto';

export default {
  name: 'tableComp',
  components: {
  },
  data: function () {
    return {
    }
  },
  props: {
    data: {
      type: Array,
      required: true,
    },
    format: {
      type: Array,
      required: true,
    },
  },
  methods: {
    openTab(idx) {
      this.$emit('openTab',{
        index: idx,
      });
    }
  }
}
</script>

<style>
.rows-container {
  height: auto;
  width: 100%;
}
.row {
  width: 100%;
  height: 50px;
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.row:nth-child(odd) {
  background-color: rgb(237, 235, 228);
}
.col {
  display: inline-flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  margin-left: 20px;
  margin-right: 20px;
}
</style>
