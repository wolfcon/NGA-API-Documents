# AppAPI

## ⚠️注意

参数等信息(比如 `%@` 为要替换的参数值) [参考这里的网页版文档](https://github.com/wolfcon/NGA-API-Documents/wiki). 

由于本 API 列表是 ~~`以某科学方式获得`~~ , 有可能会不全, 欢迎 PR 补全各项信息.

## baseURL
```js
// 如果是自己拼接 URL 则需要注意, 添加 ? 哟
https://bbs.nga.cn/app_api

// 例如: 获取首页列表
https://bbs.nga.cn/app_api?__lib=home&__act=category&_v=2
// 例如: 获取用户的收藏板块(非收藏帖子)
https://bbs.nga.cn/app_api?__lib=favorforum&__act=sync
```

## 基础参数

cookie 中需要以下 2 个值来确认基础的登录信息, 它们的值由登录后的返回值取得.

- `ngaPassportUid` : 是 NGA 账户的 UID (数字 ID)
- `ngaPassportCid` : 是 NGA 账户登录后获取的认证码 Token

### home

```js
__lib=home&__act=category&_v=2
__lib=home&__act=hasnew
__lib=home&__act=bannerrecm
__lib=home&__act=tagforums
__lib=home&__act=appcolumns
__lib=home&__act=ad
__lib=home&__act=recmthreads&_v=3
```

### subject
```js
// 仅响应为 post 请求, 参数 fid, 可选参数 page
__lib=subject&__act=list
__lib=subject&__act=topped
__lib=subject&__act=list&recommend=1
__lib=subject&__act=vote
__lib=subject&__act=search
__lib=subject&__act=subscription
__lib=subject&__act=hot
```

### favor
```js
__lib=favor&__act=all
__lib=favor&__act=`%@`
```

### favorforum
```js
__lib=favorforum&__act=sync
__lib=favorforum&__act=`%@`
```

### user
```js
__lib=user&__act=subjects
__lib=user&__act=replys
__lib=user&__act=detail
__lib=user&__act=detailname
__lib=user&__act=update
__lib=user&__act=editsignature
__lib=user&__act=thirdpartylogin
__lib=user&__act=thirdpartyregister
```

### post
```js
__lib=post&__act=list
__lib=post&__act=titletype
__lib=post&__act=recommend
__lib=post&__act=check
__lib=post&__act=new
__lib=post&__act=reply
__lib=post&__act=modify
__lib=post&__act=`%@`
```

### message
```js
__lib=message&__act=list
__lib=message&__act=leave
__lib=message&__act=send
__lib=message&__act=reply
__lib=message&__act=detail
```

### gift
```js
__lib=gift&__act=list
__lib=gift&__act=userlist
__lib=gift&__act=send
__lib=gift&__act=setreceive
```

### notify
```js
__lib=notify&__act=list
__lib=notify&__act=unreadcnt
```

### nearby
```js
__lib=nearby&__act=updLocAndGetUsersNear
```

### block
```js
__lib=block&__act=list
__lib=block&__act=`%@`
```

### forum
```js
__lib=forum&__act=search
```

### device
```js
__lib=device&__act=upload
```

### blackstore
```js
__lib=blackstore&__act=list
__lib=blackstore&__act=purchased
__lib=blackstore&__act=order
__lib=blackstore&__act=exchange
__lib=blackstore&__act=lastaddr
__lib=blackstore&__act=address
```

### addresslist
```js
__lib=addresslist&__act=get
```

### game
```js
__lib=game&__act=query
__lib=game&__act=items
__lib=game&__act=scores
```

### match
```js
__lib=match&__act=list
__lib=match&__act=items
```

### ow
```js
__lib=ow&__act=playerlist
__lib=ow&__act=playershow
__lib=ow&__act=heroshow
__lib=ow&__act=playerranking
__lib=ow&__act=heroranking
__lib=ow&__act=playerrefresh
__lib=ow&__act=playerupdate
__lib=ow&__act=playerremove
```

### wow
```js
__lib=wow&__act=characterlist
__lib=wow&__act=realmlist
__lib=wow&__act=characteradd
__lib=wow&__act=characterremove
__lib=wow&__act=charactershow
__lib=wow&__act=characterrefresh
__lib=wow&__act=characterranking
__lib=wow&__act=charactercheck
__lib=wow&__act=characteruncheck
__lib=wow&__act=guildranking
__lib=wow&__act=raidlist
```

### manage
```js
__lib=manage&__act=topicget
__lib=manage&__act=topicset
__lib=manage&__act=topicdel
__lib=manage&__act=postget
__lib=manage&__act=postset
__lib=manage&__act=gagget
__lib=manage&__act=gagset
__lib=manage&__act=scoreget
__lib=manage&__act=scoreset
```

### openim
```js
__lib=openim&__act=user
```
