<script>
	export default {
		globalData:{
			project_name:"时纯优选",
			homePage:"/pages/index/index",//首页路径getApp().globalData.homePage
			myPage:"/pages/index/index",//我的路径getApp().globalData.myPage
			interfaceApi:"",
			interfacePlatform:"h5",
			addressPage:"/pages/address/selectAdress",//选择收货地址路径getApp().globalData.addressPage
			ordersPage:"/pages/myCloudStorage/deliveryOrder",//订单列表路径getApp().globalData.ordersPage
			setinfoPage:"/pages/setting/index",//设置信息路径getApp().globalData.setinfoPage
			agencyCheckPage:"/pages/agencyInvitation/agencyCheck",//审核页面路径getApp().globalData.agencyCheckPage
			bindPage:"/pages/agencyInvitation/register",//绑定页面路径getApp().globalData.bindPage
			// #ifdef MP
			loginType:"wxapplogin",
			interfaceUrl:'https://unidemo.dcloud.net.cn',//线上
			// #endif
			// #ifdef H5
			//interfaceUrl:'http://www.nvlang.coma',//测试
			loginType:"/pages/users/loginPhone",//登录
			
			interfaceUrl:'https://unidemo.dcloud.net.cn',//线上
			// #endif
			
			appid:"wx4a0e975056cc1c6c",
			interfaceFwkey:"2587l6QEQ3mPHJZgYTAznd2sN17mlBQZ4CgMNdYoEZJ3",
		},
		
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
	}
</script>

<style>
	/*每个页面公共css */
	@import "./common/app.css";
</style>
