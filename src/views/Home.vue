<template>
  <div class="home">
    <b-pagination-nav
      :pages="pages"
      :number-of-pages="numberOfPages"
      v-model="currentPage"
      no-page-detect
      use-router
    ></b-pagination-nav>
    <b-form-checkbox v-model="showOddNumbers">Show odd numbers</b-form-checkbox>
  </div>
</template>

<script>
export default {
  name: "home",
  data() {
    return {
      showOddNumbers: false
    };
  },
  computed: {
    pages: function() {
      const pages = [];
      for (let i = 10; i <= 15; i++) {
        if (!this.showOddNumbers && i % 2 == 1) {
          continue;
        }
        pages.push({
          link: "" + i,
          text: "" + i
        });
      }
      return pages;
    },
    numberOfPages: function() {
      const len = this.pages.length;
      console.log(`numberOfPages is returning ${len}`);
      return len;
    },
    currentPage: {
      get: function() {
        const pages = this.pages;
        for (let i = 0; i < pages.length; i++) {
          const page = this.pages[i];
          if (this.$route.params.pageNumber == +page.text) {
            const ans = i + 1;
            console.log(`returning ${ans} from currentPage`);
            return ans;
          }
        }
        const index = 1;
        console.log(
          `couldn't find matching page: returning ${index} from currentPage`
        );
        return index;
      },
      set: function(newValue) {
        console.log(`Setting currentPage to ${newValue}`);
      }
    }
  },
  watch: {
    showOddNumbers: function(val) {
      console.log(`setting showOddNumbers to ${val}`);
    }
  }
};
</script>
