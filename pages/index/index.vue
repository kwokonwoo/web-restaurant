<template>
	<view class="content">
		<image src="../../static/dose-juice-sTPy-oeA3h0-unsplash_1592656605910.jpg" mode="aspectFill" class="img"></image>
		<view class="bar">
			<view class="datmo date">W{{fir}}&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspD{{day}}</view>
			<view class="datmo money">{{money}}&nbsp&nbsp&nbsp&nbsp&nbsp{{''}}</view>
		</view>
		<view class="chum chef">
			<view class="ch">
				<view class="che" style="background:linear-gradient(to right,rgb(255,183,100) 50%,rgb(255,170,0) 50%)">
					<image src="../../static/iconfinder_Chef-2_379358.png" mode="aspectFill" class="chefImg"></image>
				</view>
				<image src="../../static/iconfinder_Food-Dome_379366.png" mode="aspectFill" class="chushen" style="opacity: 0"></image>
				<view class="chefProgress">
					 <progress percent="50" stroke-width="40" activeColor="rgb(255,170,0)" backgroundColor="rgb(255,183,100)" class="pro"/>
					 <text class="tnt">UI炖LI</text>
				</view>
			</view>
			<view class="ch">
				<view class="che" style="background:linear-gradient(to right,rgb(153,50,255) 50%,rgb(148,0,211) 50%)">
					<image src="../../static/iconfinder_Chef-2_379358.png" mode="aspectFill" class="chefImg"></image>
				</view>
				<image src="../../static/iconfinder_Food-Dome_379366.png" mode="aspectFill" class="chushen" style="opacity: 1"></image>
				<view class="chefProgress">
					 <progress percent="0" stroke-width="40" activeColor="rgb(148,0,211)" backgroundColor="rgb(153,50,255)" class="pro"/>
					 <text class="tnt">鲜榨flex</text>
				</view>
			</view>
			<view class="ch">
				<view class="che" style="background:linear-gradient(to right,rgb(255,183,100) 50%,rgb(255,170,0) 50%)">
					<image src="../../static/iconfinder_Chef-2_379358.png" mode="aspectFill" class="chefImg"></image>
				</view>
				<image src="../../static/iconfinder_Food-Dome_379366.png" mode="aspectFill" class="chushen" style="opacity: 0"></image>
				<view class="chefProgress">
					 <progress percent="80" stroke-width="40" activeColor="rgb(255,170,0)" backgroundColor="rgb(255,183,100)" class="pro"/>
					 <text class="tnt">红烧HEAD</text>
				</view>
			</view>
			<view class="ch" v-for="(chef,index) in chefs" :key="chef.name">
				<view class="che" :style="{backgroundColor:chef.bC}">
					<image :src="chef.img" mode="aspectFill" class="chefImg"></image>
					<text class="addIcon delete" style="transform: rotateZ(47deg);" @tap="Dchef(index)">+</text>
				</view>
				<image src="../../static/iconfinder_Food-Dome_379366.png" mode="aspectFill" class="chushen" style="opacity: 0;"></image>
				<view class="chefProgress" style="opacity: 0;">
					<progress percent="50" stroke-width="40" :activeColor="chef.colorA" :backgroundColor="chef.colorB" class="pro"/>
					<text class="tnt">{{chef.Cname}}</text>
				</view>
			</view>
			<view class="che ad" @tap="Achef">
				<image src="../../static/whiteChef.png" mode="aspectFill" class="add"></image>
				<text class="addIcon">+</text>
			</view>
		</view>
		<view class="chum customer">
			<view v-for="(custom,index) in customs" :key="custom.name" class="po">
					<image src="../../static/iconfinder_Instagram_UI-07_2315589.png" mode="aspectFill" class="anfu" :style="{opacity:custom.anfu}"></image>
					<image src="../../static/iconfinder_Euro-Coin_379523.png" mode="aspectFill" :style="{opacity:custom.jiezhang}" class="anfus"></image>
					<image :src="custom.img" mode="aspectFill" class="custo" :style="{background:custom.bC}"></image>
					<view class="caipo">
						<view class="ppi" v-for="co in custom.cos">
							<view class="chiProgress">
								<progress :percent="co.progress" stroke-width="40" active="true" :activeColor="co.colorA" :backgroundColor="co.colorB" class="pro"/>
								<text class="tnt" :style="{'text-decoration':co.line}">{{co.Cname}}</text>
							</view>
							<view class="kpos" :style="{opacity:co.cww}">
								<image src="../../static/iconfinder_Food-Dome_379366.png" mode="aspectFill" class="kpo"></image>
							</view>
						</view>
					</view>
			</view>
		</view>
		<view class="relaxBar">
			<view class="uui" v-for="(relaxCustom,index) in relaxCustoms" :key="relaxCustom.name" :style="{'z-index':-index}">
				<image :src="relaxCustom.img" mode="aspectFill" class="relaxCustom"></image>
				<view class="wait">
					 <progress :percent="relaxCustom.progress" stroke-width="30" activeColor="rgb(0,100,255)" backgroundColor="rgb(0,181,255)" class="pro"/>
					<text class="waitText">等位中</text>
				</view>
			</view>
		</view>
		<!-- 屏幕弹窗 -->
		<uni-popup ref="popup" type="center">
			<view class="chum startMessage" v-if="noticeA">
				<text class="title">WebMOOC餐厅开业啦!</text>
				<text class="text">WebMOOC餐厅即将开业，请认真经营你的餐厅吧</text>
				<text class="text Tother">经营餐厅需要做好下面几件事情! 加油!</text>
				<view class="divBar">
					<text v-for="mo in mos" class="mo">{{mo}}</text>
				</view>
				<view class="datmo buttonS" @tap="close">
					<text class="sttr">开始经营吧</text>
				</view>
			</view>
			<view class="chum startMessage ls" v-if="noticeG">
				<text class="zaoChef">招聘新厨师</text>
				<view class="ri">
					<text class="tG">招聘一名厨师可以帮你更快地为顾客烹饪菜肴，</text>
					<text class="tG">增加餐厅收入，你最多可以拥有六名厨师。</text>
					<text class="tG">但每个厨师每周需要你支付工资 ￥ 100</text>
					<text class="tG">请问您确认新招聘一名厨师吗？</text>
				</view>
				<view class="caibutton">
					<view class="datmo caiok" @tap="back">
						<text class="sttr">是的，确认招聘</text>
					</view>
					<view class="datmo caino" @tap="back">
						<text class="sttr">先不了</text>
					</view>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from '@/components/uni-popup/uni-popup.vue';
	export default {
		components:{
			uniPopup
		},
		data() {
			return {
				fir:12,
				day:5,
				money:'1,948,343',
				chefs:[
					{img:'../../static/iconfinder_Chef-2_379358.png'}
				],
				noticeA:true,
				noticeG:false,
				customs:[
					{anfu:1,jiezhang:0,bC:'linear-gradient(to right,rgb(178,34,34) 50%,rgb(139,0,0) 50%)',cos:[{progress:100,Cname:'UI炖LI',colorA:'rgb(25,25,112)',colorB:'',cww:0,line:'line-through'},{progress:100,Cname:'鲜榨flex',colorA:'rgb(25,25,112)',colorB:'',cww:0,line:'line-through'}],img:'../../static/379446-512.png'},
					{anfu:0,jiezhang:1,bC:'linear-gradient(to right,rgb(0,255,0) 50%,rgb(34,139,34) 50%)',cos:[{progress:100,Cname:'UI炖LI',colorA:'rgb(34,139,34)',colorB:'',cww:0},{progress:100,Cname:'UI炖LI',colorA:'rgb(34,139,34)',colorB:'',cww:0},{progress:100,Cname:'UI炖LI',colorA:'rgb(34,139,34)',colorB:'',cww:0}],img:'../../static/379448-512.png'},
					{anfu:0,jiezhang:0,bC:'linear-gradient(to right,rgb(255,183,100) 50%,rgb(255,170,0) 50%)',cos:[{progress:50,Cname:'UI炖LI',colorA:'rgb(255,170,0)',colorB:'rgb(255,183,100)',cww:0}],img:'../../static/iconfinder_Boss-3_379348.png'},
					{anfu:0,jiezhang:1,bC:'linear-gradient(to right,rgb(0,255,0) 50%,rgb(34,139,34) 50%)',cos:[{progress:100,Cname:'UI炖LI',colorA:'rgb(34,139,34)',colorB:'',cww:0},{progress:100,Cname:'UI炖LI',colorA:'rgb(34,139,34)',colorB:'',cww:0},{progress:100,Cname:'红烧HEAD',colorA:'rgb(25,25,112)',colorB:'',cww:0,line:'line-through'}],img:'../../static/iconfinder_Rasta_379441.png'}
				],
				mos:['招聘厨师','迎接客人','烹饪美食'],
				relaxCustoms:[
					{img:'../../static/iconfinder_Man-16_379485.png',progress:50},
					{img:'../../static/379339-512.png',progress:10},
				],
				bC:'linear-gradient(to right,rgb(216,216,216) 50%,rgb(168,168,168) 50%)'
			}
		},
		onLoad() {

		},
		onShow() {
			
		},
		created() {
			this.start();
		},
		watch:{
			
		},
		methods: {
			start(){
				setTimeout(()=>{
					this.$refs.popup.open();
				},1000)
			},
			close(){
				this.noticeA = false;
				this.$refs.popup.close();
			},
			Achef(){
				this.noticeG = true;
				this.$refs.popup.open();
			},
			back(){
				this.noticeG = false;
				this.$refs.popup.close();
			}
		}
	}
</script>

<style>
	page{
		display: flex;
	}
	view {
		display: flex;
		position: relative;
	}
	page{
		width: 750rpx;
		height: 100%;
	}
	.content {
		width: 750rpx;
		height: 100%;
		display: flex;
		flex: 1;
		flex-direction: column;
		align-items: center;
		background-color: #2C405A;
	}
	.img{
		display: flex;
		position: fixed;
		width: 100%;
		height: 100%;
	}
	.bar{
		width: 730rpx;
		height: 90rpx;
		margin-top: 20rpx;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
	}
	.datmo{		
		height: 60rpx;
		border-radius: 40rpx;
		border-style: solid;
		border-width: 12rpx;
		border-color: #663300;
		background: linear-gradient(to bottom,rgba(255,254,162,.9) 50%,rgb(255,215,100) 50%);
		align-items: center;
		font-size: 30rpx;
	}
	.date{
		width: 200rpx;
		justify-content: center;
	}
	.money{
		width: 360rpx;
		justify-content:flex-end;
	}
	.chum{
		border-radius: 30rpx;
		border-style: solid;
		border-width: 12rpx;
		border-color: #FFFFFF;
	}
	.chef{
		width: 700rpx;
		margin-top: 40rpx;
		background-color: rgb(255,215,100);
		align-items: center;
		flex-wrap: wrap;
	}
	.chefImg{
		width: 180rpx;
		height: 180rpx;
	}
	.addIcon{
		position: relative;
		font-size: 90rpx;
		color: #663300;
		opacity: .6;
	}
	.che{
		width: 150rpx;
		height: 150rpx;
		margin-top: 20rpx;
		border-radius: 87rpx;
		border-style: solid;
		border-width: 12rpx;
		border-color: #FFFFFF;
		background: linear-gradient(to right,rgb(216,216,216) 50%,rgb(168,168,168) 50%);
		align-items: center;
		justify-content: center;
	}
	.ch{
		flex-direction: column;
		align-items: center;
		margin-left: 20rpx;
		margin-right: 20rpx;
	}
	.ad{
		background: rgb(216,216,216);
		color: #FFFFFF;
		margin-left: 20rpx;
		margin-bottom: 75rpx;
	}
	.add{
		width: 180rpx;
		height: 180rpx;
		position: fixed;
	}
	.customer{
		width: 700rpx;
		height: 480rpx;
		margin-top: 220rpx;
		background-color: rgb(255,183,100);
		align-items: center;
		flex-wrap: wrap;
	}
	.custo{
		width: 150rpx;
		height: 150rpx;
		margin-bottom: 30rpx;
		border-radius: 87rpx;
		border-style: solid;
		border-width: 12rpx;
		border-color: #FFFFFF;
		background: linear-gradient(to right,rgb(216,216,216) 50%,rgb(168,168,168) 50%);
	}
	.startMessage{
		width: 700rpx;
		height: 430rpx;
		background-color: rgb(255,215,100);
		align-items: center;
		flex-direction: column;
		z-index: 100;
	}
	.title{
		font-size: 37rpx;
		font-weight: 700;
		margin-top: 30rpx;
		margin-bottom: 10rpx;
		opacity: .7;
	}
	.text{
		font-size: 28rpx;
		font-weight: 700;
		opacity: .5;
		margin-top: 10rpx;
	}
	.Tother{
		margin-right: 140rpx;
	}
	.divBar{
		width: 600rpx;
		margin-top: 30rpx;
		display: flex;
		justify-content: space-between;
	}
	.mo{
		font-size: 30rpx;
		font-weight: 700;
		opacity: .5;
	}
	.buttonS{
		width: 600rpx;
		height: 70rpx;
		margin-top: 50rpx;
		border-radius: 100rpx;
		border-width: 5rpx;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.buttonS:active{
		opacity: .5;
	}
	.sttr{
		font-weight: 700;
		opacity: .5;
	}
	.relaxBar{
		width: 700rpx;
		margin-top: -40rpx;
		justify-content: flex-end;
		z-index: 1;
	}
	.relaxCustom{
		width: 120rpx;
		height: 120rpx;
		border-radius: 72rpx;
		border-style: solid;
		border-width: 12rpx;
		border-color: #FFFFFF;
		background: linear-gradient(to right,rgb(0,181,255) 50%,rgb(0,100,255) 50%);
	}
	.uui{
		align-items: center;
		flex-direction: column;
		margin-left: -30rpx;
	}
	.wait{
		width: 132rpx;
		height: 30rpx;
		margin-top: -35rpx;
		border-style: solid;
		border-width: 5rpx;
		border-color: #FFFFFF;
		border-radius: 5rpx;
		position: relative;
		display: flex;
		align-items: center;
		justify-content: center;
		overflow: hidden;
	}
	.waitText{
		font-size: 25rpx;
		color: #FFFFFF;
		position: absolute;
	}
	.customNotice{
		width: 500rpx;
		height: 100rpx;
		border-style: solid;
		border-width: 10rpx;
		border-color: #FFFFFF;
		border-radius: 20rpx;
		background-color: #CC9999;
		align-items: center;
		justify-content: center;
		z-index: 100;
	}
	.tB{
		font-size: 27rpx;
		font-weight: 700;
		margin-left: 50rpx;
		margin-right: 50rpx;
		opacity: .5;
	}
	.tG{
		font-size: 27rpx;
		font-weight: 700;
		opacity: .5;
	}
	.diancai{
		flex-direction: column;
		width: 700rpx;
		margin-right: 20rpx;
	}
	.diancanCustom{
		margin-bottom: -72rpx;
		z-index: 101;
		margin-left: 50rpx;
		align-items: center;
		justify-content: center;
	}
	.caipu{
		width: 700rpx;
		height: 1000rpx;
		background-color: rgb(255,215,100);
		flex-direction: column;
		align-items: center;
		z-index: 100;
	}
	.diancaiMoney{
		font-size: 33rpx;
		position: absolute;
		right: 20rpx;
		top: 15rpx;
		font-weight: 700;
		opacity: .5;
	}
	.caipuI{
		width: 600rpx;
		height: 800rpx;
		margin-top: 70rpx;
		background-color: #FFFFFF;
		border-style: solid;
		border-width: 5rpx;
		border-color: #663300;
		flex-direction: column;
		align-items: center;
	}
	.caibutton{
		width: 600rpx;
		margin-top: 30rpx;
		justify-content: space-between;
	}
	.caiok{
		border-width: 6rpx;
		width: 350rpx;
		height: 70rpx;
		justify-content: center;
	}
	.caino{
		border-width: 6rpx;
		width: 200rpx;
		height: 70rpx;
		justify-content: center;
	}
	.cai{
		width: 550rpx;
		flex-direction: column;
	}
	.wanchengdiancai{
		flex-direction: column;
		background-color: #4CD964;
	}
	.ls{
		height: 400rpx;
	}
	.zaoChef{
		font-weight: 700;
		opacity: .5;
		margin-top: 30rpx;
	}
	.ri{
		width: 600rpx;
		margin-top: 20rpx;
		flex-direction: column;
	}
	.zx{
		top: 135rpx;
		position: absolute;
		z-index: 10;
	}
	.font{
		font-size: 30rpx;
		font-weight: 700;
		color: #663300;
		opacity: .5;
		margin-top: 20rpx;
	}
	.ur{
		font-size: 28rpx;
		font-weight: 700;
		margin-top: 10rpx;
		margin-left: 40rpx;
		color: #663300;
		opacity: .5;
		flex-direction: row;
		align-items: center;
	}
	.sa{
		margin-left: 20rpx;
	}
	.sb{
		position: absolute;
		left: 260rpx;
	}
	.delete{
		position: absolute;
		top: -65rpx;
		right: -17rpx;
	}
	.chefProgress{
		width: 164rpx;
		height: 50rpx;
		margin-top: -20rpx;
		margin-bottom: 30rpx;
		border-style: solid;
		border-radius: 10rpx;
		border-width: 5rpx;
		border-color: #FFFFFF;
		overflow: hidden;
		align-items: center;
		justify-content: center;
	}
	.tnt{
		position: absolute;
		font-size: 25rpx;
		color: #FFFFFF;
		z-index: 10;
	}
	.po{
		
	}
	.anfu{
		width: 100rpx;
		height: 100rpx;
		margin-top: 80rpx;
		margin-right: -100rpx;
		z-index: 5;
	}
	.anfus{
		width: 100rpx;
		height: 100rpx;
		margin-top: 80rpx;
		margin-right: -80rpx;
		z-index: 4;
	}
	.caipo{
		width: 180rpx;
		height: 140rpx;
		margin-left: -40rpx;
		margin-top: 10rpx;
		flex-direction: column;
	}
	.ppi{
		flex-direction: row;
		align-items: center;
	}
	.kpos{
		width: 40rpx;
		height: 40rpx;
		margin-top: 10rpx;
		border-radius: 22rpx;
		background-color: #4CD964;
		align-items: center;
		justify-content: center;
		border-style: solid;
		border-width: 2rpx;
		border-color: #FFFFFF;
	}
	.kpo{
		width: 70rpx;
		height: 70rpx;
	}
	.chiProgress{
		width: 164rpx;
		height: 40rpx;
		border-style: solid;
		border-radius: 10rpx;
		border-width: 5rpx;
		border-color: #FFFFFF;
		overflow: hidden;
		margin-top: 10rpx;
		align-items: center;
		justify-content: center;
	}
	.chushen{
		width: 100rpx;
		height: 100rpx;
		margin-top: -100rpx;
		margin-left: -100rpx;
	}
	.pro{
		width: 164rpx;
		height: 60rpx;
	}

</style>
