<template>
  <div class="destinations">
    <!-- pagination controls -->
    <div
      class="destination__list-control">
      <Button
        @click.native="prevPage"
        text="Previous">
      </Button>
      <span>{{ pagination.activePage }}</span> of <span class="">{{ pagination.pageCount }}</span>
      <Button
        @click.native="nextPage"
        text="Next">
      </Button>
      <Button
        @click.native="updateView"
        text="Show Only Favorites">
      </Button>
    </div>
    
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
          id: des.id,
          isFavorite: favoriteIds.indexOf(des.id) > -1,
        }"
        @show-active-list-index-detail="showActiveListDetail"
        @update-favorite="updateFavorite"
      />
      <div
        v-if="activeList && activeList.length === 0"
        class="no-results">
        <span>List is empty!</span>
      </div>
    </div>
    
    <!-- detail info -->
    <div
      v-if="activeItem"
      class="destination__content shadow"
      :class="{
        'active': activeItem,
        'favorite': favoriteIds.indexOf(activeItem.id) > -1,
      }">
      <div class="destination__content-inner">
        <IconClose
          @click.native="closeDetailModal" />
        <h2 v-html="activeItem.geopoliticalarea"></h2>
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
import IconClose from '@/components/ui/icons/IconClose';

export default {
  name: 'Destinations',
  
  components: {
    Button,
    DestinationButton,
    IconClose,
  },
  
  data() {
    return {
      activeListIndex: null,
      destinationsData,
      favoriteIds: [],
      isShownOnlyFavorites: false,
      pagination: {
        activePage: 1,
        pageCount: 1,
        countBy: 9,
      },
      appStarted: false,
    };
  },
  
  watch: {
    isShownOnlyFavorites() {
      this.prepData();
    },
  },
  
  computed: {
    activeList() {
      const num1 = this.pagination.activePage * this.pagination.countBy;
      const num2 = num1 + this.pagination.countBy;

      return (this.filteredData.length > this.pagination.countBy)
        ? this.filteredData.slice(num1, num2)
        : this.filteredData;
    },
    
    activeItem() {
      return this.activeList[this.activeListIndex];
    },
    
    filteredData() {
      return (this.isShownOnlyFavorites)
        ? this.destinationsData.filter((i) => this.favoriteIds.indexOf(i.id) > -1)
        : this.destinationsData;
    },
  },
  
  methods: {
    nextPage() {
      if (this.pagination.activePage < this.pagination.pageCount) {
        this.pagination.activePage += 1;
      }
      
      this.closeDetailModal();
    },
    
    prevPage() {
      if (this.pagination.activePage > 1) {
        this.pagination.activePage -= 1;
      }
      
      this.closeDetailModal();
    },
    
    closeDetailModal() {
      // reset index in order to hide content
      this.activeListIndex = null;
    },
    
    prepData() {
      // reset page pagination
      this.pagination.activePage = 1;
      // set pagination count
      const num = Math.floor(this.filteredData.length / this.pagination.countBy);
      // set 1 incase Math.floor return 0
      this.pagination.pageCount = num || 1;
      // create unique id for each each to better target individual objects
      if (!this.appStarted) this.filteredData.map((i, idx) => i.id = idx);
    },
    
    showActiveListDetail(val) {
      this.activeListIndex = val;
    },
    
    updateView() {
      this.isShownOnlyFavorites = !this.isShownOnlyFavorites;
    },
    
    updateFavorite(data) {
      if (data.type === 'add' && this.favoriteIds.indexOf(data.id) === -1) {
        this.favoriteIds.push(data.id);
      } else if (data.type === 'remove') {
        this.favoriteIds.pop(data.id);
      }
    },
  },
  
  mounted() {
    this.prepData();
    this.appStarted = true;
  },
};
</script>
