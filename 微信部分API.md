##登录用户：
######用户可使用用户名，手机号，邮箱 + 密码验证

**http请求说明**

	管理平台api：cms.dmday.cn/api/login
	远程api:www.dmday.cn/apis/login
    请求方式：POST
    请求数据示例：
    {
    	user： "1776666666",
        password: "somestring"
    }
    
|参数|说明|
|---|---|
|user|用户输入信息，可以是用户名，手机号，邮箱|
|password|用户密码|

**返回说明**
	
    正常返回JSON数据
	{
    	id: "sjdhdhedhDKWKAkdskdlcKAKW4DVFD23SF4",
        token: "DOFI424tgrb5RDS4r4ghbEDFHEIOFHEUdsfv3r2g2g4g4sfI",
        created: "2015-12-02T04:05:00.396Z",
        ttl: 7200
    }
    错误返回信息
    {
    	status: 401
        message: "Unauthorized"
    }

|参数|说明|
|---|---|
|id|用户ID|
|token|用户登录凭证|
|created|用户登录时间|
|ttl|凭证有效时间|
##数据接口
用户登录后管理平台首页显示需要的数据信息
**http请求说明**

	管理平台API：cms.dyday.cn/api/usercumulate？access_token=TOKEN
    远程API： www.dyday.cn/apis/usercumulate？access_token=TOKEN
    请求方式：GET
    
**返回数据说明**
    
    成功返回数据
    {
    	user:
        {
        	all: 20000,
        	new: 10
        }
        BGRecord:{
        	all: 300,
            new: 20
        }
        forum: {
        	pv: 40000,
            uv: 3000
        },
        article: {
        	pv: 4444,
            uv: 3000
        }
    }

| 参数 | 说明 |
|--------|--------|
|   user.all     |    全部用户数量    |
|   user.new     |   新增用户数量     |
|   BG.all     |     血糖记录总量   |
|   BG.new     |    新增血糖数量    |
|   forum.pv     |    论坛昨日PV    |
|   forum.uv     |     论坛昨日UV   |
|   article.pv     |    文章昨日PV    |
|   article.uv     |     文章昨日UV   |
##微信用户关注（只争对糖友圈社区使用的公众号）
当用户关注时，获取微信用户信息发送到糖友圈（注册用户）
**http说明**

	远程API：www.dyday.cn/apis/wechat/users
    请求方式：POST
    数据示例：
    {
       "openid":" OPENID",
       " nickname": NICKNAME,
       "sex":"1",
       "province":"PROVINCE"
       "city":"CITY",
       "country":"COUNTRY",
       "headimgurl":    "http://wx.qlogo.cn/mmopen/g3MonUZtNHkdmzicIlibx6iaFqAc56vxLSUfpb6n5WKSYVY0ChQKkiaJSgQ1dZuTOgvLLrhJbERQQ4eMsv84eavHiaiceqxibJxCfHe/46", 
        "privilege":[
        "PRIVILEGE1"
        "PRIVILEGE2"
        ],
        "unionid": "o6_bmasdasdsad6_2sgVt7hMZOPfL"
	}
	返回数据
    {
    	status：200
    }
|参数|说明|
|---|---|
|openid|微信用户相对公众号ID，用户的唯一标识|
|nickname|	用户昵称|
|sex|用户的性别，值为1时是男性，值为2时是女性，值为0时是未知|
|province|	用户个人资料填写的省份|
|city|普通用户个人资料填写的城市|
|country|国家|
|headimgurl|用户头像|
|privilege|用户特权信息，json 数组|
|unionid|只有在用户将公众号绑定到微信开放平台帐号后，才会出现该字段|
##微信智能回复
用户发送信息给公众号，当服务器接收到用户发送的信息时，发送数据到www.dyday.cn.

**http说明**
	
    远程API：www.dyday.cn/apis/wechat/message？access_token=TOKEN
    请求方式：POST
    数据示例：
    {
    	ToUserName: "oe615joHIJ4i9S5-Y8aIZcFsxoqU",
        FromUserName: "oe615joHIJ4i9S5-Y8aIZcFsxoqA",
        MsgType: "text"
        Content: "some string"
        MsgId: 123456789
    }
|参数|说明|
|---|---|
|ToUserName|开发者微信号ID|
|FromUserName|微信用户ID|
|MsgType|消息类型（只有文本消息才发起请求）|
|Content|消息内容|
|MsgId|消息ID|

**返回说明**

	成功数据
    {
    	ToUserName: "oe615joHIJ4i9S5-Y8aIZcFsxoqA",
        FromUserName: "oe615joHIJ4i9S5-Y8aIZcFsxoqU",
        CreateTime: "123456789",
        MsgType: "news"
        ArticleCount: 2,
        Articles: [{
        	Title: "测试文章"
            Description: "测试测试"
            PicUrl: ""
            Url: "example.com/someurl"
        },{
        	Title: "测试文章"
            Description: "测试测试"
            PicUrl: ""
            Url: "example.com/someurl"
        }]
    }
|参数|说明|
|---|---|
|ToUserName|用户微信ID|
|FromUserName|开发者微信ID|
|CreateTime|创建时间|
|MsgType|news|
|ArticleCount|图文消息个数（最多10条）|
|Articles.Title|图文消息标题|
|Articles.Description|图文消息描述|
|Articles.PicUrl|图片链接，支持JPG、PNG格式|
|Articles.Url|点击图文消息跳转链接|

#微信文章管理
可定期将微信素材同步到文章列表内

##文章列表
通过微信接口获取文章列表，并保存到www.dyday.cn,每次发送不超过20条。

![逻辑](C:\Users\liuJD\Documents\Tencent Files\762022369\FileRecv\绘图2.png)
**HTTP说明**

	远程API： www.dyday.cn/apis/wechat/articels/count？access_token=TOKEN
    请求方式：GET
    返回数据示例：
    {
    	count: 20
    }
    
	保存数据远程API： www.dyday.cn/apis/wechat/articels？access_token=TOKEN
    请求方式：POST
    数据示例：
    [{
       "title": TITLE,
       "thumb_media_id": THUMB_MEDIA_ID,
       "thumb_url": THUMB_URL,
       "show_cover_pic": SHOW_COVER_PIC(0 / 1),
       "author": AUTHOR,
       "digest": DIGEST,
       "content": CONTENT,
       "url": URL,
       "content_source_url": CONTETN_SOURCE_URL
    }]
    返回数据示例
    {
    	status： 200
    }
    
    获取文章列表API：cms.dyday.cn/apis/wechat/articels？page=PAGE&access_token=TOKEN
    获取文章列表远程API：cms.dyday.cn/apis/wechat/articels？page=PAGE&access_token=TOKEN
    请求方式：GET
    返回示例：
    {
    	total: 3000,
        count: 20,
    	content:[{
           "id": ARTICLEID
           "title": TITLE,
           "thumb_media_id": THUMB_MEDIA_ID,
           "thumb_url": THUMB_URL,
           "show_cover_pic": SHOW_COVER_PIC(0 / 1),
           "author": AUTHOR,
           "digest": DIGEST,
           "content": CONTENT,
           "url": URL,
           "content_source_url": CONTETN_SOURCE_URL
        }]
    }
##更新文章内容
通过管理平台更新文章内容
**http说明**

	远程API： www.dyday.cn/apis/wechat/articles/ARTICLEID
    请求方式：PUT
    数据示例：
    {
       "id": ARTICLEID
       "title": TITLE,
       "thumb_media_id": THUMB_MEDIA_ID,
       "thumb_url": THUMB_URL,
       "show_cover_pic": SHOW_COVER_PIC(0 / 1),
       "author": AUTHOR,
       "digest": DIGEST,
       "content": CONTENT,
       "url": URL,
       "content_source_url": CONTETN_SOURCE_URL
    }
|参数|说明|
|---|---|
|id|文章ID（POST时没有该字段）|
|title|图文消息的标题|
|thumb_media_id|图文消息的封面图片素材id|
|thumb_url|图文消息的封面图片的地址|
|show_cover_pic|是否显示封面，0为false，即不显示，1为true，即显示|
|author|作者|
|digest|图文消息的摘要|
|content|图文消息的具体内容|
|url|图文页的URL|
|content_source_url|点击“阅读原文”后的URL|
