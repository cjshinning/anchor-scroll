<script>
export default {
  props: {
    position: {
      type: String,
      default: 'right'
    },
    customClass: {
      type: String,
      default: ''
    },
    // navs: {
    //   type: Array,
    //   default: []
    // },
    // navStyle: {
    //   type: Object,
    //   default: function () { return {} }
    // },
    // navItemStyle: {
    //   type: Object,
    //   default: function () { return {} }
    // },
    // contents: {
    //   type: Array,
    //   default: []
    // }
  },
  data() {
    return {
      switchIndex: 0
    }
  },
  created(){
  },
  mounted() {
    console.log(this.customClass);
    if(this.position === 'left') {
      document.querySelector('.scroll-nav').className = "scroll-nav left";
    }
    if(this.customClass){
      document.querySelector('.scroll-wrap').className = `scroll-wrap ${this.customClass}`;
    }
    
    // 监听滚动事件
    window.addEventListener("scroll", this.onScroll, false);
  },
  destroy() {
    // 必须移除监听器，不然当该vue组件被销毁了，监听器还在就会出错
    window.removeEventListener("scroll", this.onScroll);
  },
  methods: {
    // 滚动监听器
    onScroll() {
      // 获取所有锚点元素
      const navContents = document.querySelectorAll(".scroll-content>div");
      // 所有锚点元素的 offsetTop
      const offsetTopArr = [];
      navContents.forEach(item => {
        offsetTopArr.push(item.offsetTop);
      });
      // 获取当前文档流的 scrollTop
      const scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
      // 定义当前点亮的导航下标
      let navIndex = 0;
      for (let n = 0; n < offsetTopArr.length; n++) {
        // 如果 scrollTop 大于等于第n个元素的 offsetTop 则说明 n-1 的内容已经完全不可见
        // 那么此时导航索引就应该是n了
        if (scrollTop >= offsetTopArr[n]) {
          navIndex = n;
        }
      }
      this.switchIndex = navIndex;
    },
    // 跳转到指定索引的元素
    scrollTo(index){
      this.switchIndex=index;
      let scrollTop = document.documentElement.scrollTop || document.body.scrollTop;

      const targetOffsetTop = document.querySelector(
        `.scroll-content>div:nth-child(${index + 1})`
      ).offsetTop;

      // 定义一次跳 50 个像素，数字越大跳得越快
      const STEP = 50;
      // 判断是往下滑还是往上滑
      if (scrollTop > targetOffsetTop) {
        smoothUp();
      } else {
        smoothDown();
      }
      // 定义往下滑函数
      function smoothDown() {
        // 如果当前 scrollTop 小于 targetOffsetTop 说明视口还没滑到指定位置
        if (scrollTop < targetOffsetTop) {
          // 如果和目标相差距离大于等于 STEP 就跳 STEP
          // 否则直接跳到目标点
          if (targetOffsetTop - scrollTop >= STEP) {
            scrollTop += STEP;
          } else {
            scrollTop = targetOffsetTop;
          }
          document.body.scrollTop = scrollTop;
          document.documentElement.scrollTop = scrollTop;
          requestAnimationFrame(smoothDown);
        }
      }
      // 定义往上滑函数
      function smoothUp() {
        if (scrollTop > targetOffsetTop) {
          if (scrollTop - targetOffsetTop >= STEP) {
            scrollTop -= STEP;
          } else {
            scrollTop = targetOffsetTop;
          }
          document.body.scrollTop = scrollTop;
          document.documentElement.scrollTop = scrollTop;
          requestAnimationFrame(smoothUp);
        }
      }
      // this.$emit("change",index)
    },
    anchorScroll(createElement){
      let $navs = [];
      // let $navItems = this.$slots['nav-item'] || [];
      // let itemIndex = 0;
      let _this = this;
      // debugger;
      // $navItems.map(function(item, index){
      //   $navs.push(createElement('li',{
      //     class: {
      //       active: _this.switchIndex==index
      //     },
      //     on: {
      //       click: _this.scrollTo.bind(this, index)
      //     },
      //   },item.text))
      // })

      let $pannels = [];
      let $pannelItems = this.$slots['scroll-pannel'] || [];
      $pannelItems.map(function(item,index){
        $navs.push(createElement('li',{
          class: {
            active: _this.switchIndex==index
          },
          on: {
            click: _this.scrollTo.bind(this, index)
          },
        },item.data.attrs.title))
        $pannels.push(createElement('div',item.children))
      })
      
      return createElement('div',{
        class: 'scroll-wrap'
      },
      [
        createElement('div', {
          class: 'scroll-content',
        },
        $pannels),
        createElement('ul', {
          class: 'scroll-nav'
        },
        $navs)
      ])
      
    }
  },
  render: function(createElement){
    return this.anchorScroll(createElement);
  },
};
</script>

<style scoped>
.scroll-wrap{
  position: relative;
}
/* 内容区的样式 */
/* .scroll-content {
  background-color: white;
}
.scroll-content > div {
  width: 100%;
  height: 800px;
  font-size: 36px;
  background-color: #7ec384;
}
.scroll-content > div:nth-child(2n) {
  background-color: #847ec3;
} */
/* 导航栏的样式 */
.scroll-nav {
  position: fixed;
  top: 50%;
  transform: translate(0, -50%);
  right: 0px;
  background-color: #efefef;
}
.scroll-nav.left{
  left: 0;
  right: auto;
}
.scroll-nav li {
  padding: 0 20px;
  line-height: 1.6;
  font-size: 24px;
  cursor: pointer;
}
/* 当导航被点亮后改变颜色 */
.scroll-nav .active {
  color: #847ec3;
  background-color: #e2e2e2;
}
</style>