<template>
	<view>
		<!-- 顶部导航 -->
		<view class="d-flex border-top border-bottom" style="height: 90rpx;">
			<view class="d-flex flex-nowrap j-center a-center" style="width: 25%;" v-for="(item,index) in screen.list" :key="index" @click="clickTab(item,index)">
				<view class="tabbar " :class="screen.currentIndex == index ? 'selectColor' : 'commonColor'">{{item.name}}</view>
				<view>
					<view class="iconfont icon-paixu-shengxu line-h0" :class="screen.currentIndex == index&&item.status == 1 ? 'selectColor' : 'commonColor' "></view>
					<view class="iconfont icon-paixu-jiangxu line-h0" :class="screen.currentIndex == index&&item.status == 0 ? 'selectColor' : 'commonColor' "></view>
				</view>
			</view>
			<view style="width: 25%;text-align: center;" @click="clickDrawer">
				<view style="white-space: nowrap;line-height: 90rpx;">
					筛选
				</view>
			</view>
		</view>
		<!-- 抽屉 -->
		<uni-drawer :visible="showRigth" mode="right" @close="showRigth = false">
			<card headTitle="服务">
				<radio-group :label="label" @submig="addmsgA" ></radio-group>
			</card>
			<card headTitle="分类">
				<radio-group :label="label" @submig="addmsgB"></radio-group>
			</card>
			<!-- 按钮 -->
			<view class="d-flex position-fixed bottom-0 right-0 w-100 border-top border-light-secondary">
				<view class="flex-1 main-bg-color text-white font-md py-2 text-center" hover-class="main-bg-hover-color" @click="drawerSelect">确定</view>
				<view class="flex-1 font-md py-2 text-center"
				hover-class="bg-light-secondary" @click="drawerReset">重置</view>
			</view>
		</uni-drawer>
		<!-- 内容列表 -->
		
		<view class="a-center" v-for="(value,index) in list" :key="index" @click="clickList(value)">
			<search-item :item="value"></search-item>
			<view class="" style="height: 2rpx; background-color: #666666;"></view>
		</view>
	</view>
</template>

<script>
	import card from "@/components/common/card.vue"
	import uniDrawer from "@/components/common/uni-drawer.vue"
	import searchItem from "@/components/search-list/search-item.vue";
	import radioGroup from "@/components/common/radio-group.vue"
	export default {
		components:{
			searchItem,uniDrawer,card,radioGroup
		},
		data() {
			return {
				list:[
					{
						title:"真无限蓝牙耳机",
						titlepic:"/static/images/demo/demo6.jpg",
						desc:"雅致简约 / 分体式入耳 / 收纳盒充电 / 蓝牙5.0 / 触控操作",
						pprice:100,
						comment_num:1300,
						good_num:"98%"
					},
					{
						title:"真无限蓝牙耳机",
						titlepic:"/static/images/demo/demo6.jpg",
						desc:"雅致简约 / 分体式入耳 / 收纳盒充电 / 蓝牙5.0 / 触控操作",
						pprice:100,
						comment_num:1300,
						good_num:"98%"
					},
					{
						title:"真无限蓝牙耳机",
						titlepic:"/static/images/demo/demo6.jpg",
						desc:"雅致简约 / 分体式入耳 / 收纳盒充电 / 蓝牙5.0 / 触控操作",
						pprice:100,
						comment_num:1300,
						good_num:"98%"
					},
					{
						title:"真无限蓝牙耳机",
						titlepic:"/static/images/demo/demo6.jpg",
						desc:"雅致简约 / 分体式入耳 / 收纳盒充电 / 蓝牙5.0 / 触控操作",
						pprice:100,
						comment_num:1300,
						good_num:"98%"
					},
					{
						title:"真无限蓝牙耳机",
						titlepic:"/static/images/demo/demo6.jpg",
						desc:"雅致简约 / 分体式入耳 / 收纳盒充电 / 蓝牙5.0 / 触控操作",
						pprice:100,
						comment_num:1300,
						good_num:"98%"
					},
					{
						title:"真无限蓝牙耳机",
						titlepic:"/static/images/demo/demo6.jpg",
						desc:"雅致简约 / 分体式入耳 / 收纳盒充电 / 蓝牙5.0 / 触控操作",
						pprice:100,
						comment_num:1300,
						good_num:"98%"
					},
					{
						title:"真无限蓝牙耳机",
						titlepic:"/static/images/demo/demo6.jpg",
						desc:"雅致简约 / 分体式入耳 / 收纳盒充电 / 蓝牙5.0 / 触控操作",
						pprice:100,
						comment_num:1300,
						good_num:"98%"
					},
					{
						title:"真无限蓝牙耳机",
						titlepic:"/static/images/demo/demo6.jpg",
						desc:"雅致简约 / 分体式入耳 / 收纳盒充电 / 蓝牙5.0 / 触控操作",
						pprice:100,
						comment_num:1300,
						good_num:"98%"
					},
					{
						title:"真无限蓝牙耳机",
						titlepic:"/static/images/demo/demo6.jpg",
						desc:"雅致简约 / 分体式入耳 / 收纳盒充电 / 蓝牙5.0 / 触控操作",
						pprice:100,
						comment_num:1300,
						good_num:"98%"
					}
				],
				showRigth: false,
				selectLabelA:"",
				selectLabelB:"",
				screen:{
					currentIndex:0,
					list:[
						{ name:"综合",status:1 },
						{ name:"销量",status:0 },
						{ name:"价格",status:0 },
					]
				},
				label:{
					selected:0,
					list:[
						{name:"选项一"},
						{name:"选项二"},
						{name:"选项三"},
					]
				}
			}
		},
		onLoad(e){	//路由跳转传值
			console.log(e)
		},
		methods: {
			clickList(value){
				console.log(value.title)
			},
			clickTab(item,index){
				if(this.screen.currentIndex !== index){
					this.screen.currentIndex = index
				}else{
					if(this.screen.list[index].status == 1){
						this.screen.list[index].status = 0
					}else{
						this.screen.list[index].status = 1
					}
				}
			},
			clickDrawer(){
				this.showRigth = true
			},
			// 按钮组件传值
			addmsgA(value){
				console.log(value.target.__args__)	//这是选中的选项
				let index = value.target.__args__;
				this.selectLabelA = this.label.list[index];
			},
			addmsgB(value){
				console.log(value.target.__args__)	//这是选中的选项
				let index = value.target.__args__;
				this.selectLabelB = this.label.list[index];
			},
			//侧边栏确认
			drawerSelect(){
				console.log(`服务第${this.selectLabelA},分类${this.selectLabelB}`)
			},
			//侧边栏重置
			drawerReset(){
				//重置》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》》
			}
		}
	}
</script>

<style>
	.tabbar{
		line-height: 100rpx; 
		font-size: 25rpx;
		width: 33%;
		text-align: center;
	}
	.selectColor{
		color:#FD6801
	}
	.commonColor{
		color:#666666
	}
</style>
