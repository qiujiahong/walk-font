<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view>
			<text class="title">{{title}}</text>
		</view>
	</view>
</template>

<script>
	// import wxbizdatacrypt from "github.com/xlstudio/wxbizdatacrypt"
	var WXBizDataCrypt = require('../../common/WXBizDataCrypt.js');
	//import common from "../../common/common.js";
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {
			console.log("onload")
			var _this = this;
			wx.login({
			 success: function(res){
			   var appid = "wx0006556d6bc1bcac";
			   var secret = "97af146b32d0ebec3fab9d25e9eb6945";
			   if(res.code){
				 wx.request({
				   url: 'https://api.weixin.qq.com/sns/jscode2session?appid=' + appid + '&secret=' + secret + '&js_code=' + res.code + '&grant_type=authorization_code',
				   header: {
					 'content-type': 'json'
				   },
				   success: function(res){
					 var session_key = res.data.session_key;
					 console.log(session_key);
					 _this.getData(appid,session_key);
				   }
				 })
			   }
			 }
		   })
		},
		methods: {
			getData(appid, session_key) {
				wx.getWeRunData({
					success: function(res) {
						console.log(res);
						console.log("appid:" + appid + "session_key:" + session_key + "encryptedData:" + res.encryptedData + "iv:" + res.iv);
						var encryptedData = res.encryptedData;
						var iv = res.iv;
						//使用解密工具，链接地址：
						//https://codeload.github.com/gwjjeff/cryptojs/zip/master
						var pc = new WXBizDataCrypt(appid, session_key);
						console.log(pc);
						var data = pc.decryptData(encryptedData, iv)
						console.log(data)
						wx.showModal({
							title: '步数',
							content: JSON.stringify(data),
							showCancel: false,
							confirmText: '知道了'
						})
					},
					fail: function(res) {
						console.log(res);
						wx.showModal({
							title: '提示',
							content: '开发者未开通微信运动，请关注“微信运动”公众号后重试',
							showCancel: false,
							confirmText: '知道了'
						})
					}
				})
			}
		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
