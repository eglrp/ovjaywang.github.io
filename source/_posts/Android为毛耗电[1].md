---
title: 'Android为毛耗电[1]'
categories:
  - App强推
  - 软文
tags:
  - Android
id: 889
date: 2015-12-28 23:34:25
---

**<font color="#000000"></font>****<font color="#000000" size="4"><font face="微软雅黑 Light">本文只讨论安卓手机软节电，不负责推荐底包、rom、调频调压方案，<font color="#ff0000">刷机root后果自负。</font></font></font>**

<font color="#000000" size="4" face="微软雅黑 Light">**纯硬货，只想节电看后文。**</font>

<!-- more -->
<font color="#000000" size="4" face="微软雅黑 Light">使用安德猴主要还是谷歌的情怀。最近无可救药的恋上了无线高质量同步的Google相册和Keep。此外Google Contact和Gmail也时不时要收一下。</font>

<font color="#000000" size="4" face="微软雅黑 Light">问题是。。墙内不能随时翻。国内流氓自启和相互唤醒严重影响待机时间。如何破？首先搞清楚什么在耗电。再来解决怎么防流氓的同时不影响收发消息体验。</font>

<font color="#333333"><font size="4"><font face="微软雅黑 Light"><font color="#000000">这里提到的几个概念是安猪手机由于真后台，而造成的各种能耗电耗流量元凶——四大组件</font>**<font color="#ff0000">Activity、Service、BroadCastReceiver、ContentProvider</font>。**</font></font></font>

**<font color="#333333" size="4" face="微软雅黑 Light">耗电--一定是这四个中的一个在以某种方式运行</font>**

<font color="#000000" size="4"><font face="微软雅黑 Light"><font color="#ff0000">**Activity**</font>简言之就是前台窗体可视界面它上面可以显示一些控件也可以监听并处理用户的事件做出响应。你跳转到一个程序的界面、里面可能嵌套了很多个Activity。也有的一个Activity自成一个界面，例如第一次启动的引导界面。当然，程序猿代码风格迥异，一个<font size="4">Activity有的直接盖在一个上面，这样按下返回键销毁当前的能直接返回上一个；有的流程和任务则直接生成新Activity把当前的干掉。一些广告，一些无聊的需求，如淘宝摇一摇、美图下游戏，你完全不想要，则可以通过阻止Activity启动的方式，干掉。这样的做法可以降低内存消耗。但如果代码流程，若写入了不开启这个Activity就没法运行，很可能造成FC。因此测试Activity阻止就需要很谨慎。网路也有很多大神提供了Activity的阻止列表。但App更新极快，同时包名和Activity的命名方式更加让人难以捉摸，就相当难以防范。</font></font></font>

<font color="#000000"><font size="4"><font face="微软雅黑 Light"><font color="#ff0000">**Activity**</font>之间通过<font color="#ff0000">Intent</font>进行通信，它描述的事某一个事件（单机、浏览、编辑）。也就是说这个Activity的一些参数在Activity跳转时，通过把参数塞入Intent这样一个对象，在另一个Activity读取。在Intent的描述结构中，有两个最重要的部分：动作和动作对应的数据。而IntentFilter则对应一个Activity能做哪些Intent。IntentFilter通常写入Android的AndroidManifest文件中定义好。</font></font></font>

<font color="#000000"><font size="4"><font face="微软雅黑 Light"><font color="#ff0000">**BroadCastReceiver**</font>（广播接收器）它是监听响应各种手机变化并作出响应反应的组件。例如打进电话某个App调出号码查询，例如WiFi网络改变某App可以进行同步。这些监听并不经常是我们需要的，同时如果App写的极差，接收的广播级多，也会造成资源的浪费也相当耗电。它并不会产生一个界面，但是它能唤起一个Activity或者Service对事件进行相应。最常见的就是电话来了闪灯响铃，最讨厌的就是有Wifi了发个通知广告。甚至，当一个App装过还启动过，由于设置了开机启动的响应或网络状况的变化响应，都会产生通知。然而与Activity一样，阻止某一种广播接收同样会可能造成应用使用不正常，但FC情况相当少，测试的时候需要相当小心，但这里的组件命名方式都较为规范，因此测试起来也会比较顺利。</font></font></font>

<font color="#000000" size="4" face="微软雅黑 Light">监听广播同样可以视为一个事件，使用Intent对其参数进行传递。这些事件，就是通常意义上的权限，可以查看联系人、可以监听电话等。许多监控App都能查看并修改应用程序能够监听的内容。注册广播接收器可以写入一个App的AndroidManifest.xml中进行静态注册，若完成时间比较长必须通过线程，放进Service后台中运行，否则容易造成程序卡顿；也可以程序动态注册，当Activity关闭后，监听广播也关闭，这样的做法比较省电，但是关闭程序就无法接受一些通知和广告。（需要完全退出或者多任务杀掉）因此大多数App都采用静态注册，App不启动，也能通过订阅的广播触发，例如开机启动触发、时间变化触发等。</font>

<font color="#000000"><font size="4"><font face="微软雅黑 Light"><font color="#ff0000">**Service**</font>（服务）也是无界面的组件，它通过后台长时间的运行来进行运行一些监测程序，例如后台听歌单曲循环等，后台轮询查询最新消息的微博。配合BroadCastReceiver使用效果极佳耗电也极棒。一个App很可能有相当多的Service在后台挂着，同时一个流氓集团的Service也会相互唤醒保证一个被杀掉的时候又自启动。但乱杀也会造成严重的后果，一些闹钟，一些天气，一些消息软件误杀后没有了后台Service做消息推送，就会错过重要的事情。</font></font></font>

<font color="#000000" size="4" face="微软雅黑 Light">一个Service不能自己运行。首次启动需要create再start，第二次之后就只用start需要别的启动或触发。但Service一旦启动，就与调用者无关了。需要停止service需要调用stop方法同时销毁destroy。可以使用bindservice让service随着调用者关闭而终止。</font>

<font color="#000000"><font size="4"><font face="微软雅黑 Light"><font color="#ff0000">**ContentProvider**</font>(内容提供者)一个应用程序的指定数据集提供给其他应用程序。这些数据可以存储在文件系统中、在一个SQLite数据库、或以任何其他合理的方式。其他应用可以通过ContentResolver类(见ContentProviderAccessApp例子)从该内容提供者中获取或存入数据.(相当于在应用外包了一层壳),最常见的就是支付婊在别的应用中的调用，它提供了一个统一的支付接口，写在一个内部路径URL里。</font></font></font>

<font color="#ff0000" size="4" face="微软雅黑 Light">四大组件启动，</font>

<font color="#000000" size="4" face="微软雅黑 Light">除了ContentProvider是通过别的应用程序调用ContentResolver 发出内容请求后激活外，其他三个都是通过Intent异步消息激活。
Activity的激活通过传递一个Intent 对象至<font color="#ff0000">Context.startActivity()或Activity.startActivityForResult()</font>以载入（或指定新工作给）一个activity。 前面的函数直接启动的Activity，可以查看Intent中传入的参数。若期待新启动的Activity返回一个值（例如填写个人信息提交返回是否成功）就调用后面那个函数，并调用onActivityResult() 查询返回结果. 
Service的激活可以通过传递一个Intent 对象至<font color="#ff0000">Context.startService()或Context.bindService()</font>前者Android 调用服务的onStart()方法并将Intent 对象传递给它，后者Android 调用服务的onBind()方法将这个Intent 对象传递给它
发送广播可以通过传递一个Intent 对象至给<font color="#ff0000">Context.sendBroadcast() 、Context.sendOrderedBroadcast()或Context.sendStickyBroadcast()。</font>Android 会调用所有对此广播有兴趣的广播接收器的onReceive()方法，将intent 传递给它们</font></p>

<font color="#ff0000" size="4" face="微软雅黑 Light">四大组件销毁时，</font>

<font color="#000000"><font size="4"><font face="微软雅黑 Light"><font color="#ff0000">**ContentProvider**</font>通过别的应用程序调用，消息处理完毕即销毁（如调用图片viewer看图，调用支付接口付款）。<font color="#ff0000">**BroadCastReceiver**</font>则注册在系统中监听，这两者都无需主动人为关闭，可以直接在权限中限制。其中BroadCastReceiver的生命周期只有十秒，否则就会报ANR(Application No Response)程序无响应的消息。
**<font color="#ff0000">Activity</font>**则通过finish()函数退出。一般情况下，按下返回退出键，或在多任务窗口杀掉都能直接关闭显式的Activity。有时直接按下Home键则会在后台缓存（Process），当切换过多个应用后，切回来时还能完整的保留原先打开时候的数据和窗口。当然，这样的过程会占用内存空间（RAM），同时也消耗一定的电量（比较少）。当后台运行过多缓存时，部分低内存手机会出现明显的卡顿。Android5.0之后的系统做的不错，能够按照优先级杀掉缓存应用。
**<font color="#ff0000">Service</font>**是个比较头疼的东西。尽管App可以调用<font color="#ff0000">Context.stopService()</font>方法关闭服务，或使用<font color="#ff0000">bindService()</font>绑定调用的组件关闭，但，流氓才不会这么做。
通常，手机应用中都看到正在运行的x个进程和y个服务。进程由多个线程组成，其中，主线程主要负责全局的参数传递，一些核心启动器及主界面的显示。而一些时间较长的函数，如获取多个图片，获取大量的数据，可以写在一个子线程，对主界面交互可以进行异步刷新，否则会造成主界面的卡顿。而当程序退居后台后，子线程依然处理数据，但没有了Activity进行联系，因此可以通过Service进行管理。由于Service并不负责应用层面的复杂操作，只对数据进行处理传递，同时可以写进单独的进程中，因而更为便利。</font></font></font>

<font color="#000000" size="4" face="微软雅黑 Light">这里总结一下Service能被启动&amp;被守护的各种方式。</font>

<font color="#000000" size="4" face="微软雅黑 Light">1.打开应用后，直接显而易见的调用它想要完成的Service，此时按照一般的逻辑，理应是退出App关闭Activity后就会stopservice.</font>

<font color="#000000" size="4" face="微软雅黑 Light">2.注册一个广播，可以按时钟、按网络变化、屏幕变化等，每次触发这些广播，就会检查一次Service的状况。遇到杀掉就重启。此时应当关注app的权限及其注册的广播。</font>

<font color="#000000" size="4" face="微软雅黑 Light">3.重写Service里的函数，在被杀时自动重启；配置到单独的进程中；配置安卓persistent=true；设置前台foreground=true.这些情况，在root情况下很容易被进程管理的杀掉</font>

<font size="4"><font face="微软雅黑 Light"><font color="#000000">4.双Service或多Service守护，在AndroidManifest.xml里面定义Service时加入android:process=":service1"</font>
</font></font>

<pre class="brush: xml; gutter: true; first-line: 1; highlight: []; html-script: false">&lt;service android:enabled="true" 
android:name="com.service.demo.Service1" 
android:process=":service1"&gt;
&lt;service&gt;
&lt;service android:enabled="true" 
android:name="com.service.demo.Service2" 
android:process=":service2"&gt;
&lt;service&gt;  
</pre>

&lt;

p align="left"><span><span><font color="#000000" size="4" face="微软雅黑 Light">关键的Point是触发了service的onTrimMemory()函数。又分别重新启动。</font></span></span>

<span><span><font size="4"><font face="微软雅黑 Light"><font color="#000000"></font></font></font></span></span>&nbsp;

<span><span><font size="4"><font face="微软雅黑 Light"><font color="#000000">5.Wakelock。Android机制下有一个唤醒锁，可以唤醒休眠中的手机。</font><font color="#000000">WakeLock阻止应用处理器（Application <wbr>Processor）挂起</font><font color="#000000">，确保关键代码的运行，通过中断唤起应用处理器（Application <wbr>Processor），可以阻止屏幕变暗。一旦有有效的wakelock，系统就不能进入深度睡眠（Deep Sleep）。一般在熄屏传输文件、下歌中使用。被滥用后，后果不堪设想。</font></font></font></span></span>

<span><span><font color="#000000" size="4" face="微软雅黑 Light">AlarmManage有一个AlarmManagerService,该服务程序主要维护app注册下来的各类Alarm,并且一直监听 Alarm设备，一旦有Alarm触发，或者是Alarm事件发生，AlarmManagerService就会遍历Alarm列表，找到相应的注册 Alarm并发出广播。Alarm <wbr>Manager会维持一个cpu的wake <wbr>lock。这样能保证电话休眠时，也能处理alarm的广播。一旦alarm <wbr>receiver的onReceive() <wbr>方法执行完，wake <wbr>lock会迅速被释放。如果在receiver中开启一个service，有可能service还没启动，wake <wbr>lock已经被释放了。所以此时要实现单独的wake <wbr>lock策略。</font></span></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">这也是一般不root不能根治的唤醒service的手段。App通过反复注册系统应用，调用级别高的Wakelock使得手机很难进入低频率的待机状态。</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">6.注册成为系统app同时包名混乱的编写。隐藏需要调用的service。一般没root的做不到。</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">所以，杀进程很容易，杀会自启的service也不难，难的是杀各种唤醒。</font></span>

<font size="4" face="微软雅黑 Light"></font>

<font size="4" face="微软雅黑 Light">

<div align="left">

* * *

</div>

</font>
<span><font color="#000000" size="4" face="微软雅黑 Light">这里提到两个重要概念：</font></span>

<span><font color="#000000"><font size="4"><font face="微软雅黑 Light"><font color="#ff0000">**Wakelock**</font>。唤醒锁；<font color="#ff0000">**Alarm**</font>。定时器</font></font></font></span>

<span><font size="4"><font face="微软雅黑 Light"><font color="#000000">**Wakelock**</font><font color="#000000">定义了一个接口，能让App有权限，在停止交互、黑屏状况下</font><font color="#ff0000">阻止手机休眠</font><font color="#000000">，运行关键而必要的一些代码，通常是账户同步、消息推送。<span>Android手机有两个处理器，一个叫Application Processor（AP），一个叫Baseband Processor（BP）。AP是ARM架构的处理器，用于运行Linux+Android系统；BP用于运行实时操作系统（RTOS），通讯协议栈运行于BP的RTOS之上。非通话时间，BP的能耗基本上在5mA左右，而AP只要处于非休眠状态，能耗至少在50mA以上，执行图形运算时会更高 。此外耗电大户wifi在100mA左右，LCD灯也在100mA左右。而进入休眠的手机大部分代码会停止运行。但，并不是很容易进入深度休眠的状态。</span></font></font></font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light"><span>wakelock针对的是<font color="#ff0000">某个Activity，而不是整个app</font>。因此，获取和释放wakelock在单个Activity中进行。</span></font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light"><span>对于唤醒锁，官方文档中的解释是：</span></font></span>

[<font color="#000000" size="4" face="华文中宋">PowerManager</font>](http://developer.android.com/reference/android/os/PowerManager.html#goToSleep(long))<font color="#000000" size="4" face="华文中宋">:This class gives you control of the power state of the device.</font>

[<font color="#000000" size="4" face="华文中宋">PowerManager.WakeLock</font>](http://developer.android.com/reference/android/os/PowerManager.WakeLock.html)<font color="#000000" size="4" face="华文中宋">: lets you say that you need to have the device on.</font>

<font color="#ff0000" size="4" face="微软雅黑 Light">只要系统中存在任一有效的wake_lock，系统就不能进入深度休眠，但可以进行设备的浅度休眠操作。</font>

<font size="4"><font face="微软雅黑 Light"><font color="#000000">Android定义了几种低功耗状态，</font>：**<font color="#ff0000">earlysuspend、suspend、hibernation.</font>**</font></font>

<font size="4"><font face="微软雅黑 Light">1) <font color="#ff0000">**earlysuspend**</font><font color="#000000">（浅度休眠），</font><font color="#000000">也有称standby</font></font></font><font size="4"><font face="微软雅黑 Light"><font color="#000000">: 是一种低功耗的状态,某些设备可以选择进入某种功耗较低的状态,比如 LCD可以降低亮度或灭掉;它不会受到wakelock阻止。例如接收黑屏手势。
</font>2) <font color="#ff0000">**suspend**</font><font color="#000000">（休眠），也有称sleep（bad nomenclature）: 是指除电源管理以外的其他外围模块以及cpu均不工作,只有内存保持自刷新的状态; 一般休眠到RAM</font></font></font>

<font size="4"><font face="微软雅黑 Light">3) <font color="#ff0000">**hibernation**</font><font color="#000000">（冬眠）是指所有内存镜像都被写入磁盘（disk）中,然后系统关机,恢复后系统将能恢复到“关机”之前的状态。是最彻底的低功耗模式，它把所有内存镜像都写入磁盘中，然后系统关机，是Linux内核系统级的休眠。</font></font></font>

<font color="#000000" size="4" face="微软雅黑 Light">

PowerManager.WakeLock有加锁与解锁两种状态，而加锁的形式有两种:

①永久锁住，这种锁除非显式的放开，否则是不会解锁的，所以用起来需要非常小心！

②超时锁，到时间后就会解锁，而创建WakeLock后，有两种加锁机制: ①不计数锁机制，②计数锁机制(默认)可通过setReferenceCounted(boolean value)来指定,区别在于: 前者无论acquire( )多少次，一次release( )就可以解开锁。 而后者则需要(--count == 0)的时候，同样当(count == 0)才会去申请锁 所以，WakeLock的计数机制并不是正真意义上对每次请求进行申请/释放一个锁; 只是对同一把锁被申请/释放的次数来进行统计，然后再去操作！</font><font face="微软雅黑 Light"><font color="#000000"><font size="4">该操作可通过setReferenceCounted(boolean value)设置。</font></font></font>

<font color="#000000" face="微软雅黑 Light">当然，需要用到权限<pre>&lt;uses-permission android:name="android.permission.WAKE_LOCK"/&gt;</pre><pre>&lt;uses-permission android:name="android.permission.DEVICE_POWER"/&gt;</pre></font>

<font color="#000000" size="4" face="微软雅黑 Light">锁有两种类型：</font>

<font size="4"><font face="微软雅黑 Light"><font color="#000000">WAKE_LOCK_SUSPEND：这种锁会防止系统进入睡眠(suspend)。 
WAKE_LOCK_IDLE：这种锁不会影响系统的休眠，用于阻止系统在持有锁的过程中进入低功耗状态。即直到wake_lock被释放，系统才会从idle状态进入低功耗状态，此低功耗状态将使中断延迟或禁用一组中断</font> </font></font>

<font color="#000000" size="4" face="微软雅黑 Light">有3个地方让<font color="#ff0000">系统直接开始挂起</font>suspend()， 分别是:</font>

<font color="#000000" size="4" face="微软雅黑 Light">&nbsp;&nbsp;&nbsp; • 在wake_unlock()中， 如果发现解锁以后没有任何其他的wake lock了，就开始休眠
&nbsp;&nbsp;&nbsp; • 在定时器都到时间以后，定时器的回调函数会查看是否有其他的wake lock，如果没有，就在这里让系统进入睡眠。
&nbsp;&nbsp;&nbsp; • 在wake_lock() 中，对一个wake lock加锁以后，会再次检查一下有没有锁， 这里的检查是没有必要的， 更好的方法是使加锁的这个操作原子化，而不是繁冗的检查，而且这样的检查也有可能漏掉。</font>

<font color="#000000" size="4" face="微软雅黑 Light">如下是一些常见的调用wakelock的操作

</font>

<table width="80%" border="0">
<tbody>
<tr>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">应用</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">操作</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">唤醒锁的服务</font>
</td>
<td width="20%" align="center"><font color="#000000" size="4" face="微软雅黑 Light">运行状态</font></td></tr>
<tr>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">任意</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">按下UI中的button或listview</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">PowerManagerService</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">启用并在5秒后释放锁定</font>
</td></tr>
<tr>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">地图/导航</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">启用地图或进入导航</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">gps-lock</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">锁定并使用GPS直到退出应用或手动设置取消GPS</font>
</td></tr>
<tr>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">视频软件</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">观看视频流</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">PowerManagerService</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">视频播放过程中一直启用唤醒锁</font>
</td></tr>
<tr>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">音乐软件</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">听歌</font>
</td>
<td width="20%">

<font color="#000000" size="4" face="微软雅黑 Light">PowerManagerService</font>
</td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">音乐播放过程中一直启用唤醒锁</font></td></tr></tbody></table>

<font color="#000000" size="4" face="微软雅黑 Light">Video和 Music 应用能够很好地展示不同级别的唤醒锁。 用户播放视频时，Video应用将会启用唤醒锁。 在播放视频的整个过程中，显示器会保持开启状态（忽略系统的显示设置）。 但是，如果用户在播放过程中按下了电源按钮，设备将会挂起，这会导致显示器关闭以及音频/视频停止播放。 Music 应用在播放音频时使用不同的唤醒锁。 显示设置无法更改，因此设备的屏幕将会根据用户的显示设置来关闭。 显示器关闭后，唤醒锁会让 CPU 保持活动状态以便音频能够继续播放 — 即使用户按下了电源按钮。</font>

<font color="#000000" size="4" face="微软雅黑 Light">上图可见，<font color="#ff0000">PowerManagerService</font>是一项使用率非常高的wakelock调用的操作，它是Android上层电源管理服务，属于<font color="#ff0000">内核唤醒锁,适用于所有局部唤醒锁（partial wakelock 后文提到）的容器</font>。主要负责系统待机、屏幕背光、按键背光、键盘背光以及用户事件的处理。这些可在后文的wakelock detector软件中看到。通过锁的申请和释放以及默认待机时间来控制系统的待机状态，通过系统的灭屏时间及用户操作的事件状态来控制背光暗亮。此外该服务还包括了光线、距离传感器上层查询与控制、LCD灯控制。</font>

<font color="#000000" face="微软雅黑 Light">其他的内核唤醒锁有：</font>

<font color="#000000">Wlan_rx： 当通过 Wi-Fi* 发送或接收数据时由内核控制。</font>

<font color="#000000">Sync： 在同步流程运行时启用。</font>

<font color="#000000">Alarm_rtc： 控制告警（当应用或流程执行定期检查时使用）。</font>

<font color="#000000">Main： 保持内核处于唤醒状态。 系统进入挂起模式时，这是最后一个被释放的唤醒锁。</font>

<font color="#000000" size="4" face="微软雅黑 Light">自最初版本的Android OS 的API中就设置了Android.OS.PowerManager.WakeLock类 </font>[<font color="#000000" size="4" face="微软雅黑 Light">https://developer.xamarin.com/api/type/Android.OS.PowerManager+WakeLock/</font>](https://developer.xamarin.com/api/type/Android.OS.PowerManager+WakeLock/)

<font color="#000000" size="4" face="微软雅黑 Light">一下为Java代码应用层的操作。</font>&nbsp;

<pre class="brush: java; gutter: true; first-line: 1; highlight: []; html-script: false">PowerManager pm = (PowerManager) getSystemService(Context.POWER_SERVICE);//创建pm对象
PowerManager.WakeLock wl = pm.newWakeLock(PowerManager.SCREEN_DIM_WAKE_LOCK, "Tag");
//第一个参数为flag,即后文提到的六个标记；最后一个参数为实例名，可以换成其他的
wl.acquire(); //唤醒点亮屏幕 获取wakelock
wl.release(); //恢复屏幕到黑暗 释放wakelock</pre>

&nbsp;

<font color="#000000" size="4" face="微软雅黑 Light">2.1 API Level7开始增加了一个判断屏幕是否处于点亮状态可以使用public boolean isScreenOn ()这个方法，代码为</font>

<pre class="brush: java; gutter: true; first-line: 1; highlight: []; html-script: false">PowerManager pm = (PowerManager) getSystemService(Context.POWER_SERVICE);
boolean isScreenOn = pm.isScreenOn();
</pre>

<font color="#000000" size="4" face="微软雅黑 Light">对它进行实例化。</font>

<font size="4"><font face="微软雅黑 Light"><font color="#000000">Wakelock源码简介</font>&nbsp; </font></font>[<font size="4" face="微软雅黑 Light">http://www.07net01.com/2015/07/870479.html</font>](http://www.07net01.com/2015/07/870479.html)

<font color="#000000" size="4" face="微软雅黑 Light">PowerManager和Wakelock申请 http://blog.csdn.net/wh_19910525/article/details/8287202</font>
<p align="left"><span><font color="#000000" size="4" face="微软雅黑 Light">Android PowerManager API 介绍了4种用于更改设备电源状态的<font color="#ff0000">唤醒锁标记</font>：

</font></span>
<table width="80%" border="0">
<tbody>
<tr>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">标记值</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">CPU/场景</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">屏幕</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">键盘</font></td></tr>
<tr>
<td width="20%"><font color="#ff0000" size="4" face="微软雅黑 Light">PARTIAL_WAKE_LOCK</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">开启-长时间运行的后台service</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">关闭</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">关闭</font></td></tr>
<tr>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">SCREEN_DIM_WAKE_LOCK</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">开启-除非必须保持CPU运行至运算完成，否则尽量使用FLAG_KEEP_SCREEN_ON</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">低亮度</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">关闭</font></td></tr>
<tr>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">SCREEN_BRIGHT_WAKE_LOCK</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">同上</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">高亮度</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">关闭</font></td></tr>
<tr>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">FULL_WAKE_LOCK</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">同上</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">高亮度</font></td>
<td width="20%"><font color="#000000" size="4" face="微软雅黑 Light">调亮</font></td></tr></tbody></table>
<font color="#000000" size="4" face="微软雅黑 Light">需要注意的是 API17开始，FULL_WAKE_LOCK将被弃用，取而代之的是FLAG_KEEP_SCREEN_ON 因此有的检测软件也将屏幕亮屏所单独提出来，表明调用该锁时目的是保证屏幕不会超时熄灭。</font>

<font color="#000000" size="4" face="微软雅黑 Light">除了四个标记值外，还提供了两个Flag配合使用。</font>

<font color="#000000" size="4" face="微软雅黑 Light">ACQUIRE_CAUSES_WAKEUP：默认情况下唤醒锁并不是马上开启CPU、屏幕或者调整键盘的亮度（对于屏幕处于低亮度或高亮度、键盘处于高亮，唤醒锁只是在被开启后，延续这一状态）但如果加上这一标记，就可让屏幕或键盘亮度未开启的状态下，马上开启它们。典型的例子就是受到一个重要的notification时（短信、邮件等），需要马上点亮屏幕。</font>

<font color="#000000" size="4" face="微软雅黑 Light">ON_AFTER_RELEASE：当wake lock被释放的时候，当前调用wake lock的activity的计数器会被重置，所以屏幕会继续亮一段时间。</font>

<font size="4"><font face="微软雅黑 Light"><font color="#000000">因此，Android中通常是这么写。</font>
</font></font>
<div align="center"><pre class="brush: java; gutter: true; first-line: 1; highlight: []; html-script: false">PowerManager pm = (PowerManager) context.getSystemService(Context.POWER_SERVICE);

 WakeLock sCpuWakeLock = pm.newWakeLock( 
                PowerManager.FULL_WAKE_LOCK | 
                PowerManager.ACQUIRE_CAUSES_WAKEUP,"okTag"); 
 if (sCpuWakeLock!= null) {          
 sCpuWakeLock.release(); 
          sCpuWakeLock = null; 

}
</pre></div>

<font color="#000000" size="4" face="微软雅黑 Light"></font>&nbsp;

**<font color="#ff0000">注意</font>**：如果申请了<font color="#ff0000">partial wakelock</font>,那么即使按Power键,系统也不会进Sleep,如Music播放时。所有的锁必须成对的使用, 如果申请了而没有及时释放，会造成系统故障。如申请了partial wakelock,而没有及时释放, 那系统就永远进不了Sleep模式.

因此，partial wakelock作为6中标识中，需最为谨慎使用的一个。BBS也专门指出了partial wakelock造成的电量损耗及待机时长。其余的则可标记为屏幕锁，辅助标记CPU锁。

<font color="#000000" face="微软雅黑 Light">![](http://ww4.sinaimg.cn/large/68eb7c93gw1eztpciku00j20de0bjjsd.jpg)</font>

<font size="4"><font color="#000000" face="微软雅黑 Light">**上图表明了App内部、Android框架及内核硬件在唤醒锁交互中的流程。**</font></font>

<font size="4"><font face="微软雅黑 Light"><font color="#ff0000">**AlarmManager**</font><font color="#000000">，有一个AlarmManagerService,该服务程序主要维护app注册下来的各类Alarm,并且一直监听Alarm设备，一旦有Alarm触发，或者是Alarm事件发生，AlarmManagerService就会遍历Alarm列表，找到相应的注册Alarm并发出广播，是Android中常用的一种<font color="#ff0000">系统级别的提示服务</font>，在特定的时刻为我们广播一个指定的Intent。通常我们使用 PendingIntent，可以理解为Intent的封装包，在Intent上在加个指定的动作。在使用Intent的时候，我们还需要在执行startActivity、startService或sendBroadcast才能使Intent有用。而PendingIntent的话就是将这个动作包含在内了。</font></font></font>

<font color="#000000" size="4" face="微软雅黑 Light">闹钟响起，实际上是系统发出了为这个<font color="#ff0000">闹钟注册的广播</font>，会自动开启目标应用。这种做法可以在某一时刻当做唤醒应用。注册的闹钟在设备睡眠的时候仍然会保留，可以选择性地设置是否唤醒设备，但是当设备关机和重启后，闹钟将会被清除。在alarm的receiver的onReceive()方法被执行的时候，Alarm Manager持有一个CPU唤醒锁，这样就保证了设备在处理完广播之前不会sleep。</font>

<span><font color="#000000"><font size="4"><font face="微软雅黑 Light">有4种Alarm类型： <wbr></font></font></font></span></p>

<font color="#000000"><font size="4" face="微软雅黑 Light">1)</font><font size="4"><font face="微软雅黑 Light"><font color="#ff0000">RTC_WAKEUP <wbr>
</font>在指定的时刻（设置Alarm的时候），唤醒设备来触发Intent。（闹钟）</font></font></font><font size="4" face="微软雅黑 Light"> </font>

<span></span><span><font color="#000000"><font size="4" face="微软雅黑 Light">2)<font color="#ff0000">RTC</font> <wbr>
在一个显式的时间触发Intent，但不唤醒设备。<wbr><wbr><wbr>
3)</font><font size="4"><font face="微软雅黑 Light"><font color="#ff0000">ELAPSED_REALTIME <wbr>
</font>从设备启动后，如果流逝的时间达到总时间，那么触发Intent，但不唤醒设备。流逝的时间包括设备睡眠的任何时间。注意一点的是，时间流逝的计算点是自从它最后一次启动算起。 <wbr>&nbsp;<wbr>&nbsp;<wbr>
4)<font color="#ff0000">ELAPSED_REALTIME_WAKEUP</font> <wbr>
从设备启动后，达到流逝的总时间后，如果需要将唤醒设备并触发Intent。</font></font></font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">这样，唤醒对齐的方案就显得相当便捷，让唤醒次数大大降低。把允许唤醒的应用，按照某一合理的时刻进行排序和对齐，不会凌乱的唤醒手机而出现过度的cpu变频造成的耗电。</font></span>

<span><font color="#000000"><font size="4"><font face="微软雅黑 Light"><font color="#ff0000">软节电</font>方案：</font></font></font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">1、对不需要联网、不需要通知的 限制权限&amp;App自调 取消通知、联网等权限 杀注册广播</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">2、限制通知和自启动、互相启动、相互守护的service 禁启动</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">3、（千万少做）安全软件狂杀进程process和service</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">4、限制唤醒时长和对齐唤醒</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">5、对可识别的Activity禁止</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">6、对不需要通知、自升级、关闭软件啥也不想让他做的 结晶 禁止、半禁止一切后台</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">7、争取多冬眠service</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">8、在合理的时间重启并FQ</font></span>

<span><font color="#000000" size="4" face="微软雅黑 Light">So 开搞</font></span>

<span><font color="#000000" face="微软雅黑 Light"></font></span>参考

<span>[http://www.runoob.com/w3cnote/android-tutorial-powermanager.html](http://www.runoob.com/w3cnote/android-tutorial-powermanager.html)&nbsp; PowerManager(电源服务)</span>

[http://www.kancloud.cn/kancloud/android-tutorial/87277](http://www.kancloud.cn/kancloud/android-tutorial/87277 "http://www.kancloud.cn/kancloud/android-tutorial/87277") 这俩好像一样、

[http://forum.xda-developers.com/galaxy-s2/general/guide-complete-guide-maximum-battery-t1909996](http://forum.xda-developers.com/galaxy-s2/general/guide-complete-guide-maximum-battery-t1909996 "http://forum.xda-developers.com/galaxy-s2/general/guide-complete-guide-maximum-battery-t1909996") 真的是能关的全给关了的大全

<font size="4" face="微软雅黑 Light"></font>

<font size="4" face="微软雅黑 Light"></font>

<font size="4" face="微软雅黑 Light"></font>

[http://lockekk.github.io/jekyll-bootstrap/2014/07/22/Android-Standby/](http://lockekk.github.io/jekyll-bootstrap/2014/07/22/Android-Standby/ "http://lockekk.github.io/jekyll-bootstrap/2014/07/22/Android-Standby/") Android Standby 解析查杀软件的弊病