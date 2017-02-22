<template>
  <div class="star" :class="starType">
    <span v-for="itemClass in itemClasses" class="star-item" :class="itemClass"></span>
  </div>
</template>

<script type="text/ecmascript-6">
  const length = 5;
  const clsOn = 'on';
  const clsHalf = 'half';
  const clsOff = 'off';
  export default {
    props: {
      size: {
        type: Number
      },
      score: {
        type: Number
      }
    },
    computed: {
      starType () {
        return 'star-' + this.size;
      },
      itemClasses () {
        let result = [];
        let score = Math.floor(this.score * 2) / 2;
        let hasDecimal = score % 1 !== 0;
        let integer = Math.floor(score);
        for (let i = 0; i < integer; i++) {
          result.push(clsOn);
        }
        if (hasDecimal) {
          result.push(clsHalf);
        }
        while (result.length < length) {
          result.push(clsOff);
        }
        return result;
      }
    },
    data () {
      return {};
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../common/scss/common";

  .star {
    font-size: 0;
    .star-item {
      display: inline-block;
      background-repeat: no-repeat;
    }
    &.star-48 {
      .star-item {
        width: rem(40px);
        height: rem(40px);
        margin-right: rem(44px);
        background-size: rem(40px) rem(40px);
        &.on {
          @include bg-images('star48_on')
        }
        &.half {
          @include bg-images('star48_half')
        }
        &.off {
          @include bg-images('star48_off')
        }
      }
    }
    &.star-36 {
      .star-item {
        width: rem(30px);
        height: rem(30px);
        margin-right: rem(12px);
        background-size: rem(30px) rem(30px);
        &.on {
          @include bg-images('star36_on')
        }
        &.half {
          @include bg-images('star36_half')
        }
        &.off {
          @include bg-images('star36_off')
        }
      }
    }
    &.star-24 {
      .star-item {
        width: rem(20px);
        height: rem(20px);
        margin-right: rem(6px);
        background-size: rem(20px) rem(20px);
        &.on {
          @include bg-images('star24_on')
        }
        &.half {
          @include bg-images('star24_half')
        }
        &.off {
          @include bg-images('star24_off')
        }
      }
    }
  }
</style>
