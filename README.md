<h3>Install Raspbian OS image</h3>
  - Download img file from offical web https://www.raspberrypi.org/downloads/<br>
  - follow instructure https://www.raspberrypi.org/documentation/installation/installing-images/README.md<br>
  
<h3>Setup VNC and SSH for remote connect</h3>
  <p>- VNC serve already installed in Raspbian, only do the </p>
  <p>- $sudo raspi-config (to enable vnc & ssh from interfave setup)</p>
 
<h3>Problem : HDMI no sound</h3>
  <p>- need edit /boot/config.txt add new line than reboot</p>
  <p>   hdmi_driver=2</p>
  <p>- if it didn't work, add another line</p>
  <p>   hdmi_force_edid_audio=1</p>


<p>Refence : http://han-ya.blogspot.com/2018/08/raspberry-pi-3b-1.html</p>

<h3>Install 中文注音輸入法</h3>
   <p>- sudo apt-get install scim-chewing</p>
   <p>- sudo apt-get install ttf-wqy-microhei ttf-wqy-zenhei xfonts-wqy</>
============================================================================
<h1> Install Home assistor (Hassio)</h1>
<h3> hassio homepage</h3>
    <p>- https://www.home-assistant.io</p>
    <p>- download image file form https://www.home-assistant.io/hassio/installation/</p>
    - write image file to microSD by <b><a href="https://www.balena.io/etcher/">BalenaEtcher</a></b>
    
<h3> setup WiFi</h3>
    <p>- insert image microSD card into windows PC, creat folder/file: CONFIG/network/my-network 
  in driver/disk "hassio-boot"</p>
    <p>- type following contents into my-network file</p>
    <br>
[connection]<br>
id=my-network<br>
uuid=72111c67-4a5d-4d5c-925e-f8ee26efb3c3<br>
type=802-11-wireless<br>
<br>
[802-11-wireless]<br>
mode=infrastructure<br>
ssid=MY_SSID<br>
# Uncomment below if your SSID is not broadcasted<br>
#hidden=true<br>
<br>
[802-11-wireless-security]<br>
auth-alg=open<br>
key-mgmt=wpa-psk<br>
psk=MY_WLAN_SECRET_KEY<br>
<br>
[ipv4]<br>
method=auto<br>
<br>
[ipv6]<br>
addr-gen-mode=stable-privacy<br>
method=auto<br>
<br>
<h3> Hassio in Raspberry Pi setup and addon install</h3>
    <p>- install addon in Hassio UI</p>
    <p>*** configurator, Samba share, SSH server, DuckDNS .....</p>
    <p>ps. SSH setup : "authorized_keys"=["ssh-ras ......"] need fill.</p>
    <p>電腦上打開 powershell(這裡以 windows10 為例)。ssh-keygen 這個指令目前已經內建在 windows 10 內，如果無法使用這個指令的話，也可以使用 Putty這個軟體建立 SSH 金鑰。</p>
    <p><b>ssh-keygen -t rsa -b 4096 -C "InnovationCS"</b></p>
    <p>產生完金鑰後，到 C:\Users\你的電腦名稱.ssh 下找到公鑰: id_rsa.pub，複製到 Home Assistant 的設定裡。</p>
    <p>把整串包含 "ssh-rsa IFJOSDFNSO.....==你的註解" 複製到 "authorized_keys": ["這裡"]，使用""包起來。</p>
    <p>reference :https://ithelp.ithome.com.tw/articles/10219700</p>
    <p>DuckDNS addon install https://ithelp.ithome.com.tw/articles/10220194</p>
         
