<template>

  <div class="headerbox float-div">
    <div class="main">
      <div class="clearfix pt5 pl10 pr10 pb5">
        <div class="epet-search bgf">
          <div class="fl rela ft14 location">
            <keep-alive>
            <router-link to="/place">
              <span class="catordog c89" v-if="btn===1||btn===null">猫猫站</span>
              <span class="catordog c89" v-if="btn===2">狗狗站</span>
              <span class="catordog c89" v-if="btn===3">水族馆</span>
              <!--<span class="catordog c89" v-else="">猫猫站</span>-->
              <span class="c89">|</span>
              <span v-if="city.province"><span data-name="my-place" class="myposition c89 ft13">{{city.province.value}}</span></span>
              <span v-else=""><span data-name="my-place" class="myposition c89 ft13">北京市</span></span>
              <i></i>
            </router-link>
            </keep-alive>
            <router-view></router-view>
          </div>
          <p class="search-text">
            <a href="">
              <input type="search" placeholder="搜索商品和品牌" disabled="disabled">
              <span class="eico serach-ico"></span>
            </a>
          </p>
          <a href="" class="epet-category">
            <img src="//static.epetbar.com/static_web/wap/src/images/mydope.png" alt="">
          </a>
        </div>
      </div>
      <div class="find_nav">
        <div class="find_nav_left dscroll">
          <div class="find_nav_list dscroll-div" ref="navList">
            <ul class="dscroll-ul">
              <li class="dscroll-li" :class="{on: false}" v-for="(nav, index) in petName.headerNav" :key="index">
                <router-view></router-view>
                <router-link to="###">
                  <span class="rela">
                    <span>{{nav.title}}</span>
                    <i></i>
                  </span>
                </router-link>
              </li>
  <!--            <li class="dscroll-li">
                <a href="https://wap.epet.com/clothmall/main.html?pet_type=dog&ampfw=0">&lt;!&ndash;&ndash;&gt;
                  <span class="rela">
                    <span>服饰城</span>
                    <i></i>
                  </span>
                </a>
              </li>
              <li class="dscroll-li">
                <a href="https://wap.epet.com/main.html?menu_param=123&amppet_type=dog&ampis_single=1&ampfw=0">&lt;!&ndash;&ndash;&gt;
                  <span class="rela">
                    <span>狗狗主粮</span>
                    <i></i>
                  </span>
                </a>
              </li>
              <li class="dscroll-li">
                <a href="https://wap.epet.com/main.html?menu_param=125&amppet_type=dog&ampis_single=1&ampfw=0">&lt;!&ndash;&ndash;&gt;
                  <span class="rela">
                    <span>医疗保健</span>
                    <i></i>
                  </span>
                </a>
              </li>
              <li class="dscroll-li">
                <a href="https://wap.epet.com/main.html?menu_param=131&amppet_type=dog&ampis_single=1&ampfw=0">&lt;!&ndash;&ndash;&gt;
                  <span class="rela">
                    <span>零食玩具</span>
                    <i></i>
                  </span>
                </a>
              </li>
              <li class="dscroll-li">
                <a href="https://wap.epet.com/main.html?menu_param=134&amppet_type=dog&ampis_single=1&ampfw=0">&lt;!&ndash;&ndash;&gt;
                  <span class="rela">
                    <span>日用外出</span>
                    <i></i>
                  </span>
                </a>
              </li>
              <li class="dscroll-li">
                <a href="https://wap.epet.com/main.html?menu_param=140&amppet_type=dog&ampis_single=1&ampfw=0">&lt;!&ndash;&ndash;&gt;
                  <span class="rela">
                    <span>美容香波</span>
                    <i></i>
                  </span>
                </a>
              </li>-->
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
  import {mapState} from 'vuex'
  export default {
    data() {
      return {
        btn: 1,
        city_key:''
      }
    },
    mounted() {
      this.$nextTick(() =>{
        const navScroll = new BScroll(this.$refs.navList, {
          click:true,
          scrollX:true
        })
      })
      //
      //console.log(this.city.province);

        this.city_key = JSON.parse(localStorage.getItem('city_key') ||'{}')
        this.$store.state.city = this.city_key  //更改vuex中city的数据
        //一进入首页就会读取btn_key的值，从而判断是三个站中的哪一个
        this.btn = JSON.parse(localStorage.getItem('btn_key'))
        //console.log(this.btn);//null, 当localStorage中没保存值时

    },
    computed: {
      ...mapState(['city', 'petName']),
    }
  }


</script>

<style lang="stylus" rel="stylesheet/stylus">
  .headerbox
    position relative

  .main
    /*position absolute*/
    z-index 500
    width 100%
    background #fff
  .find_nav
    width: 100%
    height: 35px
    min-width: 320px

  .dscroll
    /*overflow-x: hidden
    overflow-y: hidden*/
    overflow hidden

  .dscroll .dscroll-ul
    white-space: nowrap
    display: flex
    width 140%

  ul, li
    list-style: none

  .dscroll .dscroll-li
    width: 25%
    padding 0 10px

  .find_nav_list ul li a
    display: block
    width: 100%
    height: 100%
    line-height: 36px
    font-size: 14px
    text-align: center
    color: #666

  .find_nav_list li i
    position: absolute
    bottom: 1px
    left: -10%
    width: 120%
    height: 2px
  .find_nav_list ul li.on i {
      background: #459d36;
  }
  .find_nav_list ul li.on span {
    color: #459d36;
    display: inline-block;
  }

  /*.router-link-active
    background lightgreen*/

</style>
