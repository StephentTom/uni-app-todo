<template>
	<view id="index-container">
		<!-- 头部 -->
		<view class="index-header" v-if="works.length !== 0">
			<!-- 左侧view -->
			<view class="index-header__left">
				<text class="active__text">{{workTypeName}}</text>
				<text>{{resultWorks.length}}条</text>
			</view>

			<!-- 右侧view -->
			<view class="index-header__right">
				<view 
					class="index-header__right-item" 
					:class="{'active_tab': workType==0}"
					@click="workTypeClick(0)"
				>全部</view>
				<view 
					class="index-header__right-item" 
					:class="{'active_tab': workType==1}"
					@click="workTypeClick(1)"
				>待办</view>
				<view 
					class="index-header__right-item"
					:class="{'active_tab': workType==2}"
					@click="workTypeClick(2)"
				>已完成</view>
			</view>
		</view>

		<!-- 内容 -->
		<view class="index-content" v-if="works.length !== 0">
			<view 
				class="index-cell" 
				:class="{'index-cell-finish': item.isChecked}"
				v-for="(item, index) in resultWorks" 
				:key="item.id"
				@click="cellClick(index)"
			>
				<view class="index-cell__checkbox"></view>
				<view class="index-cell__title">
					{{item.content}}
				</view>
			</view>
		</view>

		<!-- 没有数据时显示视图 -->
		<view class="noContentView" v-else>
			<image src="../../static/others_noMsg.png" mode="aspectFit"></image>
			<view class="noContentView-title">您还没有任何待办事项</view>
			<view class="noContentView-title">点击下方 + 号创建一个吧</view>
		</view>
		
		<!-- 底部 + 加 -->
		<view class="index-plus" @click="didClickedPlus">
			<text class="iconfont icon-add"></text>
		</view>

		<!-- 内容输入框 -->
		<view class="index-input" v-show=isActiveInput>
			<input ref="todoInput" type="text" placeholder="请输入您要创建的doto" placeholder-style="color: #a0a0a0;" v-model="textString">
			<view class="create-button" @click="createTodoClick">创建</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 数据源
				works: [],
				// 是否显示输入框
				isActiveInput: false,
				// 文本
				textString: '',
				// 事项type
				workType: 0,
				// 事项type名称
				workTypeName: '全部'
			}
		},
		computed: {
			// 计算workType下不同数据源
			resultWorks() {
				let tempWorks = [];
				
				// 点击全部
				if (this.workType === 0) {
					return this.works;
				} 
				// 点击待办
				if (this.workType === 1) {
					this.works.forEach(item=>{
						if (item.isChecked == false) {
							tempWorks.push(item);
						}
					});
					
					return tempWorks;
				}
				// 点已完成
				if (this.workType === 2) {
					this.works.forEach(item=>{
						if (item.isChecked) {
							tempWorks.push(item);
						}
					});
					return tempWorks;
				}
				return [];
			}
		},
		onLoad() {
		
		},
		methods: {
			// 点击plus事件
			didClickedPlus() {
				this.isActiveInput = !this.isActiveInput;
			},
			
			// 创建todo事件
			createTodoClick() {
				if (this.textString.length === 0) { 
					uni.showToast({
						icon: 'none',
						title: '请输入内容',
						mask: true
					});
					return ;
				}
				
				// 把新数据插到第一条
				this.works.unshift({
					// new Date().getTime(): 创建个时间戳
					id: 'id' + new Date().getTime(),
					isChecked: false,
					content: this.textString,
				});
				this.isActiveInput = false;
				this.textString = '';
			},
			
			// 点击cell事件; 取消办事项目or重启办事项目
			cellClick(index) {
				let item = this.resultWorks[index];
				item.isChecked = !item.isChecked;
			},
			
			// 事项类型点击事件
			workTypeClick(index) {
				this.workType = index;
				
				if (this.workType === 0) {this.workTypeName = "全部"}
				if (this.workType === 1) {this.workTypeName = "待办"}
				if (this.workType === 2) {this.workTypeName = "已完成"}
			}
		}
	}
</script>

<style lang="scss" scoped>
	@import './to.scss';
	@import '../../others/iconfont.css';
</style>