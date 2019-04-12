<template>
	<div>
		<ul>
			<li>
				<div>
					账号：
					<input type="text" v-model="test1" placeholder="请输入账号" maxlength="11" onkeyup="value=value.replace(/[^0-9.]/g,'') " ref="input1" @blur="changeName(test1)"><br /> 密码：
					<input type="password" v-model="test2" placeholder="请输入密码" ref="input2" @blur="changeName1(test2)"><br /> 验证码：
					<input type="text" v-model="test3" placeholder="请填写验证码" ref="input3">
					<button @click="getYzm">{{codeText}}</button><br />
				</div>
			</li>
		</ul>
		<div @click="loginBtn()">点击登录</div>
	</div>
</template>
<script type="text/javascript">
	export default {
		data() {
				return {
					test1: '',
					test2: '',
					test3: '',
					codeText: '获取验证码',
				}
			},

			methods: {
				//获取验证码
				getYzm() {
					let reg = /^1[0345789][0-9]{9}$/;
					if(this.test1 == '' || this.test2 == "") {//验证当用户输入的手机号为空或者不正确时不能进行获取验证码
						this.$message({
							message: '手机号密码不能为空！',
							type: 'warning'
						});
					} else if(!reg.test(this.test1)) {
						this.$message.error("请输入正确的手机号");
					} else {
						this.timer();
						console.log(this.test1);
					}

				},
				timer() {
					let num = 60;
					let that = this;
					that.codeText = num + "秒后重新发送";
					let time = setInterval(function() {
						if(num == 0) {
							clearInterval(time);
							time = null;
							that.codeText = "重发验证码";
							that.disabled='';
						} else {
							num--;
							that.codeText = num + "秒后重新发送";
							that.disabled='disabled';
						}

					}, 1000);
				},
				//用户名的失去光标判断
				changeName(userName) {
					let name = userName;
					if(name == '' || name == undefined || name == null) {
						// 用户名为空时，input框获得焦点
						this.$refs.input1.focus();
					} else {
						console.log(name);
					}
				},
				//密码框失去光标判断
				changeName1(pass) {
					if(pass == '' || pass == undefined || pass == null) {
						// 密码为空时，input框获得焦点
						this.$refs.input2.focus();
					} else {
						console.log(pass);
					}
				},
				loginBtn() {
					//一般来讲，获取DOM元素，需document.querySelector（".input1"）获取这个dom节点，然后在获取input1的值。但是用ref绑定之后，我们就不需要在获取dom节点了，直接在上面的input上绑定input1，然后$refs里面调用就行。然后在javascript里面这样调用：this.$refs.input1  这样就可以减少获取dom节点的消耗了
					this.test1 = this.$refs.input1.value;//获取input1的值，减少获取dom节点的消耗    
					this.test2 = this.$refs.input2.value;
					this.test3 = this.$refs.input3.value;
					if(this.test3 == '') {
						this.$message.error('请输入验证码');
					} else {
						this.$message({
							message: '恭喜你，登陆成功！',
							type: 'success'
						});
						this.$router.push({ path: '/table' });
						console.log(this.test1);
						console.log(this.test2);
						console.log(this.test3);

					}
				},

			}
	}
</script>