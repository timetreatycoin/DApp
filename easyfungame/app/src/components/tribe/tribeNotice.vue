<template>
	<div class="content">
		<div class="header">
			<a href="javascript:history.go(-1)"><img src="../../common/img/userCenter/arrowsb.png" alt="" class="back" /></a>
			<span>公告</span>
		</div>
		<div class="main">
			<div class="tit">
				<h2 v-html="getNoticeData.title"></h2>
			</div>
			<p v-html="getNoticeData.context"></p>
			<div class="foot">
				<span>{{getNoticeData.createtime}}</span>
			</div>
			<div class="line"></div>
		</div>
	</div>
</template>

<script>
	import FootView from '../../common/FootView.vue'
	export default {
		data: function() {
			return {
				getNoticeData:{}
			}
		},
		mounted: function() {
			let vm = this;
				$.ajax({
					type: "get",
					url: contextPath + "/liyu_game/api/tribe/findnoticeById",
					async: true,
					data: {
						id: vm.$route.query.newsId
					},
					dataType: "json",
					success: function(data) {
						vm.getNoticeData = data.data[0];
						console.log(vm.getNoticeData)
					}
				});
		}
	}
</script>

<style scoped >
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
	.content {
		background: #eee;
	}
	
	.mint-header {
		background: #006b8d;
		height: 0.88rem;
		font-size: 0.34rem;
	}
	
	.main {
		width: 6rem;
		/*height: 30rem;*/
		margin: 0 auto;
		background: #fff;
		margin-top: 0.2rem;
	}
	
	.line {
		width: 6rem;
		height: 0.2rem;
		background: #eee;
		position: fixed;
		bottom: 0;
	}
	
	.tit {
		width: 6rem;
		height: 0.7rem;
	}
	
	.tit h2 {
		font-size: 0.24rem;
		color: #006b8d;
		text-align: center;
		line-height: 0.7rem;
	}
	
	.main p {
		width: 5.6rem;
		margin: 0 auto;
		color: #333;
		font-size: 0.22rem;
		line-height: 0.4rem;
	}
	
	.homeimga {
		width: 6rem;
		height: 3.94rem;
		margin-top: 0.17rem;
		margin-bottom: 0.17rem;
	}
	
	.homeimga img {
		width: 5.6rem;
		height: 3.94rem;
		margin: 0 auto;
		display: block;
	}
	
	.foot {
		width: 5.6rem;
		height: 0.8rem;
		margin: 0 auto;
		margin-top: 0.2rem;
	}
	
	.foot span {
		display: block;
		float: right;
		color: #999;
		font-size: 0.22rem;
	}
	
	.foot span:nth-of-type(2) {
		float: right;
	}
	p img{
		width: 5.5rem!important;
	}
</style>