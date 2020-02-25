<template>
	<view id="index-container">
		<!-- 头部 -->
		<view class="index-header">
			<!-- 左侧view -->
			<view class="index-header__left">
				<text class="active__text">全部</text>
				<text>10条</text>
			</view>

			<!-- 右侧view -->
			<view class="index-header__right">
				<view class="index-header__right-item active_tab">全部</view>
				<view class="index-header__right-item">待办</view>
				<view class="index-header__right-item">已完成</view>
			</view>
		</view>
		
		<!-- 内容 -->
		<view class="index-content">
			<view class="index-cell">
				<view class="index-cell__checkbox"></view>
				<view class="index-cell__title">
					我的待办事项
				</view>
			</view>
			
			<view class="index-cell index-cell-finish">
				<view class="index-cell__checkbox"></view>
				<view class="index-cell__title">
					我的待办事项
				</view>
			</view>
		</view>
		
		<!-- 底部 + 加 -->
		<view class="index-plus">
			<text class="iconfont icon-add"></text>
		</view>
	
		<!-- 内容输入框 -->
		<view class="index-input">
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {

		},

		onLoad() {

		}
	}
</script>

<style lang="scss" scoped>
	@import './index.scss';
	@import '../../others/iconfont.css';
</style>
