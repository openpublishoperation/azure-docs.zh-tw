1. 將安裝程式複製到您想要保護之伺服器上的本機資料夾 (例如 /tmp)，並從終端機視窗執行下列命令。
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. 我們現在可以使用下列命令列來安裝行動服務

  ```
  sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P MobSvc.passphrase
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a>行動服務安裝程式命令列引數

|參數|類型|說明|可能的值|
|-|-|-|-|
|-t |強制|代理程式類型<br>(將在下一版中淘汰)|*兩者*|
|-a |強制|代理程式組態<br>(將在下一版中淘汰) |*主機*|
|-R |選用|代理程式的角色|代理程式<br>MasterTarget|
|-d |選用|將要安裝行動服務的位置|/usr/local/ASR|
|-i |強制|組態伺服器的 IP 位址。|任何有效的 IP 位址|
|-p |強制|組態伺服器用於接聽連入連線的連接埠|443|
|-s |強制|在安裝成功後啟動服務<br>(將在下一版中淘汰)|*y*|
|-c |強制|代理程式與處理序伺服器之間的通訊模式<br>(將在下一版中淘汰) |*https*|
|-P |強制|組態伺服器複雜密碼|任何有效的 UNC 或本機檔案路徑|


#### <a name="sample-usage"></a>範例用法
```
sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i 192.168.2.53 -p 443 -s y -c https -P /tmp/MobSvc.passphrase
```


<!--HONumber=Jan17_HO3-->


