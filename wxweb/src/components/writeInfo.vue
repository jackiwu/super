<template>
  <div>
    <div id="pop" v-if="status">
      <div class="info">
        <img class="yuan" @click="toHome()" src="https://webimages.pzlive.vip/cha_03.jpg" alt="">
        <div class="input">
          <div class="input-write">
            <div class="input-cate">姓名</div>
            <div class="mid"></div>
            <input type="text" v-model="name" class="write-text" placeholder="请输入姓名"/>
          </div>
          <div class="input-write">
            <div class="input-cate">手机号</div>
            <div class="mid"></div>
            <input type="text" v-model="phone" class="write-text" placeholder="请输入你的手机号码"/>
          </div>
          <div class="input-write code">
            <input type="text" class="write-code" v-model="code" placeholder="请输入验证码"/>
            <div class="button" @click="getCode()">{{text}}</div>
          </div>
        </div>
        <div class="submit" @click="submit()">提交</div>
      </div>
    </div>

    <div class="pop-hint" v-else>
      <div class="pop-center">
        <div class="title">
          <p>报名成功</p>
          <p>去分享给好友，一起成为合伙人吧</p>
        </div>
        <div class="pop-button" @click="toHome">
          我知道了
        </div>
      </div>
    </div>
    <div class="pop-hint" v-if="msg">
      <div class="pop-center">
        <div class="title">
          <p class="hint">{{title}}</p>
        </div>
        <div class="pop-button" @click="toB">
          我知道了
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import axios from 'axios'
  import VueAxios from 'vue-axios'
  Vue.use(VueAxios,axios)
  export default {
    name: "B",
    data() {
      return {
        name: '',
        phone: '',
        code:'',
        status: true,
        msg:false,
        title:"",
        isClick:true,
        text:"获取验证码",
        webTitle:"招募合伙人"
      }
    },
    methods: {
      //提交
      submit() {
        let that = this;
        let name = this.name;
        let phone = this.phone;
        let code = this.code;
        if (name == ''){
          this.title = "请填写姓名";
          this.msg = true;
          return
        }
        if (phone == '' || phone.length < 11){
          this.title = "请检查手机号";
          this.msg = true;
          return
        }
        if(code == ''){
          this.title = '请填写验证码';
          this.msg = true
          return
        }
        console.log(name)
        this.status = false
      },
      toB(){
        this.msg = false
      },
      //获取验证码
      getCode(){
        if (!this.isClick) {
          return false
        }
        if(this.phone == '' || this.phone.length < 11){
          this.title = "请检查手机号";
          this.msg = true;
          return
        }
        let phone = this.phone
        Vue.axios.post('https://wwwapi.pzlive.vip/index/user/sendvercode',{mobile:phone,stype:3}).then((res) => {
          this.timeOut()
        }).catch((err) => {

        })
      },
      timeOut:function(){
        let time = 60;
        let that = this;
        let i = setInterval(function () {
          time--;
          if (time < 1){
            that.text = '获取验证码';
            that.isClick = true;
            clearInterval(i);
            return
          }
          that.text = time + '秒后重发'
          that.isClick = false
        },1000)
      },
      toHome() {
        this.$router.push({path: '/'})
      }
    }
  }
</script>

<style scoped>
  #pop {
    width: 750px;
    height: 100%;
    background: rgba(0, 0, 0, 0.4);
    position: fixed;
    top: 0;
    left: 0;
  }
.hint{
  line-height: 148px;
}
  .info {
    width: 731px;
    height: 727px;
    background: #f7f7f7;
    position: absolute;
    bottom: 68px;
    left: 10px;
  }

  .input {
    margin-left: 40px;
    width: 650px;
    height: auto;
    overflow: hidden;
    margin-top: 173px;
    display: block;
  }

  .input-write {
    width: 650px;
    height: 70px;
    background: #ffffff;
    display: flex;
    display: -webkit-flex;
    justify-content: flex-start;
    align-items: center;
    margin-bottom: 35px;
  }

  .input-cate {
    display: inline-block;
    width: 135px;
    height: 70px;
    text-align-last: justify;
    line-height: 70px;
    color: #404040;
    font-size: 30px;
    /*float: left;*/
    /*letter-spacing: 6px;*/
    padding-left: 10px;
    box-sizing: border-box;
  }

  .mid {
    width: 1px;
    height: 35px;
    border: 1px solid #666666;
    opacity: 0.43;
    display: inline-block;
    margin-left: 20px;
  }

  .write-text {
    width: 510px;
    height: 70px;
    border: none;
    outline: none;
    font-size: 30px;
    letter-spacing: 4px;
    padding-left: 30px;
    box-sizing: border-box;
  }

  .code {
    background: #f7f7f7;
  }

  .write-code {
    width: 370px;
    height: 60px;
    background: #ffffff;
    font-size: 30px;
    letter-spacing: 4px;
    padding-left: 30px;
    box-sizing: border-box;
    border: none;
    outline: none;
  }

  .button {
    width: 267px;
    height: 60px;
    background: #009900;
    text-align: center;
    line-height: 60px;
    color: #ffffff;
    margin-left: 12px;
    font-size: 30px;
  }

  .submit {
    width: 730px;
    height: 88px;
    background: #e61f18;
    border-radius: 10px;
    color: #ffffff;
    font-size: 34px;
    font-family: "MicrosoftYaHei-Bold";
    font-weight: bold;
    position: absolute;
    left: 0;
    bottom: 61px;
    text-align: center;
    line-height: 88px;
    letter-spacing: 30px;
  }

  .yuan {
    width: 45px;
    height: 45px;
    position: absolute;
    top: 23px;
    right: 20px;
    z-index: 10;
  }
  .pop-hint {
    width: 750px;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.45);
    display: flex;
    display: -webkit-flex;
    justify-content: center;
    align-items: center;
  }
  .pop-center {
    width: 580px;
    /*height: 238px;*/
    overflow: hidden;
    background: #fff;
    -webkit-border-radius: 10px;
    -moz-border-radius: 10px;
    border-radius: 10px;
  }

  .title {
    width: 100%;
    height: 148px;
    text-align: center;
    /*line-height: 148px;*/
    color: #404040;
    font-size: 34px;
  }
  p:nth-of-type(2){
    font-size: 28px;
  }
  .pop-button {
    width: 100%;
    height: 90px;
    border-top: 1px solid #e2e2e2;
    display: flex;
    display: -webkit-flex;
    justify-content: center;
    font-size: 30px;
    text-align: center;
    line-height: 90px;
    color: #e61f18;
  }
</style>
