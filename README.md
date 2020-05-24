# Windows平台下使用 Rclone 挂载 OneDrive 为本地硬盘

**1、rclone下载地址**

官网下载：https://rclone.org/downloads/

下载后解压到一个英文路径中。

另外在Windows平台使用rclone还需要另一个依赖工具winfsp，下载地址：http://www.secfs.net/winfsp/download/ ，下载后一路安装即可。

**2、为rclone配置环境变量**

2.1  在电脑桌面右键点击“此电脑”的“属性”选项

2.2  选择“高级系统设置”选项

2.3  在系统变量中找到path，添加刚才解压后的路径

![markdown](https://gitee.com/wang_wx/image_bed/raw/master/202002/image-20200210093901149.png "markdown")

**3、检查rclone是否配置成功**

按```win+X```，然后按```A ```打开``` powershell``` ，当然也可以去打开 ```cmd``` ，输入```rclone --version```，如果出现下面的输出则安装成功，否则检查上面步骤的环境变量是否配置正确。

![markdown](https://gitee.com/wang_wx/image_bed/raw/master/202002/20200210102009.png "markdown")

**4、开始配置rclone**

在终端中依次输入以下命令行，请根据我下的步骤进操作。

```
D:\AutoRclone>rclone config                    // 第一步在终端输入 rclone config 
Current remotes:
​
Name                 Type
====                 ====
OneDrive             onedrive
​
e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> n                          //第二步输入n创建新的配置，                                                                  
​
name> OneDrive_local                      //第三步 输入一个英文名称 ，中间也不要有空格
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / 1Fichier
 \ "fichier"
 2 / Alias for an existing remote
 \ "alias"
 3 / Amazon Drive
 \ "amazon cloud drive"
 4 / Amazon S3 Compliant Storage Provider (AWS, Alibaba, Ceph, Digital Ocean, Dreamhost, IBM COS, Minio, etc)
 \ "s3"
 5 / Backblaze B2
 \ "b2"
 6 / Box
 \ "box"
 7 / Cache a remote
 \ "cache"
 8 / Citrix Sharefile
 \ "sharefile"
 9 / Dropbox
 \ "dropbox"
10 / Encrypt/Decrypt a remote
 \ "crypt"
11 / FTP Connection
 \ "ftp"
12 / Google Cloud Storage (this is not Google Drive)
 \ "google cloud storage"
13 / Google Drive
 \ "drive"
14 / Google Photos
 \ "google photos"
15 / Hubic
 \ "hubic"
16 / In memory object storage system.
 \ "memory"
17 / JottaCloud
 \ "jottacloud"
18 / Koofr
 \ "koofr"
19 / Local Disk
 \ "local"
20 / Mail.ru Cloud
 \ "mailru"
21 / Mega
 \ "mega"
22 / Microsoft Azure Blob Storage
 \ "azureblob"
23 / Microsoft OneDrive
 \ "onedrive"
24 / OpenDrive
 \ "opendrive"
25 / Openstack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
 \ "swift"
26 / Pcloud
 \ "pcloud"
27 / Put.io
 \ "putio"
28 / QingCloud Object Storage
 \ "qingstor"
29 / SSH/SFTP Connection
 \ "sftp"
30 / Sugarsync
 \ "sugarsync"
31 / Transparently chunk/split large files
 \ "chunker"
32 / Union merges the contents of several remotes
 \ "union"
33 / Webdav
 \ "webdav"
34 / Yandex Disk
 \ "yandex"
35 / http Connection
 \ "http"
36 / premiumize.me
 \ "premiumizeme"
 Storage> 23                             //第四步 输入要配置的网盘类型 因为我们要配置Microsoft OneDrive 因此输入23
** See help for onedrive backend at: https://rclone.org/onedrive/ **
​
Microsoft App Client Id
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_id>                              //第五步 直接回车
Microsoft App Client Secret                                  
Leave blank normally.                                        
Enter a string value. Press Enter for the default ("").      
client_secret>                           //第六步 直接回车                    
Edit advanced config? (y/n)                                  
y) Yes 
n) No (default)                                              
y/n> n                                  //第七步 输入n 不进行高级配置 
Remote config                                                
Use auto config? 
 * Say Y if not sure 
 * Say N if you are working on a remote or headless machine
y) Yes (default) 
n) No                                                        
y/n> y                                  //第八步 输入y 使用自动配置授权
​
//输入y后会打开默认浏览器 登录Microsoft账号后 选择 是 即可
 If your browser doesn't open automatically go to the following link: http://127.0.0.1:53682/auth?state=sUuYaGWtxruA81JiCokJGg
Log in and authorize rclone for access
Waiting for code...
Got code
Choose a number from below, or type in an existing value
 1 / OneDrive Personal or Business
 \ "onedrive"
 2 / Root Sharepoint site
 \ "sharepoint"
 3 / Type in driveID
 \ "driveid"
 4 / Type in SiteID
 \ "siteid"
 5 / Search a Sharepoint site
 \ "search"
Your choice>1                            //第九步 输入1 因为现在我配置的是 OneDrive Personal or Business 类型的网盘
​
Found 1 drives, please select the one you want to use:
0: OneDrive (business) id=b!qDQvcsZUTU-8eoYyKmtyyP1Jc0D8urZLlkATnfH1nWdJ1kkbrLsvQZLzVUTpeTrc
Chose drive to use:> 0              //第十步 输入0
Found drive 'root' of type 'business', URL: https://pmjs-my.sharepoint.com/personal/wld_365_w/Documents
Is that okay?
y) Yes (default)
n) No
y/n> y                               //第十一步 输入y
--------------------
[OneDrive_local]
type = onedrive
token = {"access_token":"eyJ0eXAiOiV1QiLCJub25jZSI6ImNRYjl5TDNZWE8yczdQd2N2WTlJRkV1ZXp0QVpZZV83QWpPaHZORTU0OTgiLCJhbGciOiJSUzI1NiIsIng1dCI6IkhsQzBSMTJza3hOWjFXUXdtak9GXzZ0X3RERSIsImtpZCI6IkhsQzBSMTJza3hOWjFXUXdtak9GXzZ0X3RERSJ9yJhdWQiOiIwMDAwMDAwMy0wMDAwLTAwMDAtYzAwMC0wMDAwMDAwMDAwMDAiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC84N2VjYmIxYi0wZTdlLTRlMDctOWFiMC00NWIwOTM1OTFjN2EvIiwiaWF0IjoxNTgxMzAxNLCJuYmYiOjE1ODEzMDE2MzAsImV4cCI6MTU4MTMwNTUzMCwiYWNjdCI6MCwiYWNyIjoiMSIsImFpbyI6IkFTUUyLzhPQUFBQWc2eURUazJNKzZ5YjVLNEJSN2VUR0lHT3EvSXFPT0dSZzlPWitrREoyaTg9IiwiYW1yIjpbInB3ZCJdLCJhcHBfZGlzcGxheW5hbWUiOiJyY2xvbmUiLCJhcHBpZCI6ImIxNTY2NWQ5LWVkYTYtNDA5Mi04NTM5LTBlZWMzNzZhZmQ1OSIsImFwcGlkYWNyIjoiMSIsImZhbWlseV9uYW1lIjoiV2FuZyIsImdpdmVuX25hbWUiOiJYaWFud2iwiaXBhZGRyIjoiMzkuMTI4LjIwMC4iwibmFtZSI6IldhbmdYaWFud2VuIiwib2lkIjoiZWE4ZjNjZDctN2IxYS00YmQ0LWFiNzItYzM4NDg4NTE5NDdhdGYiOiIzIiwicHVpZCI6IjEwMDMzRkZGQUVGNEE2RTUiLCJzY3A5YWIwLTQ1YjA5MzU5MWM3YSIsInVuaXF1ZV9uYW1lIjoid29ybGRAbXkzNjUudHciLCJ1cG4iOiJ3b3JsZEBteTM2NS50dyIsInV0aSI6Il85MEZWRXBZcTBTYzckFuVDluQUEiLCJ2ZXIiOiIxLjAiLCJ4bXNfc3QiOnsic3ViIjoidXlWWU96UGF5RVBVWXlSbFlEVEl6QjhUZVBkZnNTMkVHcHczNGNDM2JRTSJ9LCJ4bXNfdGNkdCI6MTUzNDQyOTU0NH0.Ki9vor6NtxXJWsdumYddz8agrzVYXRCXVg0paW7XqDTq8i_vht8GK79F0F7xp3BSKzK5Xgxb0GzwPV9dPTb4IiXM0d17P5pQB3wHLMUbVFvRbLXNwSEtSJGKLttvxL8XfT8e51k4kyyH07CtozVBsF6fmMnhftp9ZbcEVrgnFKdwTE5In83G05V7L8wDCMiKrN0KX9iTKzxT9em5QtVhGZRZJDnNS2pJTQNhiWVatjDB4VHojG2C6J1LtU6YOOOAM2uBil2ovLFhQPy0l299ZJTJeyQCLQGJki9kZgAVI42iGP4mzvVPQAJk5Oad_4nPsT87QVH4NBA","token_type":"Bearer","refresh_token":"OAQABAAAAAABeAFzDwllzTYGDLh_qYbH8falkpBpCm5PZqagAkUNWFik3Mz2ZfDPeowwW9q5mlFoHSqyYNG8FayvZxxZEUGQWUaR520MuJ5i_mj9CNs0NahNOJAtvZOBV459VLMKaNiyK9GJIGvdDe4RkaV472hbq_po8K47yC053BLRIbRji9WfsCkSMj8UP792sNJ0Tm9ptfPmy1aP_TePX8dOWaC9qZN2jDIXJDjWjCvfDesNDWXAm9bpBp1oZmObLR85EKB9Vgsz7ccZIbKEa16Aiqb67xsQICG8AzjMli76nJVFx1SB3rRc2rxSDcnVTx_Oja_6KuaUxQjhgi1XaH1Kk_c82iniwdj7EdHCbokk8eewYFyn4tBTL0xW8rwmoPDvvUvMVA7Z8Ph0AB66Ih5evroSEHsv072AyDWSwHfrEMueTeEgP5jA1aBSOXE2DDw3PySehFfbYpsh0AV3qPVP9lAHaGizEbFt9rEKl1R1bcMrEhxF9GjnvB5PChRK_abttEV2YWKWrTaEFJBTP40f96kCXZGMaE4RaUoMI7hKW4cLQrHuV5YCZQ_BQRj7r5PoUyelGPdvnW42lB8MvekksdrJAVnlUTTgVKlbpn9AUuOD2LUZ5A8IheWaLkhLXfUqjPg0UxjTLIAA","expiry":"2020-02-10T11:32:10.852646+08:00"}
drive_id = b!qDvcsZUTU8eoYyKmtyyP1Jc0D8urZLlkTnH1nWdJ1kbrLsvQZLzVUTpeTrc
drive_type = business
--------------------
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d>y                                      //第十二步 输入y
```

此时，就会出现刚刚配置好的网盘名称了

![markdown](https://gitee.com/wang_wx/image_bed/raw/master/202002/image-20200210104149803.png "markdown")

**5、挂载OneDrive为本地硬盘**

此时请使用``` git bash``` 的终端执行以下命令，因为我使用```cmd``` 和 ```powershell``` 都出现关闭终端后挂载程序退出、本地挂载的OneDrive退出的现象。 如果你的windows没有安装git ， 请[自行安装](https://www.baidu.com/s?wd=windows%20%E5%AE%89%E8%A3%85git&ie=utf-8)。。若你使用 ```cmd ```的话 ，```cmd ```是不能退出的，要保持``` cmd``` 不退出本地硬盘才一直挂载着。

在 git bash 中输入以下挂载命令：

```rclone mount OneDrive_local:/  Q: --cache-dir E:\OneDrive --vfs-cache-mode writes &```

其中：

```OneDrive_loca``` 替换为你自己前面设置的名称 。

```Q: ```替换为你想要挂载后硬盘的盘符名称即可，记得不要和本地的C盘、D盘等重复。

```E:\OneDrive ```为本地缓存目录，可自行设置 。

出现：The service rclone has been started 则说明挂载成功。

然后输入 exit 退出终端即可。

![markdown](https://gitee.com/wang_wx/image_bed/raw/master/202002/20200210124133.png "markdown")

然后就可以看见本地多了一个盘，往里面复制文件就是上传，从里面复制文件到其它盘就是下载。

![markdown](https://gitee.com/wang_wx/image_bed/raw/master/202002/20200210124455.png "markdown")

**6、设置开机自启动挂载**

创建一个名称为 ```startup_rclone.bat``` 的文件，里面填写上面的挂载命令：

```rclone mount OneDrive_local:/  Q: --cache-dir E:\OneDrive --vfs-cache-mode writes &```

将这个文件放在```C:\Users\用户名\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup ```中

![markdown](https://gitee.com/wang_wx/image_bed/raw/master/202002/20200211114237.png "markdown")

重启计算机后就会自动挂设置的云盘了，当然这样做由于调用的是``` cmd``` 因此还是不能关闭运行的 ```cmd```。
