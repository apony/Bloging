<template>
  <header>
    <div class="wrapper">
      <el-row>
        <el-col :xs="20" :sm="4" :md="4" :lg="4" :xl="4"><div class="logo">TaoLand</div></el-col>
        <el-col :xs="0" :sm="20" :md="20" :lg="20" :xl="20">
          <el-menu
            :default-active="activeIndex"
            class="el-menu-demo hidden-xs-only nav-pc"
            mode="horizontal"
            @select="handleSelect"
            background-color="#2d2d2d"
            text-color="#9d9d9d"
            active-text-color="#fff">
            <el-menu-item index="1"><router-link to="/"><i class="iconfont icon-home"></i>Home</router-link></el-menu-item>
            <el-menu-item index="2"><router-link to="/archives"><i class="iconfont icon-archives"></i>Archives</router-link></el-menu-item>
            <el-menu-item index="3"><router-link to="/categories"><i class="iconfont icon-tubiao13"></i>Categories</router-link></el-menu-item>
            <el-menu-item index="4"><router-link to="/collections"><i class="iconfont icon-shoucang"></i>Collections</router-link></el-menu-item>
            <el-menu-item index="5"><router-link to="/demo"><i class="iconfont icon-play"></i>Demo</router-link></el-menu-item>
            <el-menu-item index="6"><router-link to="/about"><i class="iconfont icon-meho"></i>About</router-link></el-menu-item>
            <el-menu-item index="7" v-if="isSignIn===0"><router-link :class="[activeIndex==7?'meBtnOn':'meBtnOff']" to="/sign">Sign In</router-link></el-menu-item>
            <el-menu-item index="7" v-else-if="isSignIn===1"><router-link :class="[activeIndex==7?'meBtnOn':'meBtnOff']" to="/admin/list">{{nickName}}</router-link></el-menu-item>
            <el-menu-item index="7" v-else-if="isSignIn===2"><router-link :class="[activeIndex==7?'meBtnOn':'meBtnOff']" to="/visiter">{{nickName}}</router-link></el-menu-item>
          </el-menu>
        </el-col>
        <el-col :xs="4" :sm="0" :md="0" :lg="0" :xl="0" class="">
          <div class="nav-mob">
            <!-- <div v-if="(isSignIn===1||isSignIn===2)&&navMobile" @click="navToggle" class="avatar"></div> -->
            <img v-if="(isSignIn===1||isSignIn===2)&&navMobile" @click="navToggle" class="avatar" :src="avatar" alt="">
            <i v-else class="el-icon-menu " @click="navToggle"></i>
            <transition  name="slide-fade">
              <div v-if="navMobile" class="content">
                <ul  @click='slideUp'>
                  <li><router-link to="/">Home</router-link></li>
                  <li><router-link to="/archives">Archives</router-link></li>
                  <li><router-link to="/categories">Categories</router-link></li>
                  <li><router-link to="/collections">Collections</router-link></li>
                  <li><router-link to="/demo">Demo</router-link></li>
                  <li><router-link to="/about">About</router-link></li>
                  <li><router-link v-if="isSignIn===1||isSignIn===2" to="/visiter">{{nickName}}</router-link></li>
                </ul>
              </div>
            </transition >
          </div>
        </el-col>
      </el-row>
    </div>
  </header>
</template>

<script>
export default {
  data () {
    return {
      // activeIndex: '1',
      navMobile: false
    }
  },
  methods: {
    handleSelect (key, keyPath) {
      this.$store.commit('changeIndex', key)
    },
    navToggle () {
      this.navMobile = !this.navMobile
    },
    slideUp () {
      this.navMobile = !this.navMobile
    }
  },
  // created(){
  //   console.log(this.$store.state.activeIndex)
  // },
  computed: {
    activeIndex () {
      return this.$store.state.activeIndex
    },
    isSignIn () {
      return this.$store.state.isSignIn
    },
    nickName () {
      return localStorage.getItem('nickName')
    },
    avatar () {
      return localStorage.getItem('avatar')
    }
  }
}
</script>

<style lang="scss" scoped>
header {
  background: #2d2d2d;
  color: #9d9d9d;
  box-shadow: 0 2px 4px 1px rgba(0, 0, 0, 0.5);
  margin-bottom: 10px;
  .logo {
    line-height: 40px;
    font-size: 16px;
    margin-left: 20px;
  }
  .nav-pc {
    border-bottom: none;
    float: right;
    > li {
      padding: 0;
      > a {
        display: inline-block;
        padding: 0 20px;
        text-align: center;
        > .iconfont {
          vertical-align: top;
          margin: 0 5px 0 0;
        }
      }
    }
  }
  .nav-mob {
    position: relative;
    z-index: 9999;
    i {
      font-size: 24px;
      position: absolute;
      right: 6px;
      top: 7px;
    }
    .avatar {
      width: 24px;
      height: 24px;
      border-radius: 50%;
      border: 1px solid #9d9d9d;
      position: absolute;
      right: 7px;
      top: 7px;
    }
    .content {
      ul {
        position: absolute;
        right: 5px;
        top: 40px;
        background: #2d2d2d;
        color: #9d9d9d;
        border-radius: 0 0 4px 4px;
        box-shadow: 0px 3px 4px 1px rgba(0, 0, 0, 0.5);
        li {
          list-style-type: none;
          padding: 6px 10px;
          text-align: center;
          border-bottom: 1px solid #696464;
        }
      }
    }
  }
  .slide-fade-enter-active,
  .slide-fade-leave-active {
    transition: all 0.3s ease;
  }
  .slide-fade-enter,
  .slide-fade-leave-to {
    transform: translateY(-10px);
    opacity: 0;
  }
}
@media (min-width: 768px) {
  //pc
  header {
    margin-bottom: 20px;
    .logo {
      line-height: 60px;
      font-size: 18px;
    }
  }
  .meBtnOff {
    transition: all 0.3s;
    background: #3b99fc !important;
    color: #fff !important;
    line-height: 60px;
    vertical-align: top;
  }
  .meBtnOn {
    transition: all 0.3s;
    background: #3b99fc !important;
    color: #fff !important;
    line-height: 58px;
    vertical-align: top;
  }
}
</style>
