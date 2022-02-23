<template>
  <div id="app">

            <el-button type="primary" :style="{'margin-top':'30px'}" :size="'small'" @click="chinese2pinyin">转换拼音</el-button>
            <span :style="{'margin-top':'30px'}">显示左侧：</span>
            <el-switch
                v-model="isShowInput"
                active-color="#13ce66"
                inactive-color="#ff4949">
            </el-switch>
            <el-button type="primary" icon="el-icon-delete-solid" :style="{'margin-top':'30px'}" :size="'small'" @click="clearWords"></el-button>



      <el-container>
        <el-aside width="300px" v-show="isShowInput">
          <div :style="{'margin-top':'30px','margin':'20px','height':'750px'}">
           <el-input
              type="textarea"
              :autosize="{ minRows: 30, maxRows: 40}"
              placeholder="请输入内容"
              v-model="textarea1">
            </el-input>
          </div>
          </el-aside>
        <el-main>
          <div :style="{'height':'750px'}">
            <!-- <el-input
              type="textarea"
              :autosize="{ minRows: 30, maxRows: 40}"
              placeholder="这里是转化后的拼音"
              v-model="textarea2">
            </el-input> -->
            <div v-for="(item,i) in resultWord" :key="i" :style="{'float':'left','margin':'5px'}" >
              <div v-show="item.pinyin != ''" :style="{'width':'35px','height':'40px'}">
                <div :style="{'width':'35px','height':'20px','float':'left','margin':'0px','padding':'0px','text-align':'center'}">
                {{item.pinyin}}
              </div>
              <div :style="{'width':'35px','height':'20px','float':'left','margin':'0px','padding':'0px','text-align':'center'}">
                {{item.chinese}}
              </div>
              </div>
              <div v-show="item.pinyin == ''" :style="{'width':'5px','height':'40px'}">
                <div :style="{'width':'5px','height':'20px','float':'left','margin':'0px','padding':'0px','text-align':'center'}">
                {{item.pinyin}}
                </div>
                <div :style="{'width':'5px','height':'20px','float':'left','margin':'0px','padding':'0px','text-align':'center'}">
                  {{item.chinese}}
                </div>
              </div>

            </div>
          </div>
        </el-main>
      </el-container>


  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      isShowInput:true,
      textarea1:'',
      resultWord:[],
    }
  },
  methods:{
    chinese2pinyin(){
      let _this = this
       var pinyin = require("chinese-to-pinyin")
       let tmpStr = _this.textarea1
       for (let i=0;i<tmpStr.length;i++){
         let res =  pinyin(tmpStr[i])
         _this.addWord(tmpStr[i],res)
       }
    },
    //一个一个添加带拼音的汉字
    addWord(chinese,pinyin){
      let item = chinese == pinyin ? {chinese:chinese,pinyin:''} : {chinese:chinese,pinyin:pinyin}
      this.resultWord.push(item)
    },
    //清空右侧内容
    clearWords(){
      this.resultWord = []
    }
  },
  mounted(){
    var pinyin = require("chinese-to-pinyin")
  //  alert(pinyin('是的'))
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
</style>
