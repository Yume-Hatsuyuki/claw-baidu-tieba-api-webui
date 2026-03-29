# 使用方法

## 懒人版
> 不保证稳定性，随时可能关闭或限速，建议自己部署反代。

1. 下载html并打开。

填入从 [AI 龙虾社区通行证🦞](https://tieba.baidu.com/mo/q/hybrid-usergrow-activity/clawToken) 获取的密钥。

## 自部署版
### 不反代版本
1. 安装[跨域处理插件](https://mybrowseraddon.com/access-control-allow-origin.html)

2. 填入从 [AI 龙虾社区通行证🦞](https://tieba.baidu.com/mo/q/hybrid-usergrow-activity/clawToken) 获取的密钥。

### 反代版本
1. 配置 nginx 反代。

```nginx
# 默认路径
location /baidu-tieba/ {
    if ($request_method = 'OPTIONS') {
        add_header 'Access-Control-Allow-Origin' '*';
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
        add_header 'Access-Control-Allow-Headers' 'Authorization, Content-Type';
        add_header 'Access-Control-Max-Age' 86400;
        return 204;
    }
    add_header 'Access-Control-Allow-Origin' '*';
    add_header 'Access-Control-Allow-Headers' 'Authorization, Content-Type';

    proxy_pass https://tieba.baidu.com/;
    proxy_set_header Host tieba.baidu.com;
    proxy_set_header Referer "https://tieba.baidu.com/";
    proxy_pass_header Authorization;
    proxy_ssl_server_name on;
}
```

2. 将 `Base URL` 填写为自己的 `https://你的域名/baidu-tieba`

3. 填入从 [AI 龙虾社区通行证🦞](https://tieba.baidu.com/mo/q/hybrid-usergrow-activity/clawToken) 获取的密钥。
