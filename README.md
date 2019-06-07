#  行走力量

* 注意的事项
  * 微信接口具备能力获取最近30天内的步数，30天以外丢失；
  * 用户必须已经关注了关注微信运动公众号，才能够获取；
  * 目前获取到了密文数据，还需要在后台解密。
  * 先按分层架构设计服务器，未来业务扩展到一定量再做微服务改造；

* 开发需要如下资源
	* 小程序账号，测试还不需要认证
	* 测试云服务器，2c, 4G内存,60G硬盘，操作系统:centos 7+
	* 云服务器需要固定IP
	* 一个备案了的域名（或者二级域名），域名指向云服务器的固定IP。

* 上线需要如下资源
	* 企业认证的小程序账号
	* 云服务器，8c, 16G内存,60G硬盘，外挂一个512G硬盘,操作系统:centos 7+（先按较低配置部署一个单点服务，如果业务扩张，要考虑高可用，要改变部署方式）
	* 云服务器需要固定IP
	* 一个备案了的域名（或者二级域名），域名指向云服务器的固定IP。

* 参考资料
  * [小程序获取步数参考资料](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/werun/wx.getWeRunData.html)
  * [APP获取步数参考资料](https://uniapp.dcloud.io/api/other/sport)
  * [解密数据](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/signature.html#method-cloud)