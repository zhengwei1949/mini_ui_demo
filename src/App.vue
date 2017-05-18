<template>
  <div id="app" >
  <mt-header fixed title="固定在顶部的导航栏"></mt-header>
  <br><br><br>
 <mt-tab-container v-model="myItem">
 <!--第一屏开始-->
  <mt-tab-container-item id="myItemaa">

   <div class="page-button-group">
      <mt-button @click="myToastFn()">点击toast</mt-button>
      <mt-button @click="myIndicatorFn()">点击弹出indicator</mt-button>
      <mt-button @click="myMessageBoxFn()">点击弹出messageBox</mt-button>
      <mt-button @click="myActionsheetFn()">点击弹出actionsheet</mt-button>
      <mt-button @click="myPopupFn()">点击弹出Popup</mt-button>
      <mt-button >未读消息<mt-badge size="small" color="red">18</mt-badge></mt-button>
    </div>



<mt-range v-model="rangeValue"></mt-range>
<br>
{{rangeValue}}
<br>


<mt-picker :slots="slots" @change="onValuesChange"></mt-picker>



    <div class="page-swipe">
      <h1 class="page-title">Swipe</h1>
      <p class="page-swipe-desc">基础用法</p>
      <mt-swipe :auto="4000">
        <mt-swipe-item class="slide1">1</mt-swipe-item>
        <mt-swipe-item class="slide2">2</mt-swipe-item>
        <mt-swipe-item class="slide3">3</mt-swipe-item>
      </mt-swipe>

      <p class="page-swipe-desc">隐藏 indicators</p>
      <mt-swipe :show-indicators="false">
        <mt-swipe-item class="slide1">1</mt-swipe-item>
        <mt-swipe-item class="slide2">2</mt-swipe-item>
        <mt-swipe-item class="slide3">3</mt-swipe-item>
      </mt-swipe>

      <p class="page-swipe-desc">取消自动播放</p>
      <mt-swipe :auto="0">
        <mt-swipe-item class="slide1">1</mt-swipe-item>
        <mt-swipe-item class="slide2">2</mt-swipe-item>
        <mt-swipe-item class="slide3">3</mt-swipe-item>
      </mt-swipe>

      <p class="page-swipe-desc">设置默认显示页</p>
      <mt-swipe :auto="0" :defaultIndex="1">
        <mt-swipe-item class="slide1">1</mt-swipe-item>
        <mt-swipe-item class="slide2">2</mt-swipe-item>
        <mt-swipe-item class="slide3">3</mt-swipe-item>
      </mt-swipe>
  </div>





    <mt-actionsheet
    cancel-text="取消actionsheet"
    :actions="actions"
    v-model="sheetVisible">
  </mt-actionsheet>

  <mt-popup v-model="popupVisible" position="right">你好，我是popup</mt-popup>

  </mt-tab-container-item>
  <!--第一屏结束-->

  <!--第二屏开始-->
  <mt-tab-container-item id="myItembb">
    <ul
      v-infinite-scroll="loadMore"
      infinite-scroll-disabled="loading"
      infinite-scroll-distance="10">
      <li v-for="item in list">{{ item }}</li>
    </ul>
  </mt-tab-container-item>
  <!--第二屏结束-->

  <mt-tab-container-item id="myItemcc">
    c
  </mt-tab-container-item>
  <mt-tab-container-item id="myItemdd">
    d
  </mt-tab-container-item>
</mt-tab-container>

    <mt-tabbar v-model="selected" :fixed="true">
      <mt-tab-item id="aa">
        <img slot="icon" src="./assets/100x100.png">
        aa
      </mt-tab-item>
      <mt-tab-item id="bb">
        <img slot="icon" src="./assets/100x100.png">
        bb
      </mt-tab-item>
      <mt-tab-item id="cc">
        <img slot="icon" src="./assets/100x100.png">
        cc
      </mt-tab-item>
      <mt-tab-item id="dd">
        <img slot="icon" src="./assets/100x100.png">
        dd
      </mt-tab-item>
    </mt-tabbar>
  </div>
</template>

<script>
import { MessageBox,Indicator,Toast } from 'mint-ui'
export default {
  name: 'app',
  data:function(){
    return {
      selected:'aa',
      myItem:'myItemaa',
      list:[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16],
      actions: [{
          name: '展示 Toast',
          method: this.myToastFn
        }, {
          name: '展示 Message Box',
          method: this.myMessageBoxFn
        }],
      sheetVisible:false,
      popupVisible:false,
      rangeValue:10,
      slots: [
        {
          flex: 1,
          values: ['2015-01', '2015-02', '2015-03', '2015-04', '2015-05', '2015-06'],
          className: 'slot1',
          textAlign: 'right'
        }, {
          divider: true,
          content: '-',
          className: 'slot2'
        }, {
          flex: 1,
          values: ['2015-01', '2015-02', '2015-03', '2015-04', '2015-05', '2015-06'],
          className: 'slot3',
          textAlign: 'left'
        }
      ]
    }
  },  
  watch:{
    selected:function(){
      this.myItem = 'myItem' + this.selected;
    }
  },
  methods:{
    myActionsheetFn:function(){
      this.sheetVisible = true;
    },
    myPopupFn:function(){
      this.popupVisible = true;
    },
    myToastFn(){
      Toast({
        message: '操作成功',
        iconClass: 'icon icon-success'
      });
    },
    myIndicatorFn(){
      Indicator.open({
        text: '加载中...',
        spinnerType: 'fading-circle'
      });
      setTimeout(function(){
        Indicator.close();//3秒后关闭
      },3000);
    },
    myMessageBoxFn:function(){
      MessageBox({
        title: '提示',
        message: '确定执行此操作?',
        showCancelButton: true
      });

    },
    loadMore() {
      this.loading = true;
      setTimeout(() => {
        let last = this.list[this.list.length - 1];
        for (let i = 1; i <= 10; i++) {
          this.list.push(last + i);
        }
        this.loading = false;
      }, 2500);
    },
    onValuesChange:function(picker,values){
      console.log(picker,values);
    }
  }
}
</script>

<style>
  li{
    height:80px;
    border-bottom:1px solid green;
  }
</style>
