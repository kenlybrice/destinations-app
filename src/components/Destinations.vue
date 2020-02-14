<template>
  <div class="destinations">
    <!-- pagination controls -->
    <div class="destination__list-control">
      <Button
        @click.native="prevPage"
        text="Previous">
      </Button>
      <span>{{ pagination.activePage }}</span> of <span class="">{{ pagination.totalCount }}</span>
      <Button
        @click.native="nextPage"
        text="Next">
      </Button>
    </div>

    <!-- sorting controls -->
    <!-- <div class="">
      Sort by: 
      <Button
        @click.native="nextPage"
        text="Year">
      </Button>
      <Button
        @click.native="nextPage"
        text="A-Z">
      </Button>
    </div> -->
    
    <!-- destination list -->
    <div
      class="destination__list"
      :class="{
        'blur-effect': activeItem,
      }"
    >
      <DestinationButton
        v-for="(des, idx) in activeList"
        :key="idx"
        :item="{
          geopoliticalarea: des.geopoliticalarea,
          last_update_date: des.last_update_date,
          index: idx,
        }"
        @show-active-list-index-detail="showActiveListDetail"
      />
    </div>
    
    <!-- detail info -->
    <div
      v-if="activeItem"
      class="destination__details shadow"
      :class="{
        'active': activeItem,
      }">
      <div class="destination__details-content">
        <h2>
          <!-- <IconLocation /> -->
          <span v-html="activeItem.geopoliticalarea"></span>
        </h2>
        <div v-html="activeItem.destination_description"></div>
        <div v-html="activeItem.safety_and_security"></div>
        <div v-html="activeItem.health"></div>
        <div v-html="activeItem.local_laws_and_special_circumstances"></div>
        <div v-html="activeItem.travel_embassyAndConsulate"></div>
        <div v-html="activeItem.travel_transportation"></div>
      </div>
    </div>
  </div>
</template>

<script>
// Data
// ref: https://catalog.data.gov/dataset/country-travel-information
import destinationsData from '@/data/csi.json';

// Components
import DestinationButton from '@/components/ui/buttons/DestinationButton';
import Button from '@/components/ui/buttons/Button';
// import IconLocation from '@/components/ui/icons/IconLocation';

export default {
  name: 'Destinations',
  
  components: {
    Button,
    DestinationButton,
    // IconLocation,
  },
  
  data() {
    return {
      destinationsData,
      activeListIndex: null,
      pagination: {
        activePage: 1,
        totalCount: 0,
        countBy: 9,
      },
    };
  },
  
  computed: {
    activeList() {
      const list = this.destinationsData;
      const num1 = this.pagination.activePage * this.pagination.countBy;
      const num2 = num1 + this.pagination.countBy;
      return list.slice(num1, num2);
    },
    
    activeItem() {
      return this.activeList[this.activeListIndex];
    },
  },
  
  methods: {
    nextPage() {
      if (this.pagination.activePage < this.pagination.totalCount) {
        this.pagination.activePage += 1;
      }
      
      // reset index in order to hide content
      this.activeListIndex = null;
    },
    
    prevPage() {
      if (this.pagination.activePage > 1) {
        this.pagination.activePage -= 1;
      }
      
      // reset index in order to hide content
      this.activeListIndex = null;
    },
    
    setPaginationCount() {
      this.pagination.totalCount = Math.floor(this.destinationsData.length / this.pagination.countBy);
    },
    
    showActiveListDetail(val) {
      this.activeListIndex = val;
    },
  },
  
  mounted() {
    this.setPaginationCount();
  },
};
</script>
