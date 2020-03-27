<template>
  <div id="gallery">

    <div id="filters">
      <form>
        <fieldset>
            <legend>Filter</legend>
            <span>
                <input type="radio" id="all" name="filters" checked v-on:click="updateFilter('all')" />
                <label for="all">All</label>
            </span>
            <span>
                <input type="radio" id="small-birds" name="filters" v-on:click="updateFilter('small-birds')" />
                <label for="animals">Small birds</label>
            </span>
            <span>
                <input type="radio" id="big-birds" name="filters" v-on:click="updateFilter('big-birds')" />
                <label for="big-birds">Big birds</label>
            </span>
        </fieldset>
      </form>
    </div>

    <div id="thumbnails">
      <transition-group name="thumbnailfade" tag="div">
        <img v-for="thumb in filteredImages"
           :key="thumb.id"
           @click="showLightbox(thumb.name)"
           :src="thumbnailDir + thumb.name"
           :alt="thumb.alt"
           :title="thumb.alt"/>
      </transition-group>
    </div>

    <lightbox id="mylightbox"
    ref="lightbox"
    :images="images"
    :filter="galleryFilter"
    :directory="thumbnailDir"
    :timeoutDuration="5000"
    ></lightbox>

  </div>
</template>

<script>
import Lightbox from 'vue-my-photos'

var images = [{'name':'bird1.jpg', 'alt':'A bird', 'filter':'small-birds', 'id':1 },
              {'name':'bird2.jpg', 'alt':'Birdie', 'filter':'small-birds', 'id':2 },
              {'name':'bird3.jpg', 'alt':'Yup, same bird', 'filter':'small-birds', 'id':3 },
              {'name':'bird4.jpg', 'alt':'Bird with fish', 'filter':'small-birds', 'id':4 },
              {'name':'bird5.jpg', 'alt':'Not so colorful bird', 'filter':'small-birds', 'id':5 },
              {'name':'bird6.jpg', 'alt':'Bird with orange and blue', 'filter':'small-birds', 'id':6 },
              {'name':'duck1.jpg', 'alt':'Duck', 'filter':'big-birds', 'id':7 },
              {'name':'duck2.jpg', 'alt':'Two ducks!', 'filter':'big-birds', 'id':8 }];

export default {
  name: 'Gallery',
  data () {
    return {
      thumbnailDir: '/img/',
      images: images,
      galleryFilter: 'all'
    }
  },
  methods: {
    showLightbox: function(imageName) {
      this.$refs.lightbox.show(imageName);
    },
    updateFilter(filterName) {
      this.galleryFilter = filterName;
    }
  },
  computed: {
    filteredImages: function() {
      if (this.galleryFilter === 'all') {
        return this.images;
      } else {
        return this.images.filter(image => image.filter === this.galleryFilter);
      }
    }
  },
  components: {
    Lightbox
  }
}
</script>

<style>
#thumbnails {
    margin-left: 150px;
    margin-right: 150px;
}
img {
  width: 400px;
  height: 300px;
  margin: 30px;
  border-radius: 3px;
  cursor: pointer;
  transition: all 0.4s ease;
  object-fit: contain;
}
#filters {
  width: 500px;
  margin: 30px auto;
}
#filters span {
  margin: 15px;
}
.thumbnailfade-leave-active,
.thumbnailfade-enter-active {
  transition: all 0.4s ease;
}
.thumbnailfade-enter-active {
  transition-delay: 0.4s;
}
.thumbnailfade-enter,
.thumbnailfade-leave-to {
  opacity: 0;
}
</style>
