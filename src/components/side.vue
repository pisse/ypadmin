<template>
  <div class="leftnav">
    <nav class="left">
      <div class="logo">
        <span class="logo-img"></span>
        <!--智鼎-->
      </div>
      <el-menu :default-active="defautActive" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose" theme="dark" :router="true">

        <el-menu-item index="/"><i class="el-icon-menu"></i>管理台</el-menu-item>

        <el-submenu index="/sys">
          <template slot="title"><i class="iconfont icon-xitong"></i>系统设置</template>
          <el-menu-item index="/sys/errsms"><!--<i class="iconfont icon-cuowu1"></i>-->错误信息</el-menu-item>
          <el-menu-item index="/sys/operator"><!--<i class="iconfont icon-yunying"></i>-->运营商</el-menu-item>
          <el-menu-item index="/sys/sensitive"><!--<i class="iconfont icon-minganxinxi"></i>-->敏感词（黑字典）</el-menu-item>
          <el-menu-item index="/sys/blacklist"><!--<i class="iconfont icon-heimingdan"></i>-->黑名单</el-menu-item>

        </el-submenu>

        <el-submenu index="/user">
          <template slot="title"><i class="iconfont icon-10"></i>用户管理</template>
          <el-menu-item index="/user/admin"><!--<i class="iconfont icon-admin"></i>-->后台用户</el-menu-item>
          <el-menu-item index="/user/role"><!--<i class="iconfont icon-admin"></i>-->角色管理(后台)</el-menu-item>
          <el-menu-item index="/user/front"><!--<i class="iconfont icon-10"></i>-->前台用户</el-menu-item>
          <el-menu-item index="/user/sign"><!--<i class="iconfont icon-gexingqianming"></i>-->签名管理</el-menu-item>
        </el-submenu>

      <!--  <el-menu-item index="/errsms"><i class="iconfont icon-cuowu1"></i>错误信息管理</el-menu-item>

        <el-menu-item index="/operator"><i class="iconfont icon-yunying"></i>运营商管理</el-menu-item>

        <el-menu-item index="/sensitive"><i class="iconfont icon-minganxinxi"></i>敏感词管理</el-menu-item>

        <el-menu-item index="/blacklist"><i class="iconfont icon-heimingdan"></i>黑名单管理</el-menu-item>-->

        <el-menu-item index="/smstask"><i class="iconfont icon-renwu"></i>短信审核</el-menu-item>

        <el-menu-item index="/taskrecord"><i class="iconfont icon-mingxi"></i>任务明细</el-menu-item>

        <el-submenu index="/stat">
          <template slot="title"><i class="iconfont icon-icon1"></i>运营分析</template>
          <el-menu-item index="/stat/channeldelay"><!--<i class="iconfont icon-tongdao"></i>-->通道延迟</el-menu-item>
          <el-menu-item index="/stat/vcode"><!--<i class="iconfont icon-yanzhengma"></i>-->验证码发送</el-menu-item>
          <el-menu-item index="/stat/errtype"><!--<i class="iconfont icon-cuowu"></i>-->错误明细</el-menu-item>
          <el-menu-item index="/stat/gateway"><!--<i class="iconfont icon-wangguan"></i>-->网关延迟</el-menu-item>
          <el-menu-item index="/stat/province"><!--<i class="iconfont icon-shengfen"></i>-->分省数据</el-menu-item>

          <!--<el-menu-item index="/stat/channelcheck">&lt;!&ndash;<i class="iconfont icon-yunying"></i>&ndash;&gt;通道对账</el-menu-item>
          <el-menu-item index="/stat/clientcheck">&lt;!&ndash;<i class="iconfont icon-kehu"></i>&ndash;&gt;客户对账</el-menu-item>
          <el-menu-item index="/stat/compare">&lt;!&ndash;<i class="iconfont icon-compare"></i>&ndash;&gt;数据对比</el-menu-item>-->

        </el-submenu>

        <el-submenu index="/finance">
          <template slot="title"><i class="iconfont icon-caiwu"></i>财务统计</template>
          <el-menu-item index="/finance/channelcheck"><!--<i class="iconfont icon-admin"></i>-->通道对账</el-menu-item>
          <el-menu-item index="/finance/clientcheck"><!--<i class="iconfont icon-admin"></i>-->客户对账</el-menu-item>
        </el-submenu>

        <el-menu-item index="/short"><i class="iconfont icon-taoduanlian"></i>短链分析</el-menu-item>

      </el-menu>
    </nav>
  </div>
</template>
<style lang="stylus" rel="stylesheet/stylus">

  .leftnav
    position: fixed
    top: 0
    left: 0
    width: 150px
    height: 100%
    font-size: 14px
    line-height: 14px
    z-index: 999;
    .iconfont
      margin-right:12px
    &:after
      position : absolute
      width: 30px
      top: 0
      content: ''
      left: 100%
      bottom: 0
      background: linear-gradient(left,#e0e0e0, #fdfdfd)
    .left
      height: 100%
      padding: 0
      overflow: auto
      background: #324157
      padding-bottom: 30px
      &::-webkit-scrollbar
        width: 0
      .logo
        height: 100px
        line-height : 100px
        font-size : 30px
        text-align : center
        color: #fff
        border-bottom : 1px solid rgb(102,102,102)
        .logo-img
          height: 100px
          display : inline-block
          width: 100px
          background-image : url('../assets/logo2.png')
          background-position: center;
          background-size: 100%;
          background-repeat: no-repeat;
</style>
<script type="text/ecmascript-6">
  export default {
    data () {
      return {
        defautActive: '/'
      }
    },
    props: {
    },
    created () {
      this.defautActive = this.$route.fullPath
    },
    methods: {
      handleOpen (key, keyPath) {
        // console.log(key, keyPath)
      },
      handleClose (key, keyPath) {
        // console.log(key, keyPath)
      }
    },
    components: {
    }
  }
</script>
