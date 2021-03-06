<template>
  <div class="button__container">
    <nuxt-link v-if="to" :to="to" :class="className">
      <slot></slot>
    </nuxt-link>
    <a v-else-if="href" :href="href" :target="target" :class="className">
      <slot></slot>
    </a>
  </div>
</template>

<script>
export default {
  name: 'BaseButton',
  props: {
    to: {
      type: String,
      default: null
    },
    href: {
      type: String,
      default: null
    },
    target: {
      type: String,
      default: '_self'
    },
    type: {
      type: String,
      default: null
    },
    isSelected: {
      type: Boolean,
      default: false
    },
    size: {
      type: String,
      default: 'md'
    }
  },
  computed: {
    className() {
      let className

      if (this.type === 'selector') {
        className = 'selector' + ' selector--' + this.size
      } else if (this.type !== null) {
        className = 'button button--' + this.type + ' button--' + this.size
      } else {
        className = 'button' + ' button--' + this.size
      }

      if (this.isSelected) {
        className = className + ' ' + this.type + '--selected'
      }
      return className
    }
  }
}
</script>

<style lang="scss">
.button {
  &__container {
    display: inline-block;
  }

  line-height: normal;
  margin: 0;
  padding: 0;
  width: auto;
  overflow: visible;
  min-height: 20px;
  padding: $space-xxs $space-sm;
  border-radius: 4px;
  font-weight: 500;
  cursor: pointer;
  background-color: $color-grey-lightest;
  color: $color-grey-darkest;
  font-size: $font-size-xs;
  box-shadow: $shadow-elevation-1;
  transition: all 0.3s ease;
  border: 1px solid $color-grey;
  display: inline-block;

  &--lg {
    font-size: $font-size-lg;
    padding: $space-xs $space-md;
    font-weight: 500;
  }

  &:hover {
    box-shadow: $shadow-elevation-3;
  }

  &:active {
    box-shadow: $shadow-elevation-2;
  }

  &:disabled {
    opacity: 0.4;
  }

  &--primary {
    background-color: $color-primary;
    color: #fff;
    border-color: $color-primary;

    &:hover {
      background-color: darken($color-primary, 5);
      border-color: darken($color-primary, 5);
      color: #fff;
    }

    &:active {
      background-color: $color-primary-darker;
      border-color: $color-primary-darker;
      color: #fff;
    }
  }
}

.selector {
  line-height: normal;
  margin: 0;
  padding: 0;
  width: auto;
  overflow: visible;
  min-height: 20px;
  padding: $space-xxs $space-sm;
  border-radius: 99px;
  font-weight: 500;
  cursor: pointer;
  background-color: $color-grey-lightest;
  color: $color-grey-darkest;
  font-size: $font-size-xs;
  transition: all 0.3s ease;
  border: 1px solid $color-grey;

  &--selected {
    background-color: $color-primary-lightest;
    color: $color-primary;
    border: 1px solid $color-primary-light;
  }

  &--lg {
    font-size: $font-size-md;
    padding: $space-xs $space-md;
    font-weight: 400;
  }
}
</style>
