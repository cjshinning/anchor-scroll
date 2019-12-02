<template>
  <div id="app">
    <!-- :position="'left'" -->
    <anchor-scroll :customClass="customClass">
      <!-- <template slot="nav-item">
        nav1
      </template>
      <template slot="nav-item">
        nav2
      </template>
      <template slot="nav-item">
        nav3
      </template> -->
      <div slot="scroll-pannel" title="nav1">
        <div class="part1">
          <p>part1</p>
        </div>
        <div class="part2">part2</div>
      </div>
      <div slot="scroll-pannel" title="nav2">
        <div class="pannel2">pannel2</div>
      </div>
      <div slot="scroll-pannel" title="nav3">
        <div class="pannel3">pannel3</div>
      </div>
    </anchor-scroll>
    <!-- <anchor-scroll :navs="navs" :navStyle="navStyle" :navItemStyle="navItemStyle" :contents="contents">
      <template slot="contentItem" slot-scope="props">
        <div v-if="props.content.id==0">111</div>
        <div v-if="props.content.id==1">222</div>
        <div v-if="props.content.id==2">333</div>
        <div v-if="props.content.id==3">444</div>
        <div v-if="props.content.id==4">555</div>
      </template>
      <template slot="navitem" slot-scope="props">
        <i :class="props.nav.icon">{{props.nav.icon}}</i>
        <span class="icon">{{props.nav.text}}</span>
      </template>
    </anchor-scroll> -->
    <!-- <tab type="simple">
      <div slot="tab-item">1</div>
      <div slot="tab-item">2</div>
    </tab> -->
    <!-- <globel-button :title="btnTitle" :styled="btnStyle">
      <span slot="first">我时第一个插槽</span>
      <span slot="last">我时最后一个插槽</span>
    </globel-button> -->
    <!-- <modal modal-title="提醒" @on-ok="ok"></modal>
    <modal>
      <ul slot="modal-content">
        <li v-for="(item,index) in list" :key="index">{{item}}</li>
      </ul>
      <div slot="modal-footer">
        <span>确定</span>
        <span>重置</span>
        <span>返回</span>
      </div>
    </modal> -->
    <!-- <achor-heading :level="l1">111</achor-heading>
    <achor-heading :level="l2"><span>222</span></achor-heading> -->
    <!-- <anchored-heading :level="1">
      <p slot="item">1</p>
      <p slot="item">2</p>
      <p slot="item">3</p>
      <p>4</p>
    </anchored-heading> -->
  </div>
</template>

<script>
import './assets/asset.css';
import AnchorScroll from './components/anchorScroll/AnchorScroll';
import Tab from './components/tab/Tab'
import GlobelButton from './components/globelButton/GlobelButton'
import Modal from './components/modal/Modal'
import AchorHeading from './components/anchorHeading/AchorHeading'
import AnchoredHeading from './components/anchoredHeading/AnchoredHeading'

var list = [...'MVC前端网'];
export default {
  name: 'App',
  data(){
    return {
      customClass: "my-scroll",
      navs: [
        {id:0, text:"Tab 1", icon: 'ic1'},
        {id:1, text:"Tab 2", icon: 'ic2'},
        {id:2, text:"Tab 3", icon: 'ic3'},
        {id:3, text:"Tab 4", icon: 'ic4'},
        {id:4, text:"Tab 5", icon: 'ic5'}
      ],
      navStyle: {
        backgroundColor: '#999'
      },
      navItemStyle: {
        color: '#f00'
      },
      contents: [
        {id:0, text:"section 1"},
        {id:1, text:"section 2"},
        {id:2, text:"section 3"},
        {id:3, text:"section 4"},
        {id:4, text:"section 5"},
      ],
      btnTitle: '我是传入的标题1',
      btnStyle: {
        backgroundColor: '#999',
        color: 'green'
      },
      list: list,
      l1: 1,
      l2: 2
    }
  },
  components: {
    AnchorScroll,
    Tab,
    GlobelButton,
    Modal,
    AchorHeading,
    AnchoredHeading
  },
  methods: {
    ok(){
      alert('改变一个div的样式');
    }
  }
}
</script>

<style scoped>
.my-scroll >>> .scroll-nav li{
  line-height: 2;
}
.part1{
  height: 800px;
  background: #2b2b2b;
}
.part2{
  height: 200px;
  background: #c1c1c1;
}
.pannel2{
  height: 800px;
  background: #5c5c5c;
}
.pannel3{
  height: 1000px;
  background: #a2a2a2;
}
</style>
