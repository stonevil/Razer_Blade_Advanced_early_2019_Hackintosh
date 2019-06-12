# Razer Blade Advanced early 2019 macOS 10.14 hackintosh

<span style="color:red">**Note: I am not responsible if you mess up your computer with this guide!**</span>


Intro
---

![About this Mac](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/about.png)

I'm long time Apple hardware and software user. Since 1996. And still macOS is best OS for my requirements.
My first computer is PowerBook 150 I bough in 1996 during my studying in Berkley. Since then I used only Apple mobile computers. PowerBook G3, PowerBook Titanium, bunch of MacBook Pro 13" and 15".
But I'm really unhappy with my latest MacBook Pro 2017. Useless keyboard with arrow keys designed for Tinker Bell? Zero ability to upgrade up to 32Gb RAM back then in 2017. This 100% Intel fail. Just like performance and thermal Intel CPU issues for last 6 years. Intel just don't care anymore about mobile CPU market.

So finally I make decision to switch to dark side and hackintosh good enough notebook. After some research I selected Razer Blade Advanced for this purpose.

**Purpose**

* Backend software development.
* ML development (requires CUDA and Nvidia GPU).
* Embedded software and hardware development (IoT).
* Cloud and DevOps.
* Once per month gaming. Usually 3A titles like
	* [Tomb Rider](https://tombraider.square-enix-games.com/en-gb)
	* [Deus Ex](https://square-enix-games.com/en_US/games/deus-ex-mankind-divided/)
	* [Tom Clancy's The Division 1/2](https://tomclancy-thedivision.ubisoft.com/game/en-us/home)
	* [Mass Effect](https://www.ea.com/games/mass-effect), etc.


Hardware
---

**Razer Blade Advanced early 2019**

 | Spec
---:|:---
Chipset | Mobile Intel HM370
CPU | Intel Core i7-8750H processor, 6 Cores / 12 Threads, 2.2GHz / 4.1GHz, 9MB Cache
Memory | 16GB dual-channel DDR4-2667MHz, up to 64GB
GPU | Intel UHD 630
dGPU | NVidia 2070 Max-Q (8GB GDDR6 VRAM)
Storage | Samsung PM981 256GB NVMe M.2
Screen | 15.6" Full HD 144Hz, 1920 x 1080 IPS
Webcam | Windows Hello built-in IR HD webcam (1MP / 720P)
WiFi | Intel Wireless-AC 9560NGW
Input & Output | USB 3.1 Gen 1 (USB-A) x3
 | Thunderbolt 3 (USB-C)
 | HDMI 2.0B
 | Mini DisplayPort 1.4
Soundboard | Realtek ALC298
Battery | 80Wh
Keyboard | Per-key RGB powered by Razer Chroma™ N-Key rollover backlit
Touchpad | Precision Glass
Dimensions | 17.8mm x 235mm x 355mm
Weight | 2.21 kg
Power | 230W power adapter


Hardware Compatibility
---

The bundled ``WiFI`` and ``NVMe`` is not compatible with macOS and should be replaced. Please find below recommended replacement parts already tested for compatibility. Usually I need to deploy for testing 4-5 node Kubernetes cluster with at least 4Gb per node. So 32GB is necessary upgrade for me.


**Accessories**

* USB mouse. Trackpad will be unavailable during macOS installation procedure.
* USB stick with at least 16Gb storage.


**WiFi**

* BCM94352Z (DW-1560). I can easily find for $24-30 on [eBay](https://www.ebay.com/sch/i.html?_from=R40&_nkw=BCM94352Z+DW-1560&_sacat=0&rt=nc&LH_BIN=1)


**Storage**

* Samsung EVO 970 NVMe [Amazon](https://www.amazon.com/gp/product/B07DB942BT/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1)
* Samsung EVO 970 Pro NVMe [Amazon](https://www.amazon.com/Samsung-PCI-Express-Solid-State-V-NAND/dp/B07DFJ3YQR/ref=sr_1_4?keywords=Samsung+970+EVO+Pro&qid=1560233808&s=electronics&sr=1-4)
* Sabrent Rocket NVMe [Amazon](https://www.amazon.com/gp/product/B07LGF54XR/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
* WD Black SN750 NVMe [Amazon](https://www.amazon.com/BLACK-SN750-500GB-Internal-Gaming/dp/B07MQ468S8/ref=sxin_3_ac_d_rm?keywords=wd%2Bblack%2Bnvme&pd_rd_i=B07MH2P5ZD&pd_rd_r=0be71a8a-a79d-4ce3-ad47-102a5ee16a25&pd_rd_w=9ZCWD&pd_rd_wg=dlFxu&pf_rd_p=0bc35c17-1e0d-4808-b361-20ab11b00973&pf_rd_r=0CKT4MYE9A5QZ8AJYEVK&qid=1560233421&s=gateway&th=1)

<span style="color:red">Note: I do recommend to use at least 1Tb NVMe for dual boot with Windows 10.</span>


**RAM**

* Ballistix Sport LT 32GB Kit (16GBx2) DDR4 2666 MT/s (PC4-21300) CL16 DR x8 SODIMM 260-Pin [Amazon](https://www.amazon.com/gp/product/B06XRBS4Y5/ref=ppx_yo_dt_b_asin_title_o03_s00?ie=UTF8&psc=1)
* Corsair Vengeance SODIMM 32GB (2x16GB) DDR4 3000 C16 Laptop [Amazon](https://www.amazon.com/Corsair-Vengeance-Performance-Unbuffered-CMSX32GX4M2A3000C16/dp/B01G260V2C/ref=sr_1_2?keywords=Corsair+Vengeance+SODIMM+32GB+%282x16GB%29+DDR4+3000+C16&qid=1560241967&s=gateway&sr=8-2)


**Recommended Upgrades**

* Advancing Gene NVMe M.2 Heatsink. Decreased temperature for about 10-12° C on heave load [Amazon](https://www.amazon.com/gp/product/B074Y5DZ4N/ref=ppx_yo_dt_b_asin_title_o04_s01?ie=UTF8&psc=1)


**Recommended Tools**

* iFixIt Pro Tech Toolkit [iFixIt](https://www.ifixit.com/Store/Tools/Pro-Tech-Toolkit/IF145-307?o=4)


**Extreme Upgrade only for Advance Gamers**

* Thermal Grizzly Conductonaut Thermal Grease Paste <span style="color:red">**(Liquid Metal)**</span> [Amazon](https://www.amazon.com/gp/product/B01A9KIGSI/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1)
* MG Chemicals 422B Silicone Modified Conformal Coating [Amazon](https://www.amazon.com/gp/product/B008O9YIV6/ref=ppx_yo_dt_b_asin_title_o01_s00?ie=UTF8&psc=1)
* 3M Scotch Super 88 Vinyl Electrical Tape [Amazon](https://www.amazon.com/3M-Scotch-Electrical-Dielectric-Strength/dp/B001DPXGSE/ref=sr_1_2_sspa?ie=UTF8&qid=1538036249&sr=8-2-spons&keywords=super+88&psc=1)


Repository
---

**BIOS\_mod**

BIOS custom updates


**EFI**

The EFI folder should be a minimal but complete EFI partition with Clover and all my kexts, config, and ACPI patches.


**Extensions**


**Tools**


Required Tools
---

* ``UniBeast`` OR ``TINU`` to build macOS installation media.
	* [UniBeast download URL](https://www.tonymacx86.com/resources/kextbeast-2-0-2.399/)
	* [TINU download URL](https://github.com/ITzTravelInTime/TINU)
* Clover Configurator, an easy to use macOS application designed to help you create custom configuration files for the Clover EFI bootloader via a streamlined graphical interface.
	* [Clover Configurator download URL](https://mackie100projects.altervista.org/download-clover-configurator/)
* ``KextBeast`` is a quick installer for .kext, .bundle, and .plugin files.
	* [KextBeast download URL](https://www.tonymacx86.com/resources/kextbeast-2-0-2.399/)
* ``Continuity Activation Tool`` tool makes the necessary changes to enable Continuity features on compatible hardware.
	* [Continuity Activation Tool download URL](https://github.com/dokterdok/Continuity-Activation-Tool)
* ``Kext Updater``, this little tool its totally easy to have up-to-date Kexts.
	* [Kext Updater download URL](https://www.insanelymac.com/forum/topic/334222-kext-updater-keep-your-kexts-fresh-with-only-one-click/)
* ``MaciASL``. A native AML compiler and IDE for OS X, with syntax coloring, tree navigation, automated patching, online patch file repositories, and iASL binary updates. Written entirely in Cocoa, conforms to OS X guidelines.
	* [MaciASL download URL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/)
* ``GenSMBIOS``, Py script that uses acidanthera's macserial to generate SMBIOS and optionally saves them to a plist.
	* [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
* ``one-key-cpufriend``, script to modify macOS CPU Performance
	* [one-key-cpufriend](https://github.com/stevezhengshiqi/one-key-cpufriend)
* ``USBMap``, Py script for mapping out USB ports and creating a custom SSDT or injector kext (WIP).
	* [USBMap](https://github.com/corpnewt/USBMap)


Guide
---

### BIOS update

Very important to make all updates fot BIOS before starting any macOS deployment. ACPI sources will be different after BIOS update and this will require to dump ACPI sources and patch them again.

Download BIOS, EC, ME Firmware and apply them from stock Windows partition.

[Razer Hardware Drivers download URL](http://drivers.razersupport.com//index.php?_m=downloads&_a=view&parentcategoryid=864&pcid=860&nav=0,350,860)

* Boot into Windows.
* Open [Razer Hardware Drivers download URL](http://drivers.razersupport.com//index.php?_m=downloads&_a=view&parentcategoryid=864&pcid=860&nav=0,350,860) in prefered browser
* Download latest BIOS, EC, ME Firmware updates.
* Apply this updates in required order. This is very important! Read documentation carefully!


**Useful information**

* [Razer Support Website](https://support.razer.com)


### BIOS unlock

Some changes for BIOS configuration should be done to make macOS bootable on Razer Blade Advanced.

* Disable VT-d. Apple droped support long time ago and will not boot in some cases with enabled VT-d. Do not mistake VT-d for VMX.
* Increase memore pre-alocated for DVMT. Usually DVMT Pre-Allocated for 32Mb. macOS requires 64Mb minimum.
* Deactivate CFG-Lock. Required by macOS Power Management.
* Disable Secure Boot.

Some of this configurations can be fixed one or another way in Clover configuration file. But better to play safe and change configuration in BIOS. And deactivation of CFG-Lock can help with power management.

In case if BIOS upgraded to latest version and

* System BIOS Version is 1.04
* EC FW Version is 1.03
* MCU FW Version is 1.00.00.00

safely to use already modded dump from ``BIOS\_mod`` folder and go to step **Flash BIOS**.

Otherwise follow to next step.


#### Export BIOS

* Boot into Windows.
* Download this repository.
* Open ``Tools\AfuWin64`` folder.
* Run ``AFUWINGUIx64.EXE`` application.
* In ``AFUWINGUI`` application click ``Save`` button to export current BIOS.
* Save BIOS to ``Desktop`` folder.
* Close ``AFUWINGUI`` application.


#### Modding BIOS

Most of this options required for next undervolting and overclocking. But part of them is necessary for macOS. This like options marked with <span style="color:red">**!**</span>

* Open ``Tools\AMIBCP64`` folder.
* Run ``AMIBCP64.exe`` application.
* In ``AMIBCP`` application click ``Open``, navigate to ``Desktop`` and open BIOS saved in previous steps.
* In ``AMIBCP`` application
	* Unfold root folder in left pane. This folder is blank and have no name.
	* Unfold ``Setup`` subfolder.
	* Click ``Power & Performance`` subfolder.
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``Power & Performance`` (second row from top)
			* ``CPU - Power Management Control`` <span style="color:red">**!**</span>
			* ``Intel(R) Speed Shift Technology``
	* Click ``CPU - Power Management Control`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``CPU - Power Management Control`` (second row from top) <span style="color:red">**!**</span>
			* ``Intel(R) SpeedStep(tm)``
			* ``Intel(R) Speed Shift Technology``
			* ``C states``
			* ``Package C State Limit``
			* ``CPU Lock Configuration`` (scroll way down) <span style="color:red">**!**</span>
	* Click ``OverClocking Performance Menu`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``OverClocking Performance Menu`` (second row from top)
			* ``XTU Interface``
			*	``Processor``
			* ``Ring``
			* ``GT``
			* ``Uncore``
			* ``Memory``
	* Unfold ``OverClocking Performance Menu`` subfolder.
	* Click ``Processor`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``Processor`` (second row from top)
			* ``Core Voltage Offset``
			* ``Offset Prefix`` below ``Core Voltage Offset``
	* Click ``GT`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``GT Domain`` (second row from top)
			* ``GT Voltage Offset``
			* ``Offset Prefix`` below ``GT Voltage Offset``
			* ``GTU Voltage Offset``
			* ``Offset Prefix`` below ``GTU Voltage Offset``
	* Click ``Uncore`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``Uncore`` (second row from top)
			* ``Uncore Voltage Offset``
			* ``Offset Prefix`` below ``Uncore Voltage Offset``
	* Click ``Memory Overclocking Menu`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``Memory Profile`` (second row from top) <span style="color:red">**RAM XMP Profile**</span>
			* ``Memory Profile`` (another one somewhere in the middle of the list) <span style="color:red">**RAM XMP profile**</span>
			* ``Memory Reference Clock`` <span style="color:red">**RAM XMP Profile**</span>
			* ``Memory Ratio`` <span style="color:red">**RAM XMP Profile**</span>
			* ``Memory Voltage`` <span style="color:red">**RAM XMP Profile**</span>
	* Click ``Chipset`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``System Agent (SA) Configuration`` (second row from top) <span style="color:red">**!**</span>
	* Unfold ``Chipset`` subfolder.
	* Click ``System Agent (SA) Configuration`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``System Agent (SA) Configuration`` (second row from top) <span style="color:red">**!**</span>
			* ``VT-d`` <span style="color:red">**!**</span>
			* ``Graphics Configuration`` <span style="color:red">**!**</span>
			* ``PEG Port Configuration``
			* ``VT-d`` (another one somewhere in the middle of the list) <span style="color:red">**!**</span>
	* Unfold ``System Agent (SA) Configuration`` folder in left pane
	* Click ``Graphics Configuration`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``Graphics Configuration`` (second row from top) <span style="color:red">**!**</span>
			* ``Primary Display``
			* ``Internal Graphics``
			* ``DVMT Pre-Allocated`` <span style="color:red">**!**</span>
			* ``DVMT Total Gfx Mem`` <span style="color:red">**!**</span>
	* Click ``PEG Port Configuration`` folder in left pane
		* In right pane change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``PEG Port Configuration`` (second row from top)
			* ``ASPM``
			* ``ASPM L0s``
* Click ``Save As`` in ``AMIBCP`` application.
* Save BIOS with new name to ``Desktop`` folder.
* Close ``AMIBCP`` application.


#### Flash BIOS

* Open ``Tools\AfuWin64`` folder.
* Run ``AFUWINGUIx64.EXE`` application.
* In ``AFUWINGUI`` application click ``Open`` button.
* Choose new modded BIOS from ``Desktop`` folder.
* Close all application except ``AFUWINGUI``. Close also all Windows TaskBar apps like Nvidia Expierence, Razer, etc.
* Click ``Flash`` button in ``AFUWINGUI`` application and confirm flashing BIOS.
* Close ``AFUWINGUI`` application.
* Reboot Windows.


**Useful information**

* [Razer Blade 2017 Ultimate CPU GPU Optimization - Unleashed Performance - BIOS Unlock](https://www.youtube.com/watch?v=O5CvK7i9a_Y)


### BIOS configuration

There are few changes in BIOS is vital to make macOS happy and bootable on RBA. Undervolting and Overclocking will explained in last dedicated chapter.

* Reboot computer.
* Repeatedly press ``DEL`` key to enter BIOS configuration menu.
* In BIOS navigate to menu
	* ``Advanced``
		* ``Power & Performance``
			* ``CPU - Power Management Control``
				* ``CPU Lock Configuration``
					* Disable ``CFG Lock``
					* Disable ``Overclocking Lock``
	* ``Advanced``
		* ``Overclocking Performance Menu``
			* Disable ``XTU Interface``
	* ``Advanced``
		* ``Thunderbolt(TM) Configuration``
			* Switch ``Security Level`` to ``No Security``
	* ``Chipset``
		* ``System Agent (SA) Configuration``
			* ``Graphics Configuration``
				* Set ``DVMT Pre-Allocated`` to ``64``
				* Set ``DVMT Total Gfx Mem`` to ``MAX``
	* ``Chipset``
		* ``System Agent (SA) Configuration``
		* Disable ``VT-d``
	* ``Chipset``
		* ``SATA And RST Configuration``
		* Check ``SATA Mode Selection`` set to ``AHCI``
	* ``Security``
		* Set ``Secure Boot`` to ``Disabled``
	* ``Boot``
		* Set ``Fast Boot`` to ``Disabled``
		* ``CSM Configuration``
			* Set ``CSM Support`` to ``Disabled``
	* ``Save and Exit``
		* Hit ``Save Changes``
		* Hit ``Save Changes and Reset``


### macOS install media preparation

Use you own OR borrow some friend Mac computer.

* On some Mac download ``UniBeast`` OR ``TINU`` up to your preferences.
* Run ``UniBeast`` OR ``TINU`` application.
* Follow instruction and build macOS installation media macOS 10.14 Mojave. Very important to build media with latest available version of Mojave.

**Useful information**

* [UniBeast: Install macOS Mojave on Any Supported Intel-based PC](https://www.tonymacx86.com/threads/unibeast-install-macos-mojave-on-any-supported-intel-based-pc.259381/)
* [TINU](https://github.com/ITzTravelInTime/TINU)


### WiFi and NVMe replacement

WiFi and NVMe replacement easy enough for this model. Just unscrew bottom case.

**Useful information**

* [How to Upgrade the Razer Blade 15 RAM & SSD](https://www.youtube.com/watch?v=6TZih3m0-Ys)
* [Razer Blade Advanced RTX 2070 SSD Replacement](https://www.youtube.com/watch?v=9-ZfDNdj2WU)


### Liquid Metal re-paste

<span style="color:red">**Be very careful and do this at your OWN RISK!**</span>

This step is not necessary and can be recommended only for hardcore gamers with experience building own rigs. Razer already using very good thermal paste so re-paste thermal paste is not very useful until liquid metal will be used. And Grizzly Conductonaut Thermal Grease Paste maybe the best one. Read more about liquid metal thermal paste and all issues he can cause before make decision and go forward.

**Useful information**

* [Razer Blade 15 Advanced Liquid Metal Repaste](https://www.youtube.com/watch?v=tGQLaFqQvOw)
* [Grizzly Liquid Metal'd my 2018 Razer Blade 15 1060](https://www.youtube.com/watch?v=7xK4SjOra1E)


### macOS installation

* Insert macOS USB install media.
* Boot/Reboot computer.
* Press repeatedly ``F12`` until you ``Boot Menu`` will show.
* Select macOS USB install media.
* Open Disk Utility from Tools menu.
* Format NVMe to APFS.
* Follow usual macOS installation procedure.
* After reboot repeatedly tap ``F12`` again until get ``Boot Menu``.
* Select macOS USB install media again.

TODO

**Useful information**

* [UniBeast: Install macOS Mojave on Any Supported Intel-based PC](https://www.tonymacx86.com/threads/unibeast-install-macos-mojave-on-any-supported-intel-based-pc.259381/)


#### Install EFI and Extensions

TODO


#### Patch ACPI

TODO


#### iMessages and FaceTime

TODO

**Useful information**

* [An iDiot's Guide To iMessage](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/)


Razer Chroma
---

Razer Chroma support for Razer Blade notebooks and most latest Razer devices is not implemented yet. And suppose will never will be implemented.

Thanks to [osx-razer-blade](https://github.com/boo-dev/osx-razer-blade) project I'm already have enough information and working already on cli tool to control Razer Blade keyboard and logo.


Undervolting
---

TODO

**Useful information**

* [Razer Blade 2017 Ultimate CPU GPU Optimization - Unleashed Performance - BIOS Unlock](https://www.youtube.com/watch?v=O5CvK7i9a_Y)
* [Razer Blade 2018 Thermal Testing - Overclocking and Undervolting](https://www.youtube.com/watch?v=rJSeG_Pb3bs)
* [Razer blade 15 undervolting with ThrottleStop](https://www.youtube.com/watch?v=ooET-Nk62VY)


Know Issues and Limitations
---

**Limitations**

* Nidia Web Driver is absent for macOS 10.14 Mojave. Nvidia do not want to implement support for Apple new 2D/3D rendering framework Metal and do not want to share access for Nvidia drivers for Apple. So, currently no support for Nvidia GPU for macOS 10.14 Mojave. It's not a problem for me because I'm using Windows 10 partition for gaming and Debian Linux partition to run ML tasks over night.
	* HDMI port connected directly to Nvidia GPU and will not work in macOS 10.14 Mojave.
	* No idea about DisplayPort. Maybe I will borrow some monitor with DisplayPort support in office for testing.
	* USB-C to HDMI should work without any issues.


**Issues**

* Sometimes screen do not wake up after first lid open from sleep. You need to close and open lid again. This issue introduced after latest BIOS update. Annoying but not important.


Conclusion
---

It's a pretty good laptop with far better keyboard than 2016-2019y MacBook Pro. Solid workstation and extremely good gaming machine. And easy to upgrade storage and RAM and WiFi. This model supports NVMe up to 2Tb and up to 64Gb RAM.

Major disadvantages is

* PC trackpads still cannot match with MacBook Pro. It's good. Much better than most PC notebook have. But still not even close to MBP.
* Screen rather mediocre compare to MacBook Pro. But 144Hz is good for gaming.


Additional Information
---

* [Razer Blade Advanced (2019) trackpad issue](https://www.tonymacx86.com/threads/need-help-razer-blade-advanced-2019-trackpad-issue.273575/)
* [Razer Blade 15 (2018) Detailed Install Guide High Sierra 10.13.6 (17G2208-17G5019)](https://www.tonymacx86.com/threads/guide-razer-blade-15-2018-detailed-install-guide-high-sierra-10-13-6-17g2208-17g5019.264017/)
* [Native Power Management for Laptops](https://www.tonymacx86.com/threads/guide-native-power-management-for-laptops.175801/)
* [A Beginner's Guide to Creating a Custom USB SSDT](https://www.tonymacx86.com/threads/a-beginners-guide-to-creating-a-custom-usb-ssdt.272505/)
* [Quick Guide to Generate a SSDT for CPU Power Management](https://www.tonymacx86.com/threads/quick-guide-to-generate-a-ssdt-for-cpu-power-management.177456/)
* [Creating a Custom SSDT for USBInjectAll.kext](https://www.tonymacx86.com/threads/guide-creating-a-custom-ssdt-for-usbinjectall-kext.211311/)
* [Generate SSDT For Coffee Lake CPU](https://www.tonymacx86.com/threads/guide-generate-ssdt-for-coffee-lake-cpu.238311/)
* [UniBeast: Install macOS Mojave on Any Supported Intel-based PC](https://www.tonymacx86.com/threads/unibeast-install-macos-mojave-on-any-supported-intel-based-pc.259381/)


**Community**

* [InsanelyMac](https://www.insanelymac.com)
* [tonymacx86](https://www.tonymacx86.com)
* [Reddit Hackintosh](https://www.reddit.com/r/hackintosh/)


Special Thanks
---

* [Acidanthera](https://github.com/acidanthera)
* [RehabMan](https://github.com/RehabMan)
* [Alexandre Daoud](https://github.com/alexandred)
* [Ben Raz](https://github.com/williambj1)
* [Steve Zheng](https://github.com/stevezhengshiqi)
* [vettz500](https://www.tonymacx86.com/members/vettz500.291395/)
* and many others