<template>
  <div class="destination-list">
    <DestinationButton
      v-for="(des, idx) in activeList"
      :key="idx"
      :item="{
        geopoliticalarea: des.geopoliticalarea,
        last_update_date: des.last_update_date,
      }"
    />
    <div class="destination-list__control">
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
  </div>
</template>

<script>
// Data
// ref: https://catalog.data.gov/dataset/country-travel-information
import destinationsData from '@/data/csi.json';

// Components
import DestinationButton from '@/components/ui/buttons/DestinationButton';
import Button from '@/components/ui/buttons/Button';

export default {
  name: 'Destinations',
  
  components: {
    Button,
    DestinationButton,
  },
  
  data() {
    return {
      destinationsData,
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
      return list.slice(this.pagination.activePage, this.pagination.countBy);
    },
  },
  
  methods: {
    nextPage() {
      if (this.pagination.activePage < this.pagination.totalCount) {
        this.pagination.activePage += 1;
      }
    },
    
    prevPage() {
      if (this.pagination.activePage > 1) {
        this.pagination.activePage -= 1;
      }
    },
    
    setPaginationCount() {
      this.pagination.totalCount = Math.floor(this.destinationsData.length / this.pagination.countBy);
    },
  },
  
  mounted() {
    this.setPaginationCount();
  },
};
</script>

<style>
.destination-list {
  display: flex;
  flex-wrap: wrap;
  height: ;
  max-width: 1024px;
  margin: 100px auto;
  width: 100%;
}
</style>