<template>
	<view>
		<view class="uni-padding-wrap">
		    <view class="page-section swiper">
		        <view class="page-section-spacing">
		            <swiper class="swiper" :indicator-dots="indicatorDots" 
					vertical='true'
					:autoplay="autoplay" :interval="interval" :duration="duration" :style="'height:' + '675' +'px;'">
		                <swiper-item v-for="i in datas" :key='i.id'>
							<view v-show="i.id!= 6?true:false">
								<view class="swiper-item" :style="'height:' + '675' +'px;'">
									<view class="swiper-text">{{i.data}}</view>
									<view class="swiper-img"><img :src="i.img" alt=""></view>
								</view>
							</view>
							<view v-show="i.id == 6?true:false">
								<image src="../../static/bg.jpg" class="bg-img"></image>
									<view class="text-box">
										<text class="name">To: 唐丫丫</text>
										<br>
										<text class="content">Merry Christmas </text>
										</view>
										<view class="cover"></view>
									<view :class="box" @tap='change'>
										<ul class="minbox" :style='st'>
											<li></li>
											<li></li>
											<li></li>
											<li></li>
											<li></li>
											<li></li>
										</ul>
										<ol class="maxbox">
											<li></li>
											<li></li>
											<li></li>
											<li></li>
											<li></li>
											<li></li>
										</ol>
									</view>
							</view>
		                </swiper-item>
		            </swiper>
		        </view>
		    </view>
		</view>
		<view style="position: fixed;top:0;width: 20px;height: 20px;z-index: 999;right: 0;">
		    <image src='../../static/yy.png' class="music" :class="on?'music1':''"  @tap='stop' ></image>
		</view>
	</view>
</template>

<script>
	let innerAudioContext = uni.createInnerAudioContext();
	export default {
		components: {
		},
		data() {
			return {
				datas:[
					{id:0 ,data: '1112221',img:'../../static/logo.png'},
					{id:1 ,data: '1133311',img:'../../static/logo.png'},
					{id:2 ,data: '1144411',img:'../../static/logo.png'},
					{id:3 ,data: '115511',img:'../../static/logo.png'},
					{id:4 ,data: '111661',img:'../../static/logo.png'},
					{id:5 ,data: '1177711',img:'../../static/logo.png'},
					{id:6,data:'',img:''}
				],
				interval: 2000,
				duration: 500,
				box: 'box',
				flag: true,
				st: '',
				on:true,
			}
		},
		methods: {
			// 获取轮播和产品数据
			stop(){
				if(this.on){
					this.on = !this.on
				}else{
					this.on = !this.on
				}
				if(!innerAudioContext.paused){//是播放状态我们就暂停
					innerAudioContext.pause();
				}else{
					innerAudioContext.play();//是暂停状态我们就播放
				}
			},
			change(){
				if(this.flag){
					this.st = 'left:10px;top:-30px;'
					this.box = 'box1'
					this.flag = !this.flag
				}else{
					this.st = ''
					this.box = 'box'
					this.flag = !this.flag
				}
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res)=> {
					this.screenHeight = res.windowHeight;
				}
			});
		innerAudioContext.src = 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.mp3';
			innerAudioContext.play();
		},
		onShow() {
			try {
			const res = uni.getSystemInfoSync();
			this.scrollHeight = res.windowHeight;
			} catch (e) {
			    // error
			}
		},
		
	}
</script>

<style lang="scss" scoped>
	.swiper-item{
		background: rgba(0,0,0,0.5);
		.swiper-text{}
		.swiper-img{}
	}
	
	.music{
		width: 25px;
		height: 25px;
		position: absolute;
		z-index: 1000;
		right: 10px;
	}
	.music1{
		animation:rotating 2.5s linear infinite;
	}
	@keyframes rotating{
	from{transform:rotate(0)}
	to{transform:rotate(360deg)}
	}
	 page{
		position: relative;
		height:100%;
	}
	.bg-img{
		display:flex;
		height: 100vh;
		justify-content: center;
		align-items:center;
		width: 130vw;
		position: absolute;
		top: 0;
		left: -15vw;

	}
	.cover{
		position: absolute;
		height: 100vh;
		width: 100vw;
		top: 0;
		background: rgba(0,0,0,0.1);
		z-index: 998;
	}
	.text-box{
		position: relative;
		z-index: 999;
		.content{
			-webkit-text-stroke: 1px #FF9933;
			-webkit-text-fill-color: transparent;
			display: block;
			text-align: center;
			font-size: 28px;
		}
		.name{
			background: linear-gradient(to bottom,#FF9933,#FFFF00);
			-webkit-text-fill-color: transparent;
			-webkit-background-clip: text;
			display: block;
			padding-left: 10px;
			margin-top: 20px;
			
		}
	}
	*{
		margin:0;
		padding:0;
	}
	body{
		max-width: 100%;
		min-width: 100%;
		height: 100%;
		background-size: cover;
		background-repeat: no-repeat;
		background-attachment: fixed;
		background-size:100% 100%;
		position: absolute;
		margin-left: auto;
		margin-right: auto;
	}
	li{
		list-style: none;
	}
	.box{
		width:100px;
		height:100px;
		background-size: cover;
		background-repeat: no-repeat;
		background-attachment: fixed;
		background-size:100% 100%;
		position: absolute;
		margin-left: 41%;
		margin-top: 65%;
		-webkit-transform-style:preserve-3d;
		-webkit-transform:rotateX(13deg);
		-webkit-animation:move 5s linear infinite;
		z-index: 999;
	}
	.box1{
		z-index: 999;
		width:100px;
		height:100px;
		background-size: cover;
		background-repeat: no-repeat;
		background-attachment: fixed;
		background-size:100% 100%;
		position: absolute;
		margin-left: 41%;
		margin-top: 65%;
		-webkit-transform-style:preserve-3d;
		-webkit-transform:rotateX(13deg);
		-webkit-animation:move 5s linear infinite;
	}
	.minbox{
		width:50px;
		height:50px;
		position: absolute;
		left:25px;
		top:10px;
		-webkit-transform-style:preserve-3d;
	}
	.minbox1{
		width:50px;
		height:50px;
		position: absolute;
		left:10px;
		top:-30px;
		-webkit-transform-style:preserve-3d;
	}
	.minbox li{
		width:50px;
		height:50px;
		position: absolute;
		left:0;
		top:0;
	}
	.minbox li:nth-child(1){
		background: url(../../static/01.png) no-repeat 0 0;
		-webkit-transform:translateZ(25px);
	}
	.minbox li:nth-child(2){
		background: url(../../static/02.png) no-repeat 0 0;
		-webkit-transform:rotateX(180deg) translateZ(25px);
	}
	.minbox li:nth-child(3){
		background: url(../../static/03.png) no-repeat 0 0;
		-webkit-transform:rotateX(-90deg) translateZ(25px);
	}
	.minbox li:nth-child(4){
		background: url(../../static/04.png) no-repeat 0 0;
		-webkit-transform:rotateX(90deg) translateZ(25px);
	}
	.minbox li:nth-child(5){
		background: url(../../static/05.png) no-repeat 0 0;
		-webkit-transform:rotateY(-90deg) translateZ(25px);
	}
	.minbox li:nth-child(6){
		background: url(../../static/06.png) no-repeat 0 0;
		-webkit-transform:rotateY(90deg) translateZ(25px);
	}
	.maxbox li:nth-child(1){
		background: url(../../static/5.png) no-repeat 0 0;
		-webkit-transform:translateZ(25px);
	}
		
	.maxbox li:nth-child(2){
		background: url(../../static/5.png) no-repeat 0 0;
		-webkit-transform:translateZ(25px);
	}
	.maxbox li:nth-child(3){
		background: url(../../static/5.png) no-repeat 0 0;
		-webkit-transform:rotateX(-90deg) translateZ(25px);
	}
	.maxbox li:nth-child(4){
		background: url(../../static/5.png) no-repeat 0 0;
		-webkit-transform:rotateX(90deg) translateZ(25px);
	}
	.maxbox li:nth-child(5){
		background: url(../../static/5.png) no-repeat 0 0;
		-webkit-transform:rotateY(-90deg) translateZ(25px);
	}
	.maxbox li:nth-child(6){
		background: url(../../static/5.png) no-repeat 0 0;
		-webkit-transform:rotateY(90deg) translateZ(25px);
	}
	.maxbox{
		width: 400px;
		height: 200px;
		position: absolute;
		left: 0;
		top: -20px;
		-webkit-transform-style: preserve-3d;
		
	}
	.maxbox li{
		width: 100px;
		height: 100px;
		background: #fff;
		border:1px solid #ccc;
		position: absolute;
		left: 0;
		top: 0;
		opacity: 0.2;
		-webkit-transition:all 1s ease;
	}
	.maxbox li:nth-child(1){
		-webkit-transform:translateZ(50px);
	}
	.maxbox li:nth-child(2){
		-webkit-transform:rotateX(180deg) translateZ(50px);
	}
	.maxbox li:nth-child(3){
		-webkit-transform:rotateX(-90deg) translateZ(50px);
	}
	.maxbox li:nth-child(4){
		-webkit-transform:rotateX(90deg) translateZ(50px);
	}
	.maxbox li:nth-child(5){
		-webkit-transform:rotateY(-90deg) translateZ(50px);
	}
	.maxbox li:nth-child(6){
		-webkit-transform:rotateY(90deg) translateZ(50px);
	}
	.box1 ol li:nth-child(1){
		-webkit-transform:translateZ(150px);
		width: 200px;
		height: 200px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box1 ol li:nth-child(2){
		-webkit-transform:rotateX(180deg) translateZ(150px);
		width: 200px;
		height: 200px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box1 ol li:nth-child(3){
		-webkit-transform:rotateX(-90deg) translateZ(150px);
		width: 200px;
		height: 200px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box1 ol li:nth-child(4){
		-webkit-transform:rotateX(90deg) translateZ(150px);
		width: 200px;
		height: 200px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box1 ol li:nth-child(5){
		-webkit-transform:rotateY(-90deg) translateZ(150px);
		width: 200px;
		height: 200px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	.box1 ol li:nth-child(6){
		-webkit-transform:rotateY(90deg) translateZ(150px);
		width: 200px;
		height: 200px;
		opacity: 0.8;
		left: -100px;
		top: -100px;
	}
	@keyframes move{
		0%{
			-webkit-transform: rotateX(13deg) rotateY(0deg);
		}
		100%{
			-webkit-transform:rotateX(13deg) rotateY(360deg);
		}
	}
</style>
