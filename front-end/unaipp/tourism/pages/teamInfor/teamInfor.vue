<template>
	<view>
		<view class="f1">
			<swiper class="swiper" :indicator-dots="true" :autoplay="true" :interval="2000" :duration="500">
				<swiper-item v-for="(item,index) in itemData.fileList" :key="index">
					<view class="img" :style="{ background: 'url(' + item + ')' }"></view>
				</swiper-item>

			</swiper>
		</view>
		<view class="con">
			<view class="introduce">
				{{itemData.introduce}}
			</view>
			<view class="">
				出发地：{{itemData.departure}}
				</br>
				目的地：{{itemData.destination}}
			</view>
			<view class="price">
				<view class="">
					￥{{itemData.price}}
				</view>
			</view>
			<button type="default" @click="toggleNumShow()">预定</button>
		</view>
		<view class="con">
			<text class="path_tite">路径介绍</text>
			<view class="path_item" v-for="(item,index) in itemData.buZhou" :key="index">
				{{index}}: &nbsp; &nbsp;{{item}}
			</view>
			<view class="ti_shi">
				温馨提示
				<br />
				【关于购物场所】
				1.在旅游行程中，个别景点景区、餐厅、休息区等场所存在商场等购物场所，上述场所非旅行社安排的指定购物场所。本公司提醒旅游者根据自身需要，理性消费并索要必要票据。如产生消费争议，请自行承担相关责任义务，由此带来的不便，敬请谅解！
				2.目的地可能有部分私人经营的娱乐、消费场所，此类组织多数无合法经营资质，存在各种隐患。为了您的安全和健康考虑，本公司提醒您，谨慎消费；
				<br />
				【关于不可抗力因素】
				1.本产品行程实际出行中，导游、司机可能会根据天气、交通等情况，对您的行程进行适当调整（如调整景点游览顺序等），以确保行程顺利进行。如因不可抗力等因素确实无法执行原行程计划，对于因此而造成的费用变更，我社实行多退少补，敬请配合；
				2.行程中的赠送项目，如因交通、天气等不可抗因素导致不能赠送的、或因您个人原因不能参观的，费用不退，敬请谅解；
				3.因玉龙雪山冰川大索道实行限票制，旺季（暑假、寒假、春节等节假日）期间出行不保证上大索道，如实际出行时上不了大索道则退门票差价安排小索道，望知晓。
				4.如遇春节、元旦、国庆、寒暑假等旺季出行，动车票资源紧张，本社会调整火车卧铺或汽车往返，请知晓！
				5.如遇春节、元旦、国庆、寒暑假等旺季出行，国际五星酒店因资源紧张无法安排，则安排至同级酒店或退差价安排商务酒店。
				<br />
				【温馨提示】
				1.全程请您妥善保管好您的身份证件及贵重物品，以免因遗失等情况影响了旅行；
				2.由于旅游产品包含因素较多，为提高客户体验，我社会对产品进行更新、升级；您拍下付款时的产品细节和您出行的产品细节会有所出入，在您抵达昆明时，我社工作人员会把准确的行程单与您核对，行程将按照行程单执行。
				3.此行程为特价打包产品，指定最少2成人及以上预定，低于此人数下单视为无效订单，不便之处，敬请谅解！
				4.因客人是失信人员导致乘坐不了飞机、火车、高铁，并未提前告知工作人员，所产生的一切费用自行承担。
				5.8人及以上出游人数下单前请先咨询客服！如果未咨询拍下付款，则视为无效订单，不便之处，敬请谅解！
				6.本行程只支持纸质版合同，会在抵达昆明的第一天由合同专员当面签署并讲解行程及注意事项，请知晓！
				7.由于铁路局政策原因，如客人由于自身原因需火车/动车退票、改期，请持身份证原件自行操作，望悉知！
				8.跟团产品需您全程跟团，期间不可出现离团及脱团行为，请您予以配合。如您擅自离团，视为您单方面违约，需承担已损失的机票、车费、住宿费，旅行社有权在您违约后终止您的后继行程及服务，包括您的回程机票，之后发生的任何事情均需您自行全权负责。
				9.该团为各地游客散拼组成，出发地不同，机票价格不一致会导致所拍价格不一致，行程段具体以合同为准，望悉知！
			</view>
			<view class="prov">
				提供商：{{itemData.provider}}
			</view>
		</view>
		<view class="wen_id">
			文章id:{{itemData.tId}}
		</view>
		<send-phone-num v-show="sendNumShow"></send-phone-num>
	</view>
</template>

<script>
	import sendPhoneNum from "../compent/sendPhoneNum.vue";
	export default {
		components:{
			sendPhoneNum
		},
		data() {
			return {
				itemData: [],
				sendNumShow:false
			}
		},
		methods: {
			toggleNumShow(){
				this.sendNumShow = !this.sendNumShow;
			}
		},
		onShow() {
			let that = this;
			uni.getStorage({
				key: 'teamInfor',
				success: function(res) {
					that.itemData = res.data;
					console.log(that.itemData);
				}
			});
		}
	}
</script>

<style scoped>
	.prov{
		font-size: 14px;
		color: #333333;
	}
	.wen_id{
		font-size: 10px;
		color: grey;
	}
	.ti_shi{
		font-size: 12px;
		color: grey;
		margin: 10px 0px;
	}
	.path_item {
		padding: 10px;
		border-radius: 4px;
		margin: 10px;
		font-size: 18px;
		font-weight: bold;
		box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
	}

	.path_tite {
		font-size: 20px;
		font-weight: bold;
	}

	.introduce {
		font-size: 26px;
		color: green;
		font-weight: bold;
	}

	.con {
		padding: 10px 20px;
		border-bottom: 1px dashed grey;
	}

	.f1 {
		padding: 10px 0;
	}

	.price {
		font-size: 24px;
		color: orange;
	}

	.img {
		width: 100%;
		height: 100%;
		background-position: center !important;
		background-size: contain !important;
		background-repeat: no-repeat !important;
	}
</style>
