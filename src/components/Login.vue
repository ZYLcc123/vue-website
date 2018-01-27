<template>
	<div class="login">
		<h4 class="login_title">
			 <div class="login_normal_title">
				 <span @click="changeLoginway('login')" :class="{login_active:loginway==='login'}">登录</span>
				 <b>·</b>
				 <span @click="changeLoginway('register')" :class="{login_active:loginway==='register'}">注册</span>
			 </div>
			 <div v-if="loginway==='login'">
				 
				 	<div class="input_div">
					 	<input type="text" v-model="num" placeholder="手机号或邮件箱" class="input_top input_normal">
					</div>
				 	<div class="input_div">
				 		<input type="password" v-model="psd" placeholder="密码" class="input_bottom input_normal">
				 	</div>
				 	<div class="forget">
				 		<span>忘记密码？</span>
				 	</div>
				 	<button class="login_button" @click="sub()">登录</button>
				    <input type="checkbox" :checked="test" @click="aa" >

			 </div>
			 <div v-if="loginway==='register'">
				 	<div class="input_div">
					 	<input type="text" placeholder="你的昵称" class="input_top input_normal" >
					</div>
				 	<div class="input_div">
				 		<input type="password" placeholder="手机号" class="input_middle input_normal">
				 	</div>
				 	<div class="input_div">
				 		<input type="password" placeholder="输入密码" class="input_bottom input_normal">
				 	</div>
				 	<button class="login_button">注册</button>
			 </div>
		</h4>
	</div>
</template>
<script type="text/javascript">
	import {ecDo} from '../assets/ec-do-1.1.4.js'
	import　　{mapGetters} from 'vuex'
	import　Axios from 'axios'
	import Vue from 'vue'
	import　VueResource from 'vue-resource'
	import　$ from 'jquery'
	 Vue.use(VueResource)  
	export default {
		 data () {
    return{
      ecDo:ecDo,   
      	num:"",
      	psd:"",
      	red:"red",
      	test:false
    }
  },
		computed:{
			...mapGetters({
				loginway:'getLoginway'
			})
		},
		mounted(){
       // this.getCookie()
       },
		methods:{
			aa(){
				this.test=!this.test;
				console.log(this.test);
			},
			getCookie () {
    if (document.cookie.length>0) {
      var arr=document.cookie.split('; ');//这里显示的格式需要切割一下自己可输出看下
      for(var i=0;i<arr.length;i++){
        var arr2=arr[i].split('=');//再次切割
        //判断查找相对应的值
        if(arr2[0]=='userName'){
          this.ruleForm.userName=arr2[1];//保存到保存数据的地方
        }else if(arr2[0]=='userPwd'){
          this.ruleForm.password=arr2[1];
        }
      }
    }
  },
			  setCookie(c_name,c_pwd,exdays) {
    var exdate=new Date();//获取时间
    exdate.setTime(exdate.getTime() + 24*60*60*1000*exdays);//保存的天数
    //字符串拼接cookie
    window.document.cookie="userName"+ "=" +c_name+";path=/;expires="+exdate.toGMTString();
    window.document.cookie="userPwd"+"="+c_pwd+";path=/;expires="+exdate.toGMTString();
  },
			sub(){
				
				if(this.test==true){
					console.log(1);
					this.setCookie(this.num,this.psd,7);
				}
				 $.ajax({  
            type:"GET",//jsonp只支持get方式  
          /*  url:"http://suggest.taobao.com/sug?code=utf-8&q=充气娃娃&callback=callback",*/
            /*url:"http://tcc.taobao.com/cc/json/mobile_tel_segment.htm?tel=18236829039",*/
            url:"http://localhost:3000",
            data:{id:123456},//需要传送的数据
            dataType:"jsonp",//规定数据传送方式  
            jsonp:"callback",//定义回调函数  
            success:function callback(data) {
            	
                console.log(data);  
            },  
            error:function(XHR) {//请求失败处理  
                console.log(XHR);
            }  
        }); 
			/*	let reg=/^\d{8}$/,
				reg2=/^\d{0,6}$/;
				if(reg.test(this.num)&&reg2.test(this.psd)){	
					
				}else if(!reg.test(this.num)&&reg2.test(this.psd)){
					console.log("num");
				}
				else if(reg.test(this.num)&&!reg2.test(this.psd)){
					console.log("mima");
				}else{
					console.log("nan");
				}
		*/
		/*	vm.$http.get("http://localhost:3000").then(function(res){  
        console.log(res)  
    }) */
				/*ecDo.ajax({
					type:'get',
      	url:'http://localhost:3000/',
      	data:{
      		num:this.data.num,
      		psd:this.data.psd
      	},
      	success:function(res){
      		console.log(res)
     	}
				}
				)*/
			},
			changeLoginway(type){
				this.$store.dispatch('changeLoginway',type)
			}
		},
		created(){
			
			this.$store.dispatch('changeShow','')
		}
	}
</script>
<style scoped>
	.login{width: 400px;margin: 0 auto 50px;padding: 20px 30px 30px 30px ;border-radius: 4px;box-shadow: 0 0 8px rgba(0,0,0,.1);height: 400px}
	.login_normal_title{text-align: center; font-weight: 400; color: #969696;font-size: 18px;margin-bottom: 20px}
	.login_normal_title span{display: inline-block;padding: 10px;cursor: pointer;box-sizing: border-box;}
	.login_normal_title span:hover{border-bottom: 2px solid #00BC9B;}
	.login_active{color: #00BC9B; border-bottom: 2px solid #00BC9B;}
	.input_div{width: 300px;margin: 0px auto}
	.forget{width: 300px;margin: 20px auto;text-align: right;font-weight: 400; color: #969696;font-size: 12px;}
	.input_top{border: 1px solid #c8c8c8;border-bottom: none;border-radius: 4px 4px 0 0;}
	.input_bottom{border:1px solid #c8c8c8;border-radius:0 0 4px 4px; }
	.input_middle{border: 1px solid #c8c8c8;border-radius: 0;border-bottom: none}
    .input_normal{background-color: hsla(0,0%,71%,.1);width: 100%;padding: 4px 0 4px 15px; height: 50px;box-sizing: border-box;}
	.login_button{display: block;font-size: 18px;color:#fff;background:#00BC9B;border: none;border-radius: 5px;outline: none;width: 300px;height: 43px;line-height: 43px;margin: 30px auto }
</style>