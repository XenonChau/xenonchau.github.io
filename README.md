 ```
 /**
	 @name 		XCCurriculumVitae.m
	 @author 	Created by XenonChau on 15-1-20.
	 @copyright Copyright (c) 2015 XenonChau. All rights reserved.
  */
 ```

```
- (void)personalInformation {
	self.name 		= @"赵振楠";
	self.gender		= @"male";
	self.birthday 	= @"1982-07-18";
	self.address	= @"上海市杨浦区淞沪路政立路";//@"辽宁省大连市开发区小孤山中里96#4-103"
	self.cellPhone	= @"186-4281-8255";
	self.eMail		= [self systemVPNAllowed] ? @"xenonchau@gmail.com" : @"godtea@msn.com";
	self.education	= @"DalianUniversity";(highSchoolGraduationDegree)//NOT graduated form university
}
```

```
#pragma mark - Companies
- (BOOL)employmentExprience:(XCCompany)aCompany {
	switch (aCompany) {
		case XCCompanyAreSoft: {//@"上海佳锐信息科技有限公司"
			[XCSchedule beginDate:@"2015-04"];
			[self areSoft];
			[XCSchedulw endDate:@"2016-01"];
			return YES;
			break;
		}
		case XCCompanyTaoGuBa: {//@"福州淘股吧网络科技有限公司"
			[XCSchedule beginDate:@"2014-07"];
			[self taoGuBa];
			[XCSchedelu  endDate:@"2015-04"];
			return YES;
			break;
		}
		case XCCompanyIDoTech: {//@"大连艾都科技有限公司"
			[XCSchedule beginDate:@"2013-09"];
			[self iDoTech];
			[XCSchedule endDate:@"2014-05"];
			return YES;
			break;
		}
		defaults: {
			[XCSchedule beginDate:[NSDate nowDateString]];
			[XCSchedule endDate:[NSDate noLimitDateString]];
			return [self upToYou];
			break;
		}
	}
}
#pragma mark - Duty Details
- (void)areSoft {
	[self projectExhibition:XCProjectOperator];			//火牛操盘家
	[self projectExhibition:XCProjectGalaxyFund];		//银河基金
	[self projectExhibition:XCProjectJoin];				//卓赢
	[self projectExhibition:XCProjectZhongOuQianGunGun];//中欧基金
	[self projectExhibition:XCProjectZhongYinFund];		//中银基金
}
- (void)taoGuBa {
	[self projectExhibition:XCProjectTaoGuBa];			//淘股吧
}
- (void)iDoTech {
	[self projectExhibition:XCProjectCleverMe];			//机智的我
}
```

```
- (void)projectExhibition:(XCProject)aProject {
	/**
	 *	@brief 项目链接见附录
	 */
	switch (aProject) {
		case XCProjectOperator: {
			/**
			 * @name 火牛操盘家
			 * @brief 模拟操盘，寻找最强基金经理人。
			 * @param 公司自营项目
			 * @remarks 项目维护（2年前的老项目）
			 * @todo 生产环境不能中断，只能在老代码的基础上修改。
			 * @todo 后台更换服务器，换了一套新接口，重新对接接口。
			 * @todo 由新接口产生的新需求，修改原有的页面逻辑。
			 * @todo 杂乱无章的经手人的代码中梳理出条理并稍作整理。
			 * @remarks 时间紧迫，没机会将整个项目重写，只重构了［首页］和［交易页］。
			 */
			break;
		}
		case XCProjectGalaxyFund: {
			/**
			 * @name 倍利宝
			 * @brief 银河基金公司自己的基金平台（老版App升级）
			 * @param 银河基金公司外包项目
			 * @remarks 技术支持
			 * @todo app架构搭建	 
			 * @remarks 周末组织同事开展技术沙龙，第三方类库代码分析
			 */
			break;
		}
		case XCProjectJoin: {
			/**
			 * @name 卓赢
			 * @brief 一款面向泛90后的股票模拟操盘app，抛弃大量年轻人看不懂的参数，用简洁明快的样式引导其步入理财的大门。
			 * @param 公司自营项目
			 * @remarks 项目负责人
			 * @todo 参与初期项目设计并提供参考意见，设计app整体架构
			 * @todo 放弃了公司原有的纯代码框架，使用Nib和AutoLayout进行适配
			 * @remarks 由于设计架构，将Socket部分的工作分配给同事去专研，项目内的AsyncSocket部分未参与。
			 */
			break;
		}
		case XCProjectZhongOuQianGunGun: {
			/**
			 * @name 中欧钱滚滚
			 * @brief 中欧基金公司自己的基金平台
			 * @param 中欧基金公司外包项目
			 * @remarks 项目主导者
			 * @todo 根据prototype从0开始搭建app，主导项目中的技术应用。
			 * @todo 指导新员工，规范代码，完善工具类，修改bug。
			 */
			break;
		}
		case XCProjectZhongYinFund: {
			/**
			 * @name 中银基金
			 * @brief 中银基金公司自己的基金平台
			 * @param 中欧基金公司外包项目
			 * @remarks 中途加入项目组
			 * @todo 增加新需求：［我的］选项卡－［交易明细］页面
			 */
			break;
		}
		case XCProjectTaoGuBa: {
			/**
			 * @name 淘股吧
			 * @brief 面向一般股民交流分享经验的社交平台
			 * @remarks 中途加入项目组
			 * @todo 根据prototype完成自选页面布局、适配及数据对接。
			 */
			break;
		}
		case XCProjectCleverMe: {
			/**
			 * @name 机智的我
			 * @brief 一款基于cocos2d-x开发的面向婴幼儿寓教于乐的游戏
			 * 游戏十分简单，单机，很基础的控件拖拽，未保存用户信息。
			 * SE,BGM均来源自网络，无版权作品。
			 * 未拉到VC，项目组解散。
			 */
			break;
		}
		defaults: {
			return [self upToYou];
			break;
		}
	}
}
```
======
#项目链接

[火牛操盘家(企业版)](http://m.51huoniu.com/down/index.html title="企业版下载链接") | [倍利宝(新版未上线)](https://itunes.apple.com/us/app/bei-li-bao/id889871326?mt=8) | [卓赢](https://itunes.apple.com/us/app/join-zhuo-ying/id1057902895?mt=8) | [中欧钱滚滚](https://itunes.apple.com/us/app/zhong-ou-qian-gun-gun-ji-jin/id1038803050?mt=8) | [中银基金](https://itunes.apple.com/us/app/zhong-yin-ji-jin/id1021177051?mt=8) | [淘股吧](https://itunes.apple.com/us/app/tao-gu-ba-gu-piao-gao-shou/id820369549?mt=8) | [机智的我]()

