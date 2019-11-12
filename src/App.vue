<template>
  <div id="app">
    <anchor-scroll :navs="navs" :navStyle="navStyle" :navItemStyle="navItemStyle" :contents="contents">
      <template slot="navitem" slot-scope="props">
        <i :class="props.nav.icon">{{props.nav.icon}}</i>
        <span class="icon">{{props.nav.text}}</span>
      </template>
    </anchor-scroll>
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
  </div>
</template>

<script>
import './assets/asset.css';
import AnchorScroll from './components/anchorScroll/AnchorScroll';
import Tab from './components/tab/Tab'
import GlobelButton from './components/globelButton/GlobelButton'
import Modal from './components/modal/Modal'
import AchorHeading from './components/anchorHeading/AchorHeading'

var list = [...'MVC前端网'];
export default {
  name: 'App',
  data(){
    return {
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
    AchorHeading
  },
  methods: {
    ok(){
      alert('改变一个div的样式');
    }
  }
}
</script>

<style>

</style>
