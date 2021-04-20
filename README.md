# AppAPI

<details>
  <summary>点击展开目录</summary>
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [注意](#%E6%B3%A8%E6%84%8F)
- [登录](#%E7%99%BB%E5%BD%95)
  - [客户端专属登录](#%E5%AE%A2%E6%88%B7%E7%AB%AF%E4%B8%93%E5%B1%9E%E7%99%BB%E5%BD%95)
  - [网页登录](#%E7%BD%91%E9%A1%B5%E7%99%BB%E5%BD%95)
- [其余网络请求](#%E5%85%B6%E4%BD%99%E7%BD%91%E7%BB%9C%E8%AF%B7%E6%B1%82)
  - [baseURL: `app_api.php`](#baseurl-app_apiphp)
  - [基础参数](#%E5%9F%BA%E7%A1%80%E5%8F%82%E6%95%B0)
    - [刮墙签到](#%E5%88%AE%E5%A2%99%E7%AD%BE%E5%88%B0)
    - [home](#home)
    - [subject](#subject)
    - [favor](#favor)
    - [favorforum](#favorforum)
    - [user](#user)
    - [post](#post)
    - [message](#message)
    - [gift](#gift)
    - [notify](#notify)
    - [nearby](#nearby)
    - [block](#block)
    - [forum](#forum)
    - [device](#device)
    - [blackstore](#blackstore)
    - [addresslist](#addresslist)
    - [game](#game)
    - [match](#match)
    - [ow](#ow)
    - [wow](#wow)
    - [manage](#manage)
    - [openim](#openim)
- [nuke.php 请求](#nukephp-%E8%AF%B7%E6%B1%82)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

</details>

## 注意

⚠️参数等信息(比如 `%@` 为要替换的参数值) [参考这里的网页版文档](https://github.com/wolfcon/NGA-API-Documents/wiki). 

由于本 API 列表是 ~~`以某科学方式获得`~~ , 有可能会不全, 欢迎 PR 补全各项信息.

## 登录

### 客户端专属登录

特殊域名: `https://account.178.com/app_api.php`

`Post` 请求参数如下:

| key      | value                  | 说明                                                |
| -------- | ---------------------- | --------------------------------------------------- |
| _act     | login                  | 动作                                                |
| app_id   | 1001                   | 针对 iOS App                                        |
| email    | <输入内容>             | 用户名/手机号/邮箱                                  |
| password | *<加密后的值>*         | 采用 ASE 128 加密                                   |
| t        | **<根据当前时间得到>** | 时间戳, timeIntervalSince1970, 多次会用到, 取相同值 |
| sign     | <客户端认证码>         | 拼接的字串取 `MD5` 值 (小写)                        |

**值得注意的是:** 

- 这里的 `AppSecret` 是 `e32fde76d79adb6326dcef8b41dcf30175a7a80b`, 

- 密码加密采用的是 AES 128, ECB 模式. 加密 `Key` 是 `AppSecret` 的后 16 位, 即为: `41dcf30175a7a80b`

- 拼接的字串为: `时间戳` + `AppSecret` + `email` + `encryptedPassword` + `app_id`

  ```swift
  let clientSign = "\(timestamp)\(appSecret)\(email)\(encryptedPassword)\(app_id)".md5.lowercased()
  ```

### 网页登录

这种方式是通过弹出 WebView 加载链接

登录过程: 

1. `WebView` 加载链接 `nuke.php?__lib=login&__act=account&login`
2. 输入用户名密码, 再填入验证码
3. 拦截消息
   - 拦截 `js` 的 `alert` 捕获错误; 
   - 拦截 `js` 的 `confirm` 捕获登录成功消息;

## 其余网络请求

### baseURL: `app_api.php`

```js
// 如果是自己拼接 URL 则需要注意, 添加 ? 哟
https://bbs.nga.cn/app_api.php

// 例如: 获取首页列表
https://bbs.nga.cn/app_api.php?__lib=home&__act=category&_v=2
// 例如: 获取用户的收藏板块(非收藏帖子)
https://bbs.nga.cn/app_api.php?__lib=favorforum&__act=sync
```

### 基础参数

cookie 中需要以下 2 个值来确认基础的登录信息, 它们的值由登录后的返回值取得.

- `ngaPassportUid` : 是 NGA 账户的 UID (数字 ID)
- `ngaPassportCid` : 是 NGA 账户登录后获取的认证码 Token

#### 刮墙签到

```js
// 签到
__lib=check_in&__act=check_in&__output=14
// 签到后获取签到数据
__lib=check_in&__act=get_stat&__output=14
```

#### home

```js
// 获取首页数据
__lib=home&__act=category&_v=2
__lib=home&__act=hasnew
__lib=home&__act=bannerrecm
__lib=home&__act=tagforums
__lib=home&__act=appcolumns
__lib=home&__act=ad
__lib=home&__act=recmthreads&_v=3
```

#### subject
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

#### favor
```js
__lib=favor&__act=all
__lib=favor&__act=`%@`
```

#### favorforum
```js
// 同步收藏版块
__lib=favorforum&__act=sync
__lib=favorforum&__act=`%@`
```

#### user
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

#### post
```js
__lib=post&__act=list
// 获取主题分类信息
__lib=post&__act=titletype
__lib=post&__act=recommend
// 获取发布信息, 比如上传地址, 上传验证码等等
__lib=post&__act=check
__lib=post&__act=new
__lib=post&__act=reply
__lib=post&__act=modify
__lib=post&__act=`%@`
```

#### message
```js
__lib=message&__act=list
__lib=message&__act=leave
__lib=message&__act=send
__lib=message&__act=reply
__lib=message&__act=detail
```

#### gift
```js
__lib=gift&__act=list
__lib=gift&__act=userlist
__lib=gift&__act=send
__lib=gift&__act=setreceive
```

#### notify
```js
__lib=notify&__act=list
__lib=notify&__act=unreadcnt
```

#### nearby
```js
__lib=nearby&__act=updLocAndGetUsersNear
```

#### block
```js
__lib=block&__act=list
__lib=block&__act=`%@`
```

#### forum
```js
__lib=forum&__act=search
```

#### device
```js
__lib=device&__act=upload
```

#### blackstore
```js
__lib=blackstore&__act=list
__lib=blackstore&__act=purchased
__lib=blackstore&__act=order
__lib=blackstore&__act=exchange
__lib=blackstore&__act=lastaddr
__lib=blackstore&__act=address
```

#### addresslist
```js
__lib=addresslist&__act=get
```

#### game
```js
__lib=game&__act=query
__lib=game&__act=items
__lib=game&__act=scores
```

#### match
```js
__lib=match&__act=list
__lib=match&__act=items
```

#### ow
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

#### wow
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

#### manage
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

#### openim
```js
__lib=openim&__act=user
```



## nuke.php 请求

```js
// 登录
nuke.php?__lib=login&__act=account&login
// 登出
nuke.php?__lib=login&__act=account&logout

nuke.php?__lib=filter&__act=get_log&fid=%@&id=%@&__output=14&jump_to=1
nuke.php?func=adminlog&f=access_log
nuke.php?__lib=login&__act=qrlogin_ui
nuke.php?__lib=app_inter&__act=recmd_topic
nuke.php?__lib=nga_index&__act=get_event_app&__output=14
nuke.php?__lib=login&__act=logout
nuke.php?__lib=login&__act=iflogin
nuke.php?__lib=item&__act=have_item&type=4&sub_type=%@
nuke.php?__lib=mission&__act=video_view_task_counter_add
nuke.php?__lib=mission&__act=video_view_task_get
nuke.php?__lib=app_inter&__act=banner_list
nuke.php?__lib=data_query&__act=topic_share_log_v2
nuke.php?__lib=filter&__act=get_log&fid=%@&id=%@&__output=14
nuke.php?__lib=load_topic&__act=load_topic_reply_ladder
```
