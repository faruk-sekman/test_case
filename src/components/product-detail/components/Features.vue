<template>
  <div>
    <div class="row mx-0 mt-2 ps-lg-3" :key="index" v-for="(data, index) in selectableAttributes">
      <div class="col-2 p-0">
        <div class="d-flex justify-content-between align-items-center h-100">
          <p class="m-0">{{ data.name }}</p>
          <p class="m-0 me-2">:</p>
        </div>
      </div>
      <div class="col-10 attributes">
        <div class="row">
          <button @click="setAttributeData(value, index)" class="float-start me-2 col" :key="valueIndex" v-for="(value, valueIndex) in data.values"
                  :class="{
                  activeColor: value === attribute.selectColor,
                  activeSize: value === attribute.selectSize
                }" :disabled="index == 1 && attribute.sizes.includes(value) == false">
            {{ value }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RateAndCommet',
  data() {
    return {}
  },
  methods: {
    setAttributeData(value, index) {
      this.$emit('setAttributeData', {value, index})
    }
  },
  props: {
    selectableAttributes: {
      type: Array,
      // eslint-disable-next-line vue/require-valid-default-prop
      default: []
    },
    attribute: {
      type: Object,
      // eslint-disable-next-line vue/require-valid-default-prop
      default: {}
    }
  }
}
</script>

<style scoped lang="scss">
.attributes {
  button {
    height: 40px;
    border: 1px solid #ddd;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    border-radius: 2px;
    background-color: white;
    margin-bottom: 0;
    transition: all 0.1s ease;
    &:hover, &.activeColor, &.activeSize {
      border: 3px solid #6d6e6e;
    }
    &[disabled] {
      border: 1px solid #ddd;
      cursor: not-allowed;
    }
  }
}
</style>
