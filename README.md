# gswitch

This is an application that puts a xorg config in place when you want to use a external GPU and can remove the config again when it's time to go back.

Important to note is to make sure to take care of Thunderbolt authorization. While waiting for the KDE team to fix Bolt into Plasma, I have a 'udev' rule that authorizes everything...

```commandline
/etc/udev/rules.d/99-local.rules:

ACTION=="add", SUBSYSTEM=="thunderbolt", ATTR{authorized}=="0", ATTR{authorized}="1"
```


But be aware that it's dangerous, someone may own your PC if you're not careful. You have been warned!

It comes with a boot service that automatically switches to your eGPU if it's connected at boot. And if it's not, it sets the configuration to internal.

To activate this feature, you do:

```commandline
sudo systemctl enable gswitch
```

The process of getting this installed is:

```commandline
git clone https://github.com/karli-sjoberg/gswitch.git
cd gswitch
sudo make install
```

Uninstalling is just as easy:

```commandline
sudo make uninstall
cd ..
rm -rf gswitch
```

To get everything set up, you do:

```commandline
sudo gswitch setup
```

Switching from internal to egpu:

```commandline
sudo gswitch egpu
```

Lastly, switching from egpu back to internal:

```commandline
sudo gswitch internal
```

Happy switching!
