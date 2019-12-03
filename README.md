<h3>Install Raspbian OS image</h3>
  - Download img file from offical web https://www.raspberrypi.org/downloads/<br>
  - follow instructure https://www.raspberrypi.org/documentation/installation/installing-images/README.md<br>
  
<h3>Setup VNC and SSH for remote connect</h3>
  <p>VNC serve already installed in Raspbian, only do the </p>
  - $sudo raspi-config (to enable vnc & ssh from interfave setup)</p>
 
<h3>Problem : HDMI no sound</h3>
  - need edit /boot/config.txt add new line than reboot
  hdmi_driver=2
  - if it didn't work, add another loine
  hdmi_force_edid_audio=1


<p>Refence : http://han-ya.blogspot.com/2018/08/raspberry-pi-3b-1.html</p>

<h3>Install 中文注音輸入法</h3>
   - sudo apt-get install scim-chewing
   - sudo apt-get install ttf-wqy-microhei ttf-wqy-zenhei xfonts-wqy
