<template>
	<div>
		<div class="header">
			<a href="javascript:history.go(-1)"><img src="../../common/img/userCenter/arrowsb.png" alt="" class="back" /></a>
			<span>谷歌验证码</span>
		</div>
		<div class="appeal">
			<p>
				若谷歌验证器丢失 <br /> 请联系客服kefu@liyugame.com申诉
			</p>
		</div>
		<div class="input">
			<input type="text" class="input-juli" maxlength="1" placeholder="-" />
			<input type="text" class="input-juli" maxlength="1" placeholder="-" />
			<input type="text" class="input-juli" maxlength="1" placeholder="-" />
			<input type="text" class="input-juli" maxlength="1" placeholder="-" />
			<input type="text" class="input-juli" maxlength="1" placeholder="-" />
			<input type="text" class="input-juli" maxlength="1" placeholder="-" />
		</div>

	</div>
</template>

<script>
	export default {
		data() {
			return {
				keyData: "",
				vType:this.$route.query.vType
			}
		},
		methods: {
			postkey: function(arg) {
				let vm = this;
				if(vm.vType==1){
					$.ajax({
					type: "post",
					url: contextPath + "/liyu_game/api/googleauthenticator/delAuthenticator",
					async: true,
					dataType: "json",
					data: {
						token: localStorage.token,
						code: arg
					},
					success: function(data) {
						mui.toast("关闭验证成功!");
						vm.$router.push("/advancedSetting");
					}
				})
				}else{
					$.ajax({
					type: "post",
					url: contextPath + "/liyu_game/api/googleauthenticator/validation",
					async: true,
					dataType: "json",
					data: {
						token: localStorage.token,
						code: arg
					},
					success: function(data) {
						mui.toast("验证成功!");
						vm.$router.push("/advancedSetting");
					}
				});
				}
			}
		},
		mounted: function() {
			let vm = this;
			
			console.log(vm.vType);
			
			var numStr="";
			$('.input-juli').on('keyup', function() {
				var $input = $(this).next('input');
				if($input.length > 0) {
					$input.focus();
				}else{
					var inputjulis =document.querySelectorAll(".input-juli");
					for (var i = 0; i < inputjulis.length; i++) {
						numStr = numStr + $(inputjulis[i]).val();
					}
					vm.postkey(numStr);
				}
			});
		}
	}
</script>

<style scoped>
	.header {
		width: 6.4rem;
		height: 0.88rem;
		background: #006b8d;
		position: fixed;
		top: 0;
		z-index: 9999;
	}
	
	.header img {
		width: 0.2rem;
		height: 0.35rem;
		margin-left: 0.2rem;
		float: left;
		margin-top: 0.25rem;
	}
	
	.header span {
		width: 5.6rem;
		color: #fff;
		display: block;
		float: left;
		line-height: 0.88rem;
		font-size: 0.34rem;
		text-align: center;
	}
	
	.appeal {
		width: 6.4rem;
		margin-top: 1.54rem;
	}
	
	.appeal p {
		width: 6rem;
		margin: 0 auto;
		color: #000000;
		font-size: 0.26rem;
		line-height: 0.37rem;
	}
	
	.input {
		width: 5.6rem;
		margin: 0 auto;
		margin-top: 0.25rem;
	}
	
	.input input {
		width: 0.76rem;
		height: 0.55rem;
		float: left;
		border: none;
		border-bottom: 1px solid #cfcfcf;
		color: #006b8d;
		font-size: 0.34rem;
		margin-left: 0.14rem;
		text-align: center;
		border-radius: 0;
	}
</style>