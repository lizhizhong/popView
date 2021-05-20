<template>
	<view>
		<view v-if="isShow" class="popupView" @click="popHide(false)">
			<view class="content" @click.stop="conClick">
				<view class="contentView">
					<view class="center">
						<image class="info" v-if="type=='info'" src="../../static/pop/success.png"></image>
						<image class="success" v-if="type=='success'" src="../../static/pop/success.png"></image>
						<image class="warn" v-if="type=='warn'" src="../../static/pop/warn.png"></image>
						<image class="error" v-if="type=='error'" src="../../static/pop/error.png"></image>
						<text>{{content}}</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'popview4',
		props:{
			isShow1:{
				type:Boolean,
				default:false,
			},
			debug1:{
				type:Boolean,
				default:false,
			},
			content1:{
				type:String,
				default:'确定要删除吗?',
			}
		},
		data() {
			return {
				debug: this.debug1,
				isShow:false,
				content:this.content1,
				type:'',
			};
		},
		watch:{
			isShow1(value){
				this.isShow = value;
			},
			debug1(value) {
				this.debug = value
			},
			content1(value) {
				this.content = value
			},
		},
		methods: {
			/*隐藏*/
			popHide(request){
				this.isShow = false;
				this.$emit('hidePop',request);
			},
			/*防止事件往下传递*/
			conClick(){
				
			},
			/*成功*/
			success(message){
				this.isShow = true;
				this.content = message;
				this.type='success';
				this.vanish();
			},
			/*失败*/
			error(message){
				this.isShow = true;
				this.content = message;
				this.type='error';
				this.vanish();
			},
			/*警告*/
			warn(message){
				this.isShow = true;
				this.content = message;
				this.type='warn';
				this.vanish();
			},
			/*提示*/
			info(message){
				this.isShow = true;
				this.content = message;
				this.type='info';
				this.vanish();
			},
			/*消失*/
			vanish(){
				setTimeout(()=>{
					this.isShow = false;
					this.content = '';
				},1000);
			}
			
			
		}
	}
</script>

<style lang="scss">
	/* 动画代码 */
	@keyframes example {
	  0%   {transform:scale(1.2,1.2)}
	  100% {transform:scale(1.0,1.0)}
	}
	.popupView{
		position: fixed;
		z-index: 999;
		
		background-color: rgba($color: #000000, $alpha: 0.2);
		
		// max-width: 800px!important;//设置页面最大宽度
		width: 100%;
		/* width: 100%;
		height: 100vh; */
		width: 100%;height: 100vh;top: 0;left: 0;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.popupView .content{
		width: 300upx;
		height: 300upx;
		display: flex;
		flex-direction: column;
		overflow: hidden;
		
		animation-name: example;//动画代码块
		animation-duration: 0.3s;//持续时间
		animation-fill-mode: forwards;//定格到最后一帧
		
		background-color: $uni-bg-color;
		
		border-radius: 10upx;
		
		
	}
	.popupView .content .contentView{
		width: 100%;
		height: 100%;
		// background-color: red;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.popupView .content .contentView .center{
		height: 100%;
		width: 100%;
		// background-color: red;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.popupView .content .contentView .center>image{
		margin-bottom: 30upx;
		width: 60upx;
		height: 60upx;
	}
	.popupView .content .contentView .center .info{
		color: #288ced;
	}
	.popupView .content .contentView .center .success{
		color: #09be70;
	}
	.popupView .content .contentView .center .warn{
		color: #ff991f;
	}
	.popupView .content .contentView .center .error{
		color: #ef4017;
	}
	.popupView .content .contentView .center>text{
		width: 100%;
		text-align: center;
		font-size: 30upx;
		padding: 0 5upx;
	}
</style>
