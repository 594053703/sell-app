<template>
  <div class="goods-wrapper">
    <div class="main-box" :style="mainViewStyle">
      <div class="main">
        <div class="main-menu-box">
          <ul class="main-menu">
            <li v-for="item in goodsLists" class="menu-item">
              <span></span>
              <span>{{item.name}}</span>
            </li>
          </ul>
        </div>
        <section class="main-views">
          <div v-for="good in goodsLists" class="menu-class">
            <div class="good-title">{{good.name}}</div>
            <ul class="food-list">
              <li class="food-wrapper" v-for="food in good.foods">
                <div class="food-pic"><img :src="food.icon" alt=""></div>
                <section class="food-text">
                  <div class="title">{{food.name}}</div>
                  <div class="text" v-if="food.description">{{food.description}}</div>
                  <div class="text">
                    <span>月售{{food.sellCount}}</span>
                    <span>好评率{{food.rating}}%</span>
                  </div>
                  <div class="price">
                    <strong class="now-price">￥{{food.price}}</strong>
                    <strong class="old-price" v-if="food.oldPrice">￥{{food.oldPrice}}</strong>
                  </div>
                </section>
              </li>
            </ul>
          </div>
        </section>
      </div>
    </div>
    <div></div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    data () {
      return {
        goodsLists: [],
        mainViewStyle: {
          height: ''
        }
      };
    },
    created () {
      this.getGoodsLists();
    },
    mounted () {
      this.mainViewHeight();
    },
    methods: {
      getGoodsLists () {
        this.$http.get('/api/goods').then((res) => {
          this.goodsLists = res.data.data;
          console.log(this.goodsLists);
        }).catch((err) => {
          console.log(err);
        });
      },
      mainViewHeight () {
        let h = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight;
        this.mainViewStyle.height = h - this.$el.offsetTop + 'px';
        console.log(this.mainViewStyle);
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "../../common/scss/common";

  .goods-wrapper {
    .main-box {
      box-sizing: border-box;
      padding-bottom: rem(116px);
      .main {
        display: flex;
        width: 100%;
        height: 100%;
        .main-menu-box{
          height:100%;
          width: rem(150px);
          overflow: hidden;
          padding:0 rem(5px);
          .main-menu {
            box-sizing: border-box;
            width: rem(160px);
            padding:0  rem(24px);
            background: #f3f5f7;
            height: 100%;
            overflow-y: auto;
            overflow-x:hidden;
            .menu-item {
              box-sizing: border-box;
              width:100%;
              padding: rem(42px) 0;
              line-height: rem(28px);
              text-align: center;
              color: rgb(20, 20, 20);
              font-size:rem(24px);
              border-bottom:1px solid rgba(7,17,27,.2);
            }
          }
        }
        .main-views {
          flex: 1;
          height: 100%;
          overflow-y: auto;
          .menu-class {
            .good-title {
              font-size:rem(24px);
              line-height:52px;
              color:rgb(147,153,159);
              background:#f3f5f7;
              border-left:5px solid #d9dde1;
              padding-left:rem(28px);
            }
            .food-list {
              .food-wrapper {
                display: flex;
                margin:0 rem(36px);
                padding:rem(36px) 0;
                border-bottom:1px solid rgba(7,17,27,.1);
                &:last-child{
                  border-bottom:none;
                }
                .food-pic {
                  width:rem(128px);
                  img{
                    width:100%;
                  }
                }
                .food-text {
                  flex: 2;
                  padding-left:rem(20px);
                  .title{
                    padding-top:rem(4px);
                    font-size:rem(28px);
                  }
                  .text{
                    color:rgb(147,153,159);
                    margin:rem(16px) 0;
                  }
                  .rating{
                    color:rgb(147,153,159);
                  }
                  .price{
                    .now-price{
                      color:rgb(240,20,20);
                      font-weight:700;
                      font-size:rem(28px);
                    }
                    .old-price{
                      position: relative;
                      color:rgb(147,153,159);
                      font-size:rem(20px);
                      margin-left:rem(16px);
                      &:after{
                        display: inline-block;
                        position: absolute;
                        content:'';
                        left:0;
                        top:rem(15px);
                        width:100%;
                        height:1px;
                        background:rgb(147,153,159);
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
</style>
