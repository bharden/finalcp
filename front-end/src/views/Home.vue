<template>
  <div class="home">
    <section class="sheet-music">
      <div class="image" v-for="item in items" :key="item.id">
        <h2>{{item.title}}</h2>
        <p>{{item.artist}}</p>
        <p>{{item.genre}}</p>
        <img :src="item.path" />
      </div>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
export default {
  name: 'Home',
  data() {
  return {
   items: [],
  }
},
created() {
  this.getItems();
},
methods: {
  async getItems() {
    try {
      let response = await axios.get("/api/items");
      this.items = response.data;
      return true;
    } catch (error) {
      console.log(error);
    }
  },
}
}
</script>

<style scoped>
.image h2 {
  font-size: 15px;
}
.image p {
  font-size: 10px;
  padding: 1px;
}

/* Masonry */
*,
*:before,
*:after {
  box-sizing: inherit;
}

. {
  column-gap: 1.5em;
}

.image {
  margin: 0 0 1.5em;
  display: inline-block;
  width: 100%;
  align-items: center;
}

.image img {
  width: 50%;
  height: 50%
}

/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .sheet-music {
    column-count: 4;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .sheet-music {
    column-count: 3;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .sheet-music {
    column-count: 2;
  }
}
</style>
