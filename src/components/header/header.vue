<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟到达
        </div>
        <div v-if="seller.supports" class="supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
          <span class="more-supports">{{seller.supports.length}}个<i class="icon-keyboard_arrow_right"></i></span>
        </div>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin"></span>
      <span class="text">{{seller.bulletin}}</span>
      <span class="icon"> > </span>
    </div>
    <div class="background">
      <img :src="seller.avatar" alt="">
    </div>
    <div v-show="showDetail" class="detail">
      <div class="detail-wrapper">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
        </div>
      </div>
      <div class="detail-close">
        <span class="icon-close"></span>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        type: 'decrease',
        showDetail: false
      };
    },
    created () {
      this.classMap = ['decrease', 'discount', 'guarantee', 'invoice', 'special'];
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
  @import "../../common/scss/common";

  .header {
    position: relative;
    color: #fff;
    background: rgba(7, 17, 27, .5);
    .content-wrapper {
      display: flex;
      padding: rem(48px) rem(24px) rem(36px) rem(48px);
      .avatar {
        width: rem(128px);
        height: rem(128px);
        margin-right: rem(32px);
        img {
          width: 100%;
          height: 100%;
        }
      }
      .content {
        flex: 1;
        color: rgb(255, 255, 255);
        .title {
          .brand {
            display: inline-block;
            vertical-align: middle;
            width: rem(60px);
            height: rem(36px);
            @include bg-images("brand");
            background-position: center center;
            background-size: cover;
            background-repeat: no-repeat;
          }
          .name {
            vertical-align: middle;
            font-size: rem(36px);
            line-height: rem(36px);
            font-weight: bold;
          }
        }
        .description {
          font-size: rem(24px);
          line-height: rem(24px);
          margin-top: rem(16px);
          font-weight: 200;
        }
        .supports {
          position: relative;
          margin-top: rem(20px);
          .text {
            font-size: rem(20px);
            line-height: rem(24px);
            font-weight: 200;
            vertical-align: middle;
          }
          .icon {
            display: inline-block;
            width: rem(24px);
            height: rem(24px);
            margin-right: 4px;
            background-size: rem(24px) rem(24px);
            background-repeat: no-repeat;
            vertical-align: middle;
            &.decrease {
              @include bg-images("decrease_1");
            }
            &.discount {
              @include bg-images("discount_1");
            }
            &.guarantee {
              @include bg-images("guarantee_1");
            }
            &.invoice {
              @include bg-images("invoice_1");
            }
            &.special {
              @include bg-images("special_1");
            }
          }
          .more-supports {
            position: absolute;
            display: block;
            right: 0;
            top: 50%;
            font-size: rem(20px);
            transform: translate(0, -50%);
            padding: rem(14px) rem(16px);
            border-radius: rem(40px);
            background-color: rgba(0, 0, 0, .2);
            .icon-keyboard_arrow_right {
              font-size: rem(20px);
              margin-left: rem(8px);
              vertical-align: middle;
            }
          }
        }
      }
    }
    .bulletin-wrapper {
      display: flex;
      height: rem(56px);
      color: rgb(255, 255, 255);
      padding: 0 rem(24px);
      align-items: center;
      background: rgba(7, 17, 27, .5);
      .bulletin {
        width: rem(44px);
        height: rem(24px);
        @include bg-images("bulletin");
        background-position: center center;
        background-size: cover;
        background-repeat: no-repeat;
        margin-right: rem(8px);
      }
      .icon:nth-of-type(3) {
        margin-left: rem(8px);
      }
      .text {
        flex: 1;
        font-size: rem(20px);
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        font-weight: 200;
      }
    }
    .background {
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      overflow: hidden;
      z-index: -1;
      img {
        width: 100%;
      }
      filter: blur(10px);
      -webkit-filter: blur(10px);
    }
    .detail {
      position: fixed;
      z-index: 100;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      overflow: auto;
      background: rgba(7, 17, 27, .8);
      .detail-wrapper {
        min-height: 90%;
        .detail-main {
          margin-top: rem(128px);
          padding-bottom: rem(128px);
          .name {
            font-size: rem(32px);
            font-weight: 700;
            color: rgb(255, 255, 255);
            line-height: rem(32px);
            text-align: center;
          }
        }
      }
      .detail-close {
        position: relative;
        width: rem(64px);
        height: rem(64px);
        font-size: rem(64px);
        margin: -(rem(128px)) auto 0 auto;
      }
    }
  }
</style>
