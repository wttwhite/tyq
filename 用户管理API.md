#用户管理
糖友圈社区用户基本信息管理，包括血糖信息，用户信息，积分信息
##用户基本信息
通过该接口获取用户姓名，手机号，血糖，积分等基本信息
**HTTP说明**

	管理平台API：cms.dmday.cn/api/users?scope=base&page=PAGE&access_token=TOKEN&filter[where][role]=1&filter[where][role]=2
    远程API：www.dmday.cn/apis/users?scope=base&page=PAGE&access_token=TOKEN&filter[where][role]=1&filter[where][role]=2
    请求方式：GET
    
|参数|说明|
|---|---|
|scope|获取数据内容，base表示为基本信息，liveness表示用户活跃度|
|page|当前请求页|
|filter[where][role]|过滤器，查询role为1的记录，role表示为用户角色，0表示黑名单，1表示普通用户，2表示管理员|
    返回数据示例：
    {
    	total: 2000,
        count: 20,
        content: [{
        	id: ID,
            headImg: HEADIMG,
            name: NAME,
            phone: PHONE,
            BGtype: TYPE,
            lastBG: LASTBGINFO,
            points: POINTS,
            role: 1
        },{
        	id: ID,
            headImg: HEADIMG,
            name: NAME,
            phone: PHONE,
            BGtype: TYPE,
            lastBG: LASTBGINFO,
            points: POINTS,
            role: 2
        }]
    }
|参数|说明|
|---|---|
|total|用户记录总量|
|count|当前返回数据记录总量|
|content|返回数据内容|
|id|用户ID|
|headImg|用户头像URL|
|name|用户名|
|phone|用户手机号|
|BGtype|糖尿病类型（数字标识）|
|lastBG|最新血糖（数字，不加单位）|
|points|用户积分|
|role|用户角色（获取黑名单是role=0）|
##用户详情
用户详细信息。包括用户姓名，性别，话题数，回复数，积分，最新血糖，健康信息，检查数据,控糖方案，控糖日志。
###基本信息
**http说明**
    
    管理平台API： cms.dmday.cn/api/users/ID？access_token=TOKEN
    远程API： www.dmday.cn/apis/users/ID？access_token=TOKEN
    请求方式：GET

|参数|说明|
|---|---|
|id|用户ID|
	
    返回示例
    {
    	id: ID,
        name: NAME,
        phone: PHONE,
        BGtype: TYPE,
        lastBG: LASTBGINFO,
        points: POINTS,
        role: ROLE,
        sex: SEX,
        topics: TOPICCOUNT,
        replies: COMMENTCOUNT
    }

|参数|说明|
|---|---|
|id|用户ID|
|name|用户名|
|phone|用户手机号|
|BGtype|糖尿病类型（数字标识）|
|lastBG|最新血糖（数字，不加单位）|
|points|用户积分|
|role|用户角色|
|sex|用户性别|
|topics|用户发表话题数|
|comments|用户回复数量|
###健康信息
**HTTP说明**

	管理平台API： cms.dmday.cn/api/users/ID/health？access_token=TOKEN
    远程API： www.dmday.cn/apis/users/ID/health？access_token=TOKEN
    请求方式：GET
    返回数据示例：
    {
    	tops：160,
        weight: 60,
        BMI: 20,
        symptoms: "多饮, 多食",
        chronic: "肾病, 眼病",
        labourIntensive: "轻体力劳动",
        medication: "二甲双X"
    }
|参数|说明|
|---|---|
|tops| 身高|
|weight| 体重|
|BMI| BMI值|
|symptoms|症状 |
|chronic| 已有症状|
|labourIntensive|劳动强度 |
|medication| 用药情况|
###检查数据
**HTTP说明**
	
    管理平台API： cms.dmday.cn/api/users/ID/examine？access_token=TOKEN
    远程API： www.dmday.cn/apis/users/ID/examine？access_token=TOKEN
    请求方式：GET
    返回数据示例：
    {
    	GDM: {
            fasting: 6.4,
            OTGG2h: 9.5,
            HBA1c: 8.7,
            INS: 4.4,
            CP: 6.6
        },
        BG: {
        	CH: 7.8,
            HDICH: 5.6,
            TC: 3.4,
            LDICH: 4.4
        },
        GPT: {
        	GPT: 3.0
        }
    }
    
|参数|说明|
|---|---|
|GDM|糖尿病检查数据|
|GDM.fasting|空腹血糖|
|GDM.OTGG2h|OTGG2h|
|GDM.HBA1c|糖化血糖蛋白|
|GDM.INS|胰岛素|
|GDM.CP|C肽|
|BG|血糖检查数据|
|BG.CH|胆固醇|
|BG.HDICH|高密度脂蛋白胆固醇|
|BG.TC|甘油三肽|
|BG.LDICH|低密度脂蛋白胆固醇|
|GPT|肝功能检查|
|GPT.GPT|丙谷转氨酶|
###控糖日志
**HTTP说明**
	
    管理平台API： cms.dmday.cn/api/users/ID/log？access_token=TOKEN
    远程API： www.dmday.cn/apis/users/ID/log？access_token=TOKEN
    请求方式：GET
    返回数据示例：
	{
    	diet: [{
        	dinnerType: 1,
            eated: [{
                type: 1,
                dosage: 150,
                unit: "g"
            }],
            remark: REMARK,
            remarkImg: [IMGURL]
        }],
        sport: [{
        	time: TIME,
            record: RECORD,
            rematk: REMARK,
            remarkImg: [IMGURL]
        }],
        ADrug: [{
        	time: TIME,
            record: RECORD,
            rematk: REMARK,
            remarkImg: [IMGURL]
        }]
    }
|参数|说明|
|---|---|
|diet|饮食记录，对象数组|
|dinnerType|用餐时间点（早中晚，加餐）|
|eated|饮食记录（食物用量记录）|
|remark|备注|
|remarkImg|备注图片|
|sport|运动记录，对象数组|
|time|时间点|
|record|记录值，字符串|
|ADrug|用药记录，对象数组|
###控糖方案
**HTTP说明**
	
    管理平台API： cms.dmday.cn/api/users/ID/schema？access_token=TOKEN
    远程API： www.dmday.cn/apis/users/ID/schema？access_token=TOKEN
    请求方式：GET
    返回数据示例：
	{
    	diet: [{
        	type: 1,
            dosage: 150,
            unit: "g"
        },{
        	foodType: 3,
            dosage: 4,
            unit: "ng/ml"
        }],
        sport: [{
        	type: 1,
            dosage: 1.2,
            unit: "mmo/l"
        }]
    }
|参数|说明|
|---|----|
|id|选择的用户ID|
|diet|饮食推荐|
|type|类型（在饮食中对应事物类型，在运动中对应运动类型）|
|dosage|对应使用量，数值|
|unit|对应单位，如kg，g，mmo/L|
|sport|运动推荐|

###血糖分析
**HTTP说明**
	
    管理平台API： cms.dmday.cn/api/users/ID/analysis？access_token=TOKEN&year=YEAR&mon=MONTH
    远程API： www.dmday.cn/apis/users/ID/analysis？access_token=TOKEN&year=YEAR&mon=MONTH
    请求方式：GET
|参数|说明|
|---|---|
|year|查询的年份|
|mon|查询的月份|
    返回数据示例：
	[{
    	day：DAY，
    	BG：[2,3,4,5,6,6,8,8]
    }]
> 返回说明：返回查询当月的数据，一维数组表示某天的数据，二维数组表示用餐时间点对于的血糖记录

##修改用户信息
对用户部分信息进行修改
###基本信息
**http说明**
    
    管理平台API： cms.dmday.cn/api/users/ID？access_token=TOKEN
    远程API： www.dmday.cn/apis/users/ID？access_token=TOKEN
    请求方式：PUT
	数据示例：
    {
    	id: ID,
        points: POINTS,
        role: ROLE
    }
|参数|说明|
|---|---|
|id|用户ID|
|points|修改的积分值|
|role|修改用户角色|
###修改健康信息
**HTTP说明**

	管理平台API： cms.dmday.cn/api/users/ID/health？access_token=TOKEN
    远程API： www.dmday.cn/apis/users/ID/health？access_token=TOKEN
    请求方式：PUT
    数据示例：
    {
    	tops：160,
        weight: 60,
        BMI: 20,
        symptoms: "多饮, 多食",
        chronic: "肾病, 眼病",
        labourIntensive: "轻体力劳动",
        medication: "二甲双X"
    }
|参数|说明|
|---|---|
|tops| 身高|
|weight| 体重|
|BMI| BMI值|
|symptoms|症状 |
|chronic| 已有症状|
|labourIntensive|劳动强度 |
|medication| 用药情况|
###修改检查数据
**HTTP说明**
	
    管理平台API： cms.dmday.cn/api/users/ID/examine？access_token=TOKEN
    远程API： www.dmday.cn/apis/users/ID/examine？access_token=TOKEN
    请求方式：PUT
    数据示例：
    {
    	GDM: {
            fasting: 6.4,
            OTGG2h: 9.5,
            HBA1c: 8.7,
            INS: 4.4,
            CP: 6.6
        },
        BG: {
        	CH: 7.8,
            HDICH: 5.6,
            TC: 3.4,
            LDICH: 4.4
        },
        GPT: {
        	GPT: 3.0
        }
    }
    
|参数|说明|
|---|---|
|GDM|糖尿病检查数据|
|GDM.fasting|空腹血糖|
|GDM.OTGG2h|OTGG2h|
|GDM.HBA1c|糖化血糖蛋白|
|GDM.INS|胰岛素|
|GDM.CP|C肽|
|BG|血糖检查数据|
|BG.CH|胆固醇|
|BG.HDICH|高密度脂蛋白胆固醇|
|BG.TC|甘油三肽|
|BG.LDICH|低密度脂蛋白胆固醇|
|GPT|肝功能检查|
|GPT.GPT|丙谷转氨酶|

###修改控糖方案
**HTTP说明**
	
    管理平台API： cms.dmday.cn/api/users/ID/schema？access_token=TOKEN
    远程API： www.dmday.cn/apis/users/ID/schema？access_token=TOKEN
    请求方式：PUT
    返回数据示例：
	{
    	diet: [{
        	type: 1,
            dosage: 150,
            unit: "g"
        },{
        	foodType: 3,
            dosage: 4,
            unit: "ng/ml"
        }],
        sport: [{
        	type: 1,
            dosage: 1.2,
            unit: "mmo/l"
        }]
    }
|参数|说明|
|---|----|
|id|选择的用户ID|
|diet|饮食推荐|
|type|类型（在饮食中对应事物类型，在运动中对应运动类型）|
|dosage|对应使用量，数值|
|unit|对应单位，如kg，g，mmo/L|
|sport|运动推荐|
#积分管理
###积分列表

	管理平台API：cms.dmday.cn/api/users/ID/points?page=PAGE&access_token=TOKEN
    远程API：www.dmday.cn/apis/users/ID/points?page=PAGE&access_token=TOKEN
    请求方式：GET
    返回数据示例：
    {
    	total: 2000,
        count: 20,
        content: [{
        	id: ID,
            created: CREATETIME,
            count: CHANGECOUNT,
            reason: {
            	message: MESSAGE,
                goodId: GOODID
            }
        },{
        	id: ID,
            created: CREATETIME,
            count: CHANGECOUNT,
            reason: {
            	message: MESSAGE,
                goodId: GOODID
            }
        }]
    }
|参数|说明|
|---|---|
|total|用户记录总量|
|count|当前返回数据记录总量|
|content|返回数据内容|
|id|用户ID|
|created|记录创建时间|
|count|积分变化数量|
|reason|积分变化原因|
|message|变化原因说明，如签到，兑换商品等等|
|goodId|如果是商品兑换着该字段对应商品ID|
###删除积分记录
	管理平台API：cms.dmday.cn/api/users/ID/points/fk?access_token=TOKEN
    远程API：www.dmday.cn/apis/users/ID/points/fk?access_token=TOKEN
    请求方式：DELETE
|参数|说明|
|---|---|
|ID|用户ID|
|fk|积分记录ID|
    返回数据示例：
    {
    	status: 200
    }


