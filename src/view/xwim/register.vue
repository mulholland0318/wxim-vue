<template>
	<div class='loginandreg'>
		<div id="register-box" class='commonbox'></div>
		<div class="cent-box register-box">
			<div class="cent-box-header">
				<h1 class="main-title hide"></h1>
				<h2 class="sub-title">生活热爱分享 - Thousands Find</h2>
			</div>

			<div class="cont-main clearfix">
				<div class="index-tab">
					<div class="index-slide-nav">
						<router-link to="/login">登录</router-link>
						<router-link to="/register" class='active'>注册</router-link>
						<div class="slide-bar slide-bar1"></div>				
					</div>
				</div>

				<div class="login form">
					<div class="group">
						<form action="" method='post'>
						<div class="group-ipt email">
							<input type="email" v-model="formdata.email" id="email" class="ipt" placeholder="邮箱地址" required>
						</div>
						<div class="group-ipt user">
							<input type="text" v-model="formdata.username" id="user" class="ipt" placeholder="选择一个用户名" required>
						</div>
						<div class="group-ipt password">
							<input type="password" v-model="formdata.password" id="password" class="ipt" placeholder="设置登录密码" required>
						</div>
						<div class="group-ipt password1">
							<input type="password" v-model="formdata.password1" id="password1" class="ipt" placeholder="重复密码" required>
						</div>
						<!-- <div class="group-ipt verify">
							<input type="text" name="verify" id="verify" class="ipt" placeholder="输入验证码" required>
							<img src="http://zrong.me/home/index/imgcode?id=" class="imgcode">
						</div> -->
						</form>
					</div>
				</div>

				<div class="button">
					<button @click='regfn' type="button" class="login-btn register-btn" id="button">注册</button>
				</div>
			</div>
		</div>

		<div class="footer">
			<p>© 2010-2016 All rights reserved. KeyCode: cheap soccer jerseys , replica soccer jerseys </p>
		</div>
	</div>
</template>

<script>
	import '../../assets/css/loginRegister.css';
	import '../../assets/plugin/particles/particles.min.js';
	import particles_background from '../../assets/plugin/particles/background.js';
	import * as types from '../../vuex/mutation-types'
	import { Indicator , MessageBox  } from 'mint-ui';
	let storage = window.localStorage;
	//storage.clear();
	export default {
		name: 'login',
		data() {
			return {
				phone:"10086",
				verify:"006",
				isverify:true,
				routeback:"",
				MY_URL:this.$store.state.MY_URL,
				formdata : {}
			}
		},
		created (){
			this.$nextTick(() => {

				particlesJS('register-box',particles_background);
			});
		},
		mounted (){			
		},
		methods:{

			regfn(){
				
				Indicator.open();
				this.$ajax({
					method:"post",
					url:this.MY_URL+"/user/reg",
					data:this.formdata
				}).then( (data)=>{
					let obj = data.data.data;
					Indicator.close();
					if(data.data.state == 'success'){
						MessageBox.alert('注册成功', '注册成功啦').then( btn => {
							this.$router.push({ path: 'wx' });
						});
						storage.setItem(types.CHECK_LOGIN_STATUS,true);
						this.$store.commit(types.CHECK_LOGIN_STATUS,{
							obj
						});
						
					}else{

						MessageBox.alert(data.data.head,"注册失败");
					}
				}).catch( (error) =>{
					Indicator.close();
					console.log("error",error);
				});
				
			}
		}
		
	}
</script>
