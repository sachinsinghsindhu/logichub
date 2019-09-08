<template>
  <div id="app">
    <tabsComp class="tabs-container"
      :data="events"
      :tabs="tabs"
      :selectedTab="selectedTab"
      @closeTab="closeTabFun"
      @selectTab="selectTabFun"
    ></tabsComp>
    <div class="event-container">
      <tableComp class="events"
        :data="events"
        :format="eventsColFormat"
        @openTab="openTabFun"
      ></tableComp>
      <tableComp class="event-data"
        :data="(selectedTab >= 0 || selectedTab < events.length) ? eventData[tabs[selectedTab]] : []"
        :format="dataColFormat"
      >
      </tableComp>
    </div>
  </div>
</template>

<script>
import tableComp from '../src/components/tableComponent';
import tabsComp from '../src/components/tabsComponent';
import { events, eventsColFormat, eventData, dataColFormat } from '../src/static/data';
export default {
  name: 'app',
  components: {
    tableComp,
    tabsComp,
  },
  data: function () {
    return {
      tabs: [],
      selectedTab: 0,
      events: [],
      eventsColFormat: [],
      data: [],
      dataColFormat: [],
    }
  },
  methods: {
    openTabFun(payload) {
      if(this.tabs.includes(payload.index)) {
        this.selectedTab = this.tabs.indexOf(payload.index);
      } else {
        this.tabs.push(payload.index);
        this.selectedTab = this.tabs.length - 1;
      }
    },
    closeTabFun(payload) {
      if (this.tabs.length == 1) return;
      this.tabs.splice(payload.index, 1);
      if (this.selectedTab >= this.tabs.length) {
        this.selectedTab = this.tabs.length - 1;
      }
    },
    selectTabFun(payload) {
      this.selectedTab = payload.index;
    }
  },
  beforeMount() {
    this.events = events;
    this.eventsColFormat = eventsColFormat;
    this.eventData = eventData;
    this.dataColFormat = dataColFormat;
    this.tabs.push(0);
    this.tabs.push(1);
  }
}
</script>

<style>
#app {
  width: 100vw;
  height: 80vh;
  /* display: flex;
  flex-direction: row; */
}
.tabs-container {
  position: relative;
  width: 70%;
  height: 50px;
  left: 30%;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
}
.event-container {
  width: 100vw;
  height: 80vh;
  display: flex;
  flex-direction: row;
}
.events {
  width: 30%;
  height: 100%;
  overflow-y: scroll;
}
.event-data {
  width: 70%;
  height: 100%;
  overflow-y: scroll;
}

</style>
