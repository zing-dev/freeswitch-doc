## NOTE

### echo
可以在FreeSWITCH中使用originate命令发起一次呼叫。下面我们看个例子。假设用户1000已经注册，那么可以运行如下命令：
```
freeswitch> originate user/1000 &echo
```
`echo`则是一个常用的应用程序（`Application，App`），它的作用是控制一个`Channel`的一端。
`echo`是一个回音程序，即它会把任何它“听到”的声音（或视频）再返回（说/播）给对方。

### 呼叫字符串
`user/1000`称为呼叫字符串（`Dial String`，有时也叫`Call URL`）。`user`是一种特殊的呼叫字符串

#### 注册信息
```
freeswitch@jessie-freeswitch> sofia status profile internal reg

Registrations:
=================================================================================================
Call-ID:    	90534ZDA1ZGE3YTBiZGZmM2RiNGZhNjk5ZDJkYzMyMWQ1N2Y
User:       	1000@10.0.2.15
Contact:    	"1000" <sip:1000@192.168.1.155:64382;rinstance=d7ced57f5d9c6b4f>
Agent:      	X-Lite release 5.2.0 stamp 90534
Status:     	Registered(UDP)(unknown) EXP(2018-04-14 02:27:20) EXPSECS(2309)
Ping-Status:	Reachable
Ping-Time:	0.00
Host:       	jessie-freeswitch
IP:         	192.168.1.155
Port:       	64382
Auth-User:  	1000
Auth-Realm: 	192.168.1.51
MWI-Account:	1000@10.0.2.15

Call-ID:    	JBqKtWXl3X0nmbAa-4_N1g..
User:       	1002@10.0.2.15
Contact:    	"" <sip:1002@192.168.1.147:34172;transport=TCP;rinstance=3f3a3f56b78ac4d2>
Agent:      	Zoiper rv2.8.87-mod
Status:     	Registered(TCP)(unknown) EXP(2018-04-14 01:55:06) EXPSECS(375)
Ping-Status:	Reachable
Ping-Time:	0.00
Host:       	jessie-freeswitch
IP:         	192.168.1.147
Port:       	34172
Auth-User:  	1002
Auth-Realm: 	192.168.1.51
MWI-Account:	1002@10.0.2.15

Call-ID:    	90533OTliNWFiMTFkNjZiZDc1YzVhMjRkZDNjODRkN2NmMzc
User:       	1001@10.0.2.15
Contact:    	"1001" <sip:1001@192.168.1.145:53582;rinstance=a5c00f203948093e>
Agent:      	X-Lite release 5.2.0 stamp 90533
Status:     	Registered(UDP)(unknown) EXP(2018-04-14 02:49:45) EXPSECS(3654)
Ping-Status:	Reachable
Ping-Time:	0.00
Host:       	jessie-freeswitch
IP:         	192.168.1.145
Port:       	53582
Auth-User:  	1001
Auth-Realm: 	192.168.1.51
MWI-Account:	1001@10.0.2.15

Total items returned: 3
=================================================================================================

```
`FreeSWITCH`根据`Contact`字段知道`1001`的SIP地址：`sip:1001@192.168.1.145:53582`。当使用`originate`命令呼叫`1001`这个呼叫字符串时，FreeSWITCH便会在用户目录中查找`1001`这个用户，找到她的`dial-string`参数 ，`dial-string`参数通常包含`1001`实际`Contact`地址的查找方法，`FreeSWITCH`进而找到`1001`的`Contact`地址`sip:1001@192.168.1.145:53582`并向其发送`INVITE`请求。


### park
```
freeswitch> originate user/1000 &park
```
初始化了一个呼叫时，在`1000`接电话后对端必须有一个人在跟其讲话（否则，如果一个`Channel`只有一端，那是不可思议的事情），而如果这时`FreeSWITCH`找不到一个合适的人跟`1000`通话，那么它可以将该电话`“挂起”`，`park`便是实现这个功能，它相当于一个`Channel`特殊的一端

### hold
等待的同时播放保持音乐（`Music on Hold，MOH`）
```
freeswitch>originate user/1000 &hold
```

播放一个特定的声音文件
```
freeswitch> originate user/1000 &playback(/root/welcome.wav)
```

直接录音
```
freeswitch> originate user/1000 &record(/tmp/voice_of_1000.wav)
```

在1000接听电话以后，bridge程序可以再启动一个UA呼叫1001，如
```
freeswitch> originate user/1000 &bridge(user/1001)
```

## 系统常量
### `global_getvar`
```
freeswitch@jessie-freeswitch> global_getvar
hostname=jessie-freeswitch
local_mask_v4=255.255.255.0
local_ip_v6=::1
base_dir=/usr
recordings_dir=/var/lib/freeswitch/recordings
sounds_dir=/usr/share/freeswitch/sounds
conf_dir=/etc/freeswitch
log_dir=/var/log/freeswitch
run_dir=/var/run/freeswitch
db_dir=/var/lib/freeswitch/db
mod_dir=/usr/lib/freeswitch/mod
htdocs_dir=/usr/share/freeswitch/htdocs
script_dir=/usr/share/freeswitch/scripts
temp_dir=/tmp
grammar_dir=/usr/share/freeswitch/grammar
fonts_dir=/usr/share/freeswitch/fonts
images_dir=/var/lib/freeswitch/images
certs_dir=/etc/freeswitch/tls
storage_dir=/var/lib/freeswitch/storage
cache_dir=/var/cache/freeswitch
data_dir=/usr/share/freeswitch
localstate_dir=/var/lib/freeswitch
switch_serial=0a00020fd6cc
default_password=1234
sound_prefix=/usr/share/freeswitch/sounds/en/us/callie
local_ip_v4=192.168.1.51
domain=192.168.1.51
hold_music=local_stream://moh
use_profile=external
rtp_sdes_suites=AEAD_AES_256_GCM_8|AEAD_AES_128_GCM_8|AES_CM_256_HMAC_SHA1_80|AES_CM_192_HMAC_SHA1_80|AES_CM_128_HMAC_SHA1_80|AES_CM_256_HMAC_SHA1_32|AES_CM_192_HMAC_SHA1_32|AES_CM_128_HMAC_SHA1_32|AES_CM_128_NULL_AUTH
zrtp_secure_media=true
global_codec_prefs=OPUS,G722,PCMU,PCMA,VP8
outbound_codec_prefs=OPUS,G722,PCMU,PCMA,VP8
xmpp_client_profile=xmppc
xmpp_server_profile=xmpps
bind_server_ip=auto
external_rtp_ip=stun:stun.freeswitch.org
external_sip_ip=stun:stun.freeswitch.org
unroll_loops=true
outbound_caller_name=FreeSWITCH
outbound_caller_id=0000000000
call_debug=false
console_loglevel=info
default_areacode=918
default_country=US
presence_privacy=false
au-ring=%(400,200,383,417);%(400,2000,383,417)
be-ring=%(1000,3000,425)
ca-ring=%(2000,4000,440,480)
cn-ring=%(1000,4000,450)
cy-ring=%(1500,3000,425)
cz-ring=%(1000,4000,425)
de-ring=%(1000,4000,425)
dk-ring=%(1000,4000,425)
dz-ring=%(1500,3500,425)
eg-ring=%(2000,1000,475,375)
es-ring=%(1500,3000,425)
fi-ring=%(1000,4000,425)
fr-ring=%(1500,3500,440)
hk-ring=%(400,200,440,480);%(400,3000,440,480)
hu-ring=%(1250,3750,425)
il-ring=%(1000,3000,400)
in-ring=%(400,200,425,375);%(400,2000,425,375)
jp-ring=%(1000,2000,420,380)
ko-ring=%(1000,2000,440,480)
pk-ring=%(1000,2000,400)
pl-ring=%(1000,4000,425)
ro-ring=%(1850,4150,475,425)
rs-ring=%(1000,4000,425)
ru-ring=%(800,3200,425)
sa-ring=%(1200,4600,425)
tr-ring=%(2000,4000,450)
uk-ring=%(400,200,400,450);%(400,2000,400,450)
us-ring=%(2000,4000,440,480)
bong-ring=v=-7;%(100,0,941.0,1477.0);v=-7;>=2;+=.1;%(1400,0,350,440)
beep=%(1000,0,640)
sit=%(274,0,913.8);%(274,0,1370.6);%(380,0,1776.7)
df_us_ssn=(?!219099999|078051120)(?!666|000|9\d{2})\d{3}(?!00)\d{2}(?!0{4})\d{4}
df_luhn=?:4[0-9]{12}(?:[0-9]{3})?|5[1-5][0-9]{14}|3[47][0-9]{13}|3(?:0[0-5]|[68][0-9])[0-9]{11}|6(?:011|5[0-9]{2})[0-9]{12}|(?:2131|1800|35\d{3})\d{11}
default_provider=example.com
default_provider_username=joeuser
default_provider_password=password
default_provider_from_domain=example.com
default_provider_register=false
default_provider_contact=5000
sip_tls_version=tlsv1,tlsv1.1,tlsv1.2
sip_tls_ciphers=ALL:!ADH:!LOW:!EXP:!MD5:@STRENGTH
internal_auth_calls=true
internal_sip_port=5060
internal_tls_port=5061
internal_ssl_enable=false
external_auth_calls=false
external_sip_port=5080
external_tls_port=5081
external_ssl_enable=false
rtp_video_max_bandwidth_in=1mb
rtp_video_max_bandwidth_out=1mb
suppress_cng=true
rtp_liberal_dtmf=true
video_mute_png=/var/lib/freeswitch/images/default-mute.png
video_no_avatar_png=/var/lib/freeswitch/images/default-avatar.png
AT_EPENT1=0 0 0 -1 -1 0 -1 0 -1 -1 0 -1
AT_EPENT2=1 1 1 -1 -1 1 -1 1 -1 -1 1 -1
AT_CPENT1=0 -1 -1 0 -1 0 0 0 -1 -1 0 -1
AT_CPENT2=1 -1 -1 1 -1 1 1 1 -1 -1 1 -1
AT_CMAJ1=0 -1 0 0 -1 0 -1 0 0 -1 0 -1
AT_CMAJ2=1 -1 1 1 -1 1 -1 1 1 -1 1 -1
AT_BBLUES=1 -1 1 -1 -1 1 -1 1 1 1 -1 -1
ATGPENT2=-1 1 -1 1 -1 1 -1 -1 1 -1 1 -1
zrtp_enabled=false
core_uuid=ae5fcc4f-928b-4d17-a407-08b56279679e

```