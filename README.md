# Razer Blade Advanced early 2019 macOS 10.14 Hackintosh

**Note: I'AM NOT RESPONSIBLE IF YOU MESS UP YOUR COMPUTER USING THIS GUIDE!**

Intro
---

![About this Mac](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/About_Mac.png)

I have been using Apple hardware and software since 1996 for macOS has been the best OS to meet my needs. My first computer was a PowerBook 150. Since then, I used mostly Apple mobile solutions: PowerBook G3, PowerBook Titanium, bunch of MacBook Pro 13" and 15".
But, I'm really dissatisfied with the latest MacBook Pro 2017 as it has a useless keyboard with arrow keys designed for Tinker Bell and zero ability to upgrade up to 32Gb RAM back then in 2017. Yes. I know. This is 100% Intel failure. Just like performance and thermal issues the Intel CPU had for the last 6 years. Intel just doesn’t care about the mobile CPU market anymore.

So, finally, I made a decision to go to the dark side and to switch to the hackintosh notebook. After doing some research, I selected Razer Blade Advanced. This has, perhaps, the best combo of design (!), performance and upgradability.

**Purpose**

* UNIX/Linux backend software development. C, Go, Python.
* ML development (requires CUDA and Nvidia GPU).
* Embedded software and hardware development (IoT).
* Cloud and DevOps.
* iOS and macOS development mostly for fun.
* Gaming maybe once per month. Usually 3A titles like
	* [Tomb Rider](https://tombraider.square-enix-games.com/en-gb)
	* [Deus Ex](https://square-enix-games.com/en_US/games/deus-ex-mankind-divided/)
	* [Tom Clancy's The Division 1/2](https://tomclancy-thedivision.ubisoft.com/game/en-us/home)
	* [Mass Effect](https://www.ea.com/games/mass-effect)
	* [Pillars of Eternity](https://eternity.obsidian.net)
	* [Divinity: Original Sin](http://www.divinityoriginalsin.com), etc.


Hardware
---

**Razer Blade Advanced early 2019**

| | Spec | macOS 10.14 compatibility |
| ---: | :--- | :--- |
| ``Chipset`` | Mobile Intel HM370 | No issues |
| ``CPU`` | Intel Core i7-8750H processor, 6 Cores / 12 Threads, 2.2GHz / 4.1GHz, 9MB Cache | No issues |
| ``Memory`` | 16GB dual-channel DDR4-2667MHz, up to 64GB | No issues |
| ``GPU`` | Intel UHD 630 | No issues |
| ``dGPU`` | Nvidia 2070 Max-Q (8GB GDDR6 VRAM) | Nvidia Drivers absent for Mojave. ACPI should be patched to disable dGPU |
| ``Storage`` | Samsung PM981 256GB NVMe M.2 | Incompatible firmware. You can try fix with [Lenovo NVMe Firmware Update Utility](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t470s/downloads/ds119265) but better to replace |
| ``Screen`` | 15.6" Full HD 144Hz, 1920 x 1080 IPS |  No issues |
| ``Webcam`` | Windows Hello built-in IR HD webcam (1MP / 720P) |  No issues. Windows Hello is not supported in macOS |
| ``WiFi`` | Intel Wireless-AC 9560NGW | Drivers absent for macOS. Should replaced |
| ``Input & Output`` | USB 3.1 Gen 1 (USB-A) x3 | No issues |
| | Thunderbolt 3 (USB-C) | No issues |
| | HDMI 2.0B | HDMI connected directly to Nvidia GPU and will not work in macOS |
| | Mini DisplayPort 1.4 | Not tested |
| ``Soundboard`` | Realtek ALC298 | No issues. ACPI patch should be added to solve sleep issue |
| ``Battery`` | 80Wh | About 3-5h after proper Power Management configuration.  ACPI should be patched to enable battery stats |
| ``Keyboard`` | Per-key RGB powered by Razer Chroma N-Key rollover backlit | No issues. Razer Chroma software absent for macOS |
| ``Touchpad`` | Precision Glass | No issues. ACPI should be patched to enable trackpad |
| ``Dimensions`` | 17.8mm x 235mm x 355mm | |
| ``Weight`` | 2.21 kg | ACPI patches will not help with this. /sarcasm |
| ``Power`` | 230W power adapter | |


Hardware Upgrades and Tools
---

The bundled ``WiFI`` and ``NVMe`` is not compatible with macOS and should be replaced. Please find below the recommended replacement parts, already tested for compatibility. Usually I need to deploy for testing 4-5 node Kubernetes cluster with at least 4Gb per node. So 32GB is a necessary upgrade for me.


**Accessories**

| Accessories | Description | Amazon URL |
| ---: | :--- | :--- |
| ``USB mouse`` | Trackpad will be unavailable during macOS installation procedure | [Amazon](https://www.amazon.com/AmazonBasics-3-Button-Wired-Mouse-Black/dp/B005EJH6RW/ref=sr_1_3?keywords=amazon+basic+mouse&qid=1561714362&s=gateway&sr=8-3) |
| ``USB storage`` with at least 16Gb storage | Installation USB media | [Amazon](https://www.amazon.com/gp/product/B076GXJJRD/ref=ppx_yo_dt_b_asin_title_o03_s00?ie=UTF8&psc=1) |
| ``USB-A to USB-C cable`` | For USB ports detection procedure | [Amazon](https://www.amazon.com/AmazonBasics-Type-C-Gen1-Female-Adapter/dp/B01GGKYXVE/ref=pd_hpb_a2a_sims_6/130-2479265-2893400?_encoding=UTF8&pd_rd_i=B01GGKYYT0&pd_rd_r=54b9f737-919c-11e9-b9d7-6915ce2a8dc3&pd_rd_w=j9bw6&pd_rd_wg=IVvh1&pf_rd_p=bfc589eb-d865-496f-a10b-5e00902c2113&pf_rd_r=G68JVK6HBAFKEDA75MYY&refRID=G68JVK6HBAFKEDA75MYY&th=1) |


**WiFi**

| WiFi module | Description | eBay or AliExpress URL | Confirmation |
| ---: | :--- | :--- | :--- |
| ``BCM94352Z (DW-1560)`` | Recommended. 2 antennas. No issues. Additional kext's are required. Easily to find for \$24-60 on | [eBay](https://www.ebay.com/sch/i.html?_from=R40&_nkw=BCM94352Z+DW-1560&_sacat=0&rt=nc&LH_BIN=1) | [community](https://osxlatitude.com/forums/topic/11138-inventory-of-supportedunsupported-wireless-cards-2-sierra-catalina/) |
| ``BCM943602BAED (DW-1830)`` | 3 antennas. RBA have only 2. Works out of the box. About \$60-120 on AliExpress | [AliExpress](https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20190707194727&SearchText=BCM943602BAED+DW1830&switch_new_app=y) | [community](https://osxlatitude.com/forums/topic/11138-inventory-of-supportedunsupported-wireless-cards-2-sierra-catalina/) |


**Storage**

| NVMe | 4k Support | Amazon URL | Confirmation |
| ---: | :--- | :--- | :--- |
| ``Samsung EVO 970 NVMe`` | NO | [Amazon](https://www.amazon.com/gp/product/B07DB942BT/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1) | [community](https://www.tonymacx86.com) |
| ``Samsung EVO 970 Pro NVMe`` | NO | [Amazon](https://www.amazon.com/Samsung-PCI-Express-Solid-State-V-NAND/dp/B07DFJ3YQR/ref=sr_1_4?keywords=Samsung+970+EVO+Pro&qid=1560233808&s=electronics&sr=1-4) | [community](https://www.tonymacx86.com) |
| ``Samsung EVO 970 Plus NVMe`` | NO | [Amazon](https://www.amazon.com/Samsung-970-EVO-Plus-MZ-V7S1T0B/dp/B07MFZY2F2/ref=sr_1_3?keywords=Samsung+EVO+970+Plus+NVMe&qid=1561343834&s=gateway&sr=8-3) | [Do the Samsung 970 Evo Plus drives work ? New Firmware Available for testing 5/20/19](https://www.tonymacx86.com/threads/do-the-samsung-970-evo-plus-drives-work-new-firmware-available-for-testing-5-20-19.270757/page-13#post-1959914) |
| ``Sabrent Rocket NVMe`` | YES | [Amazon](https://www.amazon.com/gp/product/B07LGF54XR/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) | [stonevil](https://www.tonymacx86.com/members/stonevil.254235/) |
| ``WD Black SN750 NVMe`` | - | [Amazon](https://www.amazon.com/BLACK-SN750-500GB-Internal-Gaming/dp/B07MQ468S8/ref=sxin_3_ac_d_rm?keywords=wd%2Bblack%2Bnvme&pd_rd_i=B07MH2P5ZD&pd_rd_r=0be71a8a-a79d-4ce3-ad47-102a5ee16a25&pd_rd_w=9ZCWD&pd_rd_wg=dlFxu&pf_rd_p=0bc35c17-1e0d-4808-b361-20ab11b00973&pf_rd_r=0CKT4MYE9A5QZ8AJYEVK&qid=1560233421&s=gateway&th=1) | [community](https://www.tonymacx86.com) |
| ``HP EX900 M.2 NVMe`` | - | [Amazon](https://www.amazon.com/HP-EX900-Internal-Solid-5Xm46Aa/dp/B07MFBNMF1/ref=sr_1_3?keywords=HP+EX900+NVME+1TB+drive&qid=1561283379&s=gateway&sr=8-3) | [konohasaint](https://www.tonymacx86.com/members/konohasaint.88998/) |
| ``Samsung PM981`` | NO | Bundled with Razer Blade | [suyukai](https://www.tonymacx86.com/members/suyukai.2249983/) |

**Note: Bundled Samsung NVMe PM981 can be enabled with additional macOS Extension (kext) and (ACPI hot patch). More information in ``suyukai`` post [I find a way to use macOS on SSD(pm981) in blade!...](https://www.tonymacx86.com/threads/guide-razer-blade-15-2018-detailed-install-guide-high-sierra-10-13-6-17g2208-17g5019.264017/page-65#post-1969367)**

macOS have native support and works better with 4k blocks. Check **NVMe format**.
Performance tested with [Blackmagic Disk Speed Test](https://apps.apple.com/us/app/blackmagic-disk-speed-test/id425264550?mt=12). Samsung EVO 970 1Tb NVMe and Sabrent Rocket 1Tb NMVe have the same Read/Write performance. But Samsung EVO stays about 8-12° C hotter on heave load. Even with additional passive cooling.

**Note: I do recommend to use at least 1Tb NVMe for dual boot with Windows 10.**


**RAM**

| Memory module | Modules size | Speed | CL | Amazon URL | Confirmation |
| ---: | :--- | :--- | :--- | :--- | :--- |
| ``Ballistix Sport LT 32GB`` | 2x16Gb | 2666 | CL16 | [Amazon](https://www.amazon.com/gp/product/B06XRBS4Y5/ref=ppx_yo_dt_b_asin_title_o03_s00?ie=UTF8&psc=1) | [stonevil](https://www.tonymacx86.com/members/stonevil.254235/) |
| ``Kingston Technology HyperX Impact 32GB`` | 2x16Gb | 2666 | CL15 | [Amazon](https://www.amazon.com/dp/B01NAL3TYY/?coliid=I3Q9P4ZU9V435H&colid=1ZGSQH2G88154&psc=1&ref_=lv_ov_lig_dp_it) | [Razer Blade 15 Advanced RAM upgrade](https://www.reddit.com/r/razer/comments/c1c9wl/razer_blade_15_advanced_ram_upgrade/) |


**Recommended Upgrades**

| Accessories | Description | Amazon URL | Confirmation |
| ---: | :--- | :--- | :--- |
| ``Advancing Gene NVMe M.2 Heatsink`` | Passive cooling for NVMe. Decreased temperature for about 10-12° C on heave load | [Amazon](https://www.amazon.com/gp/product/B074Y5DZ4N/ref=ppx_yo_dt_b_asin_title_o04_s01?ie=UTF8&psc=1) | [stonevil](https://www.tonymacx86.com/members/stonevil.254235/) |


**Recommended Tools**

| Tool | URL |
| ---: | :--- |
| ``iFixIt Pro Tech Toolkit`` | [iFixIt](https://www.ifixit.com/Store/Tools/Pro-Tech-Toolkit/IF145-307?o=4) |


**(Optional) Extreme Upgrade only for Advance Gamers**

| Accessories | Description | Amazon URL |
| ---: | :--- | :--- |
| ``Thermal Grizzly Conductonaut Thermal Grease Paste`` | Liquid metal thermal paste | [Amazon](https://www.amazon.com/gp/product/B01A9KIGSI/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1) |
| ``MG Chemicals 422B Silicone Modified Conformal Coating`` | Coating | [Amazon](https://www.amazon.com/gp/product/B008O9YIV6/ref=ppx_yo_dt_b_asin_title_o01_s00?ie=UTF8&psc=1) |
| ``3M Scotch Super 88 Vinyl Electrical Tape`` | Electrical tape | [Amazon](https://www.amazon.com/3M-Scotch-Electrical-Dielectric-Strength/dp/B001DPXGSE/ref=sr_1_2_sspa?ie=UTF8&qid=1538036249&sr=8-2-spons&keywords=super+88&psc=1) |


**Useful information**

* [The Mainstream Phoenix Rises: Samsung's 970 EVO (500GB & 1TB) SSDs Reviewed - Power Management Features](https://www.anandtech.com/show/12670/the-samsung-970-evo-ssd-review/8)


Repository
---

``BIOS_mod/`` folder. This folder contains the latest RBA AMI BIOS mod with all the required unlocked options.

This BIOS mod is actual only for Razer Blade Advanced early 2019 with

| | Version |
| ---: | :--- |
| ``System BIOS`` | 1.05 |
| ``EC FW`` | 1.03 |
| ``MCU FW`` | 1.00.00.00 |

Do not use this mod if your system is different! Please check with BIOS.


``BIOS_mod/Nvidia_2080_Max-Q_BIOS_mod/`` this folder contains patches for 80w or 90w TDP for Nvidia 2080 Max-Q.


``EFI/`` folder is basically a full copy of my EFI folder from EFI drive with a removed machine serial number.

ACPI Patches

* ``EFI/CLOVER/ACPI/patched/DSDT.aml``
* ``EFI/CLOVER/ACPI/patched/SSDT-12-OptTabl.aml``
* ``EFI/CLOVER/ACPI/patched/SSDT-USBX.aml``

can be different for your computer.


``Extensions/`` folder with all required macOS Extensions (kext's).


``Tools/`` folder with various tools to flash BIOS, etc. macOS IORegistryExplorer v2.1 is included with this repository. This tool is necessary for debugging USB, etc. configuration.

``Tools/AMI/`` is a folder with AMI BIOS flashing and modding tools.
``Tools/Nvidia/`` is a folder with Nvidia BIOS flashing tools.


``Development/ACPI_patches/`` is a folder with uncompiled versions of the SSDT's created for various ACPI hot patches.

``Drivers/Windows/Apple USB Ethernet drivers for Windows`` is a folder with Apple USB-A Ethernet drivers for Windows extracted from ``Apple BootCamp``.


Required Tools
---

| Tool | Description | Download URL |
| ---: | :--- | :--- |
| ``balenaEtcher`` |  a free and open-source utility used for burning image files such as .iso and .img files, as well as zipped folders to create live SD cards and USB flash drives. | [balenaEtcher](https://www.balena.io/etcher/) |
| ``UniBeast`` | a tool for building macOS installation media | [UniBeast](https://www.tonymacx86.com/resources/kextbeast-2-0-2.399/) |
| ``TINU`` | an alternative tool for building macOS installation media | [TINU](https://github.com/ITzTravelInTime/TINU) |
| ``Clover Configurator`` | an easy to use macOS application designed to help you create custom configuration files for the Clover EFI bootloader via a streamlined graphical interface | [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) |
| ``KextBeast`` | a quick installer for .kext, .bundle, and .plugin files | [KextBeast](https://www.tonymacx86.com/resources/kextbeast-2-0-2.399/) |
| ``Continuity Activation Tool`` | is a tool that makes the changes necessary to enable Continuity features on compatible hardware | [Continuity Activation Tool](https://github.com/dokterdok/Continuity-Activation-Tool) |
| ``Kext Updater`` | this little tool is totally easy to have up-to-date kext's | [Kext Updater](https://www.insanelymac.com/forum/topic/334222-kext-updater-keep-your-kexts-fresh-with-only-one-click/) |
| ``MaciASL`` | a native AML compiler and IDE for OS X, with syntax colouring, tree navigation, automated patching, online patch file repositories, and iASL binary updates, written entirely in Cocoa, conforms to OS X guidelines | [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/) |
| ``iasl`` | -//- | [iasl](https://bitbucket.org/RehabMan/acpica/downloads/iasl.zip) |
| ``GenSMBIOS`` | a Py script that uses acidanthera's macserial to generate SMBIOS and optionally saves them to a plist | [GenSMBIOS Github Repository](https://github.com/corpnewt/GenSMBIOS) |
| ``one-key-cpufriend`` | a script for modifying macOS CPU Performance | [one-key-cpufriend Github Repository](https://github.com/stevezhengshiqi/one-key-cpufriend) |
| ``USBMap`` | a Py script for mapping out USB ports and creating a custom SSDT or injector kext (WIP) | [USBMap Github Repository](https://github.com/corpnewt/USBMap) |
| ``Intel Power Gadget`` | a software-based power usage monitoring tool enabled for Intel Core processors | [Intel Power Gadget](https://software.intel.com/en-us/articles/intel-power-gadget) |
| ``iStat Menus`` | an advanced Mac system monitor | [iStat Menus](https://bjango.com/mac/istatmenus/) |
| ``Prime95`` | a free Mersenne Prime search tool. Maybe, the best tool for CPU torture testing | [Prime95](https://www.mersenne.org/download/) |
| ``UNetbootin`` | this tool allows you to create bootable USB drives for Windows and Ubuntu and other Linux distributions without burning a CD. | [UNetbootin](https://unetbootin.github.io) |


Preparation
---

### BIOS update

It is very important to make all the updates for BIOS before starting any macOS deployment. ACPI sources will be different after BIOS update and this will require to dump ACPI sources and patch them again. And, that is not a pleasant task.

Download BIOS, EC, ME, etc. Firmware and apply them from stock Windows partition.

[Razer Hardware Drivers download URL](http://drivers.razersupport.com//index.php?_m=downloads&_a=view&parentcategoryid=864&pcid=860&nav=0,350,860)

* Boot into Windows.
* Open [Razer Hardware Drivers download URL](http://drivers.razersupport.com//index.php?_m=downloads&_a=view&parentcategoryid=864&pcid=860&nav=0,350,860) in preferred browser.
* Download the latest BIOS, EC, ME, etc. Firmware updates.
* Apply these updates in a required order. This is very important! Read documentation carefully.

**Useful information**

* [Razer Support Website](https://support.razer.com)


### BIOS unlock

Certain changes for the BIOS configuration should be done to make macOS bootable on the Razer Blade Advanced.

* Disable ``VT-d``. Apple stopped supporting this long time ago and will not boot in some cases with enabled ``VT-d``. Do not mistake ``VT-d`` for ``VMX`` or ``VTX``.
* Increase memory pre-allocated for ``DVMT``. Usually ``DVMT`` is pre-allocated for ``32Mb``. MacOS requires ``64Mb`` minimum.
* Deactivate ``CFG-Lock``. Required by macOS Power Management.
* Disable ``Secure Boot``.
* etc.

Some of these configurations can be fixed one or another way in ``Clover`` configuration file. But, it is better to play safe and change configuration in BIOS. Deactivation of the ``CFG-Lock`` can help a lot with power management.

If the BIOS is upgraded to the latest version and

| | Version |
| ---: | :--- |
| ``System BIOS`` | 1.05 |
| ``EC FW`` | 1.03 |
| ``MCU FW`` | 1.00.00.00 |

it's safely to use already modded dump from ``BIOS_mod/`` folder and jump to **BIOS flashing**.

Otherwise, follow the **BIOS export** step.


### BIOS export

* Boot into Windows.
* Download this repository.
* Open ``Tools\AMI\AfuWin64\`` folder.
* Run ``AFUWINGUIx64.EXE`` application.
* In ``AFUWINGUI`` application click ``Save`` button to export current BIOS.

![AFUWINGUI_Save](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/AFUWINGUI_Save.png)

* Save BIOS to ``Desktop`` folder.
* Close ``AFUWINGUI`` application.


### BIOS modding

Most of the options are required for further undervolting and overclocking. But, some of them are necessary for the macOS. These options are marked with **!**

* Open ``Tools\AMI\AMIBCP64\`` folder.
* Run ``AMIBCP64.exe`` application.
* In ``AMIBCP`` application click ``Open``, navigate to ``Desktop`` and open BIOS saved in previous steps.
* In ``AMIBCP`` application
	* Unfold root folder in the left pane. This folder is blank and have no name.
	* Unfold ``Setup`` subfolder.
	* Click ``Power & Performance`` subfolder.
		* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
			* ``Power & Performance`` (second row from top)
			* ``CPU - Power Management Control`` **!**
			* ``Intel(R) Speed Shift Technology``

![Power_Performance](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Power_Performance.png)

* Unfold ``CPU VR Settings``
* Click `` View/Configure CPU Lock Configuration`` folder in the left pane
* In right the pane, change ``Access/Use`` from ``Default`` to ``USER`` for
	* ``CFG Lock``
	* ``Overclocking Lock``

![CPU_VR_Settings](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/CPU_VR_Settings.png)

* Click ``CPU - Power Management Control`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``CPU - Power Management Control`` (second row from top) **!**
		* ``Intel(R) SpeedStep(tm)``
		* ``Intel(R) Speed Shift Technology``
		* ``C states``
		* ``Package C State Limit``
		* ``CPU Lock Configuration`` (scroll way down) **!**

![CPU_Power_Management_Control1](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/CPU_Power_Management_Control1.png)

![CPU_Power_Management_Control2](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/CPU_Power_Management_Control2.png)

* Click ``OverClocking Performance Menu`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``OverClocking Performance Menu`` (second row from top)
		* ``XTU Interface``
		*	``Processor``
		* ``Ring``
		* ``GT``
		* ``Uncore``
		* ``Memory``

![OverClocking_Performance_Menu](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/OverClocking_Performance_Menu.png)

* Unfold ``OverClocking Performance Menu`` subfolder.
* Click ``Processor`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``Processor`` (second row from top)
		* ``Core Voltage Offset``
		* ``Offset Prefix`` below ``Core Voltage Offset``

![Processor](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Processor.png)

* Click ``Ring`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``Ring`` (second row from top)
		* ``Ring Max OC Radio``
		* ``Ring Down Bin``
		* ``Min Ring Ratio Limit``
		* ``Max Ring Ratio Limit``

![Ring](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ring.png)

* Click ``GT`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``GT Domain`` (second row from top)
		* ``GT Voltage Offset``
		* ``Offset Prefix`` below ``GT Voltage Offset``
		* ``GTU Voltage Offset``
		* ``Offset Prefix`` below ``GTU Voltage Offset``

![GT](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/GT.png)

* Click ``Uncore`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``Uncore`` (second row from top)
		* ``Uncore Voltage Offset``
		* ``Offset Prefix`` below ``Uncore Voltage Offset``

![Uncore](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Uncore.png)

* Click ``Memory Overclocking Menu`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``Memory Profile`` (second row from top) **RAM XMP Profile**
		* ``Memory Profile`` (another one somewhere in the middle of the list) **RAM XMP profile**
		* ``Memory Reference Clock`` **RAM XMP Profile**
		* ``Memory Ratio`` **RAM XMP Profile**
		* ``Memory Voltage`` **RAM XMP Profile**

![Memory_Overclocking_Menu1](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Memory_Overclocking_Menu1.png)

![Memory_Overclocking_Menu2](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Memory_Overclocking_Menu2.png)

* Click ``Chipset`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``System Agent (SA) Configuration`` (second row from top) **!**

![Chipset](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Chipset.png)

* Unfold ``Chipset`` subfolder.
* Click ``System Agent (SA) Configuration`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``System Agent (SA) Configuration`` (second row from top) **!**
		* ``VT-d`` **!**
		* ``Graphics Configuration`` **!**
		* ``PEG Port Configuration``
		* ``VT-d`` (another one somewhere in the middle of the list) **!**

![System_Agent_Configuration](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/System_Agent_Configuration.png)

* Unfold ``System Agent (SA) Configuration`` folder in the left pane
* Click ``Graphics Configuration`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``Graphics Configuration`` (second row from top) **!**
		* ``Primary Display``
		* ``Internal Graphics``
		* ``DVMT Pre-Allocated`` **!**
		* ``DVMT Total Gfx Mem`` **!**

![Graphics_Configuration](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Graphics_Configuration.png)

* Click ``PEG Port Configuration`` folder in the left pane
	* In the right pane, change ``Access/Use`` from ``Default`` to ``USER`` for
		* ``PEG Port Configuration`` (second row from top)
		* ``ASPM``
		* ``ASPM L0s``

![PEG_Port_Configuration](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/PEG_Port_Configuration.png)

* Click ``Save As`` in ``AMIBCP`` application.
* Save BIOS with new name to ``Desktop`` folder.
* Close ``AMIBCP`` application.


### BIOS flashing

* Open ``Tools\AMI\AfuWin64\`` folder.
* Run ``AFUWINGUIx64.EXE`` application.
* In ``AFUWINGUI`` application click ``Open`` button.
* Choose new modded BIOS from ``Desktop`` folder.
* Close all application except ``AFUWINGUI``. Close also all Windows TaskBar apps like Nvidia Expierence, Razer, etc.
* Click ``Flash`` button in ``AFUWINGUI`` application and confirm flashing BIOS.

![AFUWINGUI_Flash](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/AFUWINGUI_Flash.png)

* Follow ``AFUWINGUI`` application on-screen instruction.
* Close ``AFUWINGUI`` application.
* Reboot Windows.

**Useful information**

* [Razer Blade 2017 Ultimate CPU GPU Optimization - Unleashed Performance - BIOS Unlock](https://www.youtube.com/watch?v=O5CvK7i9a_Y)


### BIOS configuration

There are a few changes in the BIOS that are vital to make macOS happy and bootable on RBA. Undervolting and Overclocking are explained in the following chapter.

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


**Note: If some of these options are not available in BIOS, please, boot back in Windows and check modded BIOS dump for missing changes.**


Hardware preparation
---

### WiFi and NVMe replacement

WiFi and NVMe replacement is easy enough for this Model. You just need to unscrew the bottom case. Check the video provided below for more information.

**Useful information**

* [How to Upgrade the Razer Blade 15 RAM & SSD](https://www.youtube.com/watch?v=6TZih3m0-Ys)
* [Razer Blade Advanced RTX 2070 SSD Replacement](https://www.youtube.com/watch?v=9-ZfDNdj2WU)
* [INVENTORY OF SUPPORTED/UNSUPPORTED WIRELESS CARDS #2, SIERRA -> CATALINA](https://osxlatitude.com/forums/topic/11138-inventory-of-supportedunsupported-wireless-cards-2-sierra-catalina/)


### (Optional) NVMe format with 4k block

This step is optional. MacOS works faster and better with NVMe with 4k blocks. Usually NVMe formatted with 512 or 512e block size for unknown reason. Maybe another Windows compatibility issue. Anyway, Windows 10 works with no issues with NVMe with 4k blocks.

The best way to format NVMe drive is to boot from Linux Live USB media and use ``smartctl`` and ``nvme-cli`` tools.

* Download [balenaEtcher](https://www.balena.io/etcher/) on Windows or macOS machine.
* Download [Ubuntu Desktop Live Image](https://ubuntu.com/download/desktop) on same Windows or macOS machine.
* Insert USB media with at least 16Gb. Drive will be formatted and all data will be erased.
* Run ``balenaEtcher``
* Select image ``Ubuntu Desktop Live Image`` downloaded before.

![balenaEtcher_Select_Image](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/balenaEtcher_Select_Image.png)

* Select USB media.

![balenaEtcher_Select_Media](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/balenaEtcher_Select_Media.png)

* And press ``Flash!``.

![balenaEtcher_Flash](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/balenaEtcher_Flash.png)

**Note: Ubuntu lacks the support by default drivers for most Broadcom WiFi modules.**

There are 3 way to overcome this issue:

* Use ``USB to Ethernet`` cable.
* Install proprietary WiFi drivers installation. Follow this instruction [WifiDocs/Driver/bcm43xx](https://help.ubuntu.com/community/WifiDocs/Driver/bcm43xx)

| Accessories | Description | Amazon URL |
| ---: | :--- | :--- |
| ``USB to Ethernet`` | Internet access | [AmazonBasics USB 3.0 to 10/100/1000 Gigabit Ethernet](https://www.amazon.com/AmazonBasics-1000-Gigabit-Ethernet-Adapter/dp/B00M77HMU0/ref=sr_1_8?crid=3KJ7TSXIVKNO6&keywords=apple+usb+to+ethernet+adapter&qid=1561713591&s=gateway&sprefix=Apple+USB+to+Eth%2Caps%2C247&sr=8-8) |

* Install a new NVMe drive in the target Razer Blade.
* Insert USB media with ``Ubuntu Desktop``.
* Press ``Power Button`` to start computer.
* Press repeatedly ``F12`` until you ``Boot Menu`` will show.
* Select USB media with ``Ubuntu Desktop``.
* Select ``Try Ubuntu without installation``
* When ``Ubuntu`` starts connect computer to the Internet. This can be done from the WiFi menu in the top right corner.

![Ubuntu_Show_Applications](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Show_Applications.png)

* Click on the bottom left button and type ``Terminal`` and press ``Enter``.

![Ubuntu_Terminal](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Terminal.png)

* In ``Terminal`` application type

```
sudo apt -y install smartmontools
```

![Ubuntu_Install_smartmontools](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_smartmontools.png)

* and press Enter.
* In ``Postfix Configuration`` window select ``No configuration`` with ``Up/Down`` arrow keys and press ``Enter``.

![Ubuntu_Install_smartmontools_postfix](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_smartmontools_postfix.png)

* In ``Terminal`` application type

```
sudo apt -y install nvme-cli
```

* and press Enter.

![Ubuntu_Install_nvme_cli_fail](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_nvme_cli_fail.png)

* If previous command fails with error ``E: Unable to locate package nvme-cli`` use this URL [http://mirrors.kernel.org/ubuntu/pool/universe/n/nvme-cli/nvme-cli\_0.5-1\_amd64.deb](http://mirrors.kernel.org/ubuntu/pool/universe/n/nvme-cli/nvme-cli_0.5-1_amd64.deb) to install ``nvme-cli`` on Ubuntu.

![Ubuntu_Install_nvme_cli_url](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_nvme_cli_url.png)

![Ubuntu_Install_nvme_cli_url_open_with1](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_nvme_cli_url_open_with1.png)

![Ubuntu_Install_nvme_cli_url_open_with2](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_nvme_cli_url_open_with2.png)

![Ubuntu_Install_nvme_cli_url_open_with3](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_nvme_cli_url_open_with3.png)

![Ubuntu_Install_nvme_cli_url_open_with4](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_nvme_cli_url_open_with4.png)

* Click on a download button on the top right ``Firefox`` window corner.
* Click on the downloaded package and click ``Open``.
* In the installer window click ``Install`` button.

![Ubuntu_Install_nvme_cli_window](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_nvme_cli_window.png)

* Verify your NVMe to be recognized and manage 4K blocs by typing this command in ``Terminal`` window

```
sudo smartctl -a /dev/nvme0
```

* and press ``Enter``

![Ubuntu_Run_smartctl](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Run_smartctl.png)

* You should have two lines under ``Supported LBA sizes`` one with data ``512B`` starting with ID ``0``
one with data ``4K`` starting with ID ``1``.

![Ubuntu_Run_smartctl_result](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Run_smartctl_result.png)

* If ``4K`` is absent, NVMe does not support 4k blocks. Reboot computer and follow **macOS install media preparation**.
* Usually NVMe formatted to ``512B``. And this ``512B`` will be marked with asterix ``*``.
* Format the NVME with ``4K`` blocs with the command

```
sudo nvme format -l 1 /dev/nvme0
```

* and press ``Enter`` and follow on-screen instructions.

![Ubuntu_Install_nvme_format](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Ubuntu_Install_nvme_format.png)

* This command will erase all the information on the NVMe drive.
* To verify that the LBA 4K size is properly selected re-type the ``smartctl`` command

```
sudo smartctl -a /dev/nvme0
```

**Useful information**

* [Ubuntu WifiDocs/Driver/bcm43xx](https://help.ubuntu.com/community/WifiDocs/Driver/bcm43xx)
* [nvme-cli](https://github.com/linux-nvme/nvme-cli)
* [nvme-cli package in Ubuntu](https://launchpad.net/ubuntu/+source/nvme-cli)
* [smartmontools](https://www.smartmontools.org)
* [Gilles 4k NVMe format procedure](https://forums.macrumors.com/attachments/gilles-4k-nvme-foramt-procedure-pdf.763884/)


### (Optional) Liquid Metal re-paste

**Be very careful and do this at your OWN RISK!**

This step is not necessary and can be recommended only for hardcore gamers with experience of building their own rigs. Razer is already using very good thermal paste, so re-pasting thermal paste is not very useful until liquid metal is used. The ``Grizzly Conductonaut Thermal Grease Paste`` may be the best one. Read more about liquid metal thermal paste and all the issues it can cause before making the decision to proceed.

**Useful information**

* [Razer Blade 15 Advanced Liquid Metal Repaste](https://www.youtube.com/watch?v=tGQLaFqQvOw)
* [Grizzly Liquid Metal'd my 2018 Razer Blade 15 1060](https://www.youtube.com/watch?v=7xK4SjOra1E)


macOS
---

### macOS install media preparation

Use you own OR borrow some friend Mac computer.

* On macOS, download ``UniBeast`` OR ``TINU`` up to your preferences.
* Run ``UniBeast`` OR ``TINU`` application.
* Follow the instruction and build macOS installation media macOS 10.14 Mojave. It is very important to build media with the latest available version of Mojave.
* Copy this applications and the files to the USB installation media
	* ``Clover Configurator``
	* ``KextBeast``
	* ``MaciASL``
	* ``iasl``
	* This repository ZIP archive.

**Useful information**

* [UniBeast: Install macOS Mojave on Any Supported Intel-based PC](https://www.tonymacx86.com/threads/unibeast-install-macos-mojave-on-any-supported-intel-based-pc.259381/)
* [TINU](https://github.com/ITzTravelInTime/TINU)


### macOS installation

* Insert the macOS USB install media.
* Boot/Reboot computer.
* Press repeatedly ``F12`` until you ``Boot Menu`` will show.
* Select the macOS USB install media.
* Open ``Disk Utility`` from ``Tools`` menu.
* Format NVMe to ``APFS``.
* Follow usual macOS installation procedure.
* After reboot repeatedly tap ``F12`` again until get ``Boot Menu``.
* Select macOS USB install media again to boot in ``Clover``.
* In ``Clover``, select NVMe drive to continue installation.
* Repeat this procedure again when macOS reboots the computer.
* Follow the usual macOS installation procedure.
* You can use TimeMachine Backup restore procedure during macOS installation.

**Note: Do not try to connect the computer with iCloud before you generate proper SMBIOS! This step is explained in the 'iCloud. iMessages and FaceTime' step.**

**Useful information**

* [UniBeast: Install macOS Mojave on Any Supported Intel-based PC](https://www.tonymacx86.com/threads/unibeast-install-macos-mojave-on-any-supported-intel-based-pc.259381/)


### Install EFI and Extensions

Once the macOS installation is finished:

* Login with the user with admin privileges: usually, the first one created during the installation procedure.
* Run ``Clover Configurator`` application from the USB installation media.
* From ``Mount EFI`` on the left side mount NVMe EFI partition.
* Copy this repository ZIP archive file to ``~/Desktop/``.
* Unarchive this repository Zip archive file on ``~/Desktop/``.
* Copy the folder ``EFI`` from unpacked archive to previously mounted ``EFI`` partition.
* If you have different version of Razer Blade, please remove files listed below from ``EFI`` partition, otherwise this can cause kernel panic or other issues
	* ``EFI/CLOVER/ACPI/patched/DSDT.aml``
	* ``EFI/CLOVER/ACPI/patched/SSDT-12-OptTabl.aml``
	* ``EFI/CLOVER/ACPI/patched/SSDT-USBX.aml``
* Copy all ``.kext`` files from the folder ``Extensions`` from previously unpacked archive to the ``~/Desktop/`` folder. Do not copy ``CPUFriendDataProvider.kext`` if you have different version of Razer Blade! 
* Run ``KextBeast.pkg`` application from the USB installation media.
* Click ``Continue`` and click ``Agree``.
* Select ``/Library/Extensions`` and click ``Continue``.
* Click ``Install``.
* If extensions are installed without any issues run ``Terminal`` application from the ``/Applications/Utilities`` folder.
* In ``Terminal`` application window type

```
sudo kextcache -i /
```

* and press ``Enter``.
* When command ``kextcache`` finish execution, unmount and detach the macOS USB installation media, and reboot computer to apply new configuration.
* Repeatedly press ``DEL`` key to enter BIOS configuration menu.
* In BIOS, navigate to menu
	* ``Boot``
		* Set ``Boot Option #1`` to ``UEFI OS (drive_name)``
		* Set ``Boot Option #2`` and all next ``Boot Option #`` to ``Disabled``
	* ``Save and Exit``
		* Hit ``Save Changes``
		* Hit ``Save Changes and Reset``
* Computer should boot ``Clover`` and show ``Clover Boot Menu``.
* If you have same Razer Blade Model trackpad, battery status, audio should become available.


If you have the same Razer Blade model, you are safe to jump to step **iCloud. iMessages and FaceTime**. Otherwise, you need to generate custom ACPI hot patches and USB mapping specific to your Razer Blade model.


### Disable Hibernation

Hibernation does not work correctly with the majority of hackintosh notebooks anyway.

* Run ``Terminal`` application from ``/Applications/Utilities/`` folder.
* To disable ``hibernation`` type and execute this command in ``Terminal`` application window

```
sudo pmset -a hibernatemode 0
```

* To remove ``hibernation`` ``sleepimage`` type and execute this command in ``Terminal`` application window

```
sudo rm /var/vm/sleepimage
```

* To prevent create ``hibernation`` ``sleepimage`` in future type and execute this command in ``Terminal`` application window

```
sudo mkdir /var/vm/sleepimage
```

### Tweak Energy Saver

* Open ``System Preferences``.
* Click ``Energy Saver``.
* Click tab ``Power Adapter``.

![System_Preferences](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/System_Preferences.png)

* Disable ``Wake for Wi-Fi network access``.
* Disable ``Enable Power Nap while plugged into a power adapter``.

![System_Preferences_Energy_Saver](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/System_Preferences_Energy_Saver.png)


### ACPI patching

If you have a little bit different version of Razer Blade (just like mid 2019 Model OR Base Model OR different version of BIOS) the ACPI and USB patches will not be compatible with you Razer Blade!

In this case, ACPI hot patches should be created from scratch.

Again, it is very important to apply all BIOS patches, firmware updates before this step (!).


**ACPI export**

* Reboot computer.
* In ``Clover Boot Menu`` press ``F2`` and ``F4``.
* Repeat again with ``fn``+``F2`` and ``fn``+``F4``.
* Select normal macOS boot.


**DSDT patching for battery, trackpad**

* Login with the user with admin privileges: usually the first one created during installation procedure.
* Run ``Clover Configurator`` and mount NVMe ``EFI`` partition.
* Navigate to folder ``/Volumes/EFI/EFI/CLOVER/ACPI/``.
* Copy folder ``origin`` to ``Desktop`` folder.
* Copy ``MaciASL`` from the macOS USB installation media or re-download from Internet to ``~/Applications/`` folder.
* Copy ``iasl`` from the macOS USB installation media or re-download from Internet to.
* Unpack ``iasl.zip`` if required.
* Run ``Terminal`` application from ``/Applications/Utilities/`` folder.
* Copy ``iasl`` from ``~/Downloads/`` folder to ``/usr/local/bin/`` folder with command in ``Terminal`` application

```
sudo cp ~/Downloads/iasl /usr/local/bin/
```

* Navigate to ``~/Desktop/origin/`` folder in ``Terminal`` application with command ``cd ~/Desktop/origin/``.
* Disassembling ``.aml`` files with command in ``Terminal`` application

```
/usr/local/bin/iasl -da -dl DSDT.aml SSDT*.aml
```

* Run ``MaciASL`` application and open file ``~/Desktop/origin/DSDT.dsl``.
* Click ``Patch`` button in ``toolbar``.
* In ``Patch`` window on left panel scroll and find ``[bat] Razer Blade (2014)`` and click ``Apply``. Do not close window!
* In ``Patch`` window on the left panel, scroll and find ``[gfx0] Disable/Enable on _WAK/_PTS (DSDT)`` and click ``Apply``. Do not close the window!
* Click ``Close`` in ``Patch`` window.
* Click ``Compile`` button in ``toolbar``. ``DSDT`` should be compiled without any issues.
* Next step is hot patch DSDT for trackpad.
* Hit ``Command+F`` for ``Search`` and search for method ``SSCN`` in scope ``Scope (_SB.PCI0.I2C0)`` lines like below.

```
Method (SSCN, 0, NotSerialized)
{
    Return (PKG3 (SSH0, SSL0, SSD0))
}

Method (FMCN, 0, NotSerialized)
{
    Return (PKG3 (FMH0, FML0, FMD0))
}
```

* Copy this block
* Rename this methods to something like this:

```
Method (_SCN, 0, NotSerialized)
{
    Return (PKG3 (SSH0, SSL0, SSD0))
}

Method (_MCN, 0, NotSerialized)
{
    Return (PKG3 (FMH0, FML0, FMD0))
}
```

* Find a code like this:

```
Scope (_SB.PCI0.I2C0)
    {
        Name (I2CN, Zero)
        Name (I2CX, Zero)
        Method (_INI, 0, NotSerialized)  // _INI: Initialize
        {
            Store (SDS0, I2CN)
            Store (Zero, I2CX)
        }
        
        Device (TPD0)
```

* Above line ``Device (TPD0)`` paste the previously copied code. The result should look like this:

```
Scope (_SB.PCI0.I2C0)
    {
        Name (I2CN, Zero)
        Name (I2CX, Zero)
        Method (_INI, 0, NotSerialized)  // _INI: Initialize
        {
            Store (SDS0, I2CN)
            Store (Zero, I2CX)
        }

        Method (SSCN, 0, NotSerialized)
        {
            Return (PKG3 (SSH0, SSL0, SSD0))
        }

        Method (FMCN, 0, NotSerialized)
        {
            Return (PKG3 (FMH0, FML0, FMD0))
        }
        
        Device (TPD0)
```

* Scroll down to method ``_CRS`` for scope ``_SB.PCI0.I2C0``. It should look like this:

```
Method (_CRS, 0, NotSerialized)  // _CRS: Current Resource Settings
{
    If (LLess (OSYS, 0x07DC))
    {
        Return (SBFI)
    }

    If (LEqual (TPDM, Zero))
    {
        Return (ConcatenateResTemplate (I2CM (I2CX, BADR, SPED), SBFG))
    }

    Return (ConcatenateResTemplate (I2CM (I2CX, BADR, SPED), SBFI))
}
```

* And replace with:

```
Method (_CRS, 0, NotSerialized)  // _CRS: Current Resource Settings
{
    Return (ConcatenateResTemplate (I2CM (I2CX, BADR, SPED), SBFG))
}
```

* Click ``Compile`` button in ``toolbar``. ``SSDT-12-OptTabl`` should be complied without any issues.
* Choose ``Save`` from ``File`` menu.
* Choose ``Save As…`` from ``File`` menu.
* Down below in ``Save`` window select ``ACPI Machine Language Binary`` from ``File Format:`` menu.
* Save this file as ``DSDT.aml``. ``MaciASL`` application will recommend the file name automatically.
* Copy the newly created file ``DSDT.aml`` to ``/Volumes/EFI/EFI/CLOVER/ACPI/patched/``

** GPIO Pinning (Optional) (Must Restart after previous DSDT patches) **

* Finding hexadecimal APIC pin number
* Download [IORegistryExplorer](https://www.tonymacx86.com/threads/guide-how-to-make-a-copy-of-ioreg.58368/)
* Open IORegExplorer and search for TPD0
* Open IOInterruptSpecifiers (If you don't see a IOInterruptSpecifiers you didn't reboot after previous DSDT patches)
![IORegExplorer](https://github.com/Pauldg7/Razer_Blade_Advanced_early_2019_Hackintosh/blob/master/images/ioreg_pin_situation.png)
* Write down the first two numbers from the Value column as 0xXX (in the example the APIC Pin number is 0x33)
* Write down the label of form GPP_XYY_IRQ by searching up the APIC pin number on [Cannon Point-H Labels](https://github.com/coreboot/coreboot/blob/master/src/soc/intel/cannonlake/include/soc/gpio_defs_cnp_h.h#L42)
* Write down the decimal GPIO pin number by searching the label on [Cannon Point-H Decimal Pin Numbers](https://github.com/coreboot/coreboot/blob/master/src/soc/intel/cannonlake/include/soc/gpio_soc_defs_cnp_h.h#L40)

* Find the method ``_CRS`` from before and change to

```
Method (_CRS, 0, NotSerialized) // _CRS: Current Resource Settings
{
    Return (ConcatenateResTemplate(SBFB, SBFG))
}
```

Next step is hot patch ACPI to disable Nvidia GPU in macOS for saving battery and decreasing the overall heat.

**Nvidia GPU disable**

* Open ``SSDT-12-OptTabl.dsl`` with ``MaciASL`` application.

* Find this header:

```
\_SB.PCI0.PEG0.PEGP and expand it, click on _OFF
```

* Find this line of code:

```
Method (_OFF, 0, Serialized) // _OFF: Power Off
```

* Above the code, paste this line of code:

```
Method (_INI) {_OFF() } // added to call _OFF
```

* Once that is pasted in, click on the ``Patch`` button in ``toolbar`` and copy and paste this code into the ``Patch`` window:

```
into method label _INI parent_label \_SB.PCI0.GFX0 insert

begin

//added to turn nvidia/radeon off\n

External(\_SB.PCI0.PEG0.PEGP._OFF, MethodObj)\n

\n

end;
```

* Close the ``Patch`` window.
* Click ``Compile`` button in ``toolbar``.
* If ``SSDT-12-OptTabl.dsl`` is compiled without any issues skip to next patch. If compilation failed with error:

```
[Unknown ASL Compiler exception ID] (TGPC [Integer])
```

* Hit ``Command+F`` for ``Search``, search for a line like below and delete this line.

```
External (_SB_.PCI0.PEG0.TGPC, IntObj)    // (from opcode)
```

* Now, ``SSDT-12-OptTabl.dsl`` should be compiled without any issues.
* Click ``Patch`` button in ``toolbar``.
* Click ``Close`` in ``Patch`` window.
* Click ``Compile`` button in ``toolbar``. ``SSDT-12-OptTabl.dsl`` should be compiled without any issues.
* Choose ``Save`` from ``File`` menu.
* Choose ``Save As…`` from ``File`` menu.
* Down below in ``Save`` window select ``ACPI Machine Language Binary`` from ``File Format:`` menu.
* Save this file as ``SSDT-12-OptTabl.aml``. ``MaciASL`` application will recommend this file name automatically.
* Copy newly created file ``SSDT-12-OptTabl.aml`` to ``/Volumes/EFI/EFI/CLOVER/ACPI/patched/`` 

**Useful information**

* [Slave address not acknowledged in new ELAN devices](https://github.com/alexandred/VoodooI2C/issues/171#issuecomment-485423537)
* [Patching LAPTOP DSDT/SSDTs](https://www.tonymacx86.com/threads/guide-patching-laptop-dsdt-ssdts.152573/)
* [Native Power Management for Laptops](https://www.tonymacx86.com/threads/guide-native-power-management-for-laptops.175801/)
* [Quick Guide to Generate a SSDT for CPU Power Management](https://www.tonymacx86.com/threads/quick-guide-to-generate-a-ssdt-for-cpu-power-management.177456/)
* [Generate SSDT For Coffee Lake CPU](https://www.tonymacx86.com/threads/guide-generate-ssdt-for-coffee-lake-cpu.238311/)


### USB mapping

**Required Accessories**

| Device | USB version | USB connection type |
| ---: | :--- | :--- |
| Any | 2.0 | USB-A |
| Any | 3.0 | USB-A |
| Any | 3.x | USB-C |
| Cable |  USB-A to USB-C cable [Amazon](https://www.amazon.com/AmazonBasics-Type-C-Gen1-Female-Adapter/dp/B01GGKYXVE/ref=pd_hpb_a2a_sims_6/130-2479265-2893400?_encoding=UTF8&pd_rd_i=B01GGKYYT0&pd_rd_r=54b9f737-919c-11e9-b9d7-6915ce2a8dc3&pd_rd_w=j9bw6&pd_rd_wg=IVvh1&pf_rd_p=bfc589eb-d865-496f-a10b-5e00902c2113&pf_rd_r=G68JVK6HBAFKEDA75MYY&refRID=G68JVK6HBAFKEDA75MYY&th=1) | USB-C |

* Download ``USBMap`` repository.
	* [USBMap repository URL](https://github.com/corpnewt/USBMap)
	* Read [USBMap README](https://github.com/corpnewt/USBMap/blob/master/README.md) carefully.
* Open ``USBMap`` folder in Terminal.app OR iTerm.app if you prefer this one.
* Make ``USBMap.command`` executable with ``chmod +x USBMap.command``.
* Detach all the USB devices from the Razer Blade.
* Run ``USBMap.command`` with ``./USBMap.command``.

```
  #######################################################
 #                      USBMap                         #
#######################################################

Plist:          USB.plist
UIA Boot Args:  None
USBInjectAll:   Not Loaded - NVRAM boot-args WILL NOT WORK
AptioMemoryFix: Loaded

NVRAM Arg Options:
  E. Apply Exclusion-Arg.txt
  H. Exclude HSxx Ports (-uia_exclude_hs)
  S. Exclude SSxx Ports (-uia_exclude_ss)
  C. Clear Exclusions

R.  Remove USB.plist from Scripts Folder
T.  Reset Settings to Defaults
P.  Edit Plist & Create SSDT/Kext
D.  Discover Ports
U.  Validate USB Power Settings
Q.  Quit

Please select an option:
```

* Press ``U`` to ``Validate USB Power Settings``.
* Command will show something like this:

```
  #######################################################
 #           Validating USB Power Settings             #
#######################################################

Checking EC
 - EC is properly setup
Checking USBX requirements
 - MacBookPro15,2 not found in IOUSBHostFamily.kext - checking for USBX
 --> USBX device found: USBX@0

EC Setup Properly:   True
USBX Setup Properly: True

Press [enter] to return
```

* If command asks required confirm to install ``USBX``.
* Press ``Q`` to go back to the main screen.
* Press ``P`` to get to the ``Edit Plist & Create SSDT/Kext`` screen.
* Press ``T`` to get the list of USB types. It will be useful.

```
  #######################################################
 #                     USB Types                       #
#######################################################

0: Type A connector
1: Mini-AB connector
2: ExpressCard
3: USB 3 Standard-A connector
4: USB 3 Standard-B connector
5: USB 3 Micro-B connector
6: USB 3 Micro-AB connector
7: USB 3 Power-B connector
8: Type C connector - USB2-only
9: Type C connector - USB2 and SS with Switch
10: Type C connector - USB2 and SS without Switch
11 - 254: Reserved
255: Proprietary connector

Per the ACPI 6.2 Spec.

Press [enter] to return
```

* Press ``Enter`` to return to the ``Edit Plist & Create SSDT/Kext`` screen.
* Press ``M`` to return to the ``Main`` screen.
* Press ``D`` to ``Discover Ports``.
* If all USB devices are removed and detached properly, ``USBMap`` will show the list of internal USB devices such as Bluetooth, Integrated Camera, Razer Blade.

```
 #######################################################
 #                  Detecting Ports                    #
#######################################################

1. HS01 - Controller XHC
2. HS02 - Controller XHC
3. HS03 - Controller XHC
4. HS05 - Controller XHC
    - BCM20702A0
5. HS06 - Controller XHC
6. HS07 - Controller XHC
    - Integrated Camera
7. HS08 - Controller XHC
    - Razer Blade
8. HS09 - Controller XHC
9. HS10 - Controller XHC
10. HS11 - Controller XHC
11. HS13 - Controller XHC
12. HS14 - Controller XHC
13. SS01 - Controller XHC
14. SS02 - Controller XHC
15. SS03 - Controller XHC

Populated:  XHC:3

Press Q then [enter] to stop

Waiting 5 seconds:
```

* Write down the USB port identifications for the internal USB devices. This information will be required later to properly setup the USB type to properly enable a sleep mode. For RBA early 2019, it will be like this:
	* HS05 - Controller XHC - Bluetooth
	* HS07 - Controller XHC - Integrated Camera
	* HS08 - Controller XHC - Razer Blade
* You will need to mark these ports like ``255`` later.
* Detect properly ``USB 2.0`` ports.
	* Insert in every ``USB-A`` port for 15-20sec and detach ``USB 2.0`` (!) device. Command will highlight the newly detected ports with colour.
	* Write down the ports number.
* Detect properly ``USB 3.0`` ports.
	* Insert in every ``USB-A`` port for 15-20sec and detach ``USB 3.0 or 3.1`` (!) device. Command will highlight the newly detected ports with colour.
	* Write down the ports number.
* Detect properly ``USB-C`` ports.
	* Insert ``USB-C`` device into ``USB-C`` port for 15-20sec and detach. Command will highlight the newly detected ports with colour.
	* Write down the ports number.
	* Insert ``USB-A 2.0`` device into ``USB-C`` port with ``USB-A to USB-C`` cable for 15-20sec and detach. Command will highlight the newly detected ports with colour.
	* Write down the ports number.
* When ports are detected, press ``Q`` to go back to the ``Main`` screen.
* In the ``Main`` screen, press ``P`` to open ``Edit Plist & Create SSDT/Kext`` screen.
* All ports will be automatically marked like ``Type 3`` ports.
* Mark internal ports like ``Type 255``. This is very important to enable a sleep mode. Without this computer will wake up every 20-40secs even with the lid closed.
* Here, there are tips how to do this:

```
Select ports to toggle with comma-delimited lists (eg. 1,2,3,4,5)
Change types using this formula T:1,2,3,4,5:t where t is the type
Set custom names using this formula C:1:Name - Name = None to clear
```

* You can do this with a command. For example:

```
T:4,6,7:255
```

* Next you need to mark properly ``Type`` for ``USB-C``.
	* In my case ``SS03`` is ``Type 9``.
	* And ``SS03`` is ``USB 2.0`` ``Type 8``.
* Next is to build and install ``USBMap.kext``.
* Press ``K`` to execute ``Build USBMap.kext``.

```
  #######################################################
 #               Creating USBMap.kext                  #
#######################################################

Loading plist
Generating Info.plist
Writing to USBMap.kext
 - Created USBMap.kext!
Checking EC
 - EC is properly setup
Checking USBX requirements
 - MacBookPro15,2 not found in IOUSBHostFamily.kext - checking for USBX
 --> USBX device found: USBX@0

Created the following file:

USBMap.kext

Copy automatically to booted EFI? (y/n):
```

* Confirm to install ``USBMap.kext`` automatically.
* Press ``Q`` to ``Quit`` command.
* Reboot computer.

Verify configuration by inserting ``USB 2.0`` and ``USB 3.0`` and ``USB-C`` devices just like during detecting procedure. Also, close the lid and turn over notebook. After 20-60sec, depending on the current load, fans should stop rotating. Wait for another 3-5min. They shouldn't start spinning again. If they start and stop after 10-20sec, you have done something wrong and need to start the procedure again.

**Useful information**

* [USBMap](https://github.com/corpnewt/USBMap)
* [A Beginner's Guide to Creating a Custom USB SSDT](https://www.tonymacx86.com/threads/a-beginners-guide-to-creating-a-custom-usb-ssdt.272505/)
* [Creating a Custom SSDT for USBInjectAll.kext](https://www.tonymacx86.com/threads/guide-creating-a-custom-ssdt-for-usbinjectall-kext.211311/)


### iCloud. iMessages and FaceTime

Follow the instruction in the article [An iDiot's Guide To iMessage](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/).

**Useful information**

* [An iDiot's Guide To iMessage](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/)


### FileVault

This step is optional, but highly recommended from the security standpoint.

* Make sure you have full TimeMachine or clone backup. Some mistakes done during this procedure can make your drive and the data inaccessible!
* Make sure you have prepared macOS installation media in the worst case scenario.
* Do recommend to use
	* [Apple TimeMachine](https://support.apple.com/en-us/HT201250) backup or
	* [SuperDuper](https://www.shirt-pocket.com/SuperDuper/SuperDuperDescription.html)
* Make sure the required ``drivers`` are installed.
	* ``AptioInputFix-64`` for Bluetooth keyboard and mouse.
	* ``AppleKeyAggregator-64`` for PS/2 keyboard and mouse.
* Make sure the ``Preboot`` volume is not hidden in ``Clover Configurator``.
	* Open ``/Volumes/EFI/EFI/CLOVER/config.plist`` with ``Clover configurator`` application.
	* Open ``Gui`` section.
	* Remove ``Preboot`` volume from ``Hide Volume`` in the top right corner.
	* Hit ``Command+S`` to save configuration.

![Clover_Preboot](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Clover_Preboot.png)

* Open ``System Preferences…`` and ``Security & Privacy`` and ``FileVault`` tab.
	* Click lock to unlock ``System Preferences``.
	* Click ``Turn On FileVault…``.
	* It will take time… Depending on the drive size and a number of files, this can take up to 12h. So, be patient.

![System_Preferences_FileVault_Locked](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/System_Preferences_FileVault_Locked.png)

![System_Preferences_FileVault_Unlocked](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/System_Preferences_FileVault_Unlocked.png)

* Reboot computer.
* At the ``Clover`` screen, make sure you select the ``FileVault`` ``Preboot`` option of NVMe drive.
* Login prompt should appear.
* Keyboard should work without any issues.
* If keyboard does not work, maybe, additional drivers are required. Boot from macOS USB installation media and fix ``Clover`` boot configuration.
* Enter credentials.
* macOS should continue to boot.

**Useful information**

* [Turning on FileVault on your Hackintosh](https://davejansen.com/turning-on-filevault-on-your-hackintosh/)


Power Management
---

**BIOS tweak**

* Reboot computer.
* Repeatedly press ``DEL`` key to enter BIOS configuration menu.
* In BIOS navigate to menu
	* ``Advanced``
		* ``Power & Performance``
		* Enable ``Intel(R) Speed Shift Technology``
			* ``CPU - Power Management Control``
				* Enable ``Intel(R) SpeedStep(tm)``
				* Enable ``Intel(R) Speed Shift Technology``
			* ``CPU Lock Configuration``
				* Disable ``CFG Lock``
				* Disable ``Overclocking Lock``
		* ``Memory``
			* Set ``Memory Profile`` to the best for installed memory. Usually something like ``XMP profile 1``. 
	* ``Save and Exit``
		* Hit ``Save Changes``
		* Hit ``Save Changes and Reset``

**CPUFriendDataProvider**

* Login with the user with admin privileges: usually, the first one created during the installation procedure.
* Download [One Key CPUFriend](https://github.com/stevezhengshiqi/one-key-cpufriend) Github repository ZIP archive.
* Unpack downloaded ZIP archive.
* Run ``Terminal`` application.
* Change folder in ``Terminal`` application to unpack ZIP archive folder with command like this:

```
cd ~/Download/one-key-cpufriend-master
```

* In ``Terminal`` applications window, type the execute command:

```
./one-key-cpufriend.sh
```

* Command will show something like this:

```
-----------------------------------------
|****** Choose Low Frequency Mode ******|
-----------------------------------------
(1) Remain the same (1200/1300mhz)
(2) 800mhz
(3) Customize
Which option you want to choose? (1/2/3)
```

* For most cases, option ``2`` will be optional. Type ``2`` and press ``Enter``.
* Command will show something like this:

```
----------------------------------------
| Choose Energy Performance Preference |
----------------------------------------
(1) Max Power Saving
(2) Balance Power (Default)
(3) Balance performance
(4) Performance
Which mode is your favourite? (1/2/3/4)
```

* Option ``2`` is recommended for most cases.
* Type your option and press ``Enter``
* Command will ask for password. Type your password and press ``Enter``.
* Command will generate two customised macOS Extensions (kext's) on ``Desktop`` folder.
* Run ``KextBeast.pkg`` application.
* Click ``Continue`` and click ``Agree``.
* Select ``/Library/Extensions`` and click ``Continue``.
* Click ``Install``.
* If extensions are installed without any issues, run ``Terminal`` application from ``/Applications/Utilities`` folder.
* In ``Terminal`` application window, type:

```
sudo kextcache -i /
```

* And press ``Enter``.
* When command ``kextcache`` finish the execution unmount, detach the macOS USB installation media and reboot computer to apply new configuration.
* Reboot computer.
* With next boot macOS will enable granular and precise power management.

**Useful information**

* [Skylake HWP Enable](https://www.tonymacx86.com/threads/skylake-hwp-enable.214915/)
* [HWP(Intel Speed Shift) enable with full power management](https://www.insanelymac.com/forum/topic/321021-guide-hwpintel-speed-shift-enable-with-full-power-management/)
* [XiaoMi-Pro CPU Power management](https://github.com/daliansky/XiaoMi-Pro/issues/22)


Undervolting
---

There are several tools for Windows for undervolting and overclocking CPU and GPU. Just like:

* [Intel Extreme Tuning Utility](https://downloadcenter.intel.com/download/24075/Intel-Extreme-Tuning-Utility-Intel-XTU-)
* [MSI Afterburner](https://www.msi.com/page/afterburner)
* [ThrottleStop](https://www.techpowerup.com/download/techpowerup-throttlestop/)

With macOS, it is a different story. There are a few tools for macOS for undervolting, but they require additional macOS Extensions (kext's). Often, they are not free or not very well supported.

* [Volta](https://volta.garymathews.com)
* [VoltageShift](https://github.com/sicreative/VoltageShift)

So, I decided to go Rogue and do undervolt with BIOS. Tools like ``XTU`` provide better control, but I need a solution that will work both in Windows and Debian Linux and macOS.

AMI BIOS provides a lot of different tools for undervolting and overclocking.

The most interesting and easy to use are:

* ``Processor``
	* ``Core Voltage Offset``
* ``GT``
	* ``GT Voltage Offset``
	* ``GTU Voltage Offset``
* ``Uncore``
	* ``Uncore Voltage Offset``

To apply configuration:

* Reboot computer.
* Repeatedly press ``DEL`` key to enter BIOS configuration menu.
* In BIOS navigate to menu
	* ``Advanced``
		* ``Processor``
			* Set ``Core Voltage Offset`` to 100.
			* Set ``Offset Prefix`` to ``-`` (!).
		* ``GT``
			* Set ``GT Voltage Offset`` to 100.
			* Set ``Offset Prefix`` to ``-`` (!).
			* Set ``GTU Voltage Offset`` to 100.
			* Set ``Offset Prefix`` to ``-`` (!).
		* ``Uncore``
			* Set ``Uncore Voltage Offset`` to 60.
			* Set ``Offset Prefix`` to ``-`` (!).
		* ``Memory``
			* Set ``Memory Profile`` to the best for installed memory. Usually something like ``XMP profile 1``. 
	* ``Save and Exit``
		* Hit ``Save Changes``
		* Hit ``Save Changes and Reset``
* Boot in macOS or Windows.
* Download [Prime95](https://www.mersenne.org/download/) application.
* Run ``Torture Test...`` from ``Options`` menu for at least 1h.
* If the system works stably, repeat all the steps and incremental increase undervolting for -5. It is better to keep undervolting for ``Processor`` and ``GT/GTU`` on the same level. Repeat again ``Torture Test...``. If the system is unstable under ``Torture Test...``, freezes or reboots, revert back to the previous working configuration.

| Option | Configuration start undervolting | Recommended step | My stable working configuration |
| ---: | ---: | ---: | ---: |
| ``Processor Core Voltage Offset`` | -100 | -5 | -140 |
| ``GT Core Voltage Offset`` | -100 | -5 | -140 |
| ``GTU Core Voltage Offset`` | -100 | -5 | -140 |
| ``Uncore Voltage Offset`` | -60 | -5 | -120 |

CPU limitations can be very different even in same series. So, do not use my configuration blindly.

BIOS has many additional configurations for undervolting and overclocking, just like TDP (Thermal Design Power), but this requires extensive knowledge in CPU/Chipset/etc. and power management. This is not a part of this documentation. For more information, check the links provided at the end of the document.

**Note: It looks like the mid 2019 Razer Blade Advanced has been undervolted from factory! But there are still room for improvement.**

**Useful information**

* [Razer Blade 2017 Ultimate CPU GPU Optimization - Unleashed Performance - BIOS Unlock](https://www.youtube.com/watch?v=O5CvK7i9a_Y)
* [Razer Blade 2018 Thermal Testing - Overclocking and Undervolting](https://www.youtube.com/watch?v=rJSeG_Pb3bs)
* [Razer blade 15 undervolting with ThrottleStop](https://www.youtube.com/watch?v=ooET-Nk62VY)
* [Intel Extreme Tuning Utility (XTU) Undervolting Guide](https://www.notebookcheck.net/Intel-Extreme-Tuning-Utility-XTU-Undervolting-Guide.272120.0.html)


Nvidia BIOS flashing
---

Razer Blade Advanced mid 2019 has very few changes in comparison to the previous early 2019 model.

* Better screen refresh rate.
* Can be packed with i7 9750H CPU for extra money.

The biggest disadvantage is 80w 2080 Max-Q instead of 90w in the previous model. This is a huge difference for general performance. Check article [Comparison: 80w vs 90w RTX 2080 Max-Q](https://www.theeverydayenthusiast.com/home/comparison-80w-vs-90w-2080-max-q).

* Reboot computer.
* Select Windows 10 partition in ``Clover``.
* Download this repository ZIP archive.
* Unpack archive.
* Backup Nvidia BIOS with ``GPU-Z`` application from ``Tools\Nvidia\`` repository folder (!).
* Open ``cmd.exe`` with admin privileges.
* In ``cmd.exe`` window change folder to ``BIOS_mod\Nvidia_2080_Max-Q_BIOS_mod\`` repository folder.
* To apply 90w TDP type in ``cmd.exe`` window command

```
nvflash64.exe -6 Nvidia_2080_Max-Q_90w.rom
```

* And press ``Enter``.
* Press ``Y`` for the warning(s).
* Reboot computer.

**Useful information**

* [Razer Blade Pro 17 (2019) Review](https://www.reddit.com/r/razer/comments/c3doo2/razer_blade_pro_17_2019_review/)
* [Comparison: 80w vs 90w RTX 2080 Max-Q](https://www.theeverydayenthusiast.com/home/comparison-80w-vs-90w-2080-max-q)
* [So much better than before: Razer Blade Pro 17 Laptop Review](https://www.notebookcheck.net/So-much-better-than-before-Razer-Blade-Pro-17-Laptop-Review.424150.0.html)
* [Razer Blade Advanced OLED 80w 2080 Max-q](https://www.reddit.com/r/razer/comments/c9i1x6/razer_blade_advanced_oled_80w_2080_maxq/)
* [Razer RTX 2080 8 GB BIOS](https://www.techpowerup.com/vgabios/212123/212123)


Razer Chroma
---

Razer Chroma support for Razer Blade notebooks and the latest Razer devices has not been implemented for macOS yet. I suppose, it will never be implemented.

Thanks to [osx-razer-blade](https://github.com/boo-dev/osx-razer-blade) project, I've already had enough information, so I am working on cli tool to control Razer Blade keyboard and logo Chroma lighting.


Windows
---

### NVMe partition

* Open ``Disk Utility``
* Select ``Show All Devices`` from ``View`` menu.
* Select the NVMe drive on left pane.
* Click ``Partition`` button at the top toolbar.
* Click continue with partition.
* Add a new partition by clicking the ``[+]`` button under the circle.
* Give it a name and desired size (minimum 50Gb required for Windows 10).
* Set drive format to ``ExFat``.
* Click ``Apply``.


### Windows installation media preparation

* Download Windows 10 ISO image.
* Open [Download Windows 10 Disc Image (ISO File) URL](https://www.microsoft.com/en-us/software-download/windows10ISO) in Safari. It better to download ISO image on macOS. Microsoft detects OS and prevent download ISO image on Windows machine. It can be override by browser ``User-Agent`` replacement but still easier todo this on macOS.
* From ``Select Edition`` menu select ``Windows 10 May 2019 Update`` (!). ``Windows 10 October 2019 Update`` ISO image have issues Microsoft still have not fixed.

![Windows_Download1](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Windows_Download1.png)

* Click ``Confirm``.

![Windows_Download2](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Windows_Download2.png)

* From ``Select the product language`` menu select preferred language.

![Windows_Download3](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Windows_Download3.png)

* Click ``Confirm``.

![Windows_Download4](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Windows_Download4.png)

* Click ``64-bit Download`` button.

![Windows_Download5](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Windows_Download5.png)

* Download [UNetbootin](https://unetbootin.github.io) tool.
* Plug a USB media into Mac.
* Open ``Disk Utility``.
* Select the USB media from the left panel and click on ``Info`` button. Write down the device name.
* Run ``UNetbootin``
* Select the ``Diskimage`` radio button, click ``…`` to select a Windows 10 ISO image.

![Windows_unetbootin1](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Windows_unetbootin1.png)

* Choose ``Type`` as the USB media and select the device name of USB media.

![Windows_unetbootin2](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/Windows_unetbootin2.png)

* Click ``OK`` to start burning to the USB media.

**Useful information**

* [Create Windows 10 bootable USB from ISO on Mac without BootCamp](https://www.top-password.com/blog/create-windows-10-bootable-usb-from-iso-on-mac/)


### Windows installation

* Insert Windows 10 USB installation media.
* Reboot the computer.
* Press repeatedly ``F12`` until you ``Boot Menu`` will show.
* Select the USB installation media with Windows 10.
* Follow the usual Windows 10 installation procedure.

**Note: Be careful and select right partition created before for Windows 10. Otherwise, you can destroy the macOS installation.**

**Useful information**

* [How to Reinstall/Clean Install Windows 10](https://www.youtube.com/watch?v=OtHZueEZe9s)


### Clover Boot fix

To fix dual-booting hackintosh, rename bootmgfw.efi to bootmgfw-orig.efi causing Clover to become unblocked. Add the tag ``-orig`` to the name so that it’s still a recognizable file and is shown in the Windows EFI partition for booting in the ``Clover Boot`` loader menu.

To rename ``bootmgfw.efi``

* Boot off macOS installation media.
* Boot macOS.
* Open ``Clover Configurator`` application.
* Select ``Mount EFI`` on the left column.
* Click ``Mount Partition`` for the drive where macOS and Windows is installed on.
* Click ``Open Partition``.
* Navigate to ``EFI/Microsoft/Boot/``.
* Rename ``bootmgfw.efi`` to ``bootmgfw-orig.efi``.
* Restart.
* UEFI OS (drive_name) should be an available boot device.


#### (Optional) Override Windows Boot Manager

If for some reason the UEFI OS (drive_name) isn’t shown as an available boot device, there is a way to override ``Windows Boot Manager`` and have it redirected to ``Clover``.

* Boot off macOS installation media.
* Boot macOS.
* Open ``Clover Configurator`` application.
* Select ``Mount EFI`` on left column.
* Click ``Mount Partition`` for the drive where macOS and Windows is installed on.
* Click ``Open Partition``.
* Open the ``EFI`` partition and navigate to ``EFI/BOOT/``
* Copy ``BOOTX64.efi``.
* Navigate to ``EFI/Windows/Boot``.
* Paste ``BOOTX64.efi``.
* Rename ``BOOTX64.efi`` to ``bootmgfw.efi``.
* Restart.
* Now ``Windows Boot Manager`` will redirects to ``Clover`` instead of booting Windows.

**Note: Very often, with cumulative and security updates Windows 10 will place new ``bootmgfw.efi`` in ``EFI/Microsoft/Boot/``. You can notice this by two Windows boot options in ``Clover`` boot screen. Just remove old ``bootmgfw-orig.efi`` and rename new ``bootmgfw.efi`` to  ``bootmgfw-orig.efi``.**

**Useful information**

[Hackintosh Dual Boot Windows 10 and macOS High Sierra](https://hackintosher.com/guides/hackintosh-dual-boot-windows-10-and-macos-high-sierra/)


Known Issues and Limitations
---

**Limitations**

* Nvidia Web Drivers are not available for macOS 10.14 Mojave. Nvidia does not want to implement support for Apple 2D/3D rendering framework Metal and does not want to share access for Nvidia drivers source code for Apple. So, currently no support for Nvidia GPU for macOS 10.14 Mojave is available. It's not a problem for me because I'm using Windows 10 partition for gaming and Debian Linux partition to run the ML tasks overnight.
	* HDMI and DisplayPort ports both are connected directly to Nvidia GPU and will not work in macOS 10.14 Mojave.
	* USB-C to HDMI should work without any issues.

![HDMI_DP](https://github.com/stonevil/Razer_Blade_Advanced_early_2019_Hackintosh/raw/master/images/HDMI_DP.png)

* Windows Hello camera is not supported in macOS.
* Not all sensors are supported by VirtualSMC.


**Issues**

* Sometimes, the screen does not wake up when you open the lid after the computer was in a sleep mode. You need to close and open the lid again. This issue has appeared after the latest BIOS update. Although annoying, it is not that important.


Conclusion
---

It's a pretty good laptop with a way better keyboard than 2016-2019y MacBook Pro. It is a solid workstation and an extremely good gaming machine. It has easy to upgrade NVMe and RAM and WiFi modules. This Model supports NVMe up to 2Tb and RAM up to 64Gb.

Major disadvantages are:

* PC trackpads still cannot match with MacBook Pro. This one is good. It is much better than most PC notebooks have, but still not even close to MacBook Pro.
* The screen is rather mediocre in comparison to MacBook Pro. 144Hz is good for gaming. If you are working with text a lot just like me, maybe, it will be better to get 4K panel. For content creators, it is mandatory to get the 4K panel.

P.S. Apple, please fix the keyboard and release a real Pro MacBook. Just take a look on Razer Blade Advanced as that is a good place for starting to design a new MacBook Pro.

Additional Information
---

* [An iDiot's Guide To Lilu and its Plug-ins](https://www.tonymacx86.com/threads/an-idiots-guide-to-lilu-and-its-plug-ins.260063/)
* [Razer Blade Advanced (2019) trackpad issue](https://www.tonymacx86.com/threads/need-help-razer-blade-advanced-2019-trackpad-issue.273575/)
* [Razer Blade 15 (2018) Detailed Install Guide High Sierra 10.13.6 (17G2208-17G5019)](https://www.tonymacx86.com/threads/guide-razer-blade-15-2018-detailed-install-guide-high-sierra-10-13-6-17g2208-17g5019.264017/)
* [Razer Blade 2017](https://www.tonymacx86.com/threads/guide-razer-blade-2017.242627/)
* [UniBeast: Install macOS Mojave on Any Supported Intel-based PC](https://www.tonymacx86.com/threads/unibeast-install-macos-mojave-on-any-supported-intel-based-pc.259381/)
* [Keeping your Hackintosh up-to-date, my method](https://davejansen.com/keeping-your-hackintosh-up-to-date/)
* [Hackintosh Mojave 10.14.5 Update Guide](https://hackintosher.com/guides/hackintosh-mojave-10-14-5-update-guide/)
* [corpnewt/Hackintosh-Guide](https://github.com/corpnewt/Hackintosh-Guide/blob/master/config.plist-per-hardware/coffee-lake.md)
* [Anti-Hackintosh Buyers Guide](https://www.reddit.com/r/hackintosh/comments/c0y312/antihackintosh_buyers_guide/)
* [INVENTORY OF SUPPORTED/UNSUPPORTED WIRELESS CARDS #2, SIERRA -> CATALINA](https://osxlatitude.com/forums/topic/11138-inventory-of-supportedunsupported-wireless-cards-2-sierra-catalina/)


**Community**

* [InsanelyMac](https://www.insanelymac.com)
* [tonymacx86](https://www.tonymacx86.com)
* [OSXL](https://osxlatitude.com)
* [Reddit Hackintosh](https://www.reddit.com/r/hackintosh/)


Credits
---

* [Apple](https://www.apple.com) for macOS. It is still the best OS
* [netkas](http://netkas.org) for the original idea of creating a software SMC emulator
* [RehabMan](https://github.com/RehabMan) for Laptop-DSDT-Patch, OS-X-Clover-Laptop-Config, OS-X-MaciASL-patchmatic, and more. You are a legend!
* [Acidanthera](https://github.com/acidanthera) for VirtualSMC
* [Alexandre Daoud](https://github.com/alexandred) for VoodooI2C
* [Ben Raz](https://github.com/ben9923) for help with VoodooI2C and trackpad
* [Bat.bat](https://github.com/williambj1) for help with VoodooI2C and trackpad
* [Steve Zheng](https://github.com/stevezhengshiqi) for one-key-cpufriend
* [vettz500](https://www.tonymacx86.com/members/vettz500.291395/) for the incredibly useful information about RBA 2018
* [Kishor Prins](https://github.com/kprinssu) and [Boo](https://github.com/boo-dev) for osx-razer-blade
* Additional big thanks go to all the contributors and researchers involved in Hackintosh development!


TODO
---

- [ ] Add BIOS pre and post update procedure
