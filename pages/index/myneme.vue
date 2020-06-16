<template>
	<view class="content">
		<image :src="data1.avatarUrl" mode="" style="width: 100rpx;height: 100rpx;border-radius: 50%;"></image>
		<view v-text="data1.nickName">
			
		</view>
		<view v-text="data1.city">
			
		</view>
		<view v-text="data1.country">
			
		</view>
		
	</view>
</template>

<script>
	export default{
		data(){
			return{
				data1:{}
			}
		},
		onLoad() {
			let _this=this
			uni.getStorage({
			    key: 'nemess',
			    success: function (res) {
			        console.log(JSON.parse(res.data));
					_this.data1=JSON.parse(res.data)
			    }
			});
		}
	}
</script>

<style lang="less" scoped>
	.content{
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}
</style>
