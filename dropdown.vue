<template>
  <div
    class="dropdown"
    @click="toggleRiskLevels"
    :style="[
      { '--options-height': optionsHeight + 'px' },
      { '--option-height': optionHeight + 'px' },
      { '--dropdown-width': width + 'px' },
      { '--dropdown-background-color': backgroundColor },
      { '--dropdown-border': border },
      { '--dropdown-hover-background-color': hoverBackgroundColor },
      { '--dropdown-default-text-color': textColor }
    ]"
  >
    <span class="text">
    	{{ (config.prefix ? config.prefix : "") + " "}}
	{{ config.placeholder ? config.placeholder : "" }}
    </span>
    <i class="angle-down"></i>
    <div v-if="isBottomSectionToggled" class="options">
      <div
        v-for="option in configOptions"
        class="option"
        @click="setCurrentSelectedOption(option);"
      >
        {{ option.value }}
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "vue-dropdown",
  data() {
    return {
      isBottomSectionToggled: false,
      optionsHeight: 0,
      optionHeight: 35,
      width: 100,
      configOptions: [],
      backgroundColor: "gray",
      hoverBackgroundColor: "#0084d4",
      border: "1px solid  #232b35",
      textColor: "#fff"
    };
  },
  components: {},
  props: ["config"],
  computed: {},
  methods: {
    toggleRiskLevels() {
      this.isBottomSectionToggled = !this.isBottomSectionToggled;
    },
    setCurrentSelectedOption(option) {
      this.$emit("setSelectedOption", option);
    },
    setConfigData() {
      this.configOptions = this.config.options;
      this.width = this.config.width;
      this.placeholder = this.config.placeholder;
      if (this.config.backgroundColor) {
        this.backgroundColor = this.config.backgroundColor;
      }
      if (this.config.border) {
        this.border = this.config.border;
      }
      if (this.config.hoverBackgroundColor) {
        this.hoverBackgroundColor = this.config.hoverBackgroundColor;
      }
      if (this.config.textColor) {
        this.textColor = this.config.textColor;
      }
    },
    setOptionsHeight() {
      this.optionsHeight = this.optionHeight * this.configOptions.length;
    }
  },
  created() {
    this.setConfigData();
    this.setOptionsHeight();
  },
  beforeUdate() {
    // this.setOptionsHeight();
  },
  mounted() {}
};
</script>

<style lang="scss" scoped>
@import "./vue-dropdown";
</style>
