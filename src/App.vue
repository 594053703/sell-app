<template>
  <div id="app">
    <v-header v-if="headerShow" :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <div class="content">
      <router-view></router-view>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header.vue';
  import axios from 'axios';
  export default{
    data () {
      return {
        seller: {},
        headerShow: true
      };
    },
    components: {
      'v-header': header
    },
    mounted () {
      this.getSeller();
    },
    methods: {
      getSeller () {
        axios.get('/api/seller').then((res) => {
          this.seller = res.data.data;
          console.log(res.data.data);
        }).catch((err) => {
          console.log(err);
        });
      }
    }
  };
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "common/scss/common.scss";

  #app {
    .tab {
      display: flex;
      width: 100%;
      height: rem(80px);
      line-height: rem(80px);
      border-bottom: 1px solid rgba(7, 17, 27, 0.1);
      .tab-item {
        flex: 1;
        text-align: center;
        & > a {
          display: block;
          font-size: rem(28px);
          color: rgb(77, 85, 93);
          &.active {
            color: rgb(240, 20, 20);
          }
        }
      }
    }
  }
</style>
