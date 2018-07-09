dev branch
# 配置
- xswitch   ip地址 192.168.2.129
- AppServer ip地址 192.168.2.117
- DialPlan 是这样的

# <extension name="ai">
	<condition field="destination_number" expression="^8888$">
		<action application="answer"/>
		<action application="ai" data="{url=http://192.168.2.117:4567/ivr_entry}"/>
	</condition>
</extension>  

# X-Lite 以1018用户注册到 xswitch, 呼叫接入号8888

# 192.168.2.129(xswitch) 发 192.168.2.117(AppServer)

>     Hypertext Transfer Protocol
>     POST /ivr_entry HTTP/1.1
>     Host: 192.168.2.117:4567
>     User-Agent: freeswitch-curl/1.0
>     Content-Type: application/json
>     [Full request URI: http://192.168.2.117:4567/ivr_entry]
>     [HTTP request 1/1]
> 
>     {
>     "uuid": "eb7d45e0-4eb5-11e8-99df-53f214a93242",
>     "url": "http://192.168.2.117:4567/ivr_entry",
>     "hostname": "debian",
>     "cid_number": "1018",
>     "dest_number": "8888",
>     "call_status": "ringing",
>     "direction": "inbound",
>     "channel_data": {
>     "Caller-Direction": "inbound",
>     "Caller-Logical-Direction": "inbound",
>     "Caller-Username": "1018",
>     "Caller-Dialplan": "XML",
>     "Caller-Caller-ID-Name": "1018",
>     "Caller-Caller-ID-Number": "1018",
>     "Caller-Orig-Caller-ID-Name": "1018",
>     "Caller-Orig-Caller-ID-Number": "1018",
>     "Caller-Network-Addr": "192.168.2.120",
>     "Caller-ANI": "1018",
>     "Caller-Destination-Number": "8888",
>     "Caller-Unique-ID": "e4fdf78a-4ead-11e8-9e80-f336cab85f3b",
>     "Caller-Source": "mod_sofia",
>     "Caller-Context": "default",
>     "Caller-Channel-Name": "sofia/internal/1019@192.168.2.129",
>     "Caller-Profile-Index": "1",
>     "Caller-Profile-Created-Time": "1525336941302749",
>     "Caller-Channel-Created-Time": "1525336941302749",
>     "Caller-Channel-Answered-Time": "1525336941322578",
>     "Caller-Channel-Progress-Time": "0",
>     "Caller-Channel-Progress-Media-Time": "1525336941322578",
>     "Caller-Channel-Hangup-Time": "0",
>     "Caller-Channel-Transfer-Time": "0",
>     "Caller-Channel-Resurrect-Time": "0",
>     "Caller-Channel-Bridged-Time": "0",
>     "Caller-Channel-Last-Hold": "0",
>     "Caller-Channel-Hold-Accum": "0",
>     "Caller-Screen-Bit": "true",
>     "Caller-Privacy-Hide-Name": "false",
>     "Caller-Privacy-Hide-Number": "false"
>    }
>  }



# 192.168.2.117(AppServer) 回 192.168.2.129(xswitch)

>     Hypertext Transfer Protocol
>     HTTP/1.1 200 OK
>     Content-Type: application/json
>
>     {
>       "action":"play",
>       "file":"welcome.wav",
>       "name":"inputid",
>       "digit-timeout":"3000",
>       "input-timeout":"5000",
>       "next":"192.168.2.117:4567/play_ack",
>       "asr-engine":"ifly",
>       "asr-grammar":"default|mandarin",
>       "private_data":
>       {
>         "myseq":"1"
>       }
>     }


# 现在听到xswitch 播放的welcome.wav, 之后大声“你好”,然后等结果
# 192.168.2.129(xswitch) 把语音识别的结果发给 192.168.2.117(AppServer)

>     Hypertext Transfer Protocol
>     POST /ivr_entry HTTP/1.1
>     Host: 192.168.2.117:4567
>     User-Agent: freeswitch-curl/1.0
>     Content-Type: application/json
>     [Full request URI: http://192.168.2.117:4567/play_ack]
>
>     [HTTP request 1/1]
>     {
>       "uuid": "eb7d45e0-4eb5-11e8-99df-53f214a93242",
>       "hostname": "debian",
>       "cid_number": "1018",
>       "dest_number": "8888",
>       "call_status": "ringing",
>       "direction": "inbound",
>       "url": "192.168.2.117:4567/play_ack",
>       "input_type": "detected_speech",
>       "asr_result": {
>         "corpus_no": "cisr1PdHHBHXzVo2kG1CadWeY04BWxU1kra",
>         "err_msg": "success.",
>         "err_no": 0,
>         "result": [
>           "你好。"
>         ],
>         "sn": "3"
>       },
>       "private_data": {
>         "myseq": "1"
>       },
>       "channel_data": {
>         "Caller-Direction": "inbound",
>         "Caller-Logical-Direction": "inbound",
>         "Caller-Username": "1018",
>         "Caller-Dialplan": "XML",
>         "Caller-Caller-ID-Name": "1018",
>         "Caller-Caller-ID-Number": "1018",
>         "Caller-Orig-Caller-ID-Name": "1018",
>         "Caller-Orig-Caller-ID-Number": "1018",
>         "Caller-Network-Addr": "192.168.2.144",
>         "Caller-ANI": "1018",
>         "Caller-Destination-Number": "8888",
>         "Caller-Unique-ID": "eb7d45e0-4eb5-11e8-99df-53f214a93242",
>         "Caller-Source": "mod_sofia",
>         "Caller-Context": "default",
>         "Caller-Channel-Name": "sofia/internal/1018@192.168.2.129:5060",
>         "Caller-Profile-Index": "1",
>         "Caller-Profile-Created-Time": "1525340388181835",
>         "Caller-Channel-Created-Time": "1525340388181835",
>         "Caller-Channel-Answered-Time": "1525340388202233",
>         "Caller-Channel-Progress-Time": "0",
>         "Caller-Channel-Progress-Media-Time": "1525340388181835",
>         "Caller-Channel-Hangup-Time": "0",
>         "Caller-Channel-Transfer-Time": "0",
>         "Caller-Channel-Resurrect-Time": "0",
>         "Caller-Channel-Bridged-Time": "0",
>         "Caller-Channel-Last-Hold": "0",
>         "Caller-Channel-Hold-Accum": "0",
>         "Caller-Screen-Bit": "true",
>         "Caller-Privacy-Hide-Name": "false",
>         "Caller-Privacy-Hide-Number": "false"
>       }
>     } 
