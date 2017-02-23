<template>
  <div class="goods">
    <div class="menu-wrapper" ref="menuWrapper">
      <ul>
        <li class="menu-item" v-for="item in goods">
          <span class="text">
            <span v-show="item.type>0" :class="classMap[item.type]" class="icon"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foodsWrapper">
      <ul>
        <li v-for="item in goods" class="food-list">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item">
              <div class="icon">
                <img :src="food.icon" alt="">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">月售{{food.sellCount}}份</span>
                  <span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">¥{{food.price}}</span>
                  <span class="old" v-show="food.oldPrice">¥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll';
  export default {
    data () {
      return {
        goods: []
      };
    },
    created () {
      this.getGoods();
      this.classMap = ['decrease', 'discount', 'guarantee', 'invoice', 'special'];
    },
    mounted () {
    },
    methods: {
      getGoods () {
        this.$http.get('/api/goods').then((res) => {
          this.goods = res.data.data;
          this.$nextTick(() => {
            this._initScroll();
          });
        }).catch((err) => {
          console.log(err);
        });
      },
      _initScroll () {
        console.log(this.$refs);
        console.log(this.$refs.foodsWrapper);
        this.menuScroll = new BScroll(this.$refs.menuWrapper, {});
        this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {});
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../common/scss/common";

  .goods {
    display: flex;
    position: absolute;
    top: rem(349px);
    bottom: rem(92px);
    width: 100%;
    overflow: hidden;
    .menu-wrapper {
      flex: 0 0 rem(160px);
      width: rem(160px);
      background: #f3f5f7;
      .menu-item {
        display: table;
        height: rem(108px);
        .icon {
          display: inline-block;
          width: rem(24px);
          height: rem(24px);
          margin-right: 4px;
          background-size: rem(24px) rem(24px);
          background-repeat: no-repeat;
          vertical-align: middle;
          &.decrease {
            @include bg-images("decrease_3");
          }
          &.discount {
            @include bg-images("discount_3");
          }
          &.guarantee {
            @include bg-images("guarantee_3");
          }
          &.invoice {
            @include bg-images("invoice_3");
          }
          &.special {
            @include bg-images("special_3");
          }
        }
        .text {
          display: table-cell;
          width: rem(112px);
          vertical-align: middle;
          font-size: rem(24px);
          padding: 0 rem(24px);
          border-bottom: 1px solid rgba(7, 17, 27, .1);
          text-align: center;
        }
      }
    }
    .foods-wrapper {
      flex: 1;
      .title {
        padding-left: rem(28px);
        height: rem(52px);
        line-height: rem(52px);
        font-size: rem(28px);
        color: rgb(147, 153, 159);
        background: #f3f5f7;
        border-left: 2px solid #d9dde1;
      }
      .food-item {
        display: flex;
        margin: rem(32px);
        border-bottom: 1px solid rgba(7, 17, 27, .1);
        padding-bottom: rem(32px);
        &:last-child {
          margin-bottom: 0;
        }
        .icon {
          flex: 0 0 rem(114px);
          margin-right: rem(20px);
        }
        .content {
          flex: 1;
          .name {
            margin: rem(4px) 0 rem(16px) 0;
          }
          .desc, .extra {
            line-height: rem(20px);
            font-size: rem(20px);
            color: rgb(147, 153, 159);
            margin-bottom: rem(16px);
          }
          .desc {

          }
          .extra {
            .count {
              margin-right: rem(24px);
            }
          }
          .price {
            font-weight: 700;
            line-height: rem(48px);
            .now {
              margin-right: rem(16px);
              font-size: rem(28px);
              color: rgb(240, 20, 20);
            }
            .old {
              text-decoration: line-through;
              font-size: rem(20px);
              color: rgb(147, 153, 159);
            }
          }

        }
      }
    }
  }
</style>
