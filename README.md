# MRCP-Plugin-Demo
> Forked from [https://github.com/cotinyang/MRCP-Plugin-Demo](https://github.com/cotinyang/MRCP-Plugin-Demo)
>
> 因为需要所以进行了一定修改。

### 更改之处

1. MRCP-Plugin-Demo\unimrcp-1.5.0\plugins\xfyun-recog\src\xfyun_recog_engine.c文件。

   在大概450行后，也就是在  <kbd>message->start_line.request_state = MRCP_REQUEST_STATE_INPROGRESS;</kbd>

   后面，在<kbd>return mrcp_engine_channel_message_send(recog_channel->channel,message) </kbd> 前面。

   添加以下代码：

   ```c
   // set message body data.    by Smileyan
   message->body.buf = recog_channel->last_result;
   message->body.length =  strlen(recog_channel->last_result);	
   // log data that will be sent.      by Smileyan
   apt_log(RECOG_LOG_MARK,APT_PRIO_INFO,"[xfyun] recog_channel->last_result == %s", recog_channel->last_result);
   apt_log(RECOG_LOG_MARK,APT_PRIO_INFO,"[xfyun] message->header==%s message->body== %s", message->header,message->body);	
   ```

2. MRCP-Plugin-Demo\unimrcp-1.5.0\conf\unimrcpserver.xml文件。

   在\<plugin-factory> 标签下面，删除原来有的engine。把代码修改如下：

   ```xml
   <engine id="Demo-Recog-1" name="demorecog" enable="false"/>
   <engine id="XFyun-Recog-1" name="xfyunrecog" enable="true"/>
   <engine id="Demo-Synth-1" name="demorecog" enable="false"/>
   <engine id="XFyun-Synth-1" name="xfyunsynth" enable="true"/>
   <engine id="Recorder-1" name="mrcprecorder" enable="true"/>
   ```

   

### 使用帮助

1. 下载这个 MRCP-Plugin-Demo
2. 下载科大讯飞SDK。
3. 编辑xfyun_recog_engine.c ，设置appid。
4. 添加libmsc.so到/usr/lib。
5. 编译安装MRCP-Plugin-Demo。

#### 具体过程参考请参考以下地址

