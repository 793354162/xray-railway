## 该项目是该项目https://github.com/mixool/xrayku 的移植，感谢大佬
>[原项目教程](https://github.com/mixool/xrayku)建议对比着看就明白了~
>鉴于大佬已经把SS和trojan-go移除项目，所以不建议使用这两，用v2不香吗？
## 懒人专属！
>[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/new/template?template=https%3A%2F%2Fgithub.com%2Fwinkxx%2Fxray-railway&envs=CADDYIndexPage%2CCONFIGCADDY%2CCONFIGXRAY%2CParameterSSENCYPT%2CPORT%2CStoreFiles%2CAUUID&CADDYIndexPageDefault=https%3A%2F%2Fraw.githubusercontent.com%2Fcaddyserver%2Fdist%2Fmaster%2Fwelcome%2Findex.html&CONFIGCADDYDefault=https%3A%2F%2Fraw.githubusercontent.com%2Fmixool%2Fxrayku%2Fmaster%2Fetc%2FCaddyfile&CONFIGXRAYDefault=https%3A%2F%2Fraw.githubusercontent.com%2Fmixool%2Fxrayku%2Fmaster%2Fetc%2Fxray.json&ParameterSSENCYPTDefault=chacha20-ietf-poly1305&PORTDefault=6992&StoreFilesDefault=https%3A%2F%2Fraw.githubusercontent.com%2Fmixool%2Fxrayku%2Fmaster%2Fetc%2FStoreFiles&referralCode=dRpUXN)
  
## 部署(railway版)
1. 点击按钮,默认会新建一个仓库~
2. 下面都是带有默认值的，均是指向大佬仓库，别修改~
3. **只要修改下面的AUUID就好了！！！我可没有写入默认值，自行生成！**
  
### 客户端
* **务必替换所有的appname.herokuapp.com为railway分配的项目域名**  
* **务必替换所有的AUUID以及password为部署时设置的AUUID的值(所有！)**  
  
<details>
<summary>xray</summary>

```bash
* 客户端下载：https://github.com/XTLS/Xray-core/releases
* 代理协议：vless 或 vmess
* 地址：appname.herokuapp.com
* 端口：443
* 默认UUID：AUUID
* 加密：none
* 传输协议：ws
* 伪装类型：none
* 路径：/AUUID-vless // 默认vless使用/$uuid-vless，vmess使用/$uuid-vmess
* 底层传输安全：tls
```
</details>
  
<details>
<summary>trojan-go</summary>

```bash
* 客户端下载: https://github.com/p4gefau1t/trojan-go/releases
{
    "run_type": "client",
    "local_addr": "127.0.0.1",
    "local_port": 1080,
    "remote_addr": "appname.herokuapp.com",
    "remote_port": 443,
    "password": [
        "AUUID"
    ],
    "websocket": {
        "enabled": true,
        "path": "/AUUID-trojan",
        "host": "appname.herokuapp.com"
    }
}
```
</details>
  
<details>
<summary>shadowsocks</summary>

```bash
* 客户端下载：https://github.com/shadowsocks/shadowsocks-windows/releases/
* 服务器地址: appname.herokuapp.com
* 端口: 443
* 密码：password
* 加密：chacha20-ietf-poly1305
* 插件程序：xray-plugin_windows_amd64.exe  //需将插件https://github.com/shadowsocks/xray-plugin/releases下载解压后放至shadowsocks同目录
* 插件选项: tls;host=appname.herokuapp.com;path=/AUUID-ss
```
</details>
  
<details>
<summary>cloudflare workers example</summary>

```js
const SingleDay = 'appname.herokuapp.com'
const DoubleDay = 'appname.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
</details>
  
> [更多来自热心网友PR的使用教程](/tutorial)

