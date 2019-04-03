<template>
  <div class="backToTop" :style="'z-index: ' + zIndex" @click="backToTop" v-show="bVisible">
    <div class="icon"></div>
  </div>
</template>

<script>
  export default {
    name: 'Back2Top',
    props: {
      zIndex: {
        type: Number,
        default: 9999
      },
      triggerHeight: {
        type: Number
      },
      smooth: {
        type: Boolean,
        default: true
      },
      scrollInterval: {
        type: Number,
        default: 20
      },
      scrollHeight: {
        type: Number,
        default: 100
      }
    },
    data () {
      return {
        interval: null, // 计时器
        bVisible: false // 按钮显示状态
      }
    },
    methods: {
      resetToTop () {
        window.pageYOffset = 0;
        document.documentElement.scrollTop = 0;
        document.body.scrollTop = 0;
      },
      buttonStatus () {
        var currentHeight = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
        let browserHeight = this.triggerHeight || (window.outerHeight / 4);
        this.bVisible = currentHeight > browserHeight;
      },
      backToTop () {
        if (this.smooth) {
          var that = this,
            _interval = this.scrollInterval,
            _height = this.scrollHeight;
          // 间隔{_interval}移动{_height}
          this.interval = setInterval(function () {
            that.smoothScroll(_height)
          }, _interval)
        } else {
          this.resetToTop();
        }
      },
      smoothScroll (y) {
        if (window.pageYOffset > 0) {
          window.pageYOffset = window.pageYOffset - y;
        }
        if (document.documentElement.scrollTop > 0) {
          document.documentElement.scrollTop = document.documentElement.scrollTop - y;
        }
        if (document.body.scrollTop > 0) {
          document.body.scrollTop = document.body.scrollTop - y;
        }
        var positionNow = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
        if (positionNow <= 0) {
          clearInterval(this.interval);
          // 清除计时器后，全部重置为零，预防回滚为负数时，不再显示的bug
          this.resetToTop();
        }
      }
    },
    created () {
      window.addEventListener('scroll', this.buttonStatus)
    },
    destroyed () {
      window.removeEventListener('scroll', this.buttonStatus);
    }
  }
</script>

<style  scoped>
  .backToTop {
    position: fixed;
    right: 100px;
    bottom: 150px;
    width: 40px;
    height: 40px;
    size: 40px;
    border-radius: 20px;
    cursor: pointer;
    transition: .5s;
    box-shadow: 0 0 6px rgba(0,0,0,.12);
    background-color: #FFF;
    overflow: hidden;
    
  }
	.icon{
      position: absolute;
      margin: auto;
      left: 0;
      top: -8px;
      bottom: 0;
      right: 0;
      width: 0;
      height: 0;
      border-width: 8px;
      border-style: solid;
      border-color:   transparent transparent  #0099CC transparent;
			transition: .5s;
    }
  .backToTop:hover{
    box-shadow: 0 0 20px rgb(7, 27, 227);
		transform: scale(1.1);
  }
	.backToTop:hover .icon{
		transform: rotate(360deg);
	}
</style>
