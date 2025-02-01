<h1>Active Directory with Powershell - Virt-Manager and Virtual Bridge Configuration </h1>
This section of the lab goes through installing our hypervisor and setting up our virtual bridge.<br />

<h2>Environments and Technologies Used</h2>

- QEMU/KVM with Virt-Manager (Kernal Virtual Machine)
- Terminal (Command-Line Interface)
- Virtual Bridging (Networking)

<h2>Operating Systems Used </h2>

- Linux Mint (Host OS)
  - Desktop Environment: KDE Plasma 5.27
        
- Linux Mint (Guest OS)
  - Desktop Environment: Cinnamon

<h2>QEMU/KVM and Virt-manager</h2>

<p><b>Let's begin with the installation of QEMU/KVM and Virt-manager. This is essentially an application that turns Linux into a hypervisor while providing a 'graphical user interface' (GUI) for simpler management. Don't worry, installation is much easier than it sounds.</b>

</p>
<p align="center">
<img src="https://i.imgur.com/ZfAO3Ci.png" height="30%" width="30%" alt="virt-man logo"/>
</p>

<br />
<details>
 <summary><b>- Installation</b></summary>
<p>We open terminal and run the command: <code>sudo apt-get install virt-manager</code>. This will install Virt-manager along with the dependencies required.</p>
<p align="center">
<img src="https://i.imgur.com/MKk23To.png" height="65%" width="65%" alt="UI to add Role"/>
</p>
<p>When that finishes we search for <b>Virtual Machine Manager</b> in our application launcher menu and run it.</p>
<p align="center">
<img src="https://i.imgur.com/ZEniJdY.png" height="65%" width="65%" alt="enter role name"/>
</p>
<br />
<p>We have it installed and running, but there is one major issue: <code>QEMU/KVM - Not Connected</code> error. Fortunately, we can fix this in a few steps.</p>
<p align="center">
<img src="https://i.imgur.com/kEdM5a1.png" height="65%" width="65%" alt="list of permissions"/>
<img src="https://i.imgur.com/TJaq7F0.png" height="65%" width="65%" alt="list of permissions"/>
</p>
<br />
<p>Open terminal and enter the following commands:
    <ol>
        <li><code>sudo systemctl start libvirtd</code> - This starts the libvirtd service.</li>
        <li><code>sudo adduser [your username here] libvirt</code> - This adds our user to the group.</li>
        <li><code>sudo systemctl restart libvirtd</code> - This restarts the service to make sure the changes are applied.</li>
        <li><code>id [your username here]</code> - This displays the groups our user is in.</li>
        <li><code>reboot</code> - This reboots the vm. If the above steps didn't work we probably need to reboot.</li>
    </ol>
</p>
<p align="center">
<img src="https://i.imgur.com/WA0cpHL.png" height="65%" width="65%" alt="list of permissions"/>
</p>
<p>And when we relaunch Virt-Manager the error is gone.</p>
<p align="center">
<img src="https://i.imgur.com/Sfa18UZ.png" height="65%" width="65%" alt="list of permissions"/>
</p>
</details>    
<hr>

<h2>Virtual Bridge Connection</h2>
<p><b>Now we create a Virtual Bridge Connection for our lab. With it we can have our virtual machines communicate with each other in an internal network.</b>
<br />
<details>
 <summary><b>- Setup and Config [Desktop Environment: Cinnamon]</b></summary>
<p>In 'Network Connections' we create a new connections and choose Bridge</p>
<p align="center">
<img src="https://i.imgur.com/2CJmBer.png" height="65%" width="65%" alt="UI to add Role"/>
</p>
<br />
<p>Once we are in the 'Editing Bridge Connection' we rename the interface. Then we hit 'add' and select 'ethernet.'</p>
<p align="center">
<img src="https://i.imgur.com/VRYVC0w.png" height="65%" width="65%" alt="enter role name"/>
</p>
<br />
<p>We edit the "br0" port by selecting our ethernet device from the drop-down, then hit 'save.'</p>
<p align="center">
<img src="https://i.imgur.com/75xiYin.png" height="40%" width="40%" alt="enter role name"/>
</p>
<br />
<p>We are brought back to the previous window. We configure our tabs like so, then save.</p>
<p align="center">
<img src="https://i.imgur.com/wzkOaDQ.png" height="40%" width="40%" alt="enter role name"/>
</p>
<p align="center">
<img src="https://i.imgur.com/fUE9qw8.png" height="40%" width="40%" alt="enter role name"/>
</p>
<p align="center">
<img src="https://i.imgur.com/bkzpgwD.png" height="40%" width="40%" alt="enter role name"/>
</p>
<br />
<p>Our new bridge connection is now available for use. We can also verify through the terminal by running command: <code>ip ad</code>.</p>
<p align="center">
<img src="https://i.imgur.com/aLJkqgw.png" height="40%" width="40%" alt="enter role name"/>
</p>
<p align="center">
<img src="https://i.imgur.com/Fx7cRT4.png" height="40%" width="40%" alt="enter role name"/>
</p>
<br />
</details>    
<hr>
<details>
 <summary><b>- Setup and Config [Desktop Environment: KDE Plasma 5.27]</b></summary>
 <p><b>Aside from a different settings layout, the configuration in KDE Plasma 5.27 DE is the same as in Cinnamon DE. We will run through it quickly.</b></p>
<p>In <b>System Settings</b> we go to Network -> Connections and create a new connection. Like with Cinnamon DE we select 'bridge.'</p>
<p align="center">
<img src="https://i.imgur.com/kh1N1N3.png" height="65%" width="65%" alt="UI to add Role"/>
<img src="https://i.imgur.com/RDgFbdB.png" height="40%" width="40%" alt="UI to add Role"/>
</p>
<br />
<p>We edit the connection by naming the interface "br0" and click 'add', selecting 'ethernet.'</p>
<p align="center">
<img src="https://i.imgur.com/kJX9rwe.png" height="40%" width="40%" alt="enter role name"/>
</p>
<br />
<p>We configure "br0" interface, making sure to select our ethernet device.</p>
<p align="center">
<img src="https://i.imgur.com/7TV8PyY.png" height="40%" width="40%" alt="enter role name"/>
<img src="https://i.imgur.com/1x5WCw2.png" height="40%" width="40%" alt="enter role name"/>
</p>
<br />
<p>Now we configure the remaining tabs for connections settings.</p>
<p align="center">
<img src="https://i.imgur.com/iQSnXHw.png" height="40%" width="40%" alt="enter role name"/>
<img src="https://i.imgur.com/a6NHZYD.png" height="40%" width="40%" alt="enter role name"/>
<img src="https://i.imgur.com/AAjiWYy.png" height="40%" width="40%" alt="enter role name"/>
</p>
<br />
<p>Our new connection is now ready and we can verify via terminal by running command: <code>ip ad</code>.</p>
<p align="center">
<img src="https://i.imgur.com/KIPwjsj.png" height="20%" width="20%" alt="enter role name"/>
<img src="https://i.imgur.com/brg1Cy2.png" height="80%" width="80%" alt="enter role name"/>
</p>
<br />
</details>    
