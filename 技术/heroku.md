流程基本参考自[这里](https://www.shopee6.com/web/web-tutorial/heroku-cloudflare-v2.html)


## 创建app

通过[这个链接](https://github.com/bclswl0827/v2ray-heroku)创建app

此时已经确保登陆heroku账号

![](http://cdn.attack204.com/20200803215915.png)

![](http://cdn.attack204.com/20200803220057.png)

## 使用cloudflare反向加速

创建一个worker

![](http://cdn.attack204.com/20200803220436.png)

填写，然后点击`保存并部署`

```js
addEventListener(
  "fetch",event => {
     let url=new URL(event.request.url);
     url.hostname="改成heroku程序名.herokuapp.com";
     let request=new Request(url,event.request);
     event. respondWith(
       fetch(request)
     )
  }
)
```
## 使用v2ray连接服务器

先用软件跑可用域名


链接: https://pan.baidu.com/s/165lv5uGdQE3T5IPzVLBIBA 提取码: ugk9

点击最后一个文件，跑出来的文件在`速度测试.txt`里，把第一个填上就行

注意这里最好白天跑，晚上跑出来的可能会很慢

![](http://cdn.attack204.com/20200803220823.png)





