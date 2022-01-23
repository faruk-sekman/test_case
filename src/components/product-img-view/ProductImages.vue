<template>
  <div class="hello">
    <div class="row mx-0">
      <div class="col-12 full-image">
        <img class="img-fluid mx-auto d-block" alt="full-product-image" :src="selectImage"/>
      </div>
      <div class="col-12">
        <div class="row mx-0 h-100">
          <div class="col-1 d-flex align-items-center h-100">
            <button @click="previousImage($event)">
              <i class="fa fa-chevron-left" />
            </button>
          </div>
          <div class="col-10 mx-auto">
            <div class="thumbnail-slide text-center">
              <div class="thumbnail" :key="index" v-for="(image, index) in images">
                <img @click="setSelectImage(image)" class="img-thumbnail p-0" :src="image" :class="{ active: selectImage == image }"/>
              </div>
            </div>
          </div>
          <div class="col-1 d-flex align-items-center h-100">
            <button @click="nextImage($event)">
              <i class="fas fa-chevron-right"></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductImages',
  data () {
    return {
      selectImage: ''
    }
  },
  methods: {
    setSelectImage (image) {
      this.selectImage = image
    },
    nextImage (e) {
      const maxIndex = this.images.length - 1
      const currentIndex = this.images.indexOf(this.selectImage)
      const nextIndex = currentIndex + 1
      // eslint-disable-next-line no-unused-expressions
      nextIndex <= maxIndex ? this.setSelectImage(this.images[nextIndex]) : this.setSelectImage(this.images[0]);
      nextIndex <= maxIndex
          ? e.currentTarget.closest('.h-100').previousElementSibling.querySelector(".active").parentElement.nextElementSibling.scrollIntoView({behavior: 'smooth', block: 'start'})
          : e.currentTarget.closest('.h-100').previousElementSibling.querySelectorAll(".thumbnail")[0].scrollIntoView({behavior: 'smooth', block: 'start'})
    },
    previousImage (e) {
      const maxIndex = this.images.length - 1
      const currentIndex = this.images.indexOf(this.selectImage)
      const previousIndex = currentIndex - 1
      // eslint-disable-next-line no-unused-expressions
      previousIndex >= 0 ? this.setSelectImage(this.images[previousIndex]) : this.setSelectImage(this.images[maxIndex]);
      previousIndex >= 0
          ?  e.currentTarget.closest('.h-100').nextElementSibling.querySelector('.active').parentElement.previousElementSibling.scrollIntoView({behavior: 'smooth', block: 'start'})
          : e.currentTarget.closest('.h-100').nextElementSibling.querySelectorAll(".thumbnail")[7].scrollIntoView({behavior: 'smooth', block: 'start'})
    }
  },
  props: {
    images: {
      type: Array,
      // eslint-disable-next-line vue/require-valid-default-prop
      default: []
    }
  },
  mounted () {

  },
  created () {
    this.setSelectImage(this.images[0])
  },
  watch: {
    images () {
      this.setSelectImage(this.images[0])
    }
  }
}
</script>

<style scoped lang="scss">
.full-image {
  max-height: 500px;
}
.thumbnail-slide {
  min-width: 95%;
  overflow-x: auto;
  height: 120px;
  white-space: nowrap;
  .thumbnail {
    width: 100px;
    padding: 12px;
    display: inline-block;
    height: 100px;
    img {
      cursor: pointer;
      border-radius: 0;
      transition: all 0.1s ease-in;
      &:hover, &.active {
        border-color: #6d6e6e;
        outline: 3px solid #6d6e6e;
      }
    }
  }
}
button{
  background-color: #fff;
  border: 1px solid #ebebeb;
  height: 80px;
  margin-top: -21px;
  transition: all 0.5s ease;
  &:hover{
    background-color: #f6f6f6;
  }
  i {
    font-size: 26px;
    cursor: pointer;
  }
}

</style>
