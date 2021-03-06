```mermaid
  graph TB;

    begin("Begin Hackintosh Journey with ThinkPad X1 C6")-->getUSB
    sorry["Installation failed, please report the problem so that I can help and improve"]

    subgraph Prepare macOS Installation USB
      getUSB-->hvmac?
      hvmac?{{"Do you have an usable Mac or Hackintosh?"}}
      getInstaller["Download macOS Installer on macOS"]
      getInstallerLinux["Create macOS installer USB on Linux"]
      dosdude["Download macOS using macOS Patcher"]
      mas["Download macOS using Mac App Store"]
      getUSB["Get an USB with at least 16GB capacity"]
      thankyou["Use the script from notthebee"]
      createUSBmacOS["Use Unibeast to create the USB installer"]
      installClover["Install bootloader"]

      hvmac?-->|Yes|getInstaller
      hvmac?-->|No|getInstallerLinux
      getInstallerLinux-->thankyou
      getInstaller-->dosdude
      getInstaller-->mas
      dosdude-->createUSBmacOS
      mas-->createUSBmacOS
      createUSBmacOS-->installClover
    end

    thankyou-->finish
    installClover-->finish
    finish("You have the USB installer ready")
    finish-->changeBootOrder

    subgraph Part 1 of installation
      changeBootOrder["Change the boot order of your ThinkPad"]
      bootInstaller["Boot the macOS installer using Clover Menu"]
      bootSuccess?{{"Booted successfully?"}}

      partition["Partition your disks"]
      startInstall["Begin macOS installation"]
      installresult?{{"Part 1 of install macOS completed successfully?"}}
      reboot["Reboot your ThinkPad"]

      changeBootOrder-->bootInstaller
      bootInstaller-->bootSuccess?
      bootSuccess?-->|Yes|partition

      partition-->startInstall
      startInstall-->installresult?

    end
    bootSuccess?-->|No|sorry
    installresult?-->|No|sorry
    installresult?-->|Yes|reboot
    reboot["Reboot your ThinkPad"]
    reboot-->startInstall2

    subgraph Part 2 of installation
      startInstall2["Begin macOS installation part 2"]
      install2result?{{"Part 2 of install macOS completed successfully?"}}
      reboot2["Reboot your ThinkPad"]
      bootmac["Boot from installed macOS"]
      boot2success?{{"Did macOS boot up successfully?"}}
      startInstall2-->install2result?
      install2result?-->|Yes|reboot2
      reboot2-->bootmac
      bootmac-->boot2success?
      boot2success?-->|Yes|installSuccess

    end

    installSuccess-->setupMac

    subgraph Post-install
      setupMac["Setup your macOS on ThinkPad using Setup Assistant"]
      installKext["Install necessary Kernel Extensions"]
      disableHibernate["Disable hibernation"]
      fineTune["Fine tune your Hackintosh with the textual resources provided"]
      setupMac-->installKext
      installKext-->disableHibernate
      disableHibernate-->fineTune

    end

    complete["Installation complete and fine-tuned! Congratulations!"]
    fineTune-->complete

    boot2success?-->|No|sorry
    install2result?-->|No|sorry
    installSuccess["macOS installation is successful"]
```

