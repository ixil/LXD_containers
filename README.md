# LXD_containers
Common LXD IntelligentRoboticsLab's containers.

## Useful resources
* [Importing/exporting containers (Spanish)](https://superadmin.es/blog/devops/backup-contenedores-lxd/)
* [GUI apps](https://blog.simos.info/how-to-run-graphics-accelerated-gui-apps-in-lxd-containers-on-your-ubuntu-desktop/)

## Cheatsheet
* Launch a container from an image: `lxc launch [img-name] [cont-name] -p [profile-name]`
* List:  `lxc list`
* Start: `lxc start [cont-name]`
* Shell: `lxc exec [cont-name] -- su --login ubuntu`
* Share a directory: `lxc config device add [cont-name] shareddir1 disk path=/root/[dest_dir] source=/home/[username]/[origin_dir]`
* Rm a shared directory: `lxc config device remove [cont-name] shareddir1`
* Clone a container: `lxc copy [source-cont] [target-cont]`
* Connection through ssh (Permission denied (publickey)): https://www.digitalocean.com/community/questions/error-permission-denied-publickey-when-i-try-to-ssh 
* Add TIAGo's network profile to your container: 
  <pre><code>
    lxc profile create macvlan
    lxc profile edit macvlan
   </code></pre> 
   Paste the following:
   <pre><code>
   config:
     user.network-config: |
       version: 1
         config:
           - type: physical
             name: eth0
             subnets:
               - type: dhcp
                 ipv4: true
   description: LXD profile with LAN connection
   devices:
     eth0:
       name: eth0
       nictype: macvlan
       parent: [eth-name]
       type: nic
     root:
       path: /
       pool: default
       type: disk
   name: macvlan
   used_by:
   </code></pre>
   Add the profile to the container:
   <pre><code>lxc profile add [cont-name] macvlan </code></pre>
   
* Default network config:
  <pre><code> devices:
    eth0:
      name: eth0
      nictype: bridged
      parent: [network interface created in the initial process]
      type: nic
  </code></pre>

## Image list
- [Ubuntu 20.04 ROS2 Foxy](https://urjc-my.sharepoint.com/:u:/g/personal/jonatan_gines_urjc_es/EeZaYss1yhVJnrA9-BaBVzIBnomDGFDW4gThZ6iRO6Z8lQ?e=mDmDSy)
- [ROS2 - Follow Dynamic point - TIAGo](https://urjc-my.sharepoint.com/:u:/g/personal/jonatan_gines_urjc_es/Eem3XJ8kS2JOp3JG2jNJwg0BKOGKpXVghTOqpZZwNHPsOg?e=EBDB5t)
- [ROS Bridges - Foxy](https://urjc-my.sharepoint.com/:u:/g/personal/jonatan_gines_urjc_es/EfwgRp0QtkNMjen8-q8CQ2EBp7d8cwruDN5MChvfZoXV7w?e=y2QMlj)
- [Websites](https://github.com/ACTROS-Educational-Project/actros-educational-project.github.io/releases/download/lxc/080200225a7d601f0302aeeb998b06d7f8eb4b150ccb4c32c42526005ed75b98.tar.gz)
