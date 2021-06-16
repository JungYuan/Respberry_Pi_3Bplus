<h3>Install Raspbian OS image</h3>
  - Download img file from offical web https://www.raspberrypi.org/downloads/<br>
  - follow instructure https://www.raspberrypi.org/documentation/installation/installing-images/README.md<br>
  
<h3>use SSH connect without monitor/keyboard</h3>
  <p>- new raspberry Pi OS installer to use ctrl-shift-x for config wifi and ssh.</p>
  <p>- create a file name 'ssh'(no contect) in boot folder </p>
  <p>- create a file name 'wpa_supplicant.conf'</p>
  <pre>
      country=US
      ctrl_interface=DIR=/var/run/wpa_supplicant 
      GROUP=netdev
      update_config=1
      network={
        scan_ssid=1
        ssid="your_wifi_ssid"
        psk="your_wifi_password"
      }
   </pre>
  <p>- use Putty to connect raspberrypi.local:22</p>
  <hr>
  <p>- setup multiple WiFi</p>
  <ol>
    <li>Edit /etc/wpa_supplicant/wpa_supplicant.conf and add id_str="school" under the schools wpa info and id_str="home" under your homes wpa info. 
        Your file    should now look similar to this:<li>
  <pre>
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1

        network={
            ssid="SCHOOLS NETWORK NAME"
            psk="SCHOOLS PASSWORD"
            id_str="school"
        }

        network={
            ssid="HOME NETWORK NAME"
            psk="HOME PASSWORD"
            id_str="home"
        }
   
    Then set up /etc/network/interfaces with iface school inet static and iface home inet static in it so it looks like the following:
        This applies to Raspbian Wheezy prior to 2015-05-05 for later (and Jessie) See How do I set up networking/WiFi/Static IP
    <pre>
      auto lo

      iface lo inet loopback
      iface eth0 inet dhcp

      allow-hotplug wlan0
      iface wlan0 inet manual
      wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf

      iface school inet static
      address <school address>
      gateway <school gateway>
      netmask <school netmask>

      iface home inet static
      address <home address>
      gateway <home gateway>
      netmask <home netmask>
    </pre>
</ol>
<h3>Setup VNC and SSH for remote connect</h3>
  <p>- VNC serve already installed in Raspbian, only do the </p>
  <p>- $sudo raspi-config (to enable vnc & ssh from interfave setup)</p>
  
<h3>Enable Serial console</h3>
  <p>- editing /boot/config.txt </p>
  <p>- add enable_uart=1 on it's own line</p>
 
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
<a href="https://www.uuidgenerator.net/">uuid</a>=72111c67-4a5d-4d5c-925e-f8ee26efb3c3<br>
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
    <p><br><b>issue 1. SSH setup</b> : "authorized_keys"=["ssh-ras ......"] need fill.</p>
    <p>電腦上打開 powershell(這裡以 windows10 為例)。ssh-keygen 這個指令目前已經內建在 windows 10 內，如果無法使用這個指令的話，也可以使用 Putty這個軟體建立 SSH 金鑰。</p>
    <p><b>ssh-keygen -t rsa -b 4096 -C "InnovationCS"</b></p>
    <p>產生完金鑰後，到 C:\Users\你的電腦名稱.ssh 下找到公鑰: id_rsa.pub，複製到 Home Assistant 的設定裡。</p>
    <p>把整串包含 "ssh-rsa IFJOSDFNSO.....==你的註解" 複製到 "authorized_keys": ["這裡"]，使用""包起來。</p>
    <p>reference :https://ithelp.ithome.com.tw/articles/10219700</p>
    <p>DuckDNS addon install https://ithelp.ithome.com.tw/articles/10220194</p>
    <p><br><b>issue 2. access Samba share</b></p>
        <p>windows10: need to enable "SMB 1.0/CIFS File Sharing Support "--> "SMB 1.0/CIFS client"</p>
        <p>cmd --> optionalfeatures</p>
        
<h3> Node-RED install in Rasbin</h3>
<ol>
  <li> <a href="https://nodered.org/docs/getting-started/raspberrypi">installation introduction in NodeRED.org</a></li>
  <li> setup authentication</li>
  <ul>
    <li>sudo npm install -g node-red-admin #generate password HASH code</li>
    <li>node-red-admin hash-pw. #copy generated code</li>
    <li>cd .node-red</li>
    <li>vi settings.js</li>
    <li>edit following datas to enable user authentication</li>
      <pre>
      adminAuth: {
          type: "credentials",
          users: [{
              username: "admin",
              password: "GENERATED HASH-PW CODE",
              permissions: "*"
          }]
      },
      </pre>
    <li>install node-red-dashboard</li>
    <li>install node-red-contrib-homebridge-automation</li>
    <li>install node-red-contrib-line-messaging-api</li>
    <li>using periodly update IP address to freeDDNS by HTTP get IP address then HTTP request update to DDNS.</li>
      <pre>
        [{"id":"a272b349.f03c68","type":"inject","z":"1935bfc0.28217","name":"update_ip2dynu","props":[{"p":"payload"},
        {"p":"topic","vt":"str"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":220,"y":1820,"wires":[["5a039c93.a82a2c"]]},
        {"id":"5a039c93.a82a2c","type":"http request","z":"1935bfc0.28217","name":"","method":"GET","ret":"txt","paytoqs":"body","url":"https://api.dynu.com/nic/update?hostname=zywu0111.freeddns.org&password=38cb54c850626765d5133892033290c1","tls":"","persist":false,"proxy":"","authType":"","x":470,"y":1820,"wires":[["b887d64.d68d328"]]},
        {"id":"b887d64.d68d328","type":"debug","z":"1935bfc0.28217","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"true","targetType":"full","statusVal":"","statusType":"auto","x":680,"y":1800,"wires":[]},
          {"id":"fca05075.903978","type":"inject","z":"1935bfc0.28217","name":"","props":[{"p":"payload"},{"p":"topic","vt":"str"}],"repeat":"","crontab":"*/5 6-22 * * *","once":true,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":250,"y":1920,"wires":[["450f636d.09c42c"]]},
          {"id":"450f636d.09c42c","type":"http request","z":"1935bfc0.28217","name":"getIP","method":"GET","ret":"txt","paytoqs":"body","url":"https://myip.com.tw","tls":"","persist":false,"proxy":"","authType":"","x":460,"y":1940,"wires":[["a465e8be.dae868"]]},
          {"id":"b9c3e19a.0f8188","type":"debug","z":"1935bfc0.28217","name":"","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","statusVal":"","statusType":"auto","x":910,"y":2000,"wires":[]},
          {"id":"a465e8be.dae868","type":"html","z":"1935bfc0.28217","name":"","property":"payload","outproperty":"payload","tag":"font","ret":"html","as":"single","x":640,"y":1940,"wires":[["7f0c22d6.c1eeec"]]},
          {"id":"fe5267c5.5e6998","type":"rbe","z":"1935bfc0.28217","name":"","func":"rbe","gap":"","start":"","inout":"out","septopics":false,"property":"payload","x":770,"y":1880,"wires":[["5a039c93.a82a2c"]]},{"id":"7f0c22d6.c1eeec","type":"change","z":"1935bfc0.28217","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"payload[0]","tot":"jsonata"}],"action":"","property":"","from":"","to":"","reg":false,"x":900,"y":1940,"wires":[["fe5267c5.5e6998","b9c3e19a.0f8188"]]}]
      </pre>
  </ul>
</ol>

<h3>Setup DDNS - Dynu.org</h3>
<ol>
  <li>register Dynu.com account</li>
  <li>update ip address => https://api.dynu.com/nic/update?hostname=example.dynu.com&password=PASSWORD</li>
  <li> Method 2 </li>
  <ul>
    <li>Create a directory to put the files into</li>
    <pre>
    mkdir dynudns 
    cd dynudns
    vi dynu.sh ==>

    echo url="https://api.dynu.com/nic/update?username=USERNAME&password=PASSWORD" | curl -k -o ~/dynudns/dynu.log -K -
    
    *password can be used MD5 Hash
    <==
    chmod 700 dynu.sh
    crontab -e ==>
    
    */5 * * * * ~/dynudns/dynu.sh >/dev/null 2>&1
    
    <== update ip every 5 min
    </pre>
  </ul>
    <li>
      <span>https://api.dynu.com/nic/update?hostname=&lt;your ddns hostname&gt;&password=&lt;Password MD5/SHA-256&gt;</span>
    </li>
</ol>

<h3>Install Docker</h3>
<ol>
  <li>first, update and full-upgrade</li>
  <li>install docker command<br>curl -sSL https://get.docker.com | sh</li>
  <li>sudo systemctl enable docker</li>
  <li>Install portainer for docker container/Image manager<br>
      https://documentation.portainer.io/v2.0/deploy/ceinstalldocker/</li>
  <li>reboot</li>
  <li>https://host.local:9000</li>
  <li>register hub.docker.com</li> 
  <li>Install homebridge Image</li>
  <li>Install homebridge Plugin "Homebridge Mqttthing"</li>
</ol>
    
