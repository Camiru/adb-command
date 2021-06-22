# adb-command
adb的指令彙整
## adb 指令 <br/>
### Log分類:<br/>
Android日志主要分為kernel、radio、event、main這四種log。<br/><br/>

Kernel Log:<br/>
kernel log屬于Linux内核的log ，可以通過讀取/proc/kmsg或者通過串口來抓取。<br/>
adb 抓取kernel log的命令如下（需要有root權限）：<br/>
adb shell cat /proc/kmsg > /tmp/kernel.log<br/>
Radio Log:<br/>
Main Log:<br/>
main log和我們在eclipse裡通過DDMS中看到的log是一致的。抓取命令如下：<br/>
adb logcat -b main > /tmp/main.log<br/>
Event Log:<br/>
event log屬于system log，平時可以跟在main log之後。抓取命令如下：<br/>
adb logcat -b event -v time > /tmp/event.log<br/>
 -v time表示在log中加入每條log發生的時間。<br/>
完整Log:<br/>
adb logcat -b選項是可以復用的，因此我們抓取所有Log的命令就是復用了-b選項。抓取命令如下：<br/>
adb logcat -b main -b system -b radio -b events -v time > /tmp/all.log<br/><br/><br/>

### 狀態信息<br/>
adb shell cat /proc/kmsg # kernel日志,每cat一次清零<br/>
adb shell dmesg # kernel日志,開機信息.(var/log/demsg)<br/>
adb shell dumpstate # 系統狀態信息,比較全面,如:内存,CPU,log緩衝等。可以幫助我們確定是否有内存耗光之類的問題<br/>
adb shell dumpsys # 系統service相關信息<br/><br/><br/>

### 各種log預設存放位置<br/>
開機log<br/>
  adb shell dmesg > dmesg.txt<br/>
anr log<br/>
  adb pull /data/anr<br/>
kernel log(只有從當前時間起的很少的log)<br/>
  cat proc/kmsg > kmsg.txt<br/>
