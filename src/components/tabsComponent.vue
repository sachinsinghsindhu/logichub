<template>
  <div class="tabs-container">
      <div class="tab" v-for="(tab, tabIndx) in tabs"
        :class="{'selected': selectedTab == tabIndx}"
        @mouseenter="showCloseButton"
        @mouseleave="hideCloseButton"
        @click="selectTab(tabIndx)"
        >
        <div class="tab-elem">{{data[tab].eventType}}</div>
        <div class="tab-elem close" @click.stop="closeTab(tabIndx)">&#10006;</div>
      </div>
  </div>
</template>

<script>
import { eventsColFormat } from '../static/data';

export default {
  name: 'tabComp',
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
    tabs: {
        type: Array,
        required: true,
    },
    selectedTab: {
        type: Number,
        required:true,
    }
  },
  methods: {
      showCloseButton(event) {
          const target = event.target;
          target.classList.toggle('hovered');
          target.querySelector('.close').style.opacity = 1;
      },
      hideCloseButton(event) {
          const target = event.target;
          target.classList.toggle('hovered');
          target.querySelector('.close').style.opacity = 0;
      },
      closeTab(indx) {
          this.$emit('closeTab', {
              index: indx,
          });
      },
      selectTab(indx) {
          this.$emit('selectTab', {
              index: indx,
          });
      }
  }
}
</script>

<style>
.tab {
    display: inline-flex;
    flex-direction: row;
    box-sizing: border-box;
    width: 20%;
    height: 100%;
    padding-left: 2%;
    padding-right: 2%;
    justify-content: center;
    align-items: center;
    flex-shrink: 1;
}
.tab.hovered {
     background-color: rgb(209, 219, 189);
}
.tab.selected {
    background-color: aquamarine;
}
.tab-elem {
    display: inline-block;
    margin-right: 10px;
}
.close {
    opacity: 0;
}

</style>
