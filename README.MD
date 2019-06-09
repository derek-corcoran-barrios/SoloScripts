## To start working with and modify the sosi OS 

I need to run

```
 ./img-mount.sh /home/derek/Desktop/sosi-2018-10-23.img 
``` 

Form the cloned solo repository https://github.com/solo-system/solo within the imgTools folder

Then within the imgTools folder it creates a virtual image of the folders to modify them such as this one

```
/home/derek/Documents/Solo/solo/imgTools/vroot/boot/solo
```

### Paths that already have been modified

added the file /home/amon/amon/mics/soundblasterXFigoPro.conf

### modified the file

/usr/share/alsa/alsa.conf.d/alsa-solo.conf adding the following

    ############################################################
    #Support for: Soundblaster XFI GO! Pro

    pcm.Proplug {
	    tupe plug
	    slave.pcm { type hw card Pro device 0 }
	    route_policy copy
    }


### Paths to be modified

/boot/solo/amon.conf just as it has settings for SB2 and SB3

    ##### Sound Blaster Play 2! Microphone USB dongle settings
    # value from [0,40].  0=-15dB, 20=0dB, 40=+15dB
    SB_VOLUME=20

    ##### Sound Blaster Play 3! Microphone USB dongle settings
    # value from [0,30].  0 => 0dB, 30 => 30dB
    SB3_VOLUME=20
    
we have to add one forSoundblaster XFI GO! Pro, probably:

    ##### Sound Blaster Play 3! Microphone USB dongle settings
    #Mic Capture Volume: Volume: min=-16384, max=1536, dBmin=-6400, dBmax=600
    
    SBPRO_VOLUME=20


### Errors found

in /usr/share/alsa/alsa.conf.d/alsa-solo.conf adding the following found the error

    ############################################################
    #Support for: Soundblaster XFI GO! Pro

    pcm.Proplug {
	    tupe plug
	    slave.pcm { type hw card Pro device 0 }
	    route_policy copy
    }

change tupe por type


## Folders and info in /proc/asound/Pro

* *id*
  Pro
* pcm0c
  + *info*
  ```
    card: 2
    device: 0
    subdevice: 0
    stream: CAPTURE
    id: USB Audio
    name: USB Audio
    subname: subdevice #0
    class: 0
    subclass: 0
    subdevices_count: 1
    subdevices_avail: 1
  ```

  + sub0
    + *hw_params*
      closed
    + *info*
    ```
      card: 2
      device: 0
      subdevice: 0
      stream: CAPTURE
      id: USB Audio
      name: USB Audio
      subname: subdevice #0
      class: 0
      subclass: 0
      subdevices_count: 1
      subdevices_avail: 1
    ```
    + *status* 
      closed
    + *sw_params*
      closed
* pcm0p
  + *info*  
  ```
    card: 2
    device: 0
    subdevice: 0
    stream: PLAYBACK
    id: USB Audio
    name: USB Audio
    subname: subdevice #0
    class: 0
    subclass: 0
    subdevices_count: 1
    subdevices_avail: 1
  ```
  + sub0
    + *hw_params*
      closed
    + *info* 
    ```
      card: 2
      device: 0
      subdevice: 0
      stream: PLAYBACK
      id: USB Audio
      name: USB Audio
      subname: subdevice #0
      class: 0
      subclass: 0
      subdevices_count: 1
      subdevices_avail: 1
    ```
    + *status* 
      closed
    + *sw_params*
      closed
* *stream0* 

```
  Creative Technology Ltd Sound Blaster X-Fi Go! Pro at usb-0000:00:14.0-2,   full  : USB Audio

  Playback:
    Status: Stop
    Interface 1
      Altset 1
      Format: S16_LE
      Channels: 2
      Endpoint: 1 OUT (ASYNC)
      Rates: 44100
    Interface 1
      Altset 2
      Format: S24_3LE
      Channels: 2
      Endpoint: 1 OUT (ASYNC)
      Rates: 44100

  Capture:
    Status: Stop
    Interface 2
      Altset 1
      Format: S16_LE
      Channels: 2
      Endpoint: 1 IN (ASYNC)
      Rates: 44100
```

* *usbbus*
  002/003
* *usbid*
  041e:3233
* *usbmixer*

```
    USB Mixer: usb_id=0x041e3233, ctrlif=0, ctlerr=0
  Card: Creative Technology Ltd Sound Blaster X-Fi Go! Pro at usb-0000:00:14.0-2, full 
    Unit: 5
      Control: name="PCM Playback Volume", index=0
      Info: id=5, control=2, cmask=0x3, channels=2, type="S16"
      Volume: min=-16384, max=0, dBmin=-6400, dBmax=0
    Unit: 5
      Control: name="PCM Playback Switch", index=0
      Info: id=5, control=1, cmask=0x0, channels=1, type="INV_BOOLEAN"
      Volume: min=0, max=1, dBmin=0, dBmax=0
    Unit: 6
      Control: name="Mic Capture Volume", index=0
      Info: id=6, control=2, cmask=0x3, channels=2, type="S16"
      Volume: min=-16384, max=1536, dBmin=-6400, dBmax=600
    Unit: 6
      Control: name="Mic Capture Switch", index=0
      Info: id=6, control=1, cmask=0x0, channels=1, type="INV_BOOLEAN"
      Volume: min=0, max=1, dBmin=0, dBmax=0
```

