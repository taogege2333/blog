# 一、通过MediaRecorder实现
```js
if(navigator.mediaDevices) {
    // 获取打开麦克风权限，以及stream对象
    navigator.mediaDevices.getUserMedia({audio: true})
    .then((stream) => {
        var chunks = [];
        // 创建MediaRecorder对象，需要传入stream对象
        var mediaRecorder = new MediaRecorder(stream);

        var startBtn = document.createElement('button');
        var stopBtn = document.createElement('button');
        document.body.append(startBtn);
        document.body.append(stopBtn);
        startBtn.innerText = '开始';
        stopBtn.innerText = '结束';
		
        // 开始
        startBtn.onclick = () => {
            // 开始录音 
            mediaRecorder.start();
        }
        // 结束
        stopBtn.onclick = () => {
            // 停止录音
            mediaRecorder.stop();
        }

        // 添加事件监听
        mediaRecorder.onstart = () => {
            console.log('start', mediaRecorder.state);
        }
        mediaRecorder.onstop = () => {
            console.log('stop', mediaRecorder.state);
            // 数据块合成blob对象
            var blob = new Blob(chunks, {type: 'audio/webm;codecs=opus'});
            console.log(blob)
			
            var audio = document.createElement('audio');
            var url = (window.URL || webkitURL).createObjectURL(blob);
            audio.src = url;
            audio.controls = true;
            document.body.appendChild(audio);
            console.log(audio, url)
        }
        mediaRecorder.ondataavailable = (e) => {
            console.log('data');
            console.log(e);
            chunks.push(e.data);
        }
    }).catch((e) => {
            console.log(e);
    })
}
```
# 二、通过recorder.js实现
插件地址[https://github.com/xiangyuecn/Recorder](https://github.com/xiangyuecn/Recorder)
1. 引入recorder
```html
<script src="https://cdn.jsdelivr.net/gh/xiangyuecn/Recorder@latest/recorder.mp3.min.js"></script> <!--已包含recorder-core和mp3格式支持-->
```
2. API
```js
// 创建Recorder对象
rec = Recorder({
	type:"mp3",
	sampleRate:16000,
	bitRate:16
});

// 调用open方法进行授权
rec.open(function () {
	alert('授权成功');
	//rec.start() 此处可以立即开始录音，但不建议这样编写，因为open是一个延迟漫长的操作，通过两次用户操作来分别调用open和start是推荐的最佳流程
    },function(msg,isUserNotAllow){//用户拒绝未授权或不支持
        //dialog&&dialog.Cancel(); 如果开启了弹框，此处需要取消
}, function (msg) {
	alert(msg);
});

// 开始录音
rec.start();

// 停止录音
rec.stop(function (blob, duration) {
	console.log('blob:', blob);
	// 创建指向音频文件的URL
	var audioURL = (window.URL || webkitURL).createObjectURL(blob);

	var audio = document.createElement('audio');
	audio.src = audioURL;
	audio.controls = true;
	document.body.appendChild(audio);
	// 简单利用URL生成播放地址，注意不用了时需要revokeObjectURL，否则霸占内存
	(window.URL||webkitURL).revokeObjectURL(audioURL);
}, function (msg) {
	alert(msg);
}, function () {
	// 释放录音资源
	rec.close();
	rec = null;
});
```