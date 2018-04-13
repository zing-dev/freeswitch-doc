# freeSWITCH 安装
官网教程 <https://freeswitch.org/confluence/display/FREESWITCH/FreeSWITCH+First+Steps>

## Windows
### download page
- <http://files.freeswitch.org/windows/installer/>
- 64位 <http://files.freeswitch.org/windows/installer/x64/>
- 32位 <http://files.freeswitch.org/windows/installer/x86/>

### install
- 下载对应版本
- 默认安装目录 `C:\Program Files\FreeSWITCH`

### run
- 以管理员权限运行freeswitch命令 `FreeSwitchConsole.exe`
> ![images](images/001.png)
- 客户端 `fs_cli.exe`
> ![images](images/002.png)
**显示安装成功**

## Mac
### install
- `brew install freeswitch`
> ![images](images/003.png)

### run 
- 服务端  `brew services start freeswitch`
- 客户端  `fs_cli`
![images](images/004.png)

## Linux
### debin-jessie install
官网教程<https://freeswitch.org/confluence/display/FREESWITCH/Debian+8+Jessie>
```
aliyun source
deb http://mirrors.aliyun.com/debian/ jessie main non-free contrib
deb http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib
deb-src http://mirrors.aliyun.com/debian/ jessie main non-free contrib
deb-src http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib

wget -O - https://files.freeswitch.org/repo/deb/debian/freeswitch_archive_g0.pub | apt-key add -
echo "deb http://files.freeswitch.org/repo/deb/freeswitch-1.6/ jessie main" > /etc/apt/sources.list.d/freeswitch.list

apt-get update && apt-get install -y freeswitch-meta-all

```
### run 
- 服务端  `sudo systemctl start freeswitch.service`
> ![images](images/005.png)
- 客户端  `fs_cli`
> ![images](images/006.png)


## X-lite客户端安装
> Before you download X-Lite for Windows PC or Mac, please note that in order to use X-Lite to make audio calls to softphone/mobile/landline numbers and make video calls/send Instant Messages to softphones, a VoIP subscription with a local service provider or Internet Service Provider is required. Please contact your local service provider to subscribe.
- 官网 <http://www.counterpath.com/>
- Windows <http://counterpath.s3.amazonaws.com/downloads/X-Lite_5.2.0_90534.exe>
- Mac <http://counterpath.s3.amazonaws.com/downloads/X-Lite_5.2.0_90533.dmg>

默认安装即可

## zoiper 安装（移动端）
- 官网 <https://www.zoiper.com/>
- google play <https://play.google.com/store/apps/details?id=com.zoiperpremium.android.app&pcampaignid=MKT-Other-global-all-co-prtnr-py-PartBadge-Mar2515-1>
- apple store <https://itunes.apple.com/us/app/id787863350?mt=8>

### 开发文档
- documentation <https://www.zoiper.com/documentation/zoiper-com-api/v1.1/>
- 示例      <https://www.zoiper.com/documentation/Zoiper3-API-Examples/Zoiper3_Delphi_COM_API_Example_v1.0.zip>

