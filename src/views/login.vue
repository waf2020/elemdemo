<template>
    <div class="container">
        <div class="logo">
            <img src="../assets/images/logo.jpg">
        </div> 
      
       <inputgroup 
       type="Number"
        placeholder="请输入手机号" :butTitle="butTitle" 
        v-model="phone"
        :error="error.code"
        @btnClick='getcode'
       />

       <inputgroup 
       type="text"
       placeholder="验证码" 
        v-model="vercode"
       />
     <div class="login_des">
         <p>新用户登录剂自动注册，表示已同意 <span>《用户服务协议》</span></p>
     </div>

  <button class="login_btn">登录</button>
       
       
    </div>
</template>

<script>
import inputgroup from '../components/inputgroup.vue'
export default {
    name:'login',
    data(){
        return{
           phone:'',
           vercode:'',
           disabled:false,
           error:{},
           butTitle:'获取验证码'
           
        }
    },
    components:{
       inputgroup
    },
    methods:{
         getphone(){
             console.log("this.phone==="+this.phone)
         } ,
         getTime(){

            let Time=10;
            let timer=setInterval(()=>{
                 if(Time==0){
                     
                     this.disabled=false;
                     this.butTitle="获取验证码"
                    clearInterval(timer);
                 }else {
                     this.butTitle= Time-- + 's'
                     this.disabled=true;
                 }
            },1000)
         },
         getcode(){
             if((this.getcorrect())){

                 console.log("可以发请求啦");
                 this.getTime();
             }
         },
         getcorrect(){
             if (this.phone==''|| this.phone==null){
                 this.error={
                    phone:"手机号码不能为空"
                 }
                 return false;
             }
             else if(!/^1[345678]\d{9}$/.test(this.phone)){
                 this.error={
                    phone:"手机号码格式错误"
                 }
                 return false;
             } else {
                 console.log("手机号码格式正确");
                 this.error={};
                  return true;
             }
            

            
         }
    },
    created(){
     
    }
}
</script>

<style scoped lang="scss">

  .container {
      width: 100%;
      height: 100%;
      padding: px(32);
      box-sizing: border-box;
  }
  .logo {
      text-align: center;
      margin-bottom: px(20);
  }
  .logo img {
      width: px(150);
  }
  .login_des p {
     color: #aaa;
     font-size: px(15);
     line-height: px(22);
  }
  .login_btn {
      width: 100%;
      background-color: #48ca38;
      height: px(40);
      border: none;
      border-radius:px(5);
      color: white;
      outline: none;
     
  }
  .login_des ,
  .login_btn,
  .text_group{
      margin: px(20) 0;
  }
.login_des >p >span {
    color: deepskyblue;
}
  @media screen and (max-width: 320px) {
    .container {
        padding: px(19);
    }
}

</style>