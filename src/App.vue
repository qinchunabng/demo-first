<template>
  <div id="app">
    <h1 ref="myh1">app根组件</h1>
    <button @click="showRef">ref使用</button>
    <button @click="resetLeft">重置left组件的count</button>
    <hr/>
    <input type="text" v-if="inputVisible" @blur="showBtn" ref="inputRef"/>
    <button v-else @click="showInput">展示输入框</button>
    <hr/>
    <div class="mycom">
      <div class="left">
        <MyCount :init="9" @numchange="getNewCount" ref="leftCom"></MyCount>
      </div>
      <div class="right">
        <MyCount :init="6"></MyCount>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Count from '@/components/Count.vue'

export default {
  name: 'App',
  data(){
    return {
      numFromSon: 0,
      inputVisible: false
    }
  },
  components: {
    MyCount: Count
  },
  methods:{
    getNewCount(val){
      this.numFromSon = val
    },
    showRef(){
      //通过ref获取dom对象
      console.log(this.$refs.myh1);
    },
    //重置left组件的count值
    resetLeft(){
      let leftCom = this.$refs.leftCom;
      leftCom.count = 0;
    },
    showInput(){
      this.inputVisible = true;
      let inputRef = this.$refs.inputRef;
      console.log('inputRef', inputRef);
      //$nextTick会在dom重新渲染之后执行
      this.$nextTick(()=>{
        let inputRef = this.$refs.inputRef;
        //文本框获取焦点
        console.log('inputRef', inputRef);
        inputRef && inputRef.focus();
      });
     
    },
    showBtn(){
      this.inputVisible = false;
    }
  }
}
</script>

<style lang="less" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.mycom{
  display: flex;
  justify-content: center;
  .left,.right{
    flex-grow: 1;
  }
  .left{
    //当使用第三方插件库，需要修改第三方组件库时使用/deep/
    /deep/ h5{
      color:red;
    }
  }
}
</style>
