# mod_ai

```
make
make install
```

cp autoload_configs/ai.xml /usr/local/freeswitch/conf/configuration/.

##  ENTER INTO FreeSWITCH

	load mod_ai

## Interface

Http Method: POST,
Content-Type: application/json,
Body = action + next + variables + private_data

```
play
	"action":"play"
	"file"
	"error_file"
	"name"
	"digit-timeout"
	"input-timeout"
	"next"
	"asr-engine"
	"asr-grammar"
	"loops"
	"variables"
	{
		...
	}
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
record
	"action":"record"
	"name"
	"file"
	"next"
	"beep-file"
	"digit-timeout"
	"input-timeout"
	"terminators"
	"variables"
	{
		...
	}
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
pause
	"action":"pause"
	"next"
	"milliseconds"
	"private_data"
	{
		"seq"
		"data"
	}
```

```
speak
	"action":"speak"
	"file"
	"error_file"
	"name"
	"digit-timeout"
	"input-timeout"
	"next"
	"gender"
	"loops"
	"engine"
	"voice"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
say
	"action":"say"
	"file"
	"error_file"
	"name"
	"digit-timeout"
	"input-timeout"
	"next"
	"language"
	"type"
	"method"
	"gender"
	"loops"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
execute
	"action":"execute"
	"next"
	"application"
	"data"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
sms
	"action":"sms"
	"next"
	"to"
	"data"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
dial
	"action":"dial"
	"next"
	"context"
	"dialplan"
	"caller-id-name"
	"caller-id-number"
	"callee-id-number"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
recordCall
	"action":"recordCall"
	"name"
	"limit"
	"next"
	"private_data"
	{
		"seq"
		"data"
		...
	}

```

```
conference
	"action":"conference"
	"next"
	"profile"
	"name"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
hangup
	"action":"hangup"
	"next"
	"cause"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
break
	"action":"break"
	"next"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
log
	"action":"log"
	"next"
	"level"
	"clean"
	"message"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
continue
	"action":"continue"
	"next"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
getVar
	"action":"getVar"
	"next"
	"name"
	"permanent"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```

```
voicemail
	"action":"voicemail"
	"check"
	"auth-only"
	"next"
	"profile"
	"domain"
	"id"
	"private_data"
	{
		"seq"
		"data"
		...
	}
```
